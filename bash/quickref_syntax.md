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
    - [Conditional Expressions](#conditional-expressions)
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
| `&&`     | Logical AND                 | `cmd1 && cmd2`             |
| `\|\|`   | Logical OR                  | `cmd1 \|\| cmd2`           |
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

| Syntax   | Example                     |
|----------|-----------------------------|
| `[]`     | `[ "$var" -eq 1 ]`\*        |
| `[[ ]]`  | `[[ "$var" == "value" ]]`\* |
| `$(( ))` | `echo $((5 + 3))`           |
| `let`    | `let count+=1`              |

* `[[ ]]` is bash's extended version of the POSIX `[ ]` more versatile way to evaluate conditions and offers more features than `[ ]`.

## File Operations

| Command | Example                   |
|---------|---------------------------|
| `>`     | `cmd > file.txt`          |
| `>>`    | `echo "data" >> file.txt` |
| `<`     | `cmd < file.txt`          |
| `\|`    | `cmd1 \| cmd2`            |
| `tee`   | `cmd \| tee file.txt`     |


## Conditional Expressions

|                      | True if. . .                                             |
|----------------------|----------------------------------------------------------|
| `-a file`            | file exists                                              |
| `-d file`            | file exists and is a directory                           |
| `-e file`            | file exists                                              |
| `-f file`            | file exists and is a regular file                        |
| `-h file`            | file exists and is a symbolic link                       |
| `-r file`            | file exists and is readable                              |
| `-s file`            | file exists and has a size greater than zero             |
| `-w file`            | file exists and is writable                              |
| `-x file`            | file exists and is executable                            |
| `-L file`            | file exists and is a symbolic link                       |
| `-N file`            | file exists and has been modified since it was last read |
| `-n string`          | the length of string is non-zero                         |
| `-z string`          | the length of string is zero                             |
| `string1 == string2` | the strings are equal                                    |
| `string1 != string2` | the strings are not equal                                |
| `string1 < string2`  | string1 sorts before string2 lexicographically           |
| `string1 > string2`  | string2 sorts after string2 lexicographically            |
| `arg1 -eq arg2`      | arg1 is equal to arg2                                    |
| `arg1 -ne arg2`      | arg1 is not equal to arg2                                |
| `arg1 -lt arg2`      | arg1 is less than arg2                                   |
| `arg1 -le arg2`      | arg1 is less than or equal to arg2                       |
| `arg1 -gt arg2`      | arg1 is greater than arg2                                |
| `arg1 -ge arg2`      | arg1 is greater than or equal to arg2                    |


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
