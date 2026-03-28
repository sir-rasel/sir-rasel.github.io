---
title: "DevOps - Step By Step Learning : Part 21 (Shell Scripting - Tool For Automation Repetitive Task)"
description: "Let's learn the fundamental DevOps concepts!"
date: "2026-02-26T00:00:00Z"
tags: ["devops" , "shell", "scripting", "shell-scripting"]
draft: false
showtoc: false
tocOpen: false
hidemeta: false
comments: true
disableHLJS: false
disableShare: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowCodeCopyButtons: true
cover:
    image: "img/blogs/137-devops-shell.jfif"
    caption: "DevOps Shell Scripting"
    alt: "DevOps Shell Scripting"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 13:** [DevOps - Step By Step Learning : Part 13 (Version Controlling Using Git and GitHub in a DevOps Perspectives)]({{< ref "blogs/136-devops-vcs-git-github.md" >}})
---

{{< figure
    src="/img/blogs/137-devops-shell.jfif"
    caption="DevOps Shell Scripting (Photo Credit: Unsplash)"
    align=center
>}}

## Story:

Rasel has tried to explore the DevOps philosophy, Linux, VMs and codified VM management, programming, and others stuff until now. After all of his learning and studying real-world case studies, he came to the realization that DevOps practice is all about **automating** repetitive day-to-day tasks. And **Shell/Bash** scripting keeps taking its prestigious place. That's why Rasel decided to explore Shell/Bash scripting now.

* * *

## Shell/Bash Scripting Intro

### What is Shell and Bash?

***Shell***

*   A shell is a command-line interpreter that lets you interact with the Operating System (OS).
*   It takes human-readable commands and translates them into actions the kernel can understand.
*   Example: When you type ls, the shell runs the command to list files in a directory.

***Popular shells:***

*   sh (Bourne shell)
*   bash (Bourne Again Shell)
*   zsh (Z Shell)
*   csh (C Shell)
*   fish, dash, etc.

***Bash (Bourne Again SHell)***

*   An improved version of the original Bourne shell (sh)
*   Default shell on most Linux distributions
*   Supports scripting: conditionals, loops, functions, arrays, etc.
*   Developed by GNU
*   Platform dependent, generally used for Linux and macOS
*   Suitable for small to medium automation

> **Bash** can refers as the scripting language for writing automation scripts. For rest of the article we will use shell and bash as same meaning.

### What Is Meant by "Scripting"?

**Scripting** means writing a series of commands in a file that the shell can run automatically, line by line.

*   It’s different from programming languages like Python or C — it’s mostly about automating OS-level tasks.
*   A script is just a text file with a .sh extension.
*   Example: Instead of typing 10 commands one by one, you put them in a script and run it once.

### Why Do We Need Bash Scripts?

1.  **Automation** – Repeat tasks without manual effort.
2.  **System Administration** – Manage servers, logs, backups.
3.  **DevOps** – Automate CI/CD pipelines, Docker, Kubernetes commands.
4.  **Clean, Repeatable Tasks** – No human error.
5.  **Glue Code** – Connect multiple tools (e.g., jq, aws, docker, kubectl).

> *Bash scripting is the tool that binds together the DevOps task orderly.*

### Who Can Benefit from Bash Scripts?

*   **DevOps Engineers** – Automation, orchestration, deployment.
*   **System Admins** – Backup, monitoring, health checks.
*   **Software Developers** – Environment setup, test automation.
*   **Data Engineers** – Cron jobs, ETL scheduling.
*   **Anyone using Linux/macOS** - for automating repetitive tasks.

### Basic Syntax of Bash Script (Dissection Line by Line)

Here’s a simple Bash script:

```bash
#!/bin/bash     # Line 1: Shebang – tells OS which type shell to use 
                # This (hash) is a comment – ignored by interpreter

name="Saiful"   # Line 2: Variable assignment – no spaces around '='

echo "Hello, $name!"  # Line 3: Command with variable expansion

date            # Line 4: Built-in command – prints current date

exit 0          # Line 5: Exit script successfully        
```

**Explanation:**

*   **#!/bin/bash** - Mandatory to specify interpreter.
*   **\#** - Anything after # is ignored (used for comments).
*   **echo** - Prints to the terminal.
*   **$variable** - Use "$name" to expand variable.
*   **exit** - Terminates the script with status code (0 = success).

### How to Execute a Bash Script?

**Create a script (with .sh extension):**
```bash
touch myscript.sh
```

**Make it executable:**
```bash
chmod +x myscript.sh
```

**Run the script:**
```bash
./myscript.sh

# Alternatively,

bash myscript.sh        
```

* * *

## Bash Script Building Block Feature

### Shebang

Every shell script start with **#!** and its called shebang. It is mandatory to specify interpreter. Means it tells us which type of shell is being used for interpreting the rest of the statement.

```bash
#!/bin/bash
```

*   **which bash** - This response shows the full execution path of the shell interpreter. Make sure that the "sha-bang" line at the beginning of your script, matches this same execution path

