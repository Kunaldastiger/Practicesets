## Bash Scripting Guide

Bash (Bourne Again SHell) is a popular Unix shell and command language. It provides a powerful scripting environment for automating tasks and executing commands in a Unix-like operating system.

### Variables

Variables in Bash are used to store data and can be referenced later in the script.

Example 1: Variable assignment and usage
```bash
name="John Doe"
age=30

echo "Name: $name"
echo "Age: $age"
```

### Conditional Statements

Bash provides conditional statements to control the flow of execution based on certain conditions.

Example 2: If-else statement
```bash
age=18

if [ $age -ge 18 ]; then
    echo "You are eligible to vote."
else
    echo "You are not eligible to vote."
fi
```

### Loops

Bash supports various types of loops to iterate over lists of data or perform repetitive tasks.

Example 3: For loop
```bash
names=("Alice" "Bob" "Charlie")

for name in "${names[@]}"; do
    echo "Hello, $name!"
done
```

Example 4: While loop
```bash
count=0

while [ $count -lt 5 ]; do
    echo "Count: $count"
    count=$((count + 1))
done
```

### Command Substitution

Command substitution allows capturing the output of a command and storing it in a variable.

Example 5: Command substitution
```bash
current_date=$(date +"%Y-%m-%d")
echo "Current date: $current_date"
```

### Input/Output Redirection

Bash provides input/output redirection to control where the input comes from and where the output goes.

Example 6: Input/output redirection
```bash
# Redirecting output to a file
ls -l > file_list.txt

# Appending output to a file
echo "New line" >> file_list.txt

# Redirecting input from a file
sort < file_list.txt
```

### Pipes

Pipes allow connecting the output of one command as the input of another, enabling powerful command combinations.

Example 7: Pipes
```bash
# Listing files and filtering the output
ls -l | grep ".txt"

# Sorting and counting lines
cat file_list.txt | sort | wc -l
```

### Environment Variables

Bash provides environment variables that store system information or user-defined values.

Example 8: Environment variables
```bash
echo "User: $USER"
echo "Home directory: $HOME"
echo "Path: $PATH"
```

### Conditional Execution

Bash allows executing commands conditionally based on the success or failure of previous commands.

Example 9: Conditional execution
```bash
# Execute the second command only if the first command succeeds
command1 && command2

# Execute the second command only if the first command fails
command1 || command2
```

### Popular Bash Tools

Bash provides a variety of tools and utilities that are frequently used in shell scripting. Here are some popular ones:

#### grep: Search files for patterns.

Example 10: Using `grep`
```bash
# Search for lines containing "error" in a log file
grep "error" logfile.txt
```

#### sed: Stream editor for text transformation.

Example 11: Using `sed`
```bash
# Replace all occurrences of "foo" with "bar" in a file
sed 's/foo/bar/g' file.txt
```

#### awk: Text processing language.

Example 12: Using `awk`
```bash


# Print the second field of each line in a file
awk '{print $2}' file.txt
```

#### cut: Extract sections from lines of files.

Example 13: Using `cut`
```bash
# Extract the first column from a CSV file
cut -d ',' -f 1 data.csv
```

#### find: Search for files and directories.

Example 14: Using `find`
```bash
# Find all text files in the current directory
find . -name "*.txt"
```

#### xargs: Build and execute commands from input.

Example 15: Using `xargs`
```bash
# Remove multiple files using xargs
echo "file1.txt file2.txt file3.txt" | xargs rm
```

#### sort: Sort lines of text files.

Example 16: Using `sort`
```bash
# Sort lines in a file in alphabetical order
sort file.txt
```

#### wc: Count lines, words, or characters in a file.

Example 17: Using `wc`
```bash
# Count the number of lines in a file
wc -l file.txt
```

#### tar: Archive files.

Example 18: Using `tar`
```bash
# Create a tar archive of a directory
tar -czvf archive.tar.gz directory/
```

#### curl: Transfer data from or to a server.

Example 19: Using `curl`
```bash
# Download a file from a URL
curl -O https://example.com/file.txt
```

#### ssh: Securely connect to a remote server.

Example 20: Using `ssh`
```bash
# Connect to a remote server
ssh username@hostname
```

This guide provides a basic overview of Bash scripting, covering variables, conditional statements, loops, command substitution, input/output redirection, pipes, environment variables, conditional execution, and popular Bash tools. You can explore these topics further and combine them to create powerful scripts for various tasks in a Unix-like environment.
