# 🧭 YATT — Yet Another Task Tracker

A simple yet powerful **command-line time & project tracker**, written entirely in Bash.  
Manage projects, submodules, tags, and track your work sessions — all from your terminal.

---

## ✨ Features

- 🗂️ **Project Management** — Create, list, and remove projects
- 🧩 **Submodules** — Organize components or microservices under projects
- 🏷️ **Tags** — Add, remove, and filter entities by tags
- ⏱️ **Time Tracking** — Start, stop, and report on tracked work sessions
- 📊 **Reports** — Filter sessions by project, module, tag, or date
- 🎨 **Colored Output** — Clean, readable terminal messages
- 💡 **Auto Completion** — Built-in Bash completion for faster commands

---

## 🚀 Installation

Clone the repository and make `yatt` executable:

```bash
git clone https://github.com/<your-username>/yatt.git
cd yatt
chmod +x yatt
sudo mv yatt /usr/local/bin/
````

Now you can use it anywhere:

```bash
yatt help
```

### 🧠 Enable Bash Completion

Generate and enable command completion:

```bash
yatt completion > /etc/bash_completion.d/yatt
source /etc/bash_completion.d/yatt
```

---

## 🧱 Directory Structure

YATT keeps its data under your home directory:

```
~/.yatt/
├── projects/
│   ├── myapp.json
│   └── another_project.json
└── tracking.json
```

---

## 🧩 Usage

### 🆕 Create & Manage Projects

```bash
yatt project create myapp "Main backend project"
yatt project list
yatt project remove myapp
```

### 🧩 Submodules

```bash
yatt submodule create auth@myapp "Authentication service"
yatt submodule list myapp
yatt submodule remove auth@myapp
```

### 🏷️ Tag Management

```bash
yatt project tags add myapp backend
yatt project tags list myapp
yatt project tags remove myapp backend
yatt project tags by backend
```

### ⏱️ Time Tracking

```bash
yatt track start myapp
# ...work...
yatt track stop
yatt track status
yatt track list
```

### 📈 Reports

```bash
# Today's report
yatt track report

# Report by date
yatt track report 2025-10-23

# Filter by project
yatt track report myapp

# Filter by tag
yatt track report tag:backend
```

---

## 🧭 Example Workflow

```bash
# Create project and submodule
yatt project create myapp "Main backend service"
yatt submodule create api@myapp "REST API module"

# Add tags
yatt project tags add myapp backend
yatt project tags add api@myapp golang

# Track work
yatt track start api@myapp
# ... do some work ...
yatt track stop

# Generate report
yatt track report tag:golang
```

Output example:

```
✅ Stopped tracking 'api@myapp'. Duration: 01:32:45
📊 Report for 2025-10-23:
  - api@myapp: 1h 32m 45s
```

---

## ⚙️ Dependencies

Make sure these tools are installed:

| Tool        | Purpose           | Install command       |
| ----------- | ----------------- | --------------------- |
| `bash`      | Script runtime    | built-in              |
| `jq`        | JSON processing   | `sudo apt install jq` |
| `coreutils` | Date & time utils | usually preinstalled  |

---

## 💾 Data Storage Format

Each project and module is stored as a JSON file under `~/.yatt/projects`.

Example `myapp.json`:

```json
{
  "name": "myapp",
  "description": "Main backend project",
  "tags": ["backend"],
  "modules": [
    {
      "name": "auth",
      "description": "Authentication service",
      "tags": ["security", "jwt"]
    }
  ]
}
```

Tracking sessions are stored in `~/.yatt/tracking.json`:

```json
{
  "active_session": null,
  "sessions": [
    {
      "name": "auth@myapp",
      "start": "2025-10-23T14:00:00+03:30",
      "end": "2025-10-23T15:30:00+03:30",
      "duration_seconds": 5400,
      "date": "2025-10-23",
      "tags": ["security", "jwt"]
    }
  ]
}
```

---

## 🧩 Command Overview

| Command                               | Description                      |
| ------------------------------------- | -------------------------------- |
| `project create <name> [desc]`        | Create a new project             |
| `project remove <name>`               | Delete a project                 |
| `project list`                        | List all projects and submodules |
| `project tags add/remove/list/by`     | Manage tags                      |
| `submodule create/remove/list`        | Manage submodules                |
| `track start/stop/status/list/report` | Manage tracking sessions         |
| `completion`                          | Generate Bash completion script  |
| `help`                                | Show full usage guide            |

---

## 💡 Tips

* Use **tags** to group related work sessions.
* Run `yatt track report tag:<tag>` to see time spent on all tasks with that tag.
* Add YATT to your `.bashrc` or `.zshrc` completion for seamless use.

---

## 🧑‍💻 Contributing

1. Fork this repository
2. Create a feature branch: `git checkout -b feature/amazing-idea`
3. Commit your changes: `git commit -m 'Add amazing feature'`
4. Push the branch: `git push origin feature/amazing-idea`
5. Open a Pull Request 🎉

---

## 📜 License

MIT License © 2025 [Your Name]

---

> ⚡ “Track smart, work smarter.” — *YATT*