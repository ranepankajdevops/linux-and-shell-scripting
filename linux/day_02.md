# Day 2: User & Group Management, Services, Text Redirection & Archiving

**Cloud Environment:** Google Cloud Platform (GCP) Compute Engine VM

## 1. Package Management & Privilege Escalation
Updating package repositories and switching to the root user to manage system services.

```bash
sudo apt-get update && sudo apt install vim -y   # Update package lists and install Vim
sudo -i                                          # Switch to an interactive root shell
systemctl restart ssh                            # Restart the SSH service
systemctl restart nginx                          # Restart the Nginx web server
```

## 2. User & Group Management
Creating users, setting passwords, managing groups, and inspecting system authentication files.

```bash
useradd pankaj                    # Create a new user account (without home directory by default)
passwd pankaj                     # Set or update password for user 'pankaj'
cat /etc/passwd                   # View user account details (UID, GID, home dir, shell)
cat /etc/shadow                   # View encrypted user passwords (requires root)
userdel pankaj                    # Delete a user account

adduser pankaj                    # Interactively create a user with a home directory (/home/pankaj)
su - pankaj                       # Switch user session to 'pankaj' with their environment

groupadd devops                   # Create a new group named 'devops'
cat /etc/group                    # View all groups and their members
usermod -aG devops pankaj         # Append user 'pankaj' to the 'devops' secondary group
```

## 3. Navigation, Copying & Directory Cleanup
Moving up directory trees, checking current paths, copying files, and removing directories.

```bash
pwd                               # Print current working directory path
cd ..                             # Move up one parent directory level
rmdir empty_folder                # Remove an empty directory
rm -rf old_folder/                # Recursively and forcefully remove a non-empty directory
cp source_file backup_file        # Create a duplicate copy of a file
```

## 4. Vim Editing & Output Redirection
Viewing large files, using Vim editing shortcuts, and writing text via shell redirection.

```bash
less app.log                      # View a file page-by-page (press 'q' to quit)
echo 'Hello' > file.txt           # Overwrite file content with fresh text
echo 'World' >> file.txt          # Append text to the end of an existing file
```

**Essential Vim Shortcuts (Command Mode):**
* `o` / `Shift + O` — Insert a new line below / above the current line.
* `dd` — Delete the entire current line.
* `u` / `Shift + U` — Undo last change / undo all changes on the current line.

## 5. System Health, Logs & Troubleshooting Concepts
Checking uptime, login history, disk usage per folder, and understanding memory/process states.

```bash
uptime                            # Check how long the server has been running since last boot
last                              # Show history of recent user logins and system reboots
du -sh *                          # Check disk space used by each file/folder in current directory
cd /var/log                       # Navigate to system log directory for troubleshooting
```

**Core DevOps Concepts:**
* **Zombie Process:** A child process that has finished execution (`Z` state) but still has an entry in the process table because its parent process hasn't read its exit status. Because it is already dead, `kill -9` on the zombie PID won't work—you must notify or kill the **parent process** (`PPID`) so `systemd` cleans it up.
* **Swap Memory:** Dedicated disk space used as overflow memory when physical RAM is full, preventing out-of-memory (OOM) crashes under heavy load.

## 6. Networking, File Search & Archiving
Testing connectivity, downloading files, searching across directories, and bundling files with `tar`.

```bash
ping google.com                   # Test network reachability and latency to a host
wget https://example.com # Download a file directly from a URL

find . -name "*.log"              # Search recursively for all .log files in current directory
tar -cvf allfiles.tar myfolder/   # Bundle a directory into a single .tar archive
tar -xvf allfiles.tar             # Extract files from a .tar archive
```

## Key Takeaways
* Learned how Linux stores user credentials (`/etc/passwd`, `/etc/shadow`) and how secondary groups (`usermod -aG`) control team access in real DevOps environments.
* Practiced safe file redirection (`>` vs `>>`), directory archiving with `tar`, and checking server stability using `uptime` and `last`.
