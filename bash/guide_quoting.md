<!--
File: bash/guide_quoting.md
Repo: <https://github.com/kielmarj/cli-chronicles>
Updated: 2024-10-15
© 2024 Jessica Kielmar, (GitHub: kielmarj)
Licensed under the MIT License. See LICENSE file for details.
-->

# Guide to quoting in bash
<!-- TOC -->

- [Guide to quoting in bash](#guide-to-quoting-in-bash)
    - [Single quotes '...'](#single-quotes-)
        - [Key properties](#key-properties)
        - [Example of single-quoted special characters](#example-of-single-quoted-special-characters)
        - [Use single quotes when](#use-single-quotes-when)
    - [Double quotes "..."](#double-quotes-)
        - [Key properties](#key-properties)
        - [Example of double-quoted variable substitution](#example-of-double-quoted-variable-substitution)
        - [Example of double-quoted command substitution](#example-of-double-quoted-command-substitution)
        - [Use double quotes when](#use-double-quotes-when)
    - [Backslashes](#backslashes)
        - [Key properties](#key-properties)
        - [Backslash example](#backslash-example)
        - [Use backslashes when](#use-backslashes-when)
    - [Combining quotes](#combining-quotes)
        - [Example of mixed quotes](#example-of-mixed-quotes)
    - [Practical scenarios for quoting](#practical-scenarios-for-quoting)
        - [Handling filenames with spaces](#handling-filenames-with-spaces)
        - [Preventing Word Splitting in Loops](#preventing-word-splitting-in-loops)
    - [Common Pitfalls with Quoting](#common-pitfalls-with-quoting)
        - [Missing Quotes Around Variables](#missing-quotes-around-variables)
        - [Using Quotes with find or xargs](#using-quotes-with-find-or-xargs)
        - [Improper Mixing of Quotes](#improper-mixing-of-quotes)

<!-- /TOC -->

## Single quotes `'...'`

Single quotes are the most straightforward form of quoting in Bash. They are employed when the enclosed text should be interpreted literally, without processing special characters, variables, or escape sequences.

### Key properties

- Text within single quotes is treated verbatim.
- No interpolation occurs (variables are not expanded, and special characters are not processed).

### Example of single-quoted special characters

```bash
message='This is $100. Use "echo" to print.'
echo $message
```

```result
This is $100. Use "echo" to print.
```

Here, the `$` symbol and the double quotes `"` are taken literally, rather than being treated as a variable or special character.

### Use single quotes when

- You need to completely neutralize the interpretation of characters within a string.
- The text contains multiple special characters that should not be interpreted by the shell.

## Double quotes `"..."`

Double quotes offer an intermediate level of interpretation. They allow variable and command substitution while preserving other special characters, such as spaces.

### Key properties

- Variables and command substitutions are expanded.
- Literal interpretation is applied to other special characters, such as spaces.

### Example of double-quoted variable substitution

```bash
name="Jess"
greeting="Hello, $name! Welcome to the Bash world."
echo $greeting
```

```result
Hello, Jess! Welcome to the Bash world.
```

In this example, the variable $name is expanded within double quotes, which is useful for dynamic string construction.

### Example of double-quoted command substitution

```bash
echo "The date today is: $(date)"
```

```result
The date today is: Tue Oct 15 02:21:25 AM EDT 2024
```

This will output the current date because command substitution is expanded within double quotes.

### Use double quotes when

- You need to embed variables or commands within a string.
- The string contains spaces or other special characters that should be preserved.

## Backslashes

A backslash serves as an escape character for individual characters, causing only the character immediately following the backslash to be treated literally.

### Key properties

- Used for escaping a single special character.
- Often used to preserve a literal character within a double-quoted string.

### Backslash example

```bash
echo "This is a quote: \""
```

```result
This is a quote: "
```

In this instance, the backslash prevents the double quote from being interpreted as the end of the string.

### Use backslashes when

- You need to escape a specific character within a string without quoting the entire string.

## Combining quotes

In some cases, combining different quoting styles is necessary to achieve the desired behavior.

### Example of mixed quotes

```bash
name='Jess'
echo "Hello, $name! Here's a single quote: ' and a literal dollar sign: \$"
```

```result
Hello, Jess! Here's a single quote: ' and a literal dollar sign: $
```

In this example, double quotes allow variable expansion of "$name". Single quotes are interpreted literally. Backslash escapes the literal dollar sign.

## Practical scenarios for quoting

### Handling filenames with spaces

When dealing with files that have spaces in their names, quoting is crucial to avoid unintended word splitting.

Example:

```bash
filename="My File.txt"
echo "The filename is: $filename"
```

```result
The filename is: My File.txt
```

Without quoting, My File.txt would be treated as two separate words, leading to errors when manipulating the file.

### Preventing Word Splitting in Loops

When iterating over a list of items, quoting can help prevent issues arising from word splitting.

Example (`$files` unquoted):

```bash
files="file1.txt file2.txt file 3.txt"
for f in $files; do
  echo "$f"
done
```

```result
file1.txt
file2.txt
file
3.txt
```

Example (`"$files"` double-quoted):

```bash
files="file1.txt file2.txt file 3.txt"
for f in "$files"; do
  echo "$f"
done
```

```result
file1.txt file2.txt file 3.txt
```

## Common Pitfalls with Quoting

### Missing Quotes Around Variables

Neglecting to quote variables can result in unintended behavior, particularly when the variable contains spaces.

Example:

```bash
path="/some/path with spaces"
cd $path  # Incorrect: may fail if the variable contains spaces.
cd "$path"  # Correct: ensures that spaces are preserved.
```

### Using Quotes with find or xargs

When utilizing commands such as find or xargs, ensure proper quoting to prevent issues with filenames containing special characters.

Example for finding every .txt file in your current directory. (Note that this may output A LOT of files depending on your current directory and how much of a data hoarder you are. I CTRL+C'd somewhere in the thousands...)

```bash
find . -name "*.txt" -exec echo "Found file: {}" \;
```

### Improper Mixing of Quotes

It is important to note that single quotes cannot be nested within other single quotes without being escaped.

Incorrect Example:

```bash
echo 'It's a nice day'  # Syntax error
```

**Correct Example:**

```bash
echo 'It'\''s a nice day'
```

```result
It's a nice day
```

The sequence `'\''` effectively terminates the original single-quoted string, introduces a literal single quote, and then resumes the single-quoted string.

<sub>© 2024 [kielmarj](https://github.com/kielmarj), under the MIT License</sub>
