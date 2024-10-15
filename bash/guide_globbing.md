<!--
File: bash/guide_globbing.md
Repo: <https://github.com/kielmarj/cli-chronicles>
Updated: 2024-10-15
© 2024 Jessica Kielmar, (GitHub: kielmarj)
Licensed under the MIT License. See LICENSE file for details.
-->

# Guide to Shell Globbing
<!-- TOC -->

- [Guide to Shell Globbing](#guide-to-shell-globbing)
    - [What is globbing?](#what-is-globbing)
        - [When to use globbing](#when-to-use-globbing)
    - [Globbing is not regex](#globbing-is-not-regex)
        - [Summary of differences](#summary-of-differences)
    - [Distinctions between major shells](#distinctions-between-major-shells)
        - [Summary of distinctions](#summary-of-distinctions)
    - [Quick reference charts](#quick-reference-charts)
        - [Common globbing patterns](#common-globbing-patterns)
        - [Character classes](#character-classes)
    - [General usage notes](#general-usage-notes)

<!-- /TOC -->

## What is globbing?

Globbing is the process of using wildcard patterns to match filenames and paths in the shell. It allows users to specify multiple files or directories at once without typing each name individually. Globbing is primarily used in command-line environments to simplify file operations, such as listing, copying, moving, or deleting multiple files that match a particular pattern.

### When to use globbing

- **File Management**: To handle multiple files or directories at once. For example, `rm *.log` deletes all files with a .log extension.
- **Searching Files**: To search or list files matching a specific pattern. For instance, `ls file?.txt` lists all .txt files with names like file1.txt or fileA.txt.
- **Pattern Matching**: To perform actions on a group of files that have similar naming conventions. For example, `cp [a-c]*.txt backup/` copies files starting with a, b, or c to the backup directory.
- **Command Automation**: Useful in shell scripts to automate repetitive tasks involving similar sets of files.

## Globbing is **not** regex

Globbing and regular expressions (regex) are both pattern-matching techniques used to work with strings, but they differ significantly in their purpose, features, and complexity.

|             | Globbing                          | Regular Expressions (Regex)                         |
|-------------|-----------------------------------|-----------------------------------------------------|
| Use Case    | Filename and path matching        | Text search, extraction, validation, replacement    |
| Tools       | Shell commands (e.g., `ls`, `rm`) | grep, sed, awk, text editors, programming languages |
| Syntax      | Simple (`*`, `?`, `[ ]`)          | Complex (`^`, `$`, `\`, `+`, `\|`, `()`)            |
| Complexity  | Limited expressiveness            | Highly expressive, supports grouping, alternation   |
| Application | Automatically by the shell        | Explicit use in certain programs                    |

### Summary of differences

- **Globbing**
  - Primarily used in shells (e.g., Bash, Zsh, Fish) for matching file and directory names.
  - Simple and direct, tailored for file operations like listing `ls`, copying `cp`, deleting `rm`, etc.
    - Example: `*.txt` matches all files ending in `.txt`.
  - Simple and limited syntax. Common symbols are `*`, `?`, `[ ]`, and character classes.
  - `*` matches zero or more characters, `?` matches one character, and `[abc]` matches a set of specific characters.
  - Easier to learn and use, especially for basic file matching.
- **Regex**
  - Used for advanced pattern matching in text-processing tasks, such as text searching, extraction, or replacement.
  - Widely used in various programming languages and tools like `sed`, `awk`, `grep`, or even text editors like VSCode or Sublime.
    - Example: `^file\d+\.txt$` matches filenames like `file1.txt`, `file123.txt`.
  - Complex and highly expressive syntax, supporting multiple operators, quantifiers, assertions, lookarounds, and more.
  - Includes symbols like `^`, `$`, `\`, `+`, `|`, `()` for advanced matches.
  - More powerful, capable of complex matching logic like repetitions `+`, `*`, `{n,m}`, alternations `|`, and boundaries `\b`.

## Distinctions between major shells

The reference charts and notes included below were written with a focus on bash, but can still be useful for other shells as well.

Depending on the shell you're using, the globbing behavior can vary slightly, especially when dealing with advanced patterns. Always check the specific shell’s documentation for compatibility if you’re using less common patterns or advanced globbing.

While the basic principles and common patterns (`*`, `?`, `[ ]`) are similar across most Unix-like shells, there are subtle differences in behavior, features, and how advanced globbing patterns are handled. Here are some distinctions between major shells:

- **Bash** has extensive support for globbing.
  - It includes extended globbing with `shopt -s extglob`, allowing advanced patterns like:
    - `?(pattern)` (matches zero or one occurrence)
    - `*(pattern)` (matches zero or more occurrences)
    - `+(pattern)` (matches one or more occurrences)
    - `!(pattern)` (matches anything except the pattern)
- **Zsh** is known for its powerful and flexible globbing features, which are more advanced compared to Bash.
  - It supports additional wildcards like:
    - `**` for recursive directory matches (e.g., `**/*.txt` matches `.txt` files in all subdirectories).
  - It also provides `^` as a negation character (`^pattern` negates the pattern).
  - Zsh enables extended globbing by default without additional configuration.
- **Fish shell** has a simplified approach to globbing.
  - It supports `*`, `?`, and `[ ]` for basic globbing but does not support Bash-style extended globbing (`extglob`).
  - Recursive matching (`**`) is supported in Fish, similar to Zsh.
- **Dash** commonly used as a lightweight `/bin/sh` shell, dash only supports very basic globbing (`*`, `?`, `[ ]`).
  - It lacks support for extended or advanced globbing features like those in Bash or Zsh.
- **KornShell (ksh)** supports advanced globbing similar to Bash with extended pattern matching.
  - It also allows recursive globbing using `**` for matching files in subdirectories.

### Summary of distinctions

- **Basic Glob Patterns** (`*`, `?`, `[ ]`) are supported in all major shells.
- **Extended Globbing**: Bash and ksh require enabling features (`shopt -s extglob`).
- **Advanced Features**: Zsh offers the most robust set of globbing tools and is enabled by default.
- **Recursive Globbing**: `**` is supported in Zsh, Fish, and with `extglob` in Bash.

## Quick reference charts

### Common globbing patterns

| Pattern                 | Description & Examples                                                                                                                              |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| `*`                     | Matches zero or more characters. <br> **Example**: `*.txt` matches `file.txt`, `report.txt`. Does **not** match hidden files (e.g., `.hidden`).     |
| `?`                     | Matches exactly one character. <br> **Example**: `file?.txt` matches `file1.txt`, `fileA.txt`, but not `file12.txt`.                                |
| `[abc]`                 | Matches one character: `a`, `b`, or `c`. <br> **Example**: `file[abc].txt` matches `filea.txt`, `fileb.txt`, `filec.txt`.                           |
| `[^abc]`                | Matches one character **not** `a`, `b`, or `c`. <br> **Example**: `file[^abc].txt` matches `filed.txt`, `filee.txt`, but **not** `filea.txt`.       |
| `[x-y]`                 | Matches one character within range `x` to `y`. <br> **Example**: `[0-9]` matches any digit (`0`-`9`), `[a-f]` matches `a`, `b`, `c`, `d`, `e`, `f`. |
| `[^x-y]`                | Matches one character **not** in range `x` to `y`. <br> **Example**: `[^a-f]` matches any character **except** `a` to `f`.                          |
| `[x\-y]`                | Matches one character: `x`, `-`, or `y`. Hyphen is treated as a literal. <br> **Example**: `[a\-z]` matches `a`, `-`, `z`.                          |
| `[[:character_class:]]` | Matches one character from a predefined character class (e.g., `[:alpha:]`). <br> **Example**: `[[:digit:]]` matches `0-9`.                         |
| `[][]`                  | Matches either `[` or `]`. Useful for literal square brackets. <br> **Example**: `file[[]].txt` matches `file[.txt`, `file].txt`.                   |
| `[[:alpha:]]`           | Matches any alphabetic character (`a-z`, `A-Z`). <br> **Example**: `file[[:alpha:]].txt` matches `filea.txt`, `fileB.txt`.                          |
| `[[:alnum:]]`           | Matches any alphanumeric character (`a-z`, `A-Z`, `0-9`). <br> **Example**: `name[[:alnum:]].txt` matches `name1.txt`, `nameA.txt`.                 |
| `[[:graph:]]`           | Matches visible characters, excluding spaces. <br> **Example**: `[[:graph:]]file.txt` matches `@file.txt`, but **not** `file.txt`.                  |
| `[[:print:]]`           | Matches printable characters, including spaces. <br> **Example**: `[[:print:]]output.txt` matches `output.txt`.                                     |

### Character classes

| Class Name | Description & Examples                                                                                    |
|------------|-----------------------------------------------------------------------------------------------------------|
| `lower`    | Matches lowercase letters (`a-z`). <br> **Example**: `[[:lower:]]` matches `a`, `b`, `c`.                 |
| `upper`    | Matches uppercase letters (`A-Z`). <br> **Example**: `[[:upper:]]` matches `A`, `B`, `C`.                 |
| `digit`    | Matches digits (`0-9`). <br> **Example**: `[[:digit:]]` matches `1`, `5`, `9`.                            |
| `alnum`    | Matches letters and digits (`a-z`, `A-Z`, `0-9`). <br> **Example**: `[[:alnum:]]` matches `g`, `8`, `G`.  |
| `space`    | Matches any whitespace character (spaces, tabs). <br> **Example**: `[[:space:]]` matches space or tab.    |
| `blank`    | Matches spaces and tabs only. <br> **Example**: `echo[[:blank:]]text` matches `echo<tab>text`.            |
| `xdigit`   | Matches hexadecimal digits (`0-9`, `A-F`, `a-f`). <br> **Example**: `[[:xdigit:]]` matches `A`, `f`, `9`. |
| `punct`    | Matches punctuation characters. <br> **Example**: `[[:punct:]]` matches `.`, `,`, `!`, `?`.               |
| `cntrl`    | Matches control characters (`\n`, `\t`). <br> **Example**: `[[:cntrl:]]` matches newlines or tabs.        |
| `graph`    | Matches visible characters excluding spaces. <br> **Example**: `[[:graph:]]` matches `@`, `%`, `9`.       |
| `print`    | Matches all printable characters, including spaces. <br> **Example**: `[[:print:]]` matches ``, `A`, `?`. |

## General usage notes

- **Literal Characters**: To match `]` in brackets, place it at the beginning or escape it (`[\]]`).
- **Hyphen Usage**: Include a literal hyphen by placing it first/last or escaping it (`[x\-y]`).
- **Multiple Ranges**: Use multiple ranges to match various character sets. Example: `[0-9A-Fa-f]` matches hexadecimal characters.

<sub>© 2024 [kielmarj](https://github.com/kielmarj), under the MIT License</sub>
