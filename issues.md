# Issue Table: movie_reviews.py

Baseline (original file): Pylint 5.47/10, Bandit 4 issues (1 High, 1 Medium, 2 Low), Flake8 4 issues.
After fixes: Pylint 10.00/10, Bandit 0 issues, Flake8 0 issues.

| Issue | Type | Line(s) | Description | Fix Approach |
| ----- | ---- | ------- | ----------- | ------------ |
| Weak MD5 hash (B324) | Security (High) | 46 | `hashlib.md5()` flagged as a weak hash for security use | Pass `usedforsecurity=False`, because the hash is only a short display id; ids stay unchanged |
| Bind to all interfaces (B104) | Security (Medium) | 4 | `STREAM_HOST = "0.0.0.0"` exposes the service on every network interface | Default to `127.0.0.1`, overridable through the `STREAM_HOST` environment variable |
| Hardcoded password (B105) | Security (Low) | 6 | `MODERATOR_PASSWORD = "reviews-demo"` stored in source code | Read it from the `MODERATOR_PASSWORD` environment variable |
| Insecure random generator (B311) | Security (Low) | 41 | `random.choice` is not cryptographically secure | Use `secrets.choice` |
| Missing whitespace around operator (E225) | Style | 35 | `ranked=sorted(...)` | `ranked = sorted(...)` |
| Expected 2 blank lines (E302) | Style | 48 | Only one blank line before a function definition | Two blank lines between functions |
| Inline comment spacing (E261) | Style | 70 | One space before `# demo id` | Two spaces before `#` |
| Missing whitespace after comma (E231) | Style | 72 | `"Genres:",sorted(...)` | Add a space after the comma |
| No newline at end of file (W292) | Style | 79 | File saved without a trailing newline while applying fixes | Added a trailing newline |
| Invalid names (C0103) | Convention | 11, 16, 26, 34, 39, 45, 48, 54 | camelCase function and argument names such as `addMovie` and `reviewText` | Renamed to snake_case (`add_movie`, `review_text`, ...) |
| Constant name (C0103) | Convention | 8 | Module-level `featured` does not follow UPPER_CASE | Removed the variable, since `pick_featured()` just returns the choice |
| Missing docstrings (C0114, C0116) | Convention | 1, 11, 16, 26, 34, 39, 45, 48, 54, 58 | No module or function docstrings | Added docstrings |
| Global statement (W0603) | Warning | 40 | `global featured` modified module state | Removed the global |
| Unnecessary else after return (R1705) | Refactor | 28 | `else` after `return` in `averageRating` | Removed the `else` and de-indented |
| Iterating with range(len()) (C0200) | Refactor | 50 | Index-based loop in `printAllReviews` | `for i, title in enumerate(movies, start=1)` |
| Code runs on import | Design | end of file | `main()` called at module level | Added `if __name__ == "__main__":` |

Behaviour is unchanged, except the stream address now prints `127.0.0.1:8000` (intentional security fix).
