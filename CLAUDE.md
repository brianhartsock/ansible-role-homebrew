# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Ansible role (`brianhartsock.homebrew`) that installs Homebrew, manages homebrew packages, homebrew cask packages, and homebrew taps on macOS. Published to Ansible Galaxy.

## Commands

```bash
# Install dependencies
uv sync

# Linting (all three run via pre-commit too)
uv run ansible-lint
uv run yamllint .
uv run flake8

# Run all pre-commit hooks
uv run pre-commit run --all-files
```

No molecule tests — this is a macOS-only role and cannot be tested in Docker containers.

## Architecture

This is a simple, single-task-file role with no handlers, templates, or OS dispatch:

- `tasks/main.yml` — all role logic: checks for homebrew, installs it, updates/upgrades, configures taps, installs packages and casks
- `defaults/main.yml` — user-configurable variables (`homebrew_update`, `homebrew_packages`, `homebrew_cask_packages`, `homebrew_taps`)
- `meta/main.yml` — Galaxy metadata (namespace: `brianhartsock`, role: `homebrew`, platform: MacOSX only)

## Conventions

- Use FQCNs for all modules (e.g., `community.general.homebrew`, not `homebrew`)
- Name all tasks
- YAML linting is handled by yamllint (ansible-lint's `yaml` rule is skipped to avoid conflicts)
- All tool invocations use `uv run` prefix

## Development Workflow

Follow this workflow for all code changes.

```
Code → Document → Verify → Code Review
  ^                              |
  └──── fix issues ──────────────┘
```

### 1. Code

Make the implementation changes. Use FQCNs, name all tasks, and follow the patterns in existing task files.

### 2. Document

Update README.md and CLAUDE.md to reflect any changes to variables, platforms, commands, or architecture. If the ansible plugin is installed, use the `documentator` agent.

### 3. Verify

Run linters (yamllint, ansible-lint, flake8), pre-commit hooks, and molecule tests. All checks must pass before proceeding. If the ansible plugin is installed, use the `verifier` agent.

### 4. Code Review

Review the changes for Ansible best practices, idempotency, security, cross-platform correctness, and test coverage. If the ansible plugin is installed, use the `code-reviewer` agent.

### 5. Iterate

If verification or code review flags issues, fix them and repeat from step 2. Continue until all checks pass and the review is clean.
