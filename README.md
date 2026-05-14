# Linux-IPC-Shared-memory
Ex06-Linux IPC-Shared-memory

# AIM:
To Write a C program that illustrates two processes communicating using shared memory.

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - Shared Memory

### Step 3:

Execute the C Program for the desired output. 

# PROGRAM:


## Write a C program that illustrates two processes communicating using shared memory.
```
// shared_memory.c

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <sys/types.h>
#include <sys/wait.h>

int main() {

    key_t key = ftok("shmfile", 65);

    // Create shared memory
    int shmid = shmget(key, 1024, 0666 | IPC_CREAT);

    // Attach shared memory
    char *str = (char*) shmat(shmid, NULL, 0);

    pid_t pid = fork();

    if (pid > 0) {

        // Parent process writes
        strcpy(str, "Hello from Parent Process!");

        printf("Parent wrote: %s\n", str);

        wait(NULL);

        // Remove shared memory
        shmdt(str);
        shmctl(shmid, IPC_RMID, NULL);

    } else {

        // Child process reads
        sleep(1);

        printf("Child read: %s\n", str);

        shmdt(str);
    }

    return 0;
}
```




## OUTPUT

<img width="844" height="700" alt="image" src="https://github.com/user-attachments/assets/99302f11-2ec9-4b5a-8ec0-ea1d44ca2294" />

<img width="820" height="684" alt="image" src="https://github.com/user-attachments/assets/e84e5579-d247-489f-a363-80b05c4fb5fe" />


# RESULT:
The program is executed successfully.
