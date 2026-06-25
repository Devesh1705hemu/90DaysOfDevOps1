# Day 20 - Bash Scripting Challenge: Log Analyzer and Report Generator

## Overview

In this challenge, I built a Bash script that automates log file analysis. The script validates the input log file, counts errors, extracts critical events, identifies the most frequent error messages, generates a summary report, and archives the processed log file.

---

# Project Structure

```text
day20-scripting/
├── log_analyzer.sh
├── sample_log_generator.log
├── log_report_YYYY-MM-DD.txt
├── archive/
│   └── sample_log_generator.log
└── day-20-solution.md
```

---

# Features

* Accepts a log file as a command-line argument.
* Validates whether the file exists.
* Counts all occurrences of `ERROR` and `Failed`.
* Displays all `CRITICAL` events with line numbers.
* Finds the top 5 most common error messages.
* Generates a daily summary report.
* Archives the processed log file automatically.

---

# Script

```bash
#!/bin/bash

# ==========================================
# Day 20 - Log Analyzer and Report Generator
# ==========================================

# -------------------------------
# Task 1: Input Validation
# -------------------------------

if [ $# -eq 0 ]; then
    echo "Error: No log file provided."
    echo "Usage: ./log_analyzer.sh <log_file>"
    exit 1
fi

LOG_FILE="$1"

if [ ! -f "$LOG_FILE" ]; then
    echo "Error: File '$LOG_FILE' does not exist."
    exit 1
fi

# Variables
DATE=$(date +%Y-%m-%d)
REPORT_FILE="log_report_${DATE}.txt"
TOTAL_LINES=$(wc -l < "$LOG_FILE")

# Count errors
ERROR_COUNT=$(grep -Ei "ERROR|Failed" "$LOG_FILE" | wc -l)

# Critical events
CRITICAL_EVENTS=$(grep -n "CRITICAL" "$LOG_FILE")

# Top 5 error messages
TOP_ERRORS=$(grep "ERROR" "$LOG_FILE" \
| awk '{$1=$2=$3=""; print}' \
| sed 's/^ *//' \
| sort \
| uniq -c \
| sort -rn \
| head -5)

echo "=============================================="
echo "LOG ANALYZER REPORT"
echo "=============================================="

echo "Date         : $DATE"
echo "Log File     : $LOG_FILE"
echo "Total Lines  : $TOTAL_LINES"
echo "Total Errors : $ERROR_COUNT"

echo ""
echo "Critical Events"
echo "$CRITICAL_EVENTS"

echo ""
echo "Top 5 Error Messages"
echo "$TOP_ERRORS"

{
echo "=============================================="
echo "LOG ANALYSIS REPORT"
echo "=============================================="
echo "Date: $DATE"
echo "Log File: $LOG_FILE"
echo "Total Lines: $TOTAL_LINES"
echo "Total Errors: $ERROR_COUNT"

echo ""
echo "Top 5 Error Messages"
echo "$TOP_ERRORS"

echo ""
echo "Critical Events"
echo "$CRITICAL_EVENTS"

} > "$REPORT_FILE"

echo "Report generated: $REPORT_FILE"

mkdir -p archive
mv "$LOG_FILE" archive/

echo "Log archived successfully."
```

---

# Sample Execution

```bash
chmod +x log_analyzer.sh

./log_analyzer.sh sample_log_generator.log
```

---

# Sample Output

```text
==============================================
LOG ANALYZER REPORT
==============================================

Date         : 2026-06-25
Log File     : sample_log_generator.log
Total Lines  : 500
Total Errors : 42

Critical Events

84: CRITICAL Disk space below threshold
217: CRITICAL Database connection lost

Top 5 Error Messages

45 Connection timed out
32 File not found
28 Permission denied
15 Disk I/O error
9 Out of memory

Report generated: log_report_2026-06-25.txt

Log archived successfully.
```

---

# Generated Report

The script creates a report similar to:

```text
==============================================
LOG ANALYSIS REPORT
==============================================

Date: 2026-06-25

Log File: sample_log_generator.log

Total Lines: 500

Total Errors: 42

Top 5 Error Messages

45 Connection timed out
32 File not found
28 Permission denied
15 Disk I/O error
9 Out of memory

Critical Events

84: CRITICAL Disk space below threshold
217: CRITICAL Database connection lost
```

---

# Commands and Tools Used

* `grep`
* `awk`
* `sed`
* `sort`
* `uniq`
* `wc`
* `head`
* `date`
* `mkdir`
* `mv`
* Bash variables
* Command substitution `$( )`
* Shell scripting

---

# Key Learnings

1. Learned how to automate log analysis using Bash scripting.
2. Gained hands-on experience with text-processing tools like `grep`, `awk`, `sort`, `uniq`, and `sed`.
3. Learned to generate reports, validate user input, and archive processed files in an automated workflow.

---


This project demonstrates how Bash scripting can automate repetitive system administration tasks. By combining common Linux utilities, the script e
#90DaysOfDevOps #DevOpsKaJosh #TrainWithShubham
