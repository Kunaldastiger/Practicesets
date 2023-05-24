
## Python Scripting Guide

### Regular Expressions (regex)

Regular expressions are powerful tools for pattern matching and text manipulation. Python provides the `re` module for working with regular expressions.

Example 1: Matching a pattern in a string using regex
```python
import re

text = "Hello, my name is John Doe. I live in New York."
pattern = r"John \w+"

match = re.search(pattern, text)
if match:
    print("Match found:", match.group())
else:
    print("No match found.")
```

Example 2: Replacing a pattern in a string using regex
```python
import re

text = "Hello, my name is John Doe. I live in New York."
pattern = r"John \w+"

new_text = re.sub(pattern, "Jane Smith", text)
print("Modified text:", new_text)
```

### File and Directory Operations (os module)

The `os` module provides functions for interacting with the operating system, including file and directory operations.

Example 3: Checking if a file or directory exists
```python
import os

path = "/path/to/file.txt"

if os.path.exists(path):
    print("File or directory exists.")
else:
    print("File or directory does not exist.")
```

Example 4: Listing files in a directory
```python
import os

directory = "/path/to/directory"

files = os.listdir(directory)
for file in files:
    print(file)
```

### Running External Commands (subprocess module)

The `subprocess` module allows you to run external commands and interact with the command-line interface.

Example 5: Running a command and capturing its output
```python
import subprocess

command = "ls -l"
output = subprocess.check_output(command, shell=True)

print("Command output:")
print(output.decode("utf-8"))
```

Example 6: Running a command and getting its exit status
```python
import subprocess

command = "git status"
exit_code = subprocess.call(command, shell=True)

if exit_code == 0:
    print("Command executed successfully.")
else:
    print("Command failed with exit code:", exit_code)
```

### Error Handling

Python provides a mechanism for handling errors using try-except blocks.

Example 7: Handling exceptions
```python
try:
    # Code that might raise an exception
    result = 10 / 0
except ZeroDivisionError:
    print("Error: Division by zero.")
except Exception as e:
    print("Error:", str(e))
```

### Command-Line Arguments (sys module)

The `sys` module provides access to system-specific parameters and functions, including command-line arguments.

Example 8: Accessing command-line arguments
```python
import sys

args = sys.argv[1:]  # Exclude the script name
print("Command-line arguments:", args)
```

Example 9: Parsing command-line arguments with argparse
```python
import argparse

parser = argparse.ArgumentParser(description="A script with command-line arguments.")
parser.add_argument("-f", "--file", help="Input file path", required=True)
parser.add_argument("-o", "--output", help="Output file path")
args = parser.parse_args()

print("Input file:", args.file)
print("Output file:", args.output)
```

This guide provides a basic overview of Python scripting, covering regex, os module, subprocess module, error handling, and command-line arguments. You can explore these topics further and combine them to create powerful scripts for various tasks.
