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

### 4. GitHub commit history (blurred / 提交记录模糊设置)

The repo’s **commit history** on GitHub may show author names, tool identifiers (e.g. cursoragent), and commit messages (e.g. "chore: refine README to competition-only display"). To keep this info **obscured for evaluation**:

- **In the submission post** (see `MOLTBOOK_POST.md`): A note for evaluators states that commit author names and messages are to be treated as **anonymized / blurred** and not used for identity attribution.
- **Optional**: Use a pseudonymous GitHub account and/or set Git `user.name` / `user.email` to a handle when committing, so the history does not expose your real name.
- **Intent**: Author and commit text in the repo are for display only; evaluators should treat them as non-identifying (模糊处理，不用于身份识别).

---

## 删除旧仓库并用新仓库重新提交 (Delete old repo and resubmit)

出于隐私保护，若希望**删除当前 GitHub 仓库并重新用新仓库提交**，按以下步骤操作。

### 第一步：在 GitHub 上删除旧仓库

1. 登录 GitHub，打开仓库：`https://github.com/FinIR2020/usdc-agentic-commerce`
2. 点击 **Settings**（仓库顶部菜单）
3. 滚动到页面最底部的 **Danger Zone**
4. 点击 **Delete this repository**
5. 按提示输入仓库名 `FinIR2020/usdc-agentic-commerce` 确认删除

删除后，该 URL 将失效，提交记录（含作者名等）不再公开可查。

### 第二步：创建新仓库（建议用化名账号）

- **选项 A**：用**当前账号**新建一个空仓库（如 `usdc-agentic-commerce` 或其它名称），不导入旧仓库内容。
- **选项 B（推荐）**：用**化名/小号 GitHub 账号**新建仓库，提交记录与主身份脱钩。

在 GitHub 网页：**Your repositories** → **New** → 填写 Repository name，选 **Public**，**不要**勾选 "Add a README"（保持空仓库）→ **Create repository**。

### 第三步：本地改远程地址并推送

在本地项目目录（如 `usdc_hackthon`）执行：

```bash
# 查看当前远程（应是 origin → 旧仓库）
git remote -v

# 删除旧远程
git remote remove origin

# 添加新仓库地址（把 YOUR_USERNAME 和 NEW_REPO_NAME 换成你的新仓库）
git remote add origin https://github.com/YOUR_USERNAME/NEW_REPO_NAME.git

# 推送（若新仓库是空的，一般用 main 或 master）
git push -u origin main
```

若本地默认分支是 `master`，把上面最后一句改为 `git push -u origin master`。推送后新仓库里会有当前所有文件；**历史提交仍会保留**（作者名仍可能是你本机 Git 配置的 `user.name`）。

### 第四步：（可选）用化名提交历史

若希望**新仓库的提交记录里不出现真实姓名**，可在推送前重写作者信息（仅限尚未推送或可强制覆盖的情况）：

```bash
# 仅对当前仓库设置化名（不改全局）
git config user.name "你的化名或英文昵称"
git config user.email "与 GitHub 账号关联的邮箱或 noreply 邮箱"

# 之后的新提交会使用上述名字；已有提交需用 git filter-branch 或 BFG 重写（较复杂）
```

若已推送过，新仓库会带上原有提交历史；若**完全不要历史**，可以只推送当前文件（无历史）：

```bash
# 在新仓库目录或临时目录
git init
git add .
git commit -m "Initial commit: USDC Agentic Commerce skill"
git remote add origin https://github.com/YOUR_USERNAME/NEW_REPO_NAME.git
git branch -M main
git push -u origin main
```

（在**新文件夹**里复制项目文件再执行上述命令，可得到无历史的新仓库。）

### 第五步：替换文档中的仓库 URL

创建并推送新仓库后，把项目中**所有**旧 URL 替换为新 URL：

| 旧 URL | 替换为 |
|--------|--------|
| `https://github.com/FinIR2020/usdc-agentic-commerce` | `https://github.com/YOUR_USERNAME/NEW_REPO_NAME` |

需要替换的文件（当前项目）：

- `MOLTBOOK_POST.md` — 多处，用编辑器的「全部替换」将旧 URL 改为新 URL

替换完成后，从 `MOLTBOOK_POST.md` 复制内容到 Moltbook 发帖即可，Repo URL 填写新仓库地址。

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
