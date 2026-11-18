#!/bin/bash

LOG_DIR="/var/log"

echo "Deleting log files older than 7 days in ${LOG_DIR}..."
find "$LOG_DIR" -type f -name "*.log" -mtime +7 -delete/print for dry run
echo "Old log files deleted successfully."
