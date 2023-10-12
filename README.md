# OS-EX.6-IMPLEMENTATION-OF-INTER-PROCESS-COMMUNICATION-USING-PIPE

# AIM:
To implement interprocess communication using pipe command.
# ALGORITHM:
1. Create a child process usingfork()
2. Create a simple pipe with C, we make use of the pipe() systemcall.
3. Create two file descriptor fd[0] is set up for reading, fd[1] is set up forwriting
4. Close the read end of parent process using close() and perform writeoperation
5. Close the write end of child process and performreading
6. Display the text.

# PROGRAM:
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    int fd[2], child;
    char a[10];
    printf("\nEnter the string:");
    scanf("%s", a);

    pipe(fd);

    child = fork();
    
    if (child == 0) 
    {
        close(fd[0]); // Close the read end of the pipe in the child process
        write(fd[1], a, strlen(a) + 1);
        close(fd[1]); // Close the write end of the pipe
        wait(NULL);    // Wait for the child to finish
    } 
    else 
    {
        close(fd[1]); // Close the write end of the pipe in the parent process
        read(fd[0], a, sizeof(a));
        printf("The string received from the pipe is: %s\n", a);
        close(fd[0]); // Close the read end of the pipe
    }
    return 0;
}
```
# OUTPUT:
![image](https://github.com/ASHWINKUMAR2903/OS-EX.6-IMPLEMENTATION-OF-INTER-PROCESS-COMMUNICATION-USING-PIPE/assets/119407186/cc512bbc-3103-4e9f-b92f-c6ad01b1ff1f)

# RESULT:
Thus, IPC using pipes mechanisms is illustrated using c program successfully.
