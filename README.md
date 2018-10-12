The gdb operations using string-alike arguments require that the attached application implemented the funcion malloc.
If not, the operations will fail and return the message: *evaluation of this expression requires the program to have a function "malloc".*

The failed operations are useful for debugging, kernel-malloc-kgdb implement the funcions of malloc() and free() to support them.

kernel-malloc-kgdb uses a global char array as the memory area for sbrk(), the size is 8M.

GDB failed operations examples:

```shell
>>> p boot_command_line 
$3 = 0x8094f014 <boot_command_line> "loglevel=0 root=/dev/mmcblk0 console=ttyAMA0"

>>> call strcmp("good",boot_command_line)
evaluation of this expression requires the program to have a function "malloc".

>>> find boot_command_line,+0x100,{char[7]}"console"
A syntax error in expression, near `sizeof("console"]}"console"'.
```
GDB sucessful operations examples:
```shell
>>> p boot_command_line 
$3 = 0x8094f014 <boot_command_line> "loglevel=0 root=/dev/mmcblk0 console=ttyAMA0"

>>> call strcmp("good",boot_command_line)
$4 = -1

>>> find boot_command_line,+0x100,{char[7]}"console"
0x8094f031 <boot_command_line+29>
1 pattern found.
```

Suggest putting malloc.c into <kernel_root>/mm direcotry.
