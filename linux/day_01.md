# Day 1: Linux Essentials, Process Monitoring & Filesystem Hierarchy

**Cloud Environment:** Google Cloud Platform (GCP) Compute Engine VM

## 1. File & Directory Management
Creating, navigating, inspecting, renaming, and deleting files and directories.

```bash
mkdir project_dir        # Create a new directory
cd project_dir           # Move into the directory
touch app.log            # Create an empty file
vim indra                # Create and edit a file using Vim

ls                       # List directory contents
ls -ltr                  # List files in long format, sorted by oldest to newest
cat indra                # Print full file contents
cat indra | nl           # Print file contents with line numbers
head -10 app.log         # View the first 10 lines of a file
tail -10 app.log         # View the last 10 lines of a file

mv indra shashi          # Rename file from 'indra' to 'shashi'
rm app.log               # Remove a file
```

## 2. System Information & Networking
Checking kernel details, current user identity, and network addresses on the GCP instance.

```bash
whoami                   # Display the currently logged-in username
uname                    # Print basic OS/kernel name
uname -a                 # Print full system, kernel, and architecture details
man ls                   # Open the manual page for any command (e.g., ls)

hostname                 # Display the VM's hostname
hostname -i              # Display the internal (private) IP address
curl ifconfig.me         # Fetch the external (public) IP address
curl ifconfig.me/all     # Fetch full connection details (IP, User Agent, etc.)
curl https://example.com # Send an HTTP request to test connectivity to a URL
```

## 3. Process & Resource Monitoring
Inspecting running processes, CPU/memory usage, and disk space.

```bash
ps                       # List running processes for the current terminal session
ps -aef                  # List all running processes on the system with full details
top                      # Real-time process and resource monitor
htop                     # Interactive process viewer (enhanced version of top)
btop                     # Modern visual resource monitor for CPU, memory, and network
glances                  # Cross-platform system monitoring tool

free -h                  # Display available and used RAM/swap in human-readable format
df -h                    # Display disk space usage in human-readable format
df -T                    # Display disk space along with filesystem types
```

## 4. Navigating the Linux Filesystem Hierarchy
Understanding standard Linux directories and where system data lives.

```bash
cd ~                     # Navigate to the current user's home directory
cd /                     # Navigate to the root (/) directory

ls /etc/                 # System-wide configuration files
ls /var/log/             # System and application log files (crucial for troubleshooting)
ls /run/                 # Volatile runtime data stored since last boot
ls /proc/                # Virtual filesystem containing live kernel and process info
ls /tmp/                 # Temporary files created by system and users
ls /data/                # Custom directory often mounted for shared application data

ls /home/ubuntu          # Standard home directory for user 'ubuntu'
ls /home/abhi            # Standard home directory for user 'abhi'
cd /root/                # Home directory for the root (superuser) account
```

## Key Takeaways
* Practiced core Linux CLI navigation and file manipulation on a live GCP Linux VM.
* Learned how to check system health (`free`, `df`, `ps -aef`) and locate critical configuration (`/etc`) and log (`/var/log`) directories used daily in DevOps troubleshooting.
