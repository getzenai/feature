# Python pytest Best Practices

## Framework and Mocking

- Use [`pytest`](https://pytest.org/) as primary testing framework
- Use [`pytest-mock`](https://pytest-mock.readthedocs.io/) for mocking dependencies via [`mocker`](https://pytest-mock.readthedocs.io/en/latest/usage.html#the-mocker-fixture) fixture
- Prefer [`mocker`](https://pytest-mock.readthedocs.io/en/latest/usage.html#the-mocker-fixture) fixture over [`unittest.mock.patch`](https://docs.python.org/3/library/unittest.mock.html#patch) decorators

```python
# Prefer:
def test_something(mocker):
    mock_dep = mocker.patch('module.dependency')
    # ... test ...
```

- Patch objects where they are looked up (imported/used), not where defined

```python
# module_b.py
from module_a import utility_function # Lookup happens here

# test_module_b.py
def test_function_under_test(mocker):
    # Correct: Patch where it's looked up
    mock_util = mocker.patch("module_b.utility_function")
```

- Use [`spec=True`](https://docs.python.org/3/library/unittest.mock.html#unittest.mock.Mock.spec) or [`spec=ActualClass`](https://docs.python.org/3/library/unittest.mock.html#unittest.mock.Mock.spec) for mocks to catch attribute errors

```python
instance_mock = mocker.MagicMock(spec=Analyzer)
```

## Fixtures

- Use fixtures for test setup (mock objects, database connections, temporary files)
- Define shared fixtures in [`tests/conftest.py`](tests/conftest.py) for automatic discovery
- Name fixtures descriptively (e.g., `mock_analyzer_instance`, `tmp_repo_path`)
- Use appropriate fixture scopes (`function`, `class`, `module`, `session`) - default to `function`
- Fixtures can depend on other fixtures including [`mocker`](https://pytest-mock.readthedocs.io/en/latest/usage.html#the-mocker-fixture)

```python
# tests/conftest.py
@pytest.fixture
def mock_analyzer_class(mocker):
    mock = mocker.patch("module.under.test.Analyzer")
    instance_mock = mocker.MagicMock(spec=Analyzer)
    mock.return_value = instance_mock
    return mock

@pytest.fixture
def mock_analyzer_instance(mock_analyzer_class):
    return mock_analyzer_class.return_value
```

## Testing File System Interactions

- Use built-in [`tmp_path`](https://docs.pytest.org/en/stable/how.html#tmp-path) fixture for file/directory testing
- Avoid mocking [`pathlib.Path`](https://docs.python.org/3/library/pathlib.html) methods extensively
- Create real temporary files using [`tmp_path`](https://docs.pytest.org/en/stable/how.html#tmp-path)

```python
def test_processing_files(tmp_path, mock_analyzer_instance):
    # Setup: Create real directories and files
    repo_dir = tmp_path / "my_repo"
    repo_dir.mkdir()
    file1 = repo_dir / "config.txt"
    file1.write_text("config_content")

    # Configure mocks for dependencies
    mock_analyzer_instance.analyze_file.return_value = {"capabilities": ["test"]}

    # Execute: Pass real path to code under test
    mapper = CapabilityMapper(repo_dir)
    result = mapper.generate_capability_map()

    # Assert: Check results
    assert "capabilities" in result
    mock_analyzer_instance.analyze_file.assert_called()
```

## Testing CLIs (Click)

- Use [`click.testing.CliRunner`](https://click.palletsprojects.com/en/8.1.x/testing/) to invoke CLI commands
- Test [`--help`](https://click.palletsprojects.com/en/8.1.x/options/#help-option) options for main command and subcommands
- Test argument/option validation (missing arguments, invalid values, non-existent paths)
- Use [`--dry-run`](https://click.palletsprojects.com/en/8.1.x/options/#boolean-flags) extensively to test logic without expensive operations
- Test output files using [`tmp_path`](https://docs.pytest.org/en/stable/how.html#tmp-path) for temporary output location

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
```

## General Principles

- Use descriptive names for test functions (e.g., `test_should_do_x_when_y`) and fixtures
- Group related tests into classes (e.g., `TestAnalyzer`)
- Use specific [`assert`](https://docs.pytest.org/en/stable/how.html#assert) statements
- Compare sets for order-independent collection checks
- Aim for test independence - fixtures help achieve clean setup
