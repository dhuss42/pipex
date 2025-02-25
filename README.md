# pipex

The Pipex project is designed to replicate the behavior of UNIX pipes in C. It simulates the functionality of running two commands where the output of the first command is passed as input to the second, using file redirection. The program accepts four arguments: an input file (file1), two commands (cmd1 and cmd2), and an output file (file2), which mirrors the behavior of the following shell command:

```
< file1 cmd1 | cmd2 > file2
```

To implement this, the program opens the necessary files, creates a pipe between cmd1 and cmd2, forks processes to execute both commands, and uses dup2() to redirect the input/output. It then executes the commands with execve(). Proper error handling ensures that the program exits cleanly if any issues arise with file access or command execution.

For example, running:
```
$> ./pipex infile "ls -l" "wc -l" outfile
```
should behave exactly as if you ran:
```
$> < infile ls -l | wc -l > outfile
```
The focus of the project is on process control, file handling, and managing pipes, giving you a deeper understanding of these UNIX mechanisms in C.
