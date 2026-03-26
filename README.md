# Claude Code Dev Container

A ready-to-use development container with Claude Code pre-installed. Open any project inside this container and get Claude Code's VS Code extension running in a sandboxed environment — no manual installation needed.

## What You Get

When you open a project in this dev container, it automatically sets up:

- **Claude Code extension** in the VS Code sidebar (the �sparkles icon)
- **Node.js 20** with npm
- **Git**, GitHub CLI, and common dev tools
- **ZSH** shell with productivity enhancements
- **Persistent config** — your Claude settings and command history survive container restarts

---

## Prerequisites

You only need to install these once on your machine.

### 1. Install Docker Desktop

Download and install from [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop/).

> **Important:** Docker Desktop must be **running** (look for the whale icon in your menu bar/system tray) before you open a dev container.

### 2. Install VS Code

Download and install from [code.visualstudio.com](https://code.visualstudio.com/).

### 3. Install the Dev Containers Extension

Open VS Code, go to the Extensions panel (`Cmd+Shift+X` on Mac / `Ctrl+Shift+X` on Windows), search for **"Dev Containers"** by Microsoft, and click **Install**.

### 4. Have a Claude Code Subscription

You need an Anthropic account with a Claude Max or Team plan. Sign up at [claude.ai](https://claude.ai) if you haven't already.

---

## Quick Start — Using This Repo Directly

### Step 1: Clone the Repository

**Option A — Using the terminal:**

```bash
git clone https://github.com/YOUR-ORG/claude-code-dev-container.git
```

**Option B — Download as ZIP:**

Click the green **"Code"** button on GitHub → **"Download ZIP"** → Unzip the folder.

> **macOS tip:** The `.devcontainer` folder is hidden by default. Press `Cmd+Shift+.` in Finder to reveal it.

### Step 2: Open in VS Code

Open the cloned/unzipped folder in VS Code:

- Drag the folder onto the VS Code icon, **or**
- In VS Code: `File → Open Folder` and select the project folder

### Step 3: Reopen in Container

VS Code will detect the `.devcontainer` folder and show a popup in the bottom-right corner:

> **"Folder contains a Dev Container configuration file. Reopen folder to develop in a container."**

Click **"Reopen in Container"**.

If you miss the popup, press `Cmd+Shift+P` (Mac) or `Ctrl+Shift+P` (Windows/Linux) and type:

```
Dev Containers: Reopen in Container
```

### Step 4: Wait for the Build

The first time you open the container, it needs to build the Docker image. This takes **2–5 minutes** depending on your internet speed. Subsequent starts are much faster (a few seconds).

You can watch the progress by clicking **"Starting Dev Container (show log)"** in the bottom-right notification.

### Step 5: Start Using Claude Code

Once the container is running:

1. Look for the **Claude Code icon** (✨ spark) in the left sidebar
2. Click it to open the Claude Code panel
3. Sign in with your Anthropic account when prompted
4. Start chatting with Claude about your code

You can also open the integrated terminal (`Ctrl+`` `) and run `claude` directly from the command line.

---

## Adding This Dev Container to Your Own Project

If you have an existing project and want to add the same dev container setup:

### Option A: Copy the Folder (Simplest)

1. Download or clone this repo
2. Copy the **entire `.devcontainer` folder** into the **root** of your project:

```
your-project/
├── .devcontainer/       ← copy this folder here
│   ├── devcontainer.json
│   └── Dockerfile
├── src/
├── package.json
└── ...
```

3. Open your project in VS Code → click **"Reopen in Container"**

### Option B: Use as a GitHub Template

If this repo is set up as a **GitHub Template Repository**:

1. Go to the repo on GitHub
2. Click **"Use this template"** → **"Create a new repository"**
3. Name your new repo and clone it
4. Your new project already includes the `.devcontainer` folder

### Option C: Use GitHub Codespaces (No Local Setup Needed)

If you don't want to install Docker locally:

1. Go to the repo on GitHub
2. Click **"Code"** → **"Codespaces"** → **"Create codespace on main"**
3. A full VS Code environment opens in your browser with everything pre-configured

> **Note:** GitHub Codespaces has a free tier (60 hours/month on personal accounts). Beyond that, usage is billed.

---

## Day-to-Day Usage

### Starting the Container

After the first build, just open the project folder in VS Code. It will automatically reconnect to the container. If it doesn't, use `Cmd+Shift+P` → **"Dev Containers: Reopen in Container"**.

### Stopping the Container

Simply close VS Code. The container stops automatically. Your files and settings are preserved.

### Rebuilding the Container

If you change `devcontainer.json` or `Dockerfile`, you need to rebuild:

`Cmd+Shift+P` → **"Dev Containers: Rebuild Container"**

For a clean rebuild (e.g., after major config changes):

`Cmd+Shift+P` → **"Dev Containers: Rebuild Without Cache and Reopen in Container"**

---

## Troubleshooting

### I can't see the `.devcontainer` folder

Files starting with a dot are hidden by default on macOS. Press **`Cmd+Shift+.`** in Finder to toggle hidden files.

On Windows, in File Explorer go to **View → Show → Hidden items**.

### The container fails to start

1. Make sure **Docker Desktop is running** (check for the whale icon)
2. Try rebuilding: `Cmd+Shift+P` → **"Dev Containers: Rebuild Without Cache and Reopen in Container"**
3. If that doesn't work, remove the old container manually:
   ```bash
   docker ps -a  # find the container ID
   docker rm -f <container-id>
   ```
   Then reopen in VS Code.

### Claude Code extension isn't showing up

1. Wait for the container to fully finish building (watch the log)
2. Try reloading the window: `Cmd+Shift+P` → **"Developer: Reload Window"**
3. Check that `"anthropic.claude-code"` is listed in the extensions section of `devcontainer.json`

### Claude Code asks me to sign in every time

Make sure your `devcontainer.json` includes the volume mount for Claude config:

```json
"mounts": [
  "source=claude-code-config-${devcontainerId},target=/home/node/.claude,type=volume"
]
```

This persists your authentication between container restarts.

---

## Project Structure

```
.devcontainer/
├── devcontainer.json    # Container settings, extensions, mounts
└── Dockerfile           # Container image definition and tools
```

| File | Purpose |
|------|---------|
| `devcontainer.json` | Configures VS Code extensions, settings, environment variables, and volume mounts |
| `Dockerfile` | Defines the base image (Node.js 20), installs dev tools (git, zsh, fzf), and sets up the shell |

---

## What's Inside the Container

| Tool | Version | Purpose |
|------|---------|---------|
| Node.js | 20.x | Runtime for Claude Code |
| Claude Code | Latest | AI coding assistant (extension + CLI) |
| Git | Latest | Version control |
| GitHub CLI | Latest | GitHub operations from terminal |
| ZSH + Oh My ZSH | Latest | Enhanced shell experience |
| fzf | Latest | Fuzzy file finder |

---

## Need Help?

- **Claude Code docs:** [docs.anthropic.com/claude-code](https://docs.anthropic.com/en/docs/claude-code)
- **Dev Containers docs:** [code.visualstudio.com/docs/devcontainers](https://code.visualstudio.com/docs/devcontainers/containers)
- **Docker Desktop:** [docs.docker.com/desktop](https://docs.docker.com/desktop/)
