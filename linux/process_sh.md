cat > system_info.sh << 'Eof'
#!/bin/bash

{
  echo "=== CURRENT TIME ==="
  date +"%T"
  echo ""

  echo "=== CURRENT DATE ==="
  date +"%Y-%m-%d"
  echo ""

  echo "=== RUNNING PROCESSES ==="
  ps aux
} > info

echo "System details have been saved to the 'info' file."
Eof

 Make It Executable
chmod +x system_info.sh
./system_info.sh

Check the Output File
cat info
