Header Files and Constants:

Includes necessary standard libraries (stdio.h, stdlib.h, string.h) and POSIX libraries (unistd.h, sys/types.h, sys/wait.h).
Defines constants MAX_COMMAND_LENGTH (maximum length of a command) and MAX_ARGS (maximum number of arguments).
Main Function (main()):

Uses an infinite loop (while(1)) to continuously prompt the user with MiniShell> .
Reads the command from standard input using fgets(), removing the newline character at the end.
Calls parse_command() to tokenize the command into individual arguments stored in the args array.
Calls execute_command() to fork a child process and execute the command using execvp().
parse_command() Function:

Takes a command string and an array of strings (args) as parameters.
Uses strtok() to tokenize the command string based on whitespace.
Stores each token (argument) in the args array and terminates the list with NULL.
execute_command() Function:

Takes an array of strings (args) representing the command and its arguments.
Uses fork() to create a child process.
In the child process (pid == 0), executes the command using execvp(), which searches for the command in the system's PATH environment variable.
If execvp() fails, an error message is printed via perror() and the child process exits.
In the parent process, it waits for the child to complete using waitpid() with WUNTRACED flag to handle termination or interruption by signals.
Usage:
Compile the program (e.g., gcc minishell.c -o minishell -Wall).
Run the executable (./minishell).
Enter commands when prompted (MiniShell> ), such as ls -l, pwd, echo Hello, World!, etc.
The shell will execute these commands and wait for the next input.
Example Interaction:
shell
Copy code
MiniShell> ls
file1.txt  file2.txt  minishell  minishell.c

MiniShell> pwd
/home/user/minishell

MiniShell> echo Hello, World!
Hello, World!

MiniShell> exit
In this example:

The user enters ls, which lists files in the current directory.
Then pwd prints the current working directory.
echo Hello, World! prints the message.
Finally, exit would normally terminate the shell.
