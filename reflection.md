# Reflection

1. **Which issues were the easiest and which the hardest to fix?**
   Naming, docstrings, the `else` after `return` and line lengths were mechanical. The hardest was the MD5 finding, because the right fix depends on what the hash is for. Here it is only a short observer label, so `usedforsecurity=False` is honest; if it protected anything sensitive I would switch to SHA-256 and the printed ID would change.

2. **Did the tools report any false positives?**
   The MD5 warning is arguably one, since the ID is not security-sensitive, but it is still worth marking explicitly. The Pylint redefined-outer-name warnings were a real design smell rather than a false alarm.

3. **How would you integrate static analysis into your workflow?**
   Run Flake8, Pylint and Bandit in a pre-commit hook and in CI (for example GitHub Actions), failing the build on any Bandit finding or a Pylint score below a threshold such as 9.5.

4. **What tangible improvements did you see?**
   Pylint went from 3.46 to 10.00, Bandit findings from 3 to 0 and Flake8 warnings from 6 to 0. The code no longer has an SQL injection hole or a shared-default bug, and it is easier to read and test.
