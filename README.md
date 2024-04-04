# Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise


# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:

## C Program to print process ID and parent Process ID using Linux API system calls
```c
#include<stdio.h>
#include<sys/types.h>
#include<unistd.h>
int main(void)
{
 pid_t process_id;
 pid_t p_process_id;
 process_id = getpid();
 p_process_id=getppid();
 printf("The process id: %d\n", process_id);
 printf("The process id of parent function: %d\n", p_process_id);
 return 0;
}
```
## OUTPUT
![WhatsApp Image 2024-04-04 at 15 55 07_17cd111b](https://github.com/MeethaPrabhu/Linux-Process-API-fork-wait-exec/assets/119401038/60c7e676-bbbd-427f-9fbd-6f9b8338c93f)


## C Program to create new process using Linux API system calls fork() and exit()
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
int main() {
    int pid;
    pid = fork();
    if (pid == -1) {
        perror("fork");
        exit(EXIT_FAILURE);
    }
    else if (pid == 0) {
        printf("I am child, my pid is %d\n", getpid());
        printf("My parent pid is: %d\n", getppid());
        exit(EXIT_SUCCESS);
    }
    else {
        printf("I am parent, my pid is %d\n", getpid());
        sleep(100);
        exit(EXIT_SUCCESS);
    }
    return 0;
}
```
## OUTPUT
![WhatsApp Image 2024-04-04 at 15 55 07_5bcd2071](https://github.com/MeethaPrabhu/Linux-Process-API-fork-wait-exec/assets/119401038/7c74f740-28eb-415a-9ec2-65ad2a4ba3e7)


## C Program to execute Linux system commands using Linux API system calls exec() family
```C
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>
int main() {
    pid_t pid = fork();
    if (pid < 0) {
        perror("Fork failed");
        exit(EXIT_FAILURE);
    } else if (pid == 0) {
        printf("This is the child process. Executing 'ls' command.\n");
        execl("/bin/ls", "ls", "-l", NULL); // Lists files in long format
        perror("execl failed");
        exit(EXIT_FAILURE);
    } else {
        int status;
        waitpid(pid, &status, 0); // Wait for the child to finish
        if (WIFEXITED(status)) {
            printf("Child process exited with status %d.\n", WEXITSTATUS(status));
        } else {
            printf("Child process did not exit normally.\n");
        }
        printf("Parent process is done.\n");
    }
    return 0;
}
```
## OUTPUT
![WhatsApp Image 2024-04-04 at 15 55 07_ef87db84](https://github.com/MeethaPrabhu/Linux-Process-API-fork-wait-exec/assets/119401038/230ab687-f1b4-4e51-981a-04e21b14abe2)


# RESULT:
The programs are executed successfully.
