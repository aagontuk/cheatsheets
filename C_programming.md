### FILE I/O ###

###### High Level Access ######

```c
#include <stdio.h>	/* Header files for the bellow functions */
```

```c
FILE* fopen(char *fileName, char *mode);
```

Returns a FILE pointer associated with the file name or NULL if error occurs. Modes are r(read), w(write), a(append).
There are three special file pointer; **stdin**(standard input), **stdout**(standard output), **stderr**(standard error).

```c
int getc(FILE *filePointer);
```

Returns next character from the file stream referred to by filePointer. It returns EOF if end of file or error occurs.

```c
int putc(int c, FILE *filePointer);
```

Writes character c to the file referred to by filePointer. Retuens the character written or EOF if error occurs.

```c
int fprintf(FILE *filePointer, char *format, ...);
int fscanf(FILE *filePointer, char *format, ...);
```

For formatted input / output of files

```c
char *fgets(char *line, int MAX_CHAR, FILE *filePointer);
```

Reads the next line from the file referred to by filepointer into char array line. MAX_CHAR - 1 characters will be read.
Returns pointer to the line or NULL if EOF or error occurs.

```c
int fputs(char *line, FILE *filePointer);
```

Writes a string to a file. Returns EOF if error occurs, zero otherwise.

```c
int remove(const char *fileName);
```

Removes fileName from file system. Returns non zero if attempt fails

```c
int rename(const char *oldFileName, const char *newFileName);
```

Rename oldFileName to newFileName. Returns non zero if attempt fails.

```c
FILE* tmpfile(void);
```

Creates a temporary file of mode `wb+`. It will be removed automatically when the file is closed.

```c
int fclose(FILE *filePointer);
```

Closes a file.

###### Error Handaling ######

```c
int ferror(FILE *filePointer);	/* Returns non zero if an error occurs */
int feof(FILE *filePointer);	/* Return non zero if eof occurs */
```
```c
void perror(FILE *filePointer, chars *s);
```

Prints interactive error message to filePointer if no argument specified Or s.

##### Low Level Access #####

```c
#include <fcntl.h>	/* Header file for the bellow functions */
```

```c
int open(char *name, int flags, int perms);
```

Returns an integer associated with the file, which is called a file descriptor.
When shell runs a program three files are open automatically the standard input, standard output and standard error.
Their associated file descriptors are 0, 1 & 2.

Here are some flags:
```
O_RDONLY - Open file in read only mode
O_WRONLY - Open file in write only mode
O_RDWR - Open file in read / write mode
```

Perm is the unix file permission specified as a 3 digit octal.

```c
int create(char *name, int perms);
```

Creates a file using name and returns a file descriptor associated with it. Returns -1 if fails.

```c
#include <unistd.h>		/* Header file for the bellow functions */
```

```c
int read(int fileDescriptor, char *buffer, int n);
```

Reads n bytes from a file associated with fileDescriptor into buffer array. Returns number of bytes transferred.
A return value of zero indicates EOF and -1 indicates an error.

```c
int write(int fileDescriptor, char *buffer, int n);
```

Writes n bytes from buffer array to a file associated with fileDescriptor. It returns number of bytes written.

```c
long lseek(int fileDescriptor, long offset, int origin);
```

Set the current position of the file to offset which is taken relative to the location specified by origin.
Orgigin can be 0, 1 or 2 to specify that offset is to be measured from the begaining, current position or end of the file.

```c
int unlink(const char *path);
```

Removes a file. Returns 0 upon success otherwise -1.

```c
int close(int fileDescriptor);
```

Closes a file.
