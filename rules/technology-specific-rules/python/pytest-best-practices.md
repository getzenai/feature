# Testing Best Practices (Python with pytest)

This document outlines best practices for writing tests in this Python project using the `pytest` framework.

## 1. Framework and Mocking

- **Framework:** Use `pytest` as the primary testing framework.
- **Mocking Library:** Utilize `pytest-mock` for mocking dependencies. It provides the `mocker` fixture.
- **`mocker` Fixture:** Prefer the `mocker` fixture over `unittest.mock.patch` decorators or context managers for cleaner test setup within `pytest`.

  ```python
  # Instead of:
  # from unittest.mock import patch
  # def test_something():
  #     with patch('module.dependency') as mock_dep:
  #         # ... test ...

  # Prefer:
  def test_something(mocker):
      mock_dep = mocker.patch('module.dependency')
      # ... test ...
  ```

- **Patch Target:** Always patch objects where they are _looked up_ (i.e., in the module where they are imported and used), not where they are defined. This prevents issues where the code under test uses a different reference than the one you patched.

  ```python
  # module_a.py
  def utility_function():
      # ...
      pass

  # module_b.py
  from module_a import utility_function # Lookup happens here

  def function_under_test():
      # ...
      result = utility_function()
      # ...

  # test_module_b.py
  def test_function_under_test(mocker):
      # Correct: Patch where it's looked up in module_b
      mock_util = mocker.patch("module_b.utility_function")
      # Incorrect: mocker.patch("module_a.utility_function")

      # ... rest of test ...
  ```

- **Mock Specification (`spec=True`, `spec=Class`):** When creating mocks, especially for instances, use `spec=True` or `spec=ActualClass` to ensure the mock behaves like the real object and raises errors for non-existent attributes/methods. This helps catch errors early if the underlying class changes.

  ```python
  # In conftest.py or test:
  from module.analyzer import Analyzer

  # Mocking a class instance
  instance_mock = mocker.MagicMock(spec=Analyzer)
  instance_mock.some_method.return_value = "mocked"

  # If you try instance_mock.non_existent_method(), it will raise an AttributeError
  ```

## 2. Fixtures

- **Purpose:** Use fixtures to set up preconditions for tests (e.g., creating mock objects, setting up database connections, creating temporary files).
- **Shared Fixtures (`conftest.py`):** Define fixtures that are needed by multiple test modules in a central `tests/conftest.py` file. `pytest` automatically discovers these fixtures and makes them available to tests in that directory and subdirectories without needing explicit imports.
- **Naming:** Name fixtures descriptively (e.g., `mock_analyzer_instance`, `tmp_repo_path`).
- **Scope:** Use appropriate fixture scopes (`function`, `class`, `module`, `session`) if setup is expensive, but default to `function` scope unless there's a clear reason otherwise.
- **Dependencies:** Fixtures can depend on other fixtures (including `mocker`).

  ```python
  # tests/conftest.py
  import pytest
  from unittest.mock import MagicMock
  from module.analyzer import Analyzer

  ANALYZER_IMPORT_PATH = "module.under.test.Analyzer"

  @pytest.fixture
  def mock_analyzer_class(mocker):
      # Mocks the Analyzer class itself
      mock = mocker.patch(ANALYZER_IMPORT_PATH)
      # Configure a default instance mock
      instance_mock = mocker.MagicMock(spec=Analyzer)
      instance_mock.llm_adapter = mocker.MagicMock() # Add expected attributes
      mock.return_value = instance_mock
      return mock

  @pytest.fixture
  def mock_analyzer_instance(mock_analyzer_class):
      # Provides easy access to the configured instance mock
      # Depends on mock_analyzer_class to ensure patching happens first
      return mock_analyzer_class.return_value

  # tests/test_module.py
  # No imports needed for fixtures from conftest.py

  def test_using_instance(mock_analyzer_instance):
      # mock_analyzer_instance is the configured MagicMock(spec=Analyzer)
      mock_analyzer_instance.analyze_file.return_value = {"result": "ok"}
      # ... call code that uses the analyzer instance ...
      mock_analyzer_instance.analyze_file.assert_called_once()
  ```

## 3. Testing File System Interactions

- **Use `tmp_path`:** When testing code that reads, writes, or interacts with files and directories, use the built-in `tmp_path` fixture provided by `pytest`.
- **Avoid Mocking `Path` Internals:** Do not mock low-level `pathlib.Path` methods like `iterdir`, `relative_to`, `is_file`, `write_text` etc., extensively. This makes tests brittle and highly coupled to the implementation details.
- **Create Real Temporary Files:** Use `tmp_path` to create a temporary directory structure and real files needed for the test. Pass the `tmp_path` object (or paths derived from it) to the code under test.

  ```python
  def test_processing_files(tmp_path, mock_analyzer_instance): # Inject tmp_path
      # 1. Setup: Create real directories and files in tmp_path
      repo_dir = tmp_path / "my_repo"
      repo_dir.mkdir()
      src_dir = repo_dir / "src"
      src_dir.mkdir()
      file1 = repo_dir / "config.txt"
      file1.write_text("config_content")
      file2 = src_dir / "main.py"
      file2.write_text("print('hello')")

      # Configure mocks for dependencies (like the analyzer)
      mock_analyzer_instance.analyze_file.return_value = {"capabilities": ["test"]}

      # 2. Execute: Pass the real path (repo_dir) to the code under test
      mapper = CapabilityMapper(repo_dir) # Assumes CapabilityMapper takes a Path
      result = mapper.generate_capability_map()

      # 3. Assert: Check results based on interaction with the real temp files/dirs
      #    and the behavior of the mocked dependencies
      assert "capabilities" in result
      mock_analyzer_instance.analyze_file.assert_called()
      # ... other assertions ...
  ```

## 4. Testing CLIs (Click)

- **Use `CliRunner`:** Use `click.testing.CliRunner` to invoke CLI commands within tests.
- **Test Help:** Ensure `--help` options work for the main command and subcommands.
- **Test Argument/Option Validation:** Test edge cases like missing arguments, invalid values, non-existent paths.
- **Use `--dry-run`:** If the CLI provides a dry-run mode, use it extensively to test logic (like file discovery, parameter processing) without triggering expensive operations or external API calls. Mocking might not be necessary for dry-run tests if external dependencies are bypassed.
- **Test Output Files:** If the CLI writes to files (`--output`), use `tmp_path` to provide a temporary output location and assert that the file is created with the correct content.

  ```python
  from click.testing import CliRunner
  from my_project.cli import main_cli

  def test_cli_dry_run(tmp_path):
      runner = CliRunner()
      repo_dir = tmp_path / "sample_repo"
      repo_dir.mkdir()
      (repo_dir / "file.py").write_text("...")

      result = runner.invoke(main_cli, ["analyze", str(repo_dir), "--dry-run"])

      assert result.exit_code == 0
      assert "Dry run completed" in result.output
      # Assert other expected output based on dry run logic
  ```

## 5. General Principles

- **Descriptive Names:** Use clear, descriptive names for test functions (e.g., `test_should_do_x_when_y`) and fixtures.
- **Test Organization:** Group related tests into classes (e.g., `TestAnalyzer`).
- **Clear Assertions:** Use specific `assert` statements. Compare sets for order-independent collection checks. Adapt assertions to the _actual_ data structures returned by the code.
- **Independence:** Aim for tests that are independent of each other. Fixtures help achieve this by providing clean setup for each test (or class/module/session).
