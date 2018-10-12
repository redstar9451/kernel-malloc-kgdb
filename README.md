The gdb operations which has strings as arguments require that the attached application implemented funcion malloc.
If not, the operations will fail and returns the message: evaluation of this expression requires the program to have a function "malloc".

The failed operations are useful for debugging, kernel-malloc-kgdb implement the funcions of malloc() and free() to support them.

kernel-malloc-kgdb use a global char array as the memory area for sbrk(), the size is 8M.

