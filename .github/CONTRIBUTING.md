# Contributing to AI SQL Agent

The AI SQL Agent monitors data pipelines, diagnoses failures with Claude, generates SQL fixes, and posts plain-English explanations to Slack. Contributions are welcome for new error patterns, additional warehouse support, and improved Slack formatting.

## Local Setup

```bash
git clone https://github.com/Snehabankapalli/ai-sql-agent-for-data-analytics-automation.git
cd ai-sql-agent-for-data-analytics-automation

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

pip install -r requirements.txt
```

Create a `.env` file:

```env
ANTHROPIC_API_KEY=sk-ant-...
SNOWFLAKE_ACCOUNT=...
SNOWFLAKE_USER=...
SNOWFLAKE_PASSWORD=...
SNOWFLAKE_WAREHOUSE=...
SLACK_BOT_TOKEN=xoxb-...
SLACK_CHANNEL=#data-alerts
```

All keys are required for an end-to-end run. Unit tests mock external clients and do not require real credentials.

## Development Workflow

1. Branch from `main`, for example `feat/schema-drift-detector`.
2. Write a failing test under `tests/` that describes the new behavior.
3. Implement the change in `src/`.
4. Run the full test suite.
5. Open a pull request with a short summary and a sample Slack message screenshot when output format changes.

## Code Standards

- `black` for formatting
- `ruff` for linting
- Type hints on all public functions
- Docstrings on every analyzer and notifier class
- No hardcoded table names, channel IDs, or prompts in source
- Prompts live under `src/prompts/` and are versioned

## Testing

```bash
pytest tests/ --cov=src --cov-report=term-missing -v
```

Guidelines:

- Mock the Anthropic client, Snowflake connector, and Slack client.
- Cover every supported error pattern with at least one test.
- Include regression tests for any bug fix.

## Pull Request Checklist

- [ ] Tests added, all passing
- [ ] Coverage not reduced
- [ ] `black` and `ruff` clean
- [ ] No secrets committed
- [ ] README updated if CLI flags or env vars changed
- [ ] Example Slack output included in PR description when relevant

## Reporting Bugs

Open an issue with:

- Exact pipeline error message, redacted
- Warehouse type and version
- Agent version or commit SHA
- Python version and OS
- Full stack trace

## Security

Do not commit `.env`, Snowflake credentials, or Slack tokens. Report security issues privately through the maintainer email on the GitHub profile.
