# pipex

## Contents

1. [Project Overview](#1-Project-overview)
2. [Logic](#2-Logic)
3. [How to run](#3-How-to-run)

## 1. Project overview

The Pipex project is designed to replicate the behavior of UNIX pipes in C. It simulates the functionality of running two commands where the output of the first command is passed as input to the second, using file redirection. The program accepts four arguments: an input file (file1), two commands (cmd1 and cmd2), and an output file (file2), which mirrors the behavior of the following shell command:

```
< file1 cmd1 | cmd2 > file2
```

## 2. Logic

To implement this, the program opens the necessary files, creates a pipe between cmd1 and cmd2, forks processes to execute both commands, and uses dup2() to redirect the input/output. It then executes the commands with execve(). Proper error handling ensures that the program exits cleanly if any issues arise with file access or command execution.

For example, running:
```
$> ./pipex infile "grep i" "wc -l" outfile
```
should behave exactly as if you ran:
```
$> <infile grep "i" | wc -l > outfile
```

## 3. How to run
```
git clone https://github.com/dhuss42/pipex.git pipex
cd pipex
make
echo -e "I love pipex\nAnd bash scripting\nend" > infile
./pipex infile "grep i" "wc -l" outfile
```
