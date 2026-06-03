# Day 18 – Shell Scripting: Functions & Intermediate Concepts

## Overview

Today I learned how to write cleaner and reusable Bash scripts using functions, work with local variables, use strict mode (`set -euo pipefail`), and build a real-world system information reporting script.

---

# Task 1: Basic Functions

## Objective

Create reusable functions that:

* Greet a user
* Add two numbers

## Script: `functions.sh`

```bash
#!/bin/bash

greet() {
    echo "Hello, $1!"
}

add() {
    sum=$(( $1 + $2 ))
    echo "Sum : $sum"
}

greet "Devesh"
greet "Ramu"
greet "Muskan"

add 10 23
add 43 56
add 78 12
```

## Output

```text
Hello, Devesh!
Hello, Ramu!
Hello, Muskan!

Sum : 33
Sum : 99
Sum : 90
```

## Screenshot



### What I Learned

* How to define and call functions.
* How to pass arguments using `$1`, `$2`.
* How functions improve code reusability.

---

# Task 2: Functions with Return Values

## Objective

Create functions to check:

* Disk usage
* Memory usage

## Script: `disk_check.sh`

```bash
#!/bin/bash

check_disk() {
    echo "Disk Usage:"
    df -h /
}

check_memory() {
    echo "Memory Usage:"
    free -h
}

echo "========== System Resource Report =========="
check_disk
check_memory
```

## Output

```text
========== System Resource Report ==========

Disk Usage:
/dev/root 19G 2.8G 16G 15% /

Memory Usage:
Mem: 1.9Gi ...
```

## Screenshot



### What I Learned

* Functions can organize related tasks.
* System information can be gathered using built-in Linux commands.
* Scripts become cleaner when logic is separated into functions.

---

# Task 3: Strict Mode (`set -euo pipefail`)

## Objective

Learn safer shell scripting practices.

## Script: `strict_demo.sh`

```bash
#!/bin/bash

set -euo pipefail

echo "$username"
```

## Testing `set -u`

### Output

```text
username: unbound variable
```

### Screenshot



---

## Testing `set -e`

### Script

```bash
#!/bin/bash

set -euo pipefail

ls /path/that/does/not/exist
```

### Output

```text
ls: cannot access '/path/that/does/not/exist'
```

### Screenshot



---

## Testing `set -o pipefail`

### Script

```bash
#!/bin/bash

set -euo pipefail

cat missing_file.txt | grep "hello"
```

### Output

```text
cat: missing_file.txt: No such file or directory
```

### Screenshot



---

## Explanation of Strict Mode

### `set -e`

Stops the script immediately when a command fails.

### `set -u`

Treats undefined variables as errors.

### `set -o pipefail`

Makes the entire pipeline fail if any command inside the pipeline fails.

### Why DevOps Engineers Use Strict Mode

```bash
set -euo pipefail
```

This helps:

* Prevent silent failures.
* Catch bugs early.
* Create production-ready scripts.

---

# Task 4: Local Variables

## Objective

Understand the difference between local and global variables.

## Script: `local_demo.sh`

```bash
#!/bin/bash

local_demo() {
    local message="I am a Local Variable"
    echo "Inside local_demo(): $message"
}

global_demo() {
    message="I am a global variable"
    echo "Inside global_demo(): $message"
}

echo "Before calling functions:"
echo "message ="

local_demo

echo "After local_demo():"
echo "message ="

global_demo

echo "After global_demo():"
echo "message = $message"
```

## Output

```text
Before calling functions:
message =

Inside local_demo(): I am a Local Variable

After local_demo():
message =

Inside global_demo(): I am a global variable

After global_demo():
message = I am a global variable
```

## Screenshot



### What I Learned

* `local` variables exist only inside functions.
* Global variables remain available outside functions.
* Using `local` prevents accidental variable modification.

---

# Task 5: System Information Reporter

## Objective

Build a real-world script using functions and strict mode.

## Script: `system_info.sh`

```bash
#!/bin/bash

set -euo pipefail

print_system_info() {
    echo "===== Hostname and OS Info ====="
    echo "Hostname: $(hostname)"
    echo "OS: $(grep PRETTY_NAME /etc/os-release | cut -d= -f2)"
}

print_uptime() {
    echo "===== Uptime ====="
    uptime -p
}

print_disk_usage() {
    echo "===== Top 5 Largest Directories ====="
    sudo du -h / 2>/dev/null | sort -rh | head -n 5
}

print_memory_usage() {
    echo "===== Memory Usage ====="
    free -h
}

print_cpu_processes() {
    echo "===== Top 5 CPU Processes ====="
    ps -eo pid,ppid,cmd,%cpu --sort=-%cpu | head -n 6
}

main() {
    print_system_info
    print_uptime
    print_disk_usage
    print_memory_usage
    print_cpu_processes
}

main
```

## Output

```text
=========================================
        System Information Report
=========================================

Hostname: ip-172-31-35-110

Uptime:
up 1 hour, 49 minutes

Top 5 Largest Directories:
3.5G /usr
2.1G /usr/lib
1.1G /var
689M /snap
658M /swap
```

## Screenshot



### What I Learned

* How to build a complete reporting script.
* How to organize large scripts using functions.
* How to combine multiple Linux commands into one useful tool.

---

# Key Takeaways

## 1. Functions Improve Reusability

Functions allow code to be written once and used multiple times.

## 2. Strict Mode Improves Reliability

Using:

```bash
set -euo pipefail
```

helps catch errors early and prevents unexpected behavior.

## 3. Local Variables Reduce Bugs

Using:

```bash
local variable_name="value"
```

keeps variables limited to their functions and avoids conflicts.

---


