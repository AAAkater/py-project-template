---
name: dependencies
description: "Manage Python project dependencies with uv. Use when adding runtime or dev dependencies, updating the lockfile, or editing pyproject.toml. Covers uv add/sync commands, the dev dependency group, and keeping pyproject.toml as the single source of truth."
---

# Dependency Management

Rules for adding and managing dependencies with **uv** in a Python project.

## When to Use

- Adding a runtime or dev dependency
- Updating the lockfile / venv
- Editing `pyproject.toml` dependency sections

## Commands

```bash
uv add <package>              # runtime dependency → [project] dependencies
uv add --group dev <package>  # dev-only dependency → [dependency-groups] dev
uv sync                       # refresh the lockfile / venv
```

## Rules

- **Prefer the dev group** for test/lint/build tools
  (`uv add --group dev <package>`).
- **`pyproject.toml` is the single source of truth** — never `pip install`
  directly; always go through `uv add` so the lockfile stays in sync.
- **`pyproject.toml` is canonical** — do not create `setup.py`, `setup.cfg`,
  `requirements.txt`, or `.flake8`; all project metadata and dependency groups
  live in `pyproject.toml`. Tool-specific config may live in dedicated files
  like `ruff.toml` and `ty.toml`.
- **Run `uv sync`** after editing `pyproject.toml` by hand to refresh the venv.
