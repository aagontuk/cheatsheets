### FILE I/O ###

###### High Level Access ######

```c
FILE* fopen(char *fileName, char *mode)
```

Returns a FILE pointer associated with the file name. Modes are r(read), w(write), a(append).
There are three special file pointer; **stdin**(standard input), **stdout**(standard output), **stderr**(standard error).

```c
int fgetc(FILE *filePointer)
```

Returns one character from a file or EOF if error occurs.
