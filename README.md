🧩 Description

This Bash script automatically checks whether .dk domains (or any other top-level domain) are available or taken, based on combinations of letters and numbers.
It queries the official Punktum.dk WHOIS server directly, ensuring accurate results for Danish domains.

The script supports:
	•	✅ Custom domain endings (e.g., .dk, .com, .net)
	•	✅ Adjustable rate limit (SLEEP_TIME) to stay within WHOIS query limits (e.g., 1 request per second)
	•	✅ Configurable minimum and maximum domain length (MIN_LENGTH and MAX_LENGTH)
	•	✅ Letters and digits (a–z, 0–9) for generating combinations
	•	✅ Automatic recursive domain generation (no manual nested loops)
	•	✅ Separate result files for free and taken domains
	•	✅ Progress output while running

Each domain is checked via the WHOIS server.
If the output includes the line "No entries found for the selected source.", the domain is considered free, otherwise taken.

⸻

⚙️ How It Works
	1.	The script defines a set of valid characters: all lowercase letters (a–z) and numbers (0–9).
	2.	It then generates every possible combination of these characters within the defined MIN_LENGTH and MAX_LENGTH range.
	3.	For each generated domain, it performs a WHOIS lookup via:
