# Day 4: Introduction to Bash Shell Scripting & System Health Automation

**Cloud Environment:** Google Cloud Platform (GCP) Compute Engine VM

## 1. Creating a Script via Here-Document (`cat << 'EOF'`)
Instead of opening an editor, we can write a multi-line script directly to a file from the terminal using a Here-Document (`EOF`). Quoting `'EOF'` prevents the shell from expanding variables while writing the file.

```bash
cat > system_health.sh << 'EOF'
#!/bin/bash
# System Health Monitoring Script

echo "=== System Health Report ==="

echo "Hostname & Internal IP:"
hostname
hostname -i

echo "Running Processes:"
ps

echo "Memory Usage:"
free -h

echo "Disk Space Usage:"
df -h

summary_msg="System health check completed successfully."
echo "\$summary_msg"
EOF
```

## 2. Making the Script Executable & Running It
Before executing a new shell script, grant execute (`+x`) permissions and run it.

```bash
chmod +x system_health.sh     # Grant execute permissions to the script
./system_health.sh            # Execute the script
```

## 3. Redirecting Script Output to a Log File
To save the monitoring output into a report file instead of printing it to the screen:

```bash
./system_health.sh > health_report.log    # Overwrite file with fresh output
./system_health.sh >> health_report.log   # Append output to an existing log file
```

## Key Takeaways
* Learned that Bash requires `#!/bin/bash` on the very first line and strictly forbids spaces around `=` when assigning variables (`var="value"`).
* Practiced generating scripts non-interactively using `cat << 'EOF'` and redirecting script output into log files for automated reporting.
