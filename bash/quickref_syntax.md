<!--
File: bash/quickref_syntax.md
Repo: <https://github.com/kielmarj/cli-chronicles>
Updated: 2024-10-15
© 2024 Jessica Kielmar, (GitHub: kielmarj)
Licensed under the MIT License. See LICENSE file for details.
-->

# Bash Syntax Quick Reference

<!-- TOC -->

- [Bash Syntax Quick Reference](#bash-syntax-quick-reference)
    - [General Operators](#general-operators)
    - [Variable Expansion](#variable-expansion)
    - [Control Structures](#control-structures)
    - [Functions & Arrays](#functions--arrays)
    - [Evaluations](#evaluations)
    - [File Operations](#file-operations)
    - [Job Control](#job-control)
    - [Conditional Tests](#conditional-tests)
    - [Debugging](#debugging)
    - [Miscellaneous](#miscellaneous)

<!-- /TOC -->

## General Operators

| Operator | Description                 | Example                    |
|----------|-----------------------------|----------------------------|
| `=`      | Assign variable             | `var=value`                |
| `;`      | Command separator           | `cmd1; cmd2`               |
| `&`      | Run in background           | `cmd1 &`                   |
| `\|`     | Pipe output                 | `cmd1 \| cmd2`             |
| `&&`     | Run if success              | `cmd1 && cmd2`             |
| `\|\|`   | Run if fail                 | `cmd1 \|\| cmd2`           |
| `>`      | Redirect stdout (overwrite) | `cmd > file.txt`           |
| `>>`     | Redirect stdout (append)    | `echo "Hello" >> file.txt` |
| `2>`     | Redirect stderr             | `cmd1 2> error.log`        |
| `&>`     | Redirect stdout & stderr    | `cmd1 &> output.log`       |
| `$( )`   | Command substitution        | `var=$(cmd1)`              |

## Variable Expansion

| Syntax                | Description       | Example                   |
|-----------------------|-------------------|---------------------------|
| `${}`                 | Expand variable   | `echo ${VAR}`             |
| `${#var}`             | Length of string  | `echo ${#my_string}`      |
| `${var:start:length}` | Substring         | `echo ${my_string:2:4}`   |
| `${var/old/new}`      | Replace in string | `echo ${my_var/old/new}`  |
| `${var:-default}`     | Default if unset  | `echo ${my_var:-default}` |

## Control Structures

| Structure        | Example                                                                             |
|------------------|-------------------------------------------------------------------------------------|
| `if...then...fi` | `if [ "$var" -eq 1 ]; then echo "Variable is 1"; fi`                                |
| `if...else...fi` | `if [ "$var" -eq 1 ]; then echo "Variable is 1"; else echo "Variable is not 1"; fi` |
| `elif`           | `if [ "$var" -eq 1 ]; then echo "One"; elif [ "$var" -eq 2 ]; then echo "Two"; fi`  |
| `for` loop       | `for i in {1..5}; do echo $i; done`                                                 |
| `while` loop     | `while [ "$count" -lt 5 ]; do echo $count; ((count++)); done`                       |
| `until` loop     | `until [ "$count" -eq 5 ]; do echo $count; ((count++)); done`                       |
| `case...esac`    | `case "$var" in 1) echo "One" ;; 2) echo "Two" ;; *) echo "Other" ;; esac`          |

## Functions & Arrays

| Structure         | Example                            |
|-------------------|------------------------------------|
| `function`        | `function greet { echo "Hi $1"; }` |
| `array=( )`       | `my_array=(one two three)`         |
| `${array[@]}`     | `echo ${my_array[@]}`              |
| `${array[index]}` | `echo ${my_array[1]}`              |

## Evaluations

| Syntax   | Example                   |
|----------|---------------------------|
| `[]`     | `[ "$var" -eq 1 ]`        |
| `[[ ]]`  | `[[ "$var" == "value" ]]` |
| `$(( ))` | `echo $((5 + 3))`         |
| `let`    | `let count+=1`            |

## File Operations

| Command | Example                   |
|---------|---------------------------|
| `>`     | `cmd > file.txt`          |
| `>>`    | `echo "data" >> file.txt` |
| `<`     | `cmd < file.txt`          |
| `\|`    | `cmd1 \| cmd2`            |
| `tee`   | `cmd \| tee file.txt`     |

## Job Control

| Command  | Example              |
|----------|----------------------|
| `&`      | `cmd &`              |
| `wait`   | `wait $pid`          |
| `jobs`   | `jobs`               |
| `$!`     | `sleep 10 & echo $!` |
| `fg`     | `fg %1`              |
| `bg`     | `bg %1`              |
| `disown` | `disown %1`          |
| `kill`   | `kill 1234`          |

## Conditional Tests

| Condition           | Example             |
|---------------------|---------------------|
| `-z` (empty)        | `[[ -z $VAR ]]`     |
| `-n` (not empty)    | `[[ -n $VAR ]]`     |
| `-d` (is directory) | `[[ -d /home ]]`    |
| `-f` (is file)      | `[[ -f file.txt ]]` |
| `-r` (is readable)  | `[[ -r file.txt ]]` |

## Debugging

| Command           | Description             |
|-------------------|-------------------------|
| `set -e`          | Exit on error           |
| `set -o pipefail` | Exit on pipe error      |
| `set -o nounset`  | Error on unset variable |
| `set -o xtrace`   | Debug trace             |

## Miscellaneous

| Command  | Example                   |
|----------|---------------------------|
| `alias`  | `alias ll='ls -la'`       |
| `export` | `export VAR=value`        |
| `source` | `source script.sh`        |
| `trap`   | `trap "echo stop" SIGINT` |

<sub>© 2024 [kielmarj](https://github.com/kielmarj), under the MIT License</sub>
