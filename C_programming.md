### FILE I/O ###

###### High Level Access ######

```c
FILE* fopen(char *fileName, char *mode)
```

Returns a FILE pointer associated with the file name or NULL if error occurs. Modes are r(read), w(write), a(append).
There are three special file pointer; **stdin**(standard input), **stdout**(standard output), **stderr**(standard error).

```c
int getc(FILE *filePointer)
```

Returns next character from the file stream referred to by filePointer. It returns EOF if end of file or error occurs.

```c
int putc(int c, FILE *filePointer)
```

Writes character c to the file referred to by filePointer. Retuens the character written or EOF if error occurs.

```c
int fprintf(FILE *filePointer, char *format, ...)
int fscanf(FILE *filePointer, char *format, ...)
```

For formatted input / output of files
