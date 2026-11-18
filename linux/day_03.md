# Day 3: Kernel Logs, Process Control, Storage Mounting & Network Debugging

**Cloud Environment:** Google Cloud Platform (GCP) Compute Engine VM

## 1. Kernel Ring Buffer & Line Counting
Inspecting hardware/kernel boot messages and counting output lines.

```bash
dmesg                     # Print kernel ring buffer messages (hardware & driver logs)
dmesg | wc -l             # Count total number of lines in kernel logs
dmesg | nl                # Display kernel logs with line numbers
```

## 2. File & Directory Ownership (`chown`)
Changing user and group ownership for files and recursive directory trees.

```bash
chown new_owner file.txt                  # Change only the file owner
chown root:vinod file.txt                 # Change both user owner and group
chown :vinod file.txt                     # Change only the group ownership
chown -R new_owner:new_group /path/dir    # Recursively change ownership for a folder and its contents
```

## 3. Process Signals & Priority Tuning (`nice` / `renice`)
Managing running processes, sending control signals, and adjusting CPU scheduling priority.

```bash
ps aux                    # View all running processes (BSD syntax)
ps -ef                    # View all running processes (standard UNIX syntax)

kill <PID>                # Gracefully terminate a process (SIGTERM / 15)
kill -9 <PID>             # Forcefully kill an unresponsive process (SIGKILL / 9)
kill -3 <PID>             # Generate a thread dump for Java/JVM applications (SIGQUIT / 3)
kill -STOP <PID>          # Pause/suspend a running process (SIGSTOP / 19)
kill -CONT <PID>          # Resume a paused process (SIGCONT / 18)

renice -n 10 -p 4048      # Lower process priority (nice values range from -20 highest to 19 lowest)
renice -n -5 -p 4048      # Increase process priority (requires root/sudo)
```

## 4. Systemd Service Management (`cron`)
Checking service health, restarting daemons, and configuring boot persistence.

```bash
systemctl status cron                      # Check if the cron service is active and view recent logs
systemctl restart cron                     # Restart the cron service after config updates
systemctl enable cron                      # Enable cron to start automatically on system boot
systemctl list-units --type=service --all  # List all installed services (active, inactive, and failed)
```

## 5. System Capacity & Virtual Memory Stats
Checking CPU core count, memory in megabytes, and virtual memory/IO statistics.

```bash
nproc                     # Display the number of available CPU cores
free -m                   # Display RAM and swap usage in megabytes
vmstat 1 5                # Report virtual memory, CPU, and I/O stats every 1 second (5 times)
cd /opt                   # Navigate to /opt (standard directory for optional/third-party software)
```

## 6. Disk Partitioning, Formatting & Mounting
Attaching a new block storage volume, formatting it with `ext4`, and mounting it to the filesystem.

> **Cloud Note:** Additional attached disks typically appear as `/dev/sdb` on GCP Compute Engine and `/dev/xvdf` on AWS EC2.

```bash
lsblk                                   # List all available block devices and mount points
fdisk -l                                # Display disk partition tables
ls -ltr /boot                           # Inspect kernel and bootloader files

mkdir -p /mnt/demo-volume               # Create a mount point directory
mkfs -t ext4 /dev/xvdf                  # Format the raw disk volume with the ext4 filesystem
mount /dev/xvdf /mnt/demo-volume        # Mount the formatted volume to the directory
umount /mnt/demo-volume                 # Safely unmount the volume when finished
```

## 7. Production Network Troubleshooting Workflow
Step-by-step diagnostic flow when an application fails to connect:

```text
[App failing to connect?]
        │
        ├─► 1. Check local ports ────────► ss -tulnp
        ├─► 2. Check domain resolution ──► dig +short domain.com
        ├─► 3. Check host reachability ──► ping -c 4 <IP>
        ├─► 4. Find routing bottlenecks ─► traceroute <IP>
        └─► 5. Test HTTP/API response ───► curl -Iv https://domain.com
```

## Key Takeaways
* Learned how to format and mount raw cloud block volumes (`mkfs`, `mount`, `lsblk`) and manage service persistence with `systemctl enable`.
* Practiced sending targeted process signals (`-9`, `-3`, `-STOP`, `-CONT`) and built a structured 5-step network debugging checklist (`ss`, `dig`, `ping`, `traceroute`, `curl`).
