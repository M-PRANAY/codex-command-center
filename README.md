# Codex Command Center

A local web dashboard for launching, monitoring, and continuing Codex CLI work. It is designed as a lightweight, local-first alternative to a task board plus Codex activity view.

## What it does

- Launches dashboard-owned Codex work with `codex exec --json`.
- Lets you choose GPT-5.6 Sol, Terra, Luna, or your CLI default for new dashboard runs.
- Shows live event updates and lets you stop dashboard-owned runs, terminating their complete process tree.
- Detects local `codex` executable processes and displays a live process count.
- Watches normal Codex CLI session files under `%USERPROFILE%\.codex\sessions`.
- Opens a local transcript for CLI sessions, including user prompts, Codex responses, and recorded tool activity; open transcripts refresh as new activity is recorded.
- Sends a follow-up from the transcript window by running `codex exec resume <session-id> <prompt>`.
- Includes a small browser-local task board. Board tasks are stored in `localStorage`.

## Run locally

Prerequisites: Node.js and the Codex CLI installed and signed in.

```powershell
cd C:\Users\Pranay\Desktop\codex-command-center
npm start
```

Open `http://127.0.0.1:4173`.

## Follow-up behavior

The **Send follow-up** box does not inject keystrokes into an existing terminal. It resumes that saved Codex conversation in a dashboard-owned process. This preserves the conversation context and makes the resulting progress visible in the dashboard.

Do not send a follow-up while the original terminal session is actively making changes in the same workspace. Two concurrent agents can conflict with each other.

## Privacy and scope

The dashboard binds only to `127.0.0.1`. Session transcripts are read locally from your Codex session files and are returned only to your local browser. It does not upload session prompts, responses, or process data.

## Limitations

- A Codex process count is not the same as a task count; Codex may create helper processes.
- Only sessions recently written within the last 12 hours are listed.
- The dashboard can stop runs it started by terminating their process tree. It does not control another terminal's stdin, approvals, or terminal UI.
- Remote `codex --remote` / app-server mode is not required for dashboard runs and is intentionally not used by default.
