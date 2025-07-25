# Kali Linux Tip: Run a Custom Tmux Session Globally from Anywhere

Want to start or attach to a `tmux` session with just one command from anywhere in Kali Linux?
Use this shell script and move it to `/usr/bin` so it becomes a **global command**. Here's how you can do it:


## 📜 Step 1: Create the Shell Script
#### Create a new file, for example: `tmuxstart`
```bash
nano tmuxstart
```
#### Paste the following script inside:
```bash
#!/bin/sh
# -----------------------------------------------------------------------------
# Author: DINESH PATHRO
# Description: Start or attach to a tmux session by name (default: hacking)
# License: Free to use with credit
# -----------------------------------------------------------------------------

# Check if session name is passed as argument
if [ -z "$1" ]; then
    read -p "Enter tmux session name (default: hacking): " session_name
    session_name=${session_name:-hacking}
else
    session_name="$1"
fi

# Start or attach to the session if it already exists
if tmux has-session -t "$session_name" 2>/dev/null; then
    echo "Attaching to existing tmux session: $session_name"
    tmux attach -t "$session_name"
else
    echo "Creating new tmux session: $session_name"
    tmux new-session -s "$session_name"
fi
```
## 🔐 Step 2: Make the Script Executable
```bash
chmod +x tmuxstart
```
## 📦 Step 3: Move Script to /usr/bin for Global Use
```bash
sudo mv tmuxstart /usr/bin/tmuxstart
```
> ⚠️ `/usr/bin` is a system path, so any script placed here can be run from any directory like a built-in command.

## 🚀 Step 4: Use It from Anywhere!

Now, just run:
```bash
tmuxstart
```
 or with a custom name:
```bash
tmuxstart recon
```
If the session exists, it attaches to it. If not, it creates a new one.