### Variable and Quoting

```bash
#!/bin/bash

name="Saiful"
readonly fix=5
export out=10
echo "Hello, ${name}"
today=$(date)        
```

*   **Variable declaration**: variable_name=value. Note that no space permitted on either side of = sign when initializing variables
*   **Naming Convention**: Generally follow the traditional convention like other programming language. But used only lowercase letter is best practice
*   **Single quotes**: Treat everything literally
*   **Double quotes**: Allow variable expansion. Encapsulating the variable name with ${} is used to avoid ambiguity
*   **Backticks (\` \`) or $()**: Allow and used for command substitution
*   **Constant**: read-only modifier make a variable constant
*   **Exporting**: export modifier allow this variable by other script

### User Input & Argument

**User Input:**

```bash
#!/bin/bash

read -p "Enter your name: " name 
echo "Welcome, $name!"        
```

**Command-line arguments:**

```bash
#!/bin/bash
echo "Script name: $0"
echo "First arg: $1"
echo "Second arg: $2"        
```

**Run:**

*   **read** \- is used for user input
*   maintain order or arguments passed when run script
*   The variable **$#** holds the number of arguments passed to the script
*   The variable **$@** holds a space delimited string of all arguments passed to the script

### Array

```bash
#!/bin/bash

my_array=(apple banana "Fruit Basket" orange)
new_array[2]=lamon
echo ${#my_array[@]}        
```

*   An array is collection of variables means can hold several values under one name
*   Naming convention is same as variables
*   Initialized by assign space-delimited values enclosed in ( )
*   Array index is 0 based and some members of the array can be left uninitialized
*   The total number of elements in the array is referenced by **${#arrayname\[@\]}**

### Operator

```bash
#!/bin/bash

var=$((3+9))
echo $var

# $x -gt $y        
```

*   Bash script support +, -, /, \*\*, %, ++, --, -=, += numerical operators
*   Numerical expressions can also be calculated and stored in a variable using the syntax: var=$((expression))
*   It also support comparison logical operator like: -eq (equal), -gt (greater than), -ge (greater than equal), -lt (less than), -le (less than equal), -ne (mot equal)
*   Bash has some string operator as well: =, !=, -z (is empty), -n (is not empty)
*   Has some file test operator like: -f (file), -d (directory), -x (executable), -s (exist and not empty), -e (exist), -r (readable), -w (writeable)

### Decision Making

```bash
if [[ condition ]]
then
    statement
elif [[ condition ]]; then
    statement 
else
    do this by default
fi        
```

*   if ... else if... else is used for multiple or multilevel condition checking
*   \[ \[ \] \] is the condition block and here multiple condition is allowed by using &&, ||

```bash
case "$variable" in
    "$condition1" )
        command...
    ;;
    "$condition2" )
        command...
    ;;
esac        
```

*   case statement only can check equality
*   ;; is indicate break the case block execution

### Iteration and Looping

```bash
for arg in [list]
do
 command(s)...
done        
```

*   for loop iterate over a list or range or as long as condition true
*   allow **break** and **continue** like other programming language

```bash
while [ condition ]
do
 command(s)...
done        
```

*   while iterate as long as the condition true
*   allow **break** and **continue** like other programming language

```bash
until [ condition ]
do
 command(s)...
done        
```

*   it is opposite of while and iterate as long as condition false
*   allow **break** and **continue** like other programming language

### Function and Return (exit)

```bash
function function_name {
  command...
}

# to call function
funtion_name        
```

*   Functions help modularize your script
*   Helps to reuse redundant statement
*   function can return exit value
*   function can take argument as well
*   until call function nothing will happen
*   **$?** = exit status of the last command, (0 = success, non-zero = error)

### Piping and Redirection

```bash
command1 | command2 > output        
```

*   **Pipes** (|) is the way of combining multiple command together to execute one after another
*   **Redirection** (>, <, >>, <<, 2>, &>) is the way to redirect input output to or from a command

### Modular Script and Safe Run

```bash
source ./config.sh
set -o pipefail
trap 'echo "Something went wrong!"' ERR        
```

*   source import another bash script file into current one
*   set runs the script in safer mode with defined options
*   trap allows you to catch signals or errors and run some custom code when they occur

* * *

### Further Readings
- https://www.learnshell.org/en/Welcome

* * *

## Summary:

**Bash scripting** is a way to automate tasks by writing commands in a file and letting the system run them. It can use to manage servers, schedule backups, monitor systems, deploy apps, and more. Bash scripts has variables, loops, conditions, functions, modular support and many other features.

Good practices include using #!/bin/bash, enabling safe modes (set -euo pipefail), quoting variables, using functions for clean code, and validating inputs. Bad practices to avoid are using unquoted variables, hardcoding values, ignoring errors, or writing messy and unsafe scripts.

In short, Bash scripting is a powerful skill that lets you automate and manage systems efficiently.