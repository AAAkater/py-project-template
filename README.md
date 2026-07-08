# Python Project Template

A minimal Python 3.13+ project template using a modern development toolchain:

- **uv** for dependency management and command execution
- **ruff** for linting and formatting
- **ty** for strict type checking
- **pytest** for tests
- **pydantic v2** for data modeling and validation
- **loguru** for logging

The template is intended for small-to-medium Python projects that want a clean
baseline with strict typing, reproducible dependencies, and simple quality
checks.

## Requirements

- Python 3.13+
- uv

The Python version is pinned in `.python-version` and mirrored by
`requires-python = ">=3.13"` in `pyproject.toml`.

## Setup

Install dependencies:

```bash
uv sync
```

Run the default entry point:

```bash
uv run python main.py
```

## Project Layout

Current minimal layout:

```text
.
├── main.py
├── pyproject.toml
├── ruff.toml
├── ty.toml
├── .python-version
└── .ai/
    └── skills/
```

For real projects, prefer a `src/` layout:

```text
.
├── src/
│   └── your_package/
│       └── __init__.py
├── tests/
├── pyproject.toml
├── ruff.toml
└── ty.toml
```

## Common Commands

### Add dependencies

Runtime dependency:

```bash
uv add <package>
```

Development dependency:

```bash
uv add --group dev <package>
```

### Lint, format, type-check, and test

Run the full quality gate before committing:

```bash
uv run ruff check --fix .
uv run ruff check .
uv run ty check .
uv run pytest -vv
```

## Code Conventions

- Use Python 3.13+ syntax.
- Prefer modern typing syntax such as `str | None`, `list[str]`, and `type T = ...`.
- Do not add `from __future__ import annotations`.
- Use Pydantic v2 models for structured data that crosses boundaries (external JSON, config, payloads, parsed records, database rows, CLI input).
- Use `loguru` for logging and f-strings inside logger calls.
- Let `ruff` and `ty` report style and type issues instead of manually guessing rules.

## Configuration

### `pyproject.toml`

Defines project metadata, Python version, runtime dependencies, and dev
dependencies.

Current runtime dependencies:

- `loguru`
- `pydantic`

Current dev dependencies:

- `pytest`
- `ruff`
- `ty`

### `ruff.toml`

Configures linting and formatting:

- target Python: `py313`
- line length: `120`
- quote style: double quotes
- docstring convention: Google

### `ty.toml`

Configures strict type checking:

- Python version: `3.13`
- `all = "error"`
- terminal warnings are treated as errors

## AI Skills

This template includes project-local AI guidance under `.ai/skills/`:

- `python-project` — entry-point skill index
- `code-style` — Python 3.13 syntax, typing, Pydantic, and logging conventions
- `dependencies` — uv and `pyproject.toml` dependency management
- `testing` — pytest and pre-commit quality gate

These skills help AI coding agents follow the same conventions as the project.

## Notes

- `pyproject.toml` is the canonical source for project metadata and dependencies.
- Do not create `setup.py`, `setup.cfg`, `requirements.txt`, or `.flake8` unless a downstream integration explicitly requires it.
- Keep generated files, virtual environments, build artifacts, and caches out of version control.
