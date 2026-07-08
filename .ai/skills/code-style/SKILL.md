---
name: code-style
description: "Apply Python 3.13 code conventions, strict typing, Pydantic-first data modeling, and loguru logging. Use when writing Python code, adding type annotations, defining schemas/models, choosing dataclass vs Pydantic, adding logger calls, or fixing lint/type errors. Let ruff report formatting/lint issues and ty report type issues."
---

# Code Style, Typing & Data Modeling

Use modern Python 3.13 syntax, Pydantic-first data modeling, and loguru logging.
For formatting, lint, and type correctness, rely on tool feedback: ruff owns
formatting/lint and ty owns type checking. Trust their reports instead of
guessing style rules manually.

## When to Use

- Writing or modifying Python code
- Adding type annotations to a function or module
- Defining data schemas, parsed records, API payloads, settings, or validation models
- Choosing between Pydantic models and dataclasses
- Adding or reviewing loguru logger calls
- Fixing a ruff lint or format error
- Fixing a ty type error or warning

## Python 3.13 Syntax Preferences

Prefer modern Python 3.13 syntax. Do not write legacy typing patterns unless a
dependency or public API explicitly requires them.

Prefer built-in generics and modern syntax (`list[str]`, `dict[str, int]`,
`str | None`, `type T = ...`) over legacy `typing` aliases such as `List`,
`Dict`, `Optional`, `Union`, and `TypeAlias`.

Additional rules:

- Never add `from __future__ import annotations`.
- Use absolute imports within the package (`from pkg.module import thing`), not
  relative imports (`from .module import thing`).
- Do not import `List`, `Dict`, `Tuple`, `Set`, `Optional`, `Union`, or `Type`
  from `typing` for normal annotations.
- Use the `type` statement for type aliases. Import `typing.TypeAlias` only for
  compatibility or when a tool explicitly requires it.
- Use `typing.Protocol`, `typing.TypedDict`, and `typing.Literal` only when
  those constructs are actually needed.
- Prefer `match` / `case` for clear structural dispatch when it improves
  readability, but do not force it over simple `if` / `elif` chains.

## Pydantic-first Data Modeling

Use **Pydantic v2** as the default choice for structured data that crosses a
boundary: external JSON, API payloads, config/settings, parsed files, database
records, CLI inputs, and anything that needs validation or serialization.

Prefer Pydantic models over loose dictionaries:

- Prefer `BaseModel` subclasses for domain records and IO payloads.
- Avoid returning or passing `dict[str, Any]` across module boundaries when a
  typed Pydantic model can express the schema.
- Keep raw `dict` usage local to parsing/adapter code; validate immediately
  with `Model.model_validate(raw)` before handing data to business logic.
- Use `model_dump()` / `model_dump_json()` for serialization; avoid legacy
  Pydantic v1 methods like `.dict()` and `.json()`.
- Use `Field(...)` for constraints, descriptions, aliases, and
  `default_factory` for mutable defaults.
- Use `ConfigDict` via `model_config` for model behavior; do not use v1-style
  inner `class Config`.
- Use `field_validator` / `model_validator` for normalization and validation;
  validators should be deterministic and side-effect free.
- Prefer explicit models composed from smaller models rather than deeply nested
  `dict[str, object]` or `dict[str, Any]` shapes.

## Logging

- **No bare `print` in library code** — use **loguru** for logging. Add it with
  `uv add loguru`, then `from loguru import logger`. Configure sinks once at the
  application entry point. `print` is acceptable only in `main.py` entry points
  and throwaway scripts.
- **Use f-strings in logger calls**: `logger.info(f"Saved {count} items")`.
  Do not use loguru `{}` placeholders (`logger.info("Saved {} items", count)`)
  or printf-style formatting (`logger.info("Saved %s items", count)`).
