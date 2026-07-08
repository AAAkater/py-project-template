---
name: python-project
description: "Index of Python project skills for a uv + ruff + ty + pytest toolchain targeting Python 3.13+. Use as the entry point when writing Python code, adding dependencies, or running quality checks. Points to specialized sub-skills: code-style, dependencies, testing."
---

# Python Project — Skill Index

Entry point for Python projects using a modern toolchain. Load the relevant
sub-skill below for the task at hand instead of reading everything at once.

## Toolchain

| Tool       | Role                                                     | Config                     |
| ---------- | -------------------------------------------------------- | -------------------------- |
| **uv**     | Package manager & runner (`uv sync`, `uv add`, `uv run`) | `pyproject.toml`           |
| **ruff**   | Linter + formatter                                       | `ruff.toml`                |
| **ty**     | Static type checker (strict)                             | `ty.toml`                  |
| **pytest** | Test runner                                              | `pyproject.toml` dev group |

Always invoke tools through `uv run` so the project venv is used.

## Sub-skills

| Task                                                         | Load skill     |
| ------------------------------------------------------------ | -------------- |
| Writing code, syntax, type annotations, Pydantic, logging    | `code-style`   |
| Adding runtime/dev dependencies, `pyproject.toml` management | `dependencies` |
| Writing tests, running the pre-commit quality gate           | `testing`      |
