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

```c
char *fgets(char *line, int MAX_CHAR, FILE *filePointer)
```

Reads the next line from the file referred to by filepointer into char array line. MAX_CHAR - 1 characters will be read.
Returns pointer to the line or NULL if EOF or error occurs.

```c
int fputs(char *line, FILE *filePointer)
```

Writes a string to a file. Returns EOF if error occurs, zero otherwise.

###### Error Handaling ######

```c
int ferror(FILE *filePointer)	/* Returns non zero if an error occurs */
int feof(FILE *filePointer)		/* Return non zero if eof occurs */
```
```c
void perror(FILE *filePointer, chars *s)
```

Prints interactive error message to filePointer if no argument specified Or s.
