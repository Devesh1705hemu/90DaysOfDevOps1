# Day 17 - Shell Scripting Basics

## Overview

Today I explored the fundamentals of Shell Scripting and learned how automation can simplify repetitive Linux administration tasks. I worked with loops, command-line arguments, package installation automation, and error handling techniques.

---

## Task 1: For Loops

### Fruit List Loop

Created a script that loops through a list of fruits and prints each fruit.

```bash
#!/bin/bash

fruits=("Apple" "Banana" "Mango" "Orange" "Grapes")

for fruit in "${fruits[@]}"
do
    echo "$fruit"
done
```

### Count from 1 to 10

```bash
#!/bin/bash

for ((i=1; i<=10; i++))
do
    echo "$i"
done
```

### Key Learnings

* Using `for` loops in Bash
* Iterating through arrays
* C-style loop syntax in Shell Scripting

---

## Task 2: While Loop

### Countdown Script

Created a countdown script that accepts a number from the user and counts down to zero.

```bash
#!/bin/bash

read -p "Enter a number: " num

while [ $num -ge 0 ]
do
    echo "$num"
    ((num--))
done

echo "Done!"
```

### Key Learnings

* Using `while` loops
* User input with `read`
* Numeric comparisons using `-ge`
* Increment and decrement operators

---

## Task 3: Command-Line Arguments

### Greeting Script

```bash
#!/bin/bash

if [ $# -eq 0 ]
then
    echo "Usage: ./greet.sh <name>"
else
    echo "Hello, $1!"
fi
```

### Arguments Demo

```bash
#!/bin/bash

echo "Script Name: $0"
echo "Total Arguments: $#"
echo "All Arguments: $@"
```

### Key Learnings

* `$0` → Script name
* `$1` → First argument
* `$#` → Total number of arguments
* `$@` → All arguments

---

## Task 4: Package Installation Automation

Created a script that checks whether packages are installed and installs them if missing.

```bash
#!/bin/bash

packages=("nginx" "curl" "wget")

for package in "${packages[@]}"
do
    if dpkg -s "$package" > /dev/null 2>&1
    then
        echo "$package is already installed. Skipping..."
    else
        echo "$package is not installed. Installing..."
        apt-get install -y "$package"
    fi
done
```

### Key Learnings

* Package management using APT
* Checking package status using `dpkg -s`
* Automating software installation
* Looping through package lists

---

## Task 5: Error Handling

### Safe Script

```bash
#!/bin/bash

set -e

mkdir /tmp/devops-test || echo "Directory already exists"

cd /tmp/devops-test || {
    echo "Failed to enter directory"
    exit 1
}

touch test.txt || {
    echo "Failed to create file"
    exit 1
}

echo "Script completed successfully."
```

### Root User Validation

```bash
if [ "$EUID" -ne 0 ]
then
    echo "Please run this script as root."
    exit 1
fi
```

### Key Learnings

* Using `set -e` for automatic exit on errors
* Error handling with `||`
* Root privilege verification using `EUID`
* Writing safer and more reliable scripts

---


