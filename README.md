# 🧭 YATT — Yet Another Task Tracker

A simple yet powerful **command-line time & project tracker**, written entirely in Bash.  
Manage projects, submodules, tags, and track your work sessions — all from your terminal.

---

## ✨ Features

- 🗂️ **Project Management** — Create, list, edit, and remove projects
- 🧩 **Submodules** — Organize components or microservices under projects
- 📝 **Task Management** — Create, list, update states (todo/doing/done/verified), edit, and remove tasks
- 🏷️ **Tags** — Add, remove, and filter entities by tags
- ⏱️ **Task Time Tracking** — Track time for projects/modules or specific tasks; auto-log durations
- 📊 **Reports** — Filter sessions by project, module, tag, or date
- 💾 **Backup Management** — Backup and restore of all YATT data
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

Autocompletion helps you quickly navigate available commands and entities.

Enable it by running:

```bash
yatt completion > ~/.yatt/yatt-completion.sh
source ~/.yatt/yatt-completion.sh
```

or append the following line into your `~/.bashrc`

```bash
if command -v yatt &> /dev/null; then
    source <(yatt completion)
fi
```

Then try typing:

```bash
yatt [TAB]
yatt project [TAB]
yatt backup [TAB]
```

---

## 🧱 Directory Structure

YATT keeps its data under your home directory:

```
~/.yatt/
├── backups/
│   ├── yatt_backup_20251020_100322.tar.gz
│   ├── yatt_backup_20251026_085449.tar.gz
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
yatt project edit myapp
```

### 🧩 Submodules

```bash
yatt submodule create auth@myapp "Authentication service"
yatt submodule list myapp
yatt submodule remove auth@myapp
```

### 📝 Tasks (w/ States & Time Logs)
```bash
# Create tasks (titles support spaces!)
yatt task create myapp "Setup CI/CD"
yatt task create auth@myapp "Implement OAuth2"

# List & manage
yatt task list myapp
yatt task update myapp "Setup CI/CD"
yatt task edit auth@myapp "OAuth2"
yatt task remove myapp "Setup CI/CD"
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
# Track project
yatt track start myapp
# Track **specific task** 👈
yatt track start myapp "Setup CI/CD"
# Live elapsed timer
yatt track status

# ...work...

# Logs duration to task!
yatt track stop
# Filtered history
yatt track list myapp
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

### 💾 Backup Management

```bash
yatt backup create
yatt backup list
yatt backup restore <file>
```

🗂️ Backups are stored in:

```bash
~/.yatt/backups/
```

**Sample Output:**

```bash
📅 Report for 2025-10-30 (filtered by: myapp)
  • myapp: 02:45:12
      - Task: Setup CI/CD: 01:23:45
  • auth@myapp: 01:21:30

━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Total time: 04:06:42

📊 Task Time Summary:
  • myapp :: Setup CI/CD
      Total: 01:23:45 (2 sessions)
```


---

## 🧭 Example Workflow

```bash
# Setup
yatt project create backend "My API"
yatt submodule create api@backend "REST API"
yatt project tags add backend golang

# Tasks
yatt task create backend "Init project"
yatt task create api@backend "User endpoints"

# Track
yatt track start api@backend "User endpoints"
# 💻 work...
yatt track stop

# Report
yatt track report tag:golang
yatt backup create
```

Output example:

```
✅ Stopped tracking 'api@myapp'. Duration: 01:32:45
📊 Report for 2025-10-23:
  - api@myapp: 1h 32m 45s
✅ Backup created: /home/mhmd/.yatt/backups/yatt_backup_20251026_101530.tar.gz
📦 Available backups:
  - yatt_backup_20251026_101530.tar.gz
⚠️  This will overwrite your current YATT data. Continue? (y/N): y
✅ Backup restored from 'yatt_backup_20251026_101530.tar.gz'
```

---

## ⚙️ Dependencies

Make sure these tools are installed:

| Tool        | Purpose           | Install command       |
| ----------- | ----------------- | --------------------- |
| `bash`      | Script runtime    | built-in              |
| `jq`        | JSON processing   | `sudo apt install jq` |

---

## 💾 Data Storage Format

Each project and module is stored as a JSON file under `~/.yatt/projects`.

Example `myapp.json`:

```json
{
  "name": "myapp",
  "description": "...",
  "tags": ["backend"],
  "tasks": [
    {
      "title": "Setup CI/CD",
      "state": "done",
      "real_duration": [{"start": "...", "duration_seconds": 5000}]
    }
  ],
  "modules": [{"name": "auth", "tasks": [...]}]
}
```

Tracking sessions are stored in `~/.yatt/tracking.json`:

```json
{
  "active_session": null,
  "sessions": [
    { "name": "api@backend", 
      "duration_seconds": 5400, 
      "tags": ["golang"]
      }
    ]
}
```

---

## 🧩 Command Overview

| Category | Commands |
| -------- | -------- |
| Project | `create <name> [desc] remove <name> list edit <name> tags add/remove/list/by <entity> [tag]` |
| Submodule | `create <mod>@<proj> [desc] remove/edit/list <mod>@<proj> tags ... (same as project)` |
| Task | `create <entity> <title> list <entity> update <entity> <title> <state> edit/remove <entity> <title>` |
| Track | `start <entity> [task] stop status list [filter] report [filter] [date]` |
| Backup | `create list restore <file>` |
| Other | `completion help` |


---

## 💡 Tips

* Use **tags** to group related work sessions.
* Run `yatt track report tag:<tag>` to see time spent on all tasks with that tag.
* Add YATT to your `.bashrc` or `.zshrc` completion for seamless use.

---

## 💡 Pro Tips

Task Tracking 🚀: track start entity task_title → auto-logs to task!
Tags Everywhere: Filter reports: track report tag:security
States: todo → doing → done → verified
Aliases: Add alias t='yatt track' to .bashrc
Daily Report: alias today='yatt track report'

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