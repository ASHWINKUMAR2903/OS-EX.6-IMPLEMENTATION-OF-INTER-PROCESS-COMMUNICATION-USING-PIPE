# OS-EX.6-IMPLEMENTATION-OF-INTER-PROCESS-COMMUNICATION-USING-PIPE

# AIM:
To implement interprocess communication using pipe command.
# ALGORITHM:
1.	 Start
2.	Create a child and parent using fork()
3.	Allow communication between both the process
4.	Stop

# PROGRAM:
```
#include <stdio.h>
#include <unistd.h>
#include <string.h>

int main() {
    int p[2];
    char msg1[30], msg2[30];
    
    if (pipe(p) < 0) {
        perror("Pipe creation failed");
        return 1;
    }
    
    pid_t pid = fork();
    
    if (pid < 0) {
        perror("Fork failed");
        return 1;
    }
    
    if (pid == 0) {
        // Child process
        sleep(1);
        read(p[0], msg1, sizeof(msg1));
        printf("%s\n", msg1);
        write(p[1], "Says hello to grandpa", 21);
    } else {
        // Parent process
        sleep(2);
        write(p[1], "Grand child says hello", 22);
        read(p[0], msg2, sizeof(msg2));
        printf("%s\n", msg2);
    }
    
    return 0;
}
```
# OUTPUT:
![image](https://github.com/ASHWINKUMAR2903/OS-EX.6-IMPLEMENTATION-OF-INTER-PROCESS-COMMUNICATION-USING-PIPE/assets/119407186/3ab61f2c-726a-4f08-ab29-eb5af082ee53)

# RESULT:
Thus, IPC using pipes mechanisms is illustrated using c program successfully.
