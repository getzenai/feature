# FEATURE's Roo-Code Rules

A collection of rules, best practices, and custom modes to enhance AI-assisted coding with Roo-Code.

## Overview

This repository contains carefully crafted rules that significantly improve our AI agent coding results. Based on our experience, providing context about the repository and establishing clear rules for implementation tasks are crucial for achieving high-quality AI-assisted development.

The rules are primarily designed for integration with Roo-Code, but can be adapted for use with other AI coding assistants. Feel free to copy and paste these rules into any system you use for AI-assisted development.

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

### 1. Add Rules to Your Project

Copy the rules you want to use into your project's `.roo/` directory:

```bash
# Create the .roo directory if it doesn't exist
mkdir -p /path/to/your/project/.roo

# Copy all rules (adjust as needed for specific rule sets)
cp -r /path/to/this/repo/rules/* /path/to/your/project/.roo/
```

When copied to your project, the structure will be similar but with `.roo/` as the root folder instead of `rules/`. For example, what is `rules/rules/` here will become `.roo/rules/` in your project.

### 2. Add Custom Modes

To add the custom modes to your Roo-Code instance:

**Option 1:** If you don't have a `.roomodes` file yet:

```bash
cp /path/to/this/repo/modes/.roomodes /path/to/your/project/
```

**Option 2:** If you already have a `.roomodes` file:

- Copy the content from this repository's `.roomodes` file
- Add it to your existing `.roomodes` file
- If your existing file uses the old JSON format, convert it to YAML first (you can ask Roo-Code to do this for you)

### 3. Start with Repository Analysis

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

While these rules are primarily designed for Roo-Code, you can adapt them for use with any AI coding assistant by copying the relevant content and formatting it appropriately for your tool of choice.

## Rule Categories

- **General Rules**: Core principles applied across all modes
- **Mode-Specific Rules**: Tailored for specific Roo-Code modes (Architect, Code, Orchestrator)
- **Technology-Specific Rules**: Best practices for specific frameworks and libraries

## Contributing

Contributions are welcome! If you have rules that have improved your AI coding experience, please consider sharing them through a pull request.
