# 🐧 Linux Fundamentals — Command Guide

![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![Level](https://img.shields.io/badge/Level-Beginner-success?style=for-the-badge)

## 📚 Before You Start

Open Ubuntu (WSL) or a Linux terminal. A terminal is a place where you type commands to interact with your computer. Type each command and press Enter. In examples, replace placeholder names such as `folder`, `file.txt`, `URL`, and `user@server` with your own values. Options such as `-l` change how a command behaves.

Practice in a separate folder first. No previous Linux experience is required.

> Part of the [DevOps Learning Journey](https://github.com/MohanRukshika/DevOps-learning-journey). This guide starts with **why Linux matters**, then explains commands with practical examples. Examples assume Ubuntu in Windows Subsystem for Linux (WSL), but most commands also work on Linux servers.

## 1. 💡 What is Linux?

Linux is the kernel (core) of an operating system. It helps software communicate with computer hardware. **Ubuntu** is a Linux distribution: a complete operating system built around the Linux kernel. It lets you manage files, applications, users, and network connections.

You do **not** need to replace Windows to learn Linux. With **WSL**, you can run Ubuntu and Linux commands on a Windows computer.

## 2. 🚀 Why learn Linux for DevOps?

DevOps is about helping teams **build, test, deliver, and operate software reliably**. Linux matters because it is widely used in the environments where software runs.

| Where Linux is used | What a DevOps Engineer does there | Example |
| --- | --- | --- |
| **Cloud servers** (e.g., AWS EC2) | Connects to servers, installs software, configures services | SSH into an Ubuntu server to deploy a Node.js API |
| **Application hosting** | Runs apps and web servers, inspects failures | Check whether a backend process is running |
| **Docker containers** | Builds and troubleshoots Linux-based container images | Run a MERN backend inside a container |
| **CI/CD pipelines** | Runs build, test, and deployment scripts | Execute tests in a Linux-based GitHub Actions runner |
| **Monitoring and troubleshooting** | Reads logs, checks CPU, RAM, disk, and network | Use `tail -f` to inspect app logs |
| **Automation** | Writes Bash scripts for repeatable tasks | Automate backups or routine checks |
| **Security and access** | Manages users, file permissions, and updates | Control who can execute a deployment script |

### A real-world example

Imagine you have a React frontend and a Node.js/Express API. The API works on your laptop, but you want to run it on a cloud server. You may need to:

1. Connect to the server using `ssh`.
2. Navigate to the application directory with `cd` and inspect files with `ls`.
3. Check whether Node.js is available with `which node`.
4. Inspect application logs using `tail` or `less`.
5. Check resources with `free -h` and `df -h`.
6. Update code through Git and use an automated deployment pipeline.

**Main idea:** Linux commands let you understand, operate, and troubleshoot the environment where your software runs. DevOps is broader than Linux, but Linux is a foundational skill.

## 3. 📁 Understand the Linux filesystem

Linux paths begin at the **root directory** `/`. A typical directory tree includes:

```text
/
├── home/        # Users' home directories
│   └── student/ # Example Ubuntu user
├── etc/         # System configuration
├── var/         # Variable data, often logs in /var/log
├── usr/         # Programs and shared resources
├── tmp/         # Temporary files
└── mnt/         # Common location for mounted filesystems
    └── e/       # Windows E: drive in a typical WSL setup
```

| Path or symbol | Meaning |
| --- | --- |
| `/` | Filesystem root; also separates path components |
| `~` | Current user's home directory, such as `/home/student` |
| `.` | Current directory |
| `..` | Parent directory |
| `/mnt/e/Devops` | `E:\Devops` as typically seen from Ubuntu WSL |
| `./script.sh` | A script in the current directory |

**Absolute vs. relative paths:** `/mnt/e/Devops` is an absolute path (starts at `/`). `01-linux-fundamentals/exercises` is relative to your current directory.

> **WSL note:** Windows drives are normally mounted under `/mnt/`, but this can be configured differently. Linux file permissions and performance can behave differently on Windows-mounted drives.

## 4. 🧭 Navigation commands

| Command | What it does | Example / when to use it |
| --- | --- | --- |
| `pwd` | Prints your current directory | Run before creating files to confirm your location |
| `ls` | Lists files and folders | `ls` |
| `ls -l` | Shows detailed file information, including permissions | `ls -l` |
| `ls -a` | Includes hidden entries (names beginning with `.`) | `ls -a` to see `.git` |
| `ls -la` | Detailed list including hidden entries | `ls -la` |
| `ls -R` | Lists directories recursively | `ls -R 01-linux-fundamentals` |
| `cd folder` | Enters a folder | `cd 01-linux-fundamentals` |
| `cd ..` | Moves to the parent directory | `cd ..` |
| `cd ~` | Returns to your home directory | `cd ~` |
| `cd -` | Returns to your previous directory | `cd -` |
| `clear` | Clears visible terminal output | `clear` |

```bash
# Create a safe practice folder in your Linux home directory
mkdir -p ~/linux-practice
cd ~/linux-practice
pwd                  # Confirm where you are
ls -la               # Inspect files, including hidden entries
```

## 5. 📄 Creating, copying, moving, and deleting files

| Command | What it does | Example |
| --- | --- | --- |
| `mkdir folder` | Creates a directory | `mkdir exercises` |
| `mkdir -p a/b` | Creates nested directories, including missing parents | `mkdir -p practice/logs` |
| `touch file.txt` | Creates an empty file if missing; otherwise updates timestamps | `touch notes.txt` |
| `cp source destination` | Copies a file | `cp notes.txt backup.txt` |
| `cp -i source destination` | Asks before overwriting the destination | `cp -i notes.txt backup.txt` |
| `mv source destination` | Moves or renames a file | `mv draft.txt notes.txt` |
| `rm file.txt` | Removes a file | `rm temporary.txt` |
| `rmdir folder` | Removes an **empty** directory | `rmdir empty-folder` |
| `rm -r folder` | Recursively removes a folder and contents | `rm -r old-practice` |

**Understand `cp` vs. `mv`:** `cp hello.txt backup.txt` leaves both files; `mv hello.txt backup.txt` renames or moves the original. Both commands can replace existing destination files depending on the circumstances.

> ⚠️ **Safety:** `rm` usually does not send files to the Recycle Bin. Check your location with `pwd` and inspect targets with `ls` before deleting. Never copy-paste destructive commands without understanding their paths.

## 6. ✏️ Reading, searching, and editing files

| Command | What it does | Example / use |
| --- | --- | --- |
| `cat file.txt` | Prints the file's contents | `cat notes.txt` for a short file |
| `less file.txt` | Opens an interactive, scrollable viewer | `less app.log` for long logs |
| `head file.txt` | Shows the first 10 lines by default | `head app.log` |
| `tail file.txt` | Shows the last 10 lines by default | `tail app.log` |
| `tail -n 20 file.txt` | Shows the last 20 lines | `tail -n 20 app.log` |
| `tail -f file.txt` | Follows new lines as they are appended | `tail -f app.log` while debugging; `Ctrl+C` to stop |
| `grep "error" file.txt` | Finds lines matching text (case-sensitive) | `grep "error" app.log` |
| `grep -i "error" file.txt` | Finds matching lines regardless of case | `grep -i "error" app.log` |
| `nano file.txt` | Opens a beginner-friendly terminal text editor | `nano notes.txt` |
| `vim file.txt` | Opens a powerful modal terminal text editor | `vim notes.txt` |
| `which nano` | Shows the executable path found in `PATH` | `which nano` may show `/usr/bin/nano` |

**Useful controls:** In `less`, use `Space` to advance, `/word` to search, and `q` to quit. In Nano, use `Ctrl+O` then Enter to save, and `Ctrl+X` to exit. In Vim, press `Esc`, type `:q`, then Enter to quit if no changes need saving.

### DevOps log example

```bash
# Create a sample log in your practice folder
printf 'INFO Server started\nERROR Database unavailable\n' > app.log
cat app.log
less app.log
# Press q to exit less
grep -i "error" app.log
# Remove the sample log only when finished
```

## 7. 🔄 Output, redirection, and pipes

Redirection saves command output to a file. A pipe passes output directly to another command. Think of a pipe as connecting two commands so they can work together.

| Syntax | Meaning | Example |
| --- | --- | --- |
| `echo "Hello"` | Prints text | `echo "Hello DevOps"` |
| `>` | Writes command output to a file, **overwriting** it | `echo "Day 1" > notes.txt` |
| `>>` | Appends output to a file | `echo "Day 2" >> notes.txt` |
| `\|` | Sends output from one command into another | `cat notes.txt \| grep "Day"` |

```bash
echo "Linux fundamentals" > notes.txt
echo "Learning command line" >> notes.txt
cat notes.txt
cat notes.txt | grep "Linux"
```

**Important:** `>` can erase a file's previous content. Use `>>` to add lines without replacing what was already there.

## 8. 📊 System information and process monitoring

A process is a running program. RAM is temporary working memory, and disk space is storage for files. These commands help you check whether a server has enough resources to run an application.

| Command | What it does | Why it matters in DevOps |
| --- | --- | --- |
| `whoami` | Prints the current username | Confirm which account runs a command |
| `hostname` | Prints the machine hostname | Identify a server |
| `uname -a` | Shows kernel/system information | Diagnose environment differences |
| `date` | Displays system date and time | Check timestamps |
| `uptime` | Shows uptime and load averages | Investigate server activity |
| `df -h` | Shows filesystem space usage in readable units | Detect low disk space |
| `free -h` | Shows RAM and swap usage | Investigate memory pressure |
| `top` | Interactively displays running processes | Find CPU/memory-intensive processes; press `q` to exit |
| `ps aux` | Lists running processes | Check whether an application process exists |

```bash
whoami
uname -a
free -h
df -h
```

## 9. 🔐 Permissions and package management — first look

| Command | What it does | Example |
| --- | --- | --- |
| `ls -l` | Displays file permissions and ownership | `ls -l script.sh` |
| `chmod +x script.sh` | Adds execute permission to a script | `chmod +x script.sh` |
| `sudo apt update` | Runs Ubuntu's package-index refresh with elevated privileges | `sudo apt update` |

**Concepts:** `chmod` changes permissions; `sudo` runs a command with elevated privileges when authorized; `apt` is Ubuntu's package manager. Only run privileged commands you understand. We'll cover permissions, users, and package management in depth later.

## 10. 🌐 Networking commands — first look

An IP address identifies a device on a network. A port identifies a network service on that device. These commands help you check connections and troubleshoot applications.

| Command | What it does | DevOps use |
| --- | --- | --- |
| `ip addr` | Shows network interfaces and IP addresses | Inspect network configuration |
| `ping google.com` | Sends ICMP echo requests (when permitted) | Basic reachability test; stop with `Ctrl+C` |
| `curl https://example.com` | Requests a URL and prints its response | Test a website or API |
| `wget URL` | Downloads content from a URL | Retrieve a file |
| `ss -tuln` | Lists listening TCP/UDP sockets numerically | Check which ports are listening |
| `ssh user@server` | Opens a secure remote shell connection | Manage a Linux server remotely |

**Note:** Some servers block `ping`; a failed ping does not always mean the server is down.

## 11. 🌿 Git commands used in this learning journey

Git is separate from Linux, but we use it in our Linux terminal to save and share lessons.

| Command | What it does |
| --- | --- |
| `git clone URL` | Copies a remote Git repository to your computer |
| `git remote -v` | Shows configured remote names and fetch/push URLs |
| `git status` | Shows the branch and current changes |
| `git add .` | Stages changes from the current directory downward |
| `git commit -m "message"` | Records staged changes as a local commit |
| `git push origin main` | Pushes the local `main` branch to the `origin` remote |
| `git branch -M main` | Renames the current branch to `main` |

```bash
# Run from your repository folder
git status
git remote -v
git add 01-linux-fundamentals/commands.md
git commit -m "docs: add beginner Linux command guide"
git push origin main
```

**Before pushing:** Review `git status` and never commit passwords, access tokens, private keys, or `.env` secrets. The push example assumes your branch is named `main` and your remote is configured.

## 12. ⌨️ Terminal shortcuts

| Shortcut | What it does |
| --- | --- |
| `Ctrl+C` | Interrupts a running command |
| `Ctrl+L` | Clears the visible terminal display |
| `Tab` | Attempts command/path completion |
| `↑` | Recalls an earlier command |
| `Ctrl+O`, Enter | Saves a file in Nano |
| `Ctrl+X` | Exits Nano |
| `Ctrl+W` | Searches within Nano |
| `q` | Exits `less` or `top` |

## 13. 💻 Hands-on exercise: create and inspect files

> Work inside a practice folder to avoid modifying important files. For this exercise, first clone or locate your learning repository. Replace the example path below with its actual location. Use a fresh lesson folder so existing files are not overwritten.

```bash
# 1. Enter the repository (adjust this path if necessary)
cd ~/DevOps-learning-journey

# 2. Check your location
pwd

# 3. Create a nested exercise directory
mkdir -p 01-linux-fundamentals/exercises/lesson-01

# 4. Enter the exercise directory
cd 01-linux-fundamentals/exercises/lesson-01

# 5. Create and populate a text file
touch hello.txt
echo "I am learning Linux for DevOps" > hello.txt

# 6. Read it
cat hello.txt

# 7. Copy and rename a backup
cp -i hello.txt backup.txt
mv backup.txt notes.txt

# 8. Inspect results
ls -la
cat notes.txt

# 9. Return to repository root
cd ../../..
git status
```

**Expected result:** `lesson-01/` contains `hello.txt` and `notes.txt`, both with the same line of text. You should see the new files listed by `git status` as untracked until you stage them.

### 🧠 Check your understanding

1. What is the difference between `pwd` and `ls`?
2. Why does `mkdir -p` help with nested folders?
3. How does `cp` differ from `mv`?
4. Why is `rm -r` risky?
5. When would you use `less` instead of `cat`?
6. What is the difference between `>` and `>>`?
7. Why might a DevOps Engineer run `tail -f app.log`?
8. What does `git remote -v` tell you?

## 14. 📝 Quick revision: the essential first commands

Start by practicing these until they feel natural:

```text
pwd       Where am I?
ls        What's here?
cd        Move to another directory
mkdir     Create a directory
touch     Create a file (if missing)
cat       Read a short file
less      Read a long file
cp        Copy
mv        Move / rename
rm        Remove carefully
nano      Edit text
which     Locate an executable in PATH
```



---

## 🎯 Key Takeaways

- Linux is a foundational skill for managing servers and applications in DevOps.
- Check your current directory before creating, moving, or deleting files.
- Practice commands in a safe folder and understand their purpose before using them on a real server.
- Use monitoring and networking commands to investigate problems.

*Part of my [DevOps Learning Journey](../README.md).*
