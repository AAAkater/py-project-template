---
name: testing
description: "Write and run Python tests with pytest, and run the pre-commit quality gate (ruff + ty + pytest). Use when adding tests, running the test suite, or preparing a change for commit. Covers test layout, naming, and the 4-step quality workflow."
---

# Testing & Quality Gate

Rules for writing tests with **pytest** and running the pre-commit quality gate
(ruff + ty + pytest) before committing.

## When to Use

- Adding a test
- Running the test suite
- Reviewing a change before commit (pre-commit quality gate)

## Add a Test

1. Place tests in `tests/` mirroring the `src/` layout
   (`src/<pkg>/foo.py` → `tests/test_foo.py`).
2. Name test functions `test_<behavior>`; use `pytest` fixtures as needed.
3. Keep tests pure and fast — no network/IO unless explicitly required.

## Pre-commit Quality Gate

Run all four, in order, before committing:

```bash
uv run ruff check --fix .   # auto-fix lint + format issues
uv run ruff check .          # verify clean (no changes)
uv run ty check .            # strict type check — must pass with 0 errors
uv run pytest -vv            # run the test suite
```

A change is ready to commit only when **all four pass**. If `ruff check --fix`
alters files, re-run `ruff check .` to confirm, then re-run `ty check` and
`pytest` since formatting can shift line-level behavior.
