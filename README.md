# FEATURE's Roo-Code Rules

A collection of rules, best practices, and custom modes to enhance AI-assisted coding with Roo-Code.

## Overview

This repository contains carefully crafted rules that significantly improve our AI agent coding results. Based on our experience, providing context about the repository and establishing clear rules for implementation tasks are crucial for achieving high-quality AI-assisted development.

The rules are primarily designed for integration with Roo-Code, but can be adapted for use with other AI coding assistants. Feel free to copy and paste these rules into any system you use for AI-assisted development.

## Custom Instructions Integration

This setup leverages the [Roo-Code custom instructions system](https://docs.roocode.com/features/custom-instructions/), where custom instructions can be organized in the `.roo/rules` folders and `.roomodes` file within your project. The custom instructions system allows you to provide context-specific guidance to AI assistants, ensuring consistent and high-quality code generation tailored to your project's needs.

When you copy the rules from this repository to your project's `.roo/` directory, roocode automatically loads and applies these instructions during AI-assisted coding sessions, making your development workflow more efficient and aligned with your team's best practices.

## GitHub Feature Branch Workflow

The orchestrator rules include a comprehensive GitHub feature branch workflow, described in detail in [`rules/rules-orchestrator/feature-branch-workflow.md`](rules/rules-orchestrator/feature-branch-workflow.md), that coordinates complete feature implementation through structured Git processes. This workflow manages the entire feature lifecycle from initial specification to final merge, with GitHub issues serving as the central communication hub between different AI modes. It relies on the [`rules/rules-architect/github_issue_specification.md`](rules/rules-architect/github_issue_specification.md) template, where implementation steps and the test plan are described to provide better guidance for the coding model.

- **Issue-Driven Development**: Every feature starts with a detailed GitHub issue that serves as the single source of truth
- **Mode Coordination**: The Orchestrator delegates tasks to specialized modes (Architect, Code, Review) while maintaining progress tracking
- **Quality Gates**: Built-in checkpoints ensure tests pass and code reviews are completed before merging
- **Full Traceability**: Clear links between issues, branches, commits, and pull requests

### Workflow Phases

1. **Specification Evaluation**: Clarify requirements and create detailed GitHub issues
2. **Feature Branch Creation**: Create properly named feature branches linked to issues
3. **Implementation**: Code mode implements features with incremental commits
4. **Code Review**: Review mode performs comprehensive code analysis
5. **Review Resolution**: Address feedback through iterative improvement cycles
6. **Merge and Completion**: Merge approved changes and clean up branches

This workflow ensures consistent, high-quality feature delivery with complete audit trails and collaborative transparency. The GitHub MCP tool integration enables seamless automation of branch creation, pull requests, code reviews, and merging processes.

## Repository Structure

Current structure in this repository:

```
.
├── rules/                      # All rules are organized here
│   ├── rules/                  # General rules applied to all modes
│   │   ├── coding_mantra.md    # Core coding principles
│   │   ├── github_tool_use.md  # GitHub integration guidelines
│   │   └── terminal_commands.md # Terminal command best practices
│   │
│   ├── rules-architect/        # Rules specific to Architect mode
│   ├── rules-code/             # Rules specific to Code mode
│   ├── rules-orchestrator/     # Rules specific to Orchestrator mode
│   │
│   └── technology-specific-rules/ # Rules for specific technologies
│       ├── python/             # Python-specific guidelines
│       └── sveltekit/          # SvelteKit development best practices
│
└── modes/                      # Custom modes for Roo-Code
    └── .roomodes               # Repository overview mode definition
```

## Getting Started

### 1. Clone and Install Rules

Navigate to your project directory and run these commands:

```bash
# Clone the repository temporarily into your project
git clone https://github.com/getzenai/feature.git

# Create the .roo directory if it doesn't exist
mkdir -p .roo

# Copy all rules to your project
cp -r feature/rules/* .roo/

# Copy custom modes
cp feature/modes/.roomodes .

# Clean up - remove the cloned repository
rm -rf feature
```

When copied to your project, the structure will be similar but with `.roo/` as the root folder instead of `rules/`. For example, what is `rules/rules/` here will become `.roo/rules/` in your project.

### 2. Customize Rules for Your Project

After installation, adapt the rules to your specific needs:

#### General Rules

The rules in `.roo/rules/` apply to all modes and can be used as-is or customized for your workflow.

#### Mode-Specific Rules

- **`.roo/rules-architect/`** - Rules specific to Architect mode
- **`.roo/rules-code/`** - Rules specific to Code mode
- **`.roo/rules-orchestrator/`** - Rules specific to Orchestrator mode

#### Technology-Specific Rules

The `.roo/technology-specific-rules/` folder contains rules for specific technologies. You have two options:

**Option A: Move to mode-specific folders**

```bash
# Example: Move Python rules to Code mode
mv .roo/technology-specific-rules/python/* .roo/rules-code/
```

**Option B: Move to general rules**

```bash
# Move all technology rules to general rules folder
mv .roo/technology-specific-rules/* .roo/rules/
```

### 3. Handle Existing `.roomodes` File

If you already have a `.roomodes` file in your project:

1. Back up your existing file: `cp .roomodes .roomodes.backup`
2. Merge the content from the new `.roomodes` file with your existing one
3. If your existing file uses the old JSON format, convert it to YAML first (you can ask Roo-Code to do this for you)

### 4. Start with Repository Analysis

We recommend starting with the Codebase Analyzer mode to create a comprehensive overview of your repository:

1. Open Roo-Code in your project
2. Select the "📊 Codebase Analyzer" mode
3. Ask it to analyze your repository
4. The analyzer will examine your codebase and create a detailed markdown file in your `.roo/rules` directory

This analysis provides valuable context for all future AI coding tasks.

## Customizing Rules

These rules are meant to be adapted to your specific workflow and preferences:

1. Review the rules in each category
2. Keep what works for your team
3. Modify or remove what doesn't fit your needs
4. Add your own rules based on your team's best practices

**💡 Protip**: Ask your coding agent to help adapt existing rules or create new ones based on your chat history. When you notice patterns in how you work together or areas where the agent could perform better, you can say something like "Based on our conversation, can you create a rule that will help you implement similar tasks more effectively next time?" This iterative approach helps build a personalized rule set that improves over time.

While these rules are primarily designed for Roo-Code, you can adapt them for use with any AI coding assistant by copying the relevant content and formatting it appropriately for your tool of choice.

## Contributing

Contributions are welcome! If you have rules that have improved your AI coding experience, please consider sharing them through a pull request.
