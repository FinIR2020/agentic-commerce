# Privacy Protection Guide — Submitting to Moltbook Safely

This guide helps you submit this project to Moltbook without exposing personal information from your computer or identity.

---

## Recommended Strategy: Minimal Exposure

### 1. Submit Without Running OpenClaw Locally

You do **not** need OpenClaw running to submit to Moltbook.

- **Moltbook web UI**: Go to [m/usdc](https://www.moltbook.com/m/usdc), create a new post, paste content from `MOLTBOOK_POST.md`.
- **Replace** `[YOUR_REPO_URL]` with your public GitHub or GitPad URL only.
- **No local paths, usernames, or machine info** should appear in the post.

This keeps your submission entirely in the browser; Moltbook does not need access to your filesystem.

### 2. Use a Pseudonymous or Separate GitHub Account (Optional)

If you prefer not to link your main identity:

- Create a GitHub account with a pseudonym or handle used only for hackathons.
- Push this repo to that account.
- Use that repo URL in your Moltbook post.

### 3. Content You Must Never Include

Before posting, ensure your content does **not** contain:

- Local file paths (e.g. `/Users/yourname/Desktop/...`, `C:\Users\...`)
- Your real username, machine name, or hostname
- Mac/PC model or OS version
- API keys, private keys, or credentials
- Email or other contact info (unless you intentionally share it)

The skill's Safety Checklist already instructs agents to avoid including such data in outputs.

---

## Optional: Run OpenClaw in Docker for Testing

If you want to **test** the skill with OpenClaw before submitting, use Docker to isolate the environment and limit what the agent can access.

### Step 1: Install OpenClaw in Docker

```bash
git clone https://github.com/openclaw/openclaw
cd openclaw
./docker-setup.sh
```

### Step 2: Mount Only This Project

By default, OpenClaw Docker mounts:

- `~/.openclaw` — config, memory, API keys
- `~/openclaw/workspace` — agent-accessible files

**Privacy-safe approach**: Put **only** this hackathon project in the workspace:

```bash
mkdir -p ~/openclaw/workspace
cp -r /path/to/usdc_hackthon/* ~/openclaw/workspace/
```

Or use `OPENCLAW_EXTRA_MOUNTS` to mount only the project folder (adjust paths for your system):

```bash
export OPENCLAW_EXTRA_MOUNTS="$HOME/path/to/usdc_hackthon:/home/node/workspace:rw"
./docker-setup.sh
```

The agent will then see only this project, not your full home directory.

### Step 3: Test the Skill Inside the Container

- Copy `skills/usdc-agentic-commerce/` into the workspace.
- Ask the agent: *"How do I pay 10 USDC to an agent on testnet?"*
- Verify the response matches the skill's output conventions (amount, recipient, purpose, "Testnet only").

### Step 4: Submit via Web (Not from the Agent)

When ready to submit, use the Moltbook web UI in your browser. Do not have the agent post on your behalf from inside the container unless you are comfortable with the agent having Moltbook API access.

---

## Alternative: Submit from a Cloud VM

For maximum isolation:

1. Deploy this repo to a cloud VM (Hetzner, Railway, GCP, etc.).
2. Run OpenClaw in Docker on the VM (see [Hetzner Docker VPS](https://docs.clawd.bot/install/hetzner)).
3. Test and submit from the VM. Your personal machine is never involved.

---

## Checklist Before Posting

- [ ] Replaced `[YOUR_REPO_URL]` with your public repo URL (no local paths)
- [ ] No usernames, paths, or machine identifiers in the post content
- [ ] Repo is public and contains only project files (no sensitive data)
- [ ] Post title starts with `#USDCHackathon ProjectSubmission AgenticCommerce`
- [ ] Submitted via Moltbook web UI or API (not from an agent session that might leak context)

---

## Summary

| Action                    | Privacy Benefit                         |
|---------------------------|-----------------------------------------|
| Submit via Moltbook web   | No local files or paths exposed         |
| Use pseudonymous repo URL | Decouples submission from identity      |
| Docker + project-only mount | Agent sees only this project          |
| Cloud VM submission       | Personal machine never involved         |
| Follow Safety Checklist   | Skill avoids leaking user data in output |

Good luck with your submission.
