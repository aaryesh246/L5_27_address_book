# Lab 5: Static Code Analysis — Reflection

## 1. What is static code analysis, and why is it useful?

Static code analysis examines source code without executing the program. It helps identify potential programming errors, security weaknesses, and coding-style violations early in development. This makes code easier to maintain and helps developers address problems before deployment.

## 2. What is the difference between Pylint, Bandit, and Flake8?

Pylint checks general Python code quality, including naming conventions, missing docstrings, and potential programming issues. Bandit checks for common security risks in Python code. Flake8 checks style and formatting issues, such as whitespace, blank lines, and line length. Using all three tools provides complementary checks.

## 3. What issues were identified and how were they addressed?

The original Bandit report identified four findings: importing `pickle`, a hard-coded password-like string, use of MD5, and use of `pickle.load()` to restore data. The code was updated to remove the unnecessary hard-coded value, use SHA-256 for contact ID generation, and replace pickle-based backup and restoration with JSON. The code was also updated to use clearer `snake_case` names, include docstrings, specify UTF-8 encoding for file operations, and improve formatting.

## 4. How does static code analysis improve software quality?

Static analysis helps improve consistency, readability, and maintainability by identifying issues without requiring the program to be run. Security analysis can also highlight potentially unsafe coding patterns. However, static analysis does not replace testing or code review, so the program was also executed to check that contact management and backup restoration continued to work.

## Verification

After making the changes, the program was run and its output showed that three contacts were restored and that the restored contacts matched the in-memory address book. Bandit subsequently reported no issues. Pylint and Flake8 were rerun to identify remaining quality and formatting findings; their final results should be recorded after the latest version of `address_book.py` has been checked.
