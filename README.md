# Pemystack Regressor

AI-powered regression detection for every PR. Analyzes code changes against known bug patterns and flags potential regressions before they ship.

## Quick start

Add to `.github/workflows/regressor.yml`:

```yaml
name: Regressor

on:
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  regressor:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: pemystack/regressor-action@v1
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          # Provide ONE of these:
          anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}
          # openai_api_key: ${{ secrets.OPENAI_API_KEY }}
          # gemini_api_key: ${{ secrets.GEMINI_API_KEY }}
```

## What it does

1. Reads the PR diff
2. AI analyzes changed code for regression risk patterns
3. Checks against known bug patterns (null safety, auth bypasses, concurrency issues, etc.)
4. Posts a risk assessment as a PR comment

## Supported languages

Works with any language — risk analysis is based on code change patterns, not language-specific tooling.

## Free plan

- 20 reviews/month
- Public repos
- Basic risk analysis
- [Upgrade to Pro](https://github.com/marketplace/pemystack) for unlimited reviews and private repos

## Inputs

| Input | Required | Description |
|-------|----------|-------------|
| `github_token` | Yes | GitHub token for PR comments |
| `anthropic_api_key` | One of three | Anthropic (Claude) API key |
| `openai_api_key` | One of three | OpenAI (GPT) API key |
| `gemini_api_key` | One of three | Google (Gemini) API key |

## License

MIT
