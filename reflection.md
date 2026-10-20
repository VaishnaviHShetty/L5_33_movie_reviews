# Reflection

**1. Which tool was most useful, and why?**
For me Bandit was the most useful, because it found the problems that could actually cause harm: the weak MD5 hash, the server bound to 0.0.0.0, the hardcoded password and the insecure random function. Pylint and Flake8 never mentioned any of these. Pylint helped the most with readability, since it took my score from 5.47 to 10.00, and Flake8 was the quickest and easiest to fix.

**2. Did you find any false positives or findings you disagreed with?**
The MD5 warning felt like a false positive to me, because the hash is only used to make a short review id and not to protect anything. Instead of changing the algorithm and changing every id, I kept MD5 and marked it as not security-related. I also think the random.choice warning is very low risk for picking a featured movie, but switching to secrets.choice was a one-word change, so I did it anyway.

**3. How did you prioritise fixes?**
I started with Bandit because security issues matter most, and I did the High and Medium ones first. Flake8 came next because those were simple formatting fixes, and I left Pylint for last because it needed the most edits (renaming functions, adding docstrings, removing the global). I made one commit per tool so each change is easy to see and review.

**4. How does static analysis improve code quality and maintainability?**
It checks code without running it, so it finds problems early and consistently. Everyone on a team gets the same rules, which makes code easier to read and review. I also saw it catch a small mistake of my own: while applying the fixes I saved a file without a final newline, and Flake8 flagged it straight away (W292). It cannot replace testing, though. These tools would still pass code with a wrong average calculation, so tests are still needed.
