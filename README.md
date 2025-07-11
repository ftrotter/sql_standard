NDH SQL Naming Convention Enforcement with SQLFluff
=========

This document outlines which naming conventions from the style guide can or cannot currently be enforced using SQLFluff, and provides configuration settings for enforceable rules.

⸻

❌ Rules Not Currently Enforceable by SQLFluff
------

These require either a custom rule, external linter, or manual review:
	•	Use full English words, not abbreviations
	•	Don’t use data types as names
	•	Use singular nouns for table names
	•	Primary key should be named id
	•	Foreign keys should follow the pattern <table>_id
	•	Name indexes explicitly with table and column
	•	Name constraints clearly

⸻

✅ Rules Enforceable by SQLFluff
------

These can be configured using standard SQLFluff rules:
	•	Avoid quoted identifiers
→ L014: Discourages use of quoted identifiers.
	•	Use all lowercase for identifiers
→ L010: Enforces case on keywords and identifiers.
	•	Use underscores to separate words (snake_case)
→ L040: Enforces naming convention patterns.
	•	Avoid reserved words as identifiers
→ L036: Detects use of reserved keywords as identifiers.

⸻

✅ .sqlfluff Configuration
----

```conf
[sqlfluff]
dialect = postgres

[sqlfluff:rules]
exclude_rules = L009  # Optional: skip alias prefixing if undesired

[sqlfluff:rules:L010]
capitalisation_policy = lower  # Force lowercase for identifiers

[sqlfluff:rules:L014]
extended_capitalisation_policy = lower  # Reinforce lowercase for quoted identifiers
ignore_words = ''  # Do not allow any exceptions

[sqlfluff:rules:L036]
# No config needed — enabled by default

[sqlfluff:rules:L040]
capitalisation_policy = lower
naming_convention = snake_case
```

