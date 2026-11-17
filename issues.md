# Issues found in wildlife_sightings.py

Before: Pylint 3.46/10, Bandit 1 High + 1 Medium + 1 Low, Flake8 6 warnings.
After: Pylint 10.00/10, Bandit 0 issues, Flake8 0 warnings. Output unchanged (`5455c3 25 Leopard`).

| Issue | Type | Line(s) | Description | Fix Approach |
|-------|------|---------|-------------|--------------|
| Weak MD5 hash (Bandit B324, High) | Security | 15 | `hashlib.md5` flagged as a weak hash for security use | The ID is only a short label, not a security value, so kept MD5 with `usedforsecurity=False` (output stays the same) |
| SQL injection (Bandit B608, Medium) | Security | 9 | INSERT built with `.format()`, so species/zone text can inject SQL | Parameterized query with `?` placeholders |
| `assert` used (Bandit B101, Low) | Security / Bug | 36 | Asserts are removed when Python runs with `-O`, so the check can vanish | Replaced with an `if` that raises `ValueError` |
| Mutable default argument (Pylint W0102) | Bug | 8 | `extras={}` is shared across calls | Default `None`, create a new dict inside the function |
| Redefined outer name `conn` (Pylint W0621) | Design | 4, 8, 18, 26 | Global `conn` shadowed by function parameters | Moved connection creation into `create_connection()` and call it in `main()` |
| Ambiguous name `l` and missing spaces (Flake8 E741, E225) | Style | 28 | Variable `l` looks like `1`, and `l=min(...)` lacks spaces | Renamed to `rare`, added spaces |
| camelCase names (Pylint C0103) | Style | 8, 14, 18 | Not snake_case | Renamed to `log_sighting`, `observer_id`, `zone_summary` |
| Missing docstrings (Pylint C0114, C0116) | Docs | 1, 8, 14, 18, 26, 32 | No module or function docstrings | Added docstrings |
| Unnecessary `else` after `return` (Pylint R1705) | Refactor | 20 | Redundant `else` | Removed it |
| Long lines (Flake8 E501, Pylint C0301) | Style | 5, 9, 19, 27 | Lines over 79 characters | Wrapped long lines |
| f-string suggestion (Pylint C0209) | Style | 9 | String `.format()` used | Resolved by the parameterized query |
| `main()` runs on import | Best practice | 40 | Script runs when imported | Added `if __name__ == "__main__":` guard |
