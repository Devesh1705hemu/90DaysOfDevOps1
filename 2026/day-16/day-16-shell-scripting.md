# Day 16 - Shell Scripting Basics

## Overview

Today I started my Shell Scripting journey and learned the fundamentals required to automate tasks in Linux.

Topics covered:

* Shebang (`#!/bin/bash`)
* Variables
* User Input using `read`
* Conditional Statements (`if-else`)
* File Existence Checks
* Service Status Checks

---

# Task 1: Your First Script

## hello.sh

```bash
#!/bin/bash

echo "Hello, DevOps!"
```

### Make Executable

```bash
chmod +x hello.sh
./hello.sh
```

### Output

```bash
Hello, DevOps!
```

### What happens if the shebang is removed?

The shebang (`#!/bin/bash`) tells Linux which interpreter should execute the script.

Without the shebang:

* The script may still run if executed with `bash script.sh`
* Running `./script.sh` may fail or use a different shell
* Behavior can vary depending on the environment

---

# Task 2: Variables

## variables.sh

```bash
#!/bin/bash

NAME="Devesh"
ROLE="DevOps Engineer"

echo "Hello, I am $NAME and I am a $ROLE"
```

### Output

```bash
Hello, I am Devesh and I am a DevOps Engineer
```

### Single Quotes vs Double Quotes

```bash
NAME="Devesh"

echo '$NAME'
echo "$NAME"
```

### Output

```bash
$NAME
Devesh
```

### Difference

* Single quotes (`' '`) treat everything literally.
* Double quotes (`" "`) allow variable expansion.

---

# Task 3: User Input with read

## greet.sh

```bash
#!/bin/bash

read -p "Enter your name: " NAME
read -p "Enter your favourite tool: " TOOL

echo "Hello $NAME, your favourite tool is $TOOL"
```

### Sample Output

```bash
Enter your name: Devesh
Enter your favourite tool: Docker

Hello Devesh, your favourite tool is Docker
```

---

# Task 4: If-Else Conditions

## check_number.sh

```bash
#!/bin/bash

read -p "Enter a number: " NUMBER

if [ "$NUMBER" -gt 0 ]; then
    echo "$NUMBER is positive"
elif [ "$NUMBER" -lt 0 ]; then
    echo "$NUMBER is negative"
else
    echo "$NUMBER is zero"
fi
```

### Sample Output

```bash
Enter a number: -5
-5 is negative
```

---

## file_check.sh

```bash
#!/bin/bash

read -p "Enter a filename: " FILENAME

if [ -f "$FILENAME" ]; then
    echo "$FILENAME exists"
else
    echo "$FILENAME does not exist"
fi
```

### Sample Output

```bash
Enter a filename: test.txt
test.txt exists
```

---

# Task 5: Combine It All

## server_check.sh

```bash
#!/bin/bash

SERVICE="sshd"

read -p "Do you want to check the status? (y/n): " CHOICE

if [ "$CHOICE" = "y" ]; then

    if command -v systemctl >/dev/null 2>&1; then

        if systemctl is-active --quiet "$SERVICE"; then
            echo "$SERVICE is active."
        else
            echo "$SERVICE is not active."
        fi

        systemctl status "$SERVICE"

    else
        echo "systemctl command is not available on this system."
    fi

elif [ "$CHOICE" = "n" ]; then
    echo "Skipped."

else
    echo "Invalid choice."
fi
```

### Sample Output

```bash
Do you want to check the status? (y/n): y
systemctl command is not available on this system.
```

---

# Key Learnings

## 1. Shebang is Important

The shebang specifies which interpreter executes the script and ensures consistent behavior.

## 2. Variables Make Scripts Dynamic

Variables allow storing and reusing values, making scripts easier to maintain.

## 3. Conditions Enable Decision Making

Using `if`, `elif`, and `else` helps automate actions based on user input or system state.

---

# Commands Used

```bash
chmod +x hello.sh
chmod +x variables.sh
chmod +x greet.sh
chmod +x check_number.sh
chmod +x file_check.sh
chmod +x server_check.sh
```

---

