# XV6-Scheduler
Implemented the dynamic priorty scheduling and added layers for indirection
Implemented the dynamic Priority Scheduling

A global clock variable has been added (defs.h) and is used to track the time taken by processes in swtch().
The process state has a number of new components (see struct proc declaration in file proc.h).
The scheduler, in proc.c, does a regular pass over the processes to adjust their priorities, calling adjustpriority(p) for every process p.
All the things related to dynamic priority can be found in proc.c, adjustpriority function.


Edited bmap() in file fs.c to have the extra levels of indirection. In the original xv6 (and Linux), the disk block size and the size of each block containing indirection pointers is the same, and both can be found on disk and in memory, so one allocation call is used to get storage for them (balloc()).

In this simulator, we have shrunk things a bit so there are only 3 direct addresses, instead of 12, and each indirection table has only 4 entries, rather than 128. This means we cannot allocate such tables using balloc() as the size is different. Instead a new allocate function called indalloc() is used instead.


A short guide to compiling/running the simulator is given below
Compiling and running xv6
For the first time, and every time after modifying proc.h, do make clean and then make, from the command line.

At other times just make is enough

If you can't use make (e.g. on Windows), then do:

cc -c -o ide.o ide.c
cc -c -o console.o console.c
cc -c -o bio.o bio.c
cc -c -o fs.o fs.c
cc -c -o file.o file.c
cc -c -o swtch.o swtch.c
cc -c -o proc.o proc.c
cc -c -o main.o main.c
cc -o sim ide.o console.o bio.o fs.o file.o swtch.o proc.o main.o 

To run, just do  ./sim < file.dat

All scenarios are now in .dat files

near120.dat - scenario with process static priorities in range 118..121
frw.dat - scenario reading and writing files
fpanic.dat - scenario that fails with panic because file is too large. Will work fine when Task 3 is done.
