# Reflection

**1. Which tool was most useful, and why?**
Bandit was the most useful for real risk. It caught the High-severity MD5 usage and the all-interfaces network bind, which Pylint and Flake8 cannot detect. Pylint gave the biggest quality improvement (5.47 to 10.00), and Flake8 was the quickest to fix.

**2. Did you find any false positives or findings you disagreed with?**
The MD5 warning is arguably a false positive here, because the hash is only a short display id and not used for security. I kept MD5 but marked it `usedforsecurity=False`, so existing ids do not change. The `random.choice` warning is also low risk for picking a featured movie, but `secrets.choice` costs nothing.

**3. How did you prioritise fixes?**
By severity. Bandit High and Medium came first (MD5, 0.0.0.0), then the Low security items (hardcoded password, random generator), then Flake8 formatting, and finally Pylint warnings and refactors. Each tool got its own commit, so the history is easy to review.

**4. How does static analysis improve code quality and maintainability?**
It finds bugs, insecure patterns and style problems without running the program. It enforces one standard across a team, makes code review faster, and can run automatically in CI. It does not replace tests: all three tools could pass code with a wrong average calculation.
