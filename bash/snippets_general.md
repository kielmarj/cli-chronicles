<!--
File: bash/snippets_general.md
Repo: <https://github.com/kielmarj/cli-chronicles>
Updated: 2024-10-15
© 2024 Jessica Kielmar, (GitHub: kielmarj)
Licensed under the MIT License. See LICENSE file for details.
-->

# Bash snippets

General bash snippets for various scripting purposes.

<!-- TOC -->

- [Bash snippets](#bash-snippets)
    - [Basic Script Structure](#basic-script-structure)
    - [Variables](#variables)
    - [User Input](#user-input)
    - [Conditional Statements](#conditional-statements)
    - [For Loop](#for-loop)
    - [While Loop](#while-loop)
    - [Functions](#functions)
    - [Array Handling](#array-handling)
    - [String Operations](#string-operations)
    - [Check if a file exists](#check-if-a-file-exists)
    - [Reading from a file](#reading-from-a-file)
    - [Redirection and Piping](#redirection-and-piping)
    - [Process Management](#process-management)
    - [Error Handling](#error-handling)
    - [Argument Validation and Processing](#argument-validation-and-processing)
        - [Check if an argument is provided](#check-if-an-argument-is-provided)
        - [Positional arguments](#positional-arguments)
        - [Validate if Argument is a Number](#validate-if-argument-is-a-number)
        - [Validate if Argument is a File](#validate-if-argument-is-a-file)
        - [Validate if Argument is a Directory](#validate-if-argument-is-a-directory)
        - [Validate IP Address Format](#validate-ip-address-format)
        - [Validate Email Format](#validate-email-format)
        - [Validate Multiple Arguments File and Number](#validate-multiple-arguments-file-and-number)
    - [Case Statement](#case-statement)
    - [Environment Variables](#environment-variables)
    - [Date and Time](#date-and-time)
    - [Logging](#logging)
    - [Trap and Cleanup](#trap-and-cleanup)
    - [Working with JSON using jq](#working-with-json-using-jq)
    - [Networking](#networking)

<!-- /TOC -->

## Basic Script Structure

```bash
#!/bin/bash
# This is a comment

# Run the script with: ./script.sh
```

## Variables

```bash
# Declare variables
name="John"
age=25

# Access variables
echo "Name: $name, Age: $age"
```

## User Input

```bash
# Read user input
echo "Enter your name: "
read user_name
echo "Hello, $user_name!"
```

## Conditional Statements

```bash
# If-else condition
if [ "$age" -ge 18 ]; then
  echo "You are an adult."
else
  echo "You are a minor."
fi

# Using elif
if [ "$name" == "John" ]; then
  echo "Hello, John!"
elif [ "$name" == "Doe" ]; then
  echo "Hello, Doe!"
else
  echo "Who are you?"
fi
```

## For Loop

```bash
# Iterating over a list of items
for i in 1 2 3 4 5; do
  echo "Number: $i"
done

# Looping over files in a directory
for file in /path/to/dir/*; do
  echo "File: $file"
done
```

## While Loop

```bash
# While loop example
count=1
while [ $count -le 5 ]; do
  echo "Count: $count"
  count=$((count+1))
done
```

## Functions

```bash
# Define a function
greet() {
  local name=$1  # Local variable within function
  echo "Hello, $name!"
}

# Call a function
greet "Alice"
```

## Array Handling

```bash
# Declare an array
arr=("apple" "banana" "cherry")

# Access array elements
echo ${arr[0]}   # Outputs: apple
echo ${arr[@]}   # Outputs all elements: apple banana cherry

# Iterate over an array
for element in "${arr[@]}"; do
  echo "$element"
done
```

## String Operations

```bash
# String length
str="Hello"
echo ${#str}  # Outputs: 5

# Substring extraction
echo ${str:1:3}  # Outputs: ell (from index 1, length 3)

# String replacement
new_str=${str/Hello/Hi}
echo $new_str  # Outputs: Hi
```

## Check if a file exists

```bash
if [ -f "/path/to/file" ]; then
  echo "File exists."
else
  echo "File does not exist."
fi
```

## Reading from a file

```bash
# Read line by line
while IFS= read -r line; do
  echo "$line"
done < /path/to/file.txt
```

## Redirection and Piping

```bash
# Redirect output to a file
echo "Hello World" > output.txt  # Overwrites file
echo "Another line" >> output.txt  # Appends to file

# Redirect stderr
command 2> error.log  # Redirects errors to a file

# Pipe output to another command
ls -l | grep ".txt"
```

## Process Management

```bash
# Get process ID of the current script
echo $$

# Run a command in the background
long_running_command &

# Wait for background jobs to finish
wait
```

## Error Handling

```bash
# Exit immediately if any command exits with a non-zero status
set -e

# Capture exit status of a command
command
if [ $? -eq 0 ]; then
  echo "Command succeeded."
else
  echo "Command failed."
fi
```

## Argument Validation and Processing

### Check if an argument is provided

```bash
#!/bin/bash

# Check if at least one argument is passed
if [ "$#" -eq 0 ]; then
  echo "Usage: $0 arg1 arg2 ..."
  exit 1
fi
```

### Positional arguments

```bash
```bash
# Access positional arguments
echo "First argument: $1"
echo "Second argument: $2"
echo "All arguments: $@"

# Check number of arguments
if [ "$#" -lt 2 ]; then
  echo "Usage: ./script.sh arg1 arg2"
  exit 1
fi
```

### Validate if Argument is a Number

```bash
#!/bin/bash

validate_number() {
  re='^[0-9]+$'  # Regular expression to check for numbers
  if ! [[ "$1" =~ $re ]]; then
    echo "Error: $1 is not a valid number."
    exit 1
  fi
}

# Example usage
validate_number "$1"  # Pass first argument for validation

echo "Number $1 is valid."
```

### Validate if Argument is a File

```bash
#!/bin/bash

validate_file() {
  if [ ! -f "$1" ]; then
    echo "Error: File $1 does not exist."
    exit 1
  fi
}

# Example usage
validate_file "$1"  # Pass first argument for validation

echo "File $1 exists."
```

### Validate if Argument is a Directory

```bash
#!/bin/bash

validate_directory() {
  if [ ! -d "$1" ]; then
    echo "Error: Directory $1 does not exist."
    exit 1
  fi
}

# Example usage
validate_directory "$1"  # Pass first argument for validation

echo "Directory $1 exists."
```

### Validate IP Address Format

```bash
#!/bin/bash

validate_ip() {
  local ip=$1
  local stat=1

  if [[ $ip =~ ^([0-9]{1,3}\.){3}[0-9]{1,3}$ ]]; then
    stat=0
    for i in {1..4}; do
      if [ "$(echo "$ip" | cut -d. -f$i)" -gt 255 ]; then
        stat=1
        break
      fi
    done
  fi

  if [ $stat -ne 0 ]; then
    echo "Error: Invalid IP address $ip."
    exit 1
  fi
}

# Example usage
validate_ip "$1"  # Pass first argument for validation

echo "IP Address $1 is valid."
```

### Validate Email Format

```bash
#!/bin/bash

validate_email() {
  local email=$1
  local regex="^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$"

  if ! [[ $email =~ $regex ]]; then
    echo "Error: Invalid email address $email."
    exit 1
  fi
}

# Example usage
validate_email "$1"  # Pass first argument for validation

echo "Email $1 is valid."
```

### Validate Multiple Arguments (File and Number)

```bash
#!/bin/bash

# Check if correct number of arguments is provided
if [ "$#" -ne 2 ]; then
  echo "Usage: $0 <file> <number>"
  exit 1
fi

# Validate file
if [ ! -f "$1" ]; then
  echo "Error: $1 is not a valid file."
  exit 1
fi

# Validate number
if ! [[ "$2" =~ ^[0-9]+$ ]]; then
  echo "Error: $2 is not a valid number."
  exit 1
fi

echo "File $1 and number $2 are both valid."
```

## Case Statement

```bash
# Case statement example
case "$1" in
  start)
    echo "Starting..."
    ;;
  stop)
    echo "Stopping..."
    ;;
  restart)
    echo "Restarting..."
    ;;
  *)
    echo "Usage: $0 {start|stop|restart}"
    exit 1
esac
```

## Environment Variables

```bash
# Access environment variables
echo "Home directory: $HOME"
echo "Shell: $SHELL"

# Set an environment variable
export MY_VAR="value"
```

## Date and Time

```bash
# Get current date and time
echo "Current date: $(date)"

# Format date
echo "Formatted date: $(date +"%Y-%m-%d %H:%M:%S")"
```

## Logging

```bash
# Simple logging to file
log_file="/path/to/logfile.log"
echo "$(date +"%Y-%m-%d %H:%M:%S") - Log message" >> $log_file
```

## Trap and Cleanup

```bash
# Trap signals and perform cleanup
trap "echo 'Script terminated'; exit" SIGINT SIGTERM

# Example cleanup function
cleanup() {
  echo "Cleaning up..."
  rm -f /tmp/tempfile
}
trap cleanup EXIT
```

## Working with JSON (using jq)

```bash
# Parse JSON with jq
json='{"name": "John", "age": 30}'
echo $json | jq '.name'  # Outputs: "John"
```

## Networking

```bash
# Ping a host
ping -c 4 google.com

# Fetch content from a URL
curl https://example.com

# Download a file
wget https://example.com/file.zip
```

<sub>© 2024 [kielmarj](https://github.com/kielmarj), under the MIT License</sub>
