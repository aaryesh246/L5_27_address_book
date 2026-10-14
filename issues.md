# Static Code Analysis Issues

## Original Bandit Findings

The following issues were identified in the original `address_book.py` source based on the Bandit report.

| No. | Issue / Bandit ID | Type | Location reported | Severity | Description | Fix approach |
|---:|---|---|---|---|---|---|
| 1 | `B403: blacklist` — `pickle` import | Security | `address_book.py:3:0` | Low | Bandit flags importing `pickle` because pickle can be unsafe when used to deserialize untrusted data. | Replace pickle-based backup and restoration with JSON serialization where possible. |
| 2 | `B105: hardcoded_password_string` | Security | `address_book.py:6:16` | Low | The hard-coded string `contacts-demo` is assigned to `SYNC_PASSWORD`. | Remove the constant if it is unused. If a real password is required, load it from an appropriate secret-management mechanism rather than hard-coding it. |
| 3 | `B324: hashlib` — weak MD5 hash | Security | `address_book.py:19:11` | High | `contactId()` uses MD5 to generate a contact ID. Bandit warns that MD5 is a weak hash algorithm. | Use SHA-256 or another suitable approach. If retaining a shortened hash, be aware that collisions are possible and do not use it as a security credential. |
| 4 | `B301: pickle` deserialization | Security | `address_book.py:67:15` | Medium | `pickle.load()` is used to restore the backup. Deserializing untrusted pickle data can execute malicious code. | Replace pickle serialization/deserialization with JSON for the simple contact data, or ensure only trusted data is loaded. |

## Notes

- These are the four findings visible in the provided Bandit report. Pylint and Flake8 may report additional issues; include those separately if they appear in their reports.
- The `pickle` import warning (`B403`) and the `pickle.load()` warning (`B301`) are related but refer to different locations and risks.
- After applying fixes, rerun Bandit and update this document with the final verification results. Do not mark an issue as fixed until the updated report confirms the relevant finding is gone.
- The screenshot also shows a PowerShell `NativeCommandError`/redirection message in the report. That is command-output handling, not one of the four Bandit security findings. Run the command directly in the terminal to inspect the output, or use `2> bandit_errors.txt` if you need to capture standard error separately.
