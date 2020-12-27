# FileSystem Search

## Project Overview

This program finds the path of a file in any current working directory as well as its subdirectories. The find program utilizes concurrent programming design and implementation
so that the user can try to find different files at the same time. 

<img src="/image/link/to/file">

## Motivations and Goals
What was the context of building this project? What were you looking to learn? Was this for a class? 

This project was my final project for my systems programming class. It is an amalgum of all the different concepts that I learned in the class, including dup2(), pipe(), and how
to redirect stdin. 


## Challenges

Challenges should follow this template:

### Understanding
There were a lot of moving parts in this project, and it was overwhelming to manage. This is a common problem when working on any project, but it was especially prevalent in
this project. First of all, I had to have a solid grip on how to establish a pipeline between the child and the parent. I also had to figure out how to use <dirent.h> and <sys/stat.h>
so that I could parse specific files.

**My Approach**

What did you do to tackle this challenge? Walk us through the steps you took to solve it. 

I extensively researched all capabilities of `pipe()`, `signal()`, `kill()`, `<dirent.h>`, and `<stat/sys.h>`, and I parsed out what functionalities I thought I needed for the program.
I then wrote procedures on how to use all these functionalities on sticky notes for my own reference. I find it lot easier if I only reference my own understanding of a function when 
solving a problem or debugging rather than referencing someone else understanding on stackoverflow or online resources. 

// Include the filename for reference


Here is how I used a pipe in the program. (This is code in my child process, both the parent and the child have a copy of the pipe)

```
close(fd[0]); //close read
.
.
.
strcat(childreport,"\0");//null terminator is important, because pipe!
int length = strlen(filesrch.report);
write(fd[1],filesrch.report, length);
close(fd[1]); //close write
kill(parentPid,SIGUSR1);

```

On the parent's side, there is an interrupt function that overrides stdin:

```
void myfct(int y){
    dup2(fd[0],STDIN_FILENO); //Overwrite userinput
    overridemode=1;
}
```

## Project Learnings
Through this project, I established my foundations in concurrent programming, including how pipe between a child and parent, how to use signals to override stdin, and how redirect the 
read end of a pipe to stdin using dup and dup2. I have applied this knowledge to other parallelization projects, like matrix multiplication parallelization, which can be seen [here](https://github.com/krishnakalakkad/parallel_matrix_multiplication).


## How to use this program
**OPTIONAL** 
Include how to download and install dependancies. Here would also be a good place to define anything that is currently WIP. 


