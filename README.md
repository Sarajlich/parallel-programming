# Muhamed-Sarajlic-Parallel-Programming-Assignments

Before fixed code:

student@itcenter-lab128:~/Desktop/Muhamed-Sarajlic-Parallel-Programming-Assignments$ make valgrind
valgrind --leak-check=full --show-leak-kinds=all --track-origins=yes ./assignment
==10035== Memcheck, a memory error detector
==10035== Copyright (C) 2002-2017, and GNU GPL'd, by Julian Seward et al.
==10035== Using Valgrind-3.18.1 and LibVEX; rerun with -h for copyright info
==10035== Command: ./assignment
==10035== 
==10035== Invalid write of size 4
==10035==    at 0x1091C6: main (main.c:10)
==10035==  Address 0x4a9e068 is 0 bytes after a block of size 40 alloc'd
==10035==    at 0x4848899: malloc (in /usr/libexec/valgrind/vgpreload_memcheck-amd64-linux.so)
==10035==    by 0x109185: main (main.c:6)
==10035== 
==10035== Conditional jump or move depends on uninitialised value(s)
==10035==    at 0x1091F4: main (main.c:13)
==10035==  Uninitialised value was created by a stack allocation
==10035==    at 0x109169: main (main.c:3)
==10035== 
==10035== Invalid read of size 4
==10035==    at 0x1091EF: main (main.c:13)
==10035==  Address 0x4a9e068 is 0 bytes after a block of size 40 alloc'd
==10035==    at 0x4848899: malloc (in /usr/libexec/valgrind/vgpreload_memcheck-amd64-linux.so)
==10035==    by 0x109185: main (main.c:6)
==10035== 
==10035== 
==10035== HEAP SUMMARY:
==10035==     in use at exit: 40 bytes in 1 blocks
==10035==   total heap usage: 1 allocs, 0 frees, 40 bytes allocated
==10035== 
==10035== 40 bytes in 1 blocks are definitely lost in loss record 1 of 1
==10035==    at 0x4848899: malloc (in /usr/libexec/valgrind/vgpreload_memcheck-amd64-linux.so)
==10035==    by 0x109185: main (main.c:6)
==10035== 
==10035== LEAK SUMMARY:
==10035==    definitely lost: 40 bytes in 1 blocks
==10035==    indirectly lost: 0 bytes in 0 blocks
==10035==      possibly lost: 0 bytes in 0 blocks
==10035==    still reachable: 0 bytes in 0 blocks
==10035==         suppressed: 0 bytes in 0 blocks
==10035== 
==10035== For lists of detected and suppressed errors, rerun with: -s
==10035== ERROR SUMMARY: 14 errors from 4 contexts (suppressed: 0 from 0)

-----------------------------------------------------------------------------------

Explanation:

1) ipos = 0 --> I gave it starting value for index position (ipos), so if user doesnt enter it, its by default 0, because its uninitialized, so uninitialized memory issue is prevented

2) ival = 0 --> I gave it starting value for input value (ival), so if user doesnt enter it, its by default 0, because its uninitialized, so uninitialized memory issue is prevented

3) i<10 --> in line 10 and 12, inside for loop, i changed "i<=10" to "i<10" because valid array has 10 elements and arrays start at index 0, so valid indexes are 0 to 9, if we used "i<=10" we would try to access iarray[10] which doesnt exist and it would cause some kind of out of bounds memory error

4) free(iarray) --> malloc() allocates memory and free() realises it to prevent memory leaks; so we use it to release the memory that was previously allocated with malloc

-----------------------------------------------------------------------------------
After fixed code:

student@itcenter-lab128:~/Desktop/Muhamed-Sarajlic-Parallel-Programming-Assignments$ make valgrind
valgrind --leak-check=full --show-leak-kinds=all --track-origins=yes ./assignment
==11460== Memcheck, a memory error detector
==11460== Copyright (C) 2002-2017, and GNU GPL'd, by Julian Seward et al.
==11460== Using Valgrind-3.18.1 and LibVEX; rerun with -h for copyright info
==11460== Command: ./assignment
==11460== 
==11460== 
==11460== HEAP SUMMARY:
==11460==     in use at exit: 0 bytes in 0 blocks
==11460==   total heap usage: 1 allocs, 1 frees, 40 bytes allocated
==11460== 
==11460== All heap blocks were freed -- no leaks are possible
==11460== 
==11460== For lists of detected and suppressed errors, rerun with: -s
==11460== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)