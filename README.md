# pi-quota-display

[Pi](https://pi.dev) extension that shows your OpenAI Codex or GitHub Copilot quota in the footer.

## Features

- shows available Codex quota windows (for example 5h and/or weekly)
- shows the number of banked Codex resets when available
- shows GitHub Copilot monthly quota as used vs. goal
- uses your existing pi `/login`
- keeps the weekly Codex reset countdown current in the footer

## Setup

1. Install the extension:
   ```bash
   pi install git:github.com/fxwin/pi-quota-display
   ```

2. Reload pi:
   ```bash
   /reload
   ```

3. Log in to the providers you use:
   - For OpenAI quota, run `/login openai-codex` and sign in to your ChatGPT account. That login is what the usage endpoint accepts for both `openai-codex` and `openai` models. If that access token expires while the login session is still valid, the extension refreshes it automatically. Log in again only if the refresh fails.
   - For GitHub Copilot quota, run `/login github-copilot`.

## Provider-specific quota

The footer displays quota for the active model's provider, not all logged-in accounts at once.

- An OAuth model under `openai-codex` or `openai` shows the 5-hour and weekly Codex windows from the `openai-codex` login, plus banked resets. Sign in with ChatGPT tokens are rejected by the usage endpoint, so `openai` models use that same Codex login.
- An OAuth model under `github-copilot` shows that Copilot account's monthly premium-interaction quota.
- API-key models and other providers do not show subscription quota.

Both OpenAI providers need `/login openai-codex`. If no Codex login is available, use `/quota` to see the error.

## Commands

```text
/quota
/quota reset
```

`/quota reset` refreshes the available banked resets, lets you choose one by expiration date, asks for confirmation, and then refreshes the displayed quota.
