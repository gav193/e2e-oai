# Study Notes

## Topic 1 : Pointers review
Reference : [C Pointers | GeeksforGeeks](https://www.geeksforgeeks.org/c-pointers/)
### Overview
A pointer is a variable that stores the **memory address** of another variable.
In a sense, pointers **point** towards the said variable and creates a reference that can be especially useful in functions or other scenarios that needs indirect access of the variable itself. 

Declaring a pointer (data_type* name)

```int *ptr;```

To initialize a pointer or to assign a value to the pointer, use the "&" operator to get the memory address of a variable (in this case 'var')

```int *ptr = &var;```

Size of pointers on a 32-bit system occupy 4 bytes. Meanwhile, on a 64-bit system occupies 8 bytes. (this value stays constant regardless of the data type)

Pointers allow for dynamic memory allocation/deallocation and allows for complex data structures such as linked lists, stacks, trees, etc. 
However, problems might arise from the use of pointers such as memory corruption, special cases of memory allocation faults, and the complexity itself causing it to be hard to understood.

### Special cases:
- NULL pointers do not point to any memory. It represents the absence of address and allows us to check whether the pointer is pointing to a valid memory.
  
```int *ptr = NULL;```

- Void type pointers do not have any associated data type, it's used as a generic pointer that can point to any type.
  
```void *ptr;```

- Wild pointers are pointers that are declared, but not initialized to any value or memory. Wild pointers can cause problems within the program and eventually cause it to crash or corrupt.

- Dangling Pointers are pointers that point**ed** to a location that has been deleted or freed. Dangling pointers can lead to bugs and unexpected behaviors within the program. Can usually be resolved by re-assigning the pointer to a new memory location or to set it as NULL.

### Relation to array
The name of an array acts like a pointer constant. Ex : array named val has the same address as val[0]
A concept called constant pointers can be used to store a memory address within a pointer that cannot be modified (as a reference of sorts).

```int* const ptr = &a;``` 

-> ptr will not change values when reassigned

### Relation to Function
Pointers can be used for callback or event-driven programs where functions can be passed as arguments and invoked dynamically. 
Ex : we have an "add" function as such

``` int add(int a, int b) {return a + b;} ```

and we want to call it dynamically through a pointer (within main)

``` int (*fptr)(int,int); //pointer declaration```

``` fptr = &add;\n ```

-> Whenever fptr is called, "add" function will be called dynamically

### Multilevel Pointers
Basically stages of pointers, or "pointers of pointers of .... and so on" 
It stores the memory location of another pointer in another address. 
Ex : 

```int *ptr1 = &var```

```int **ptr2 = &ptr1```

## Topic 2 : Memory Allocation
Reference : [Dynamic Memory Allocation in C | GeeksforGeeks](https://www.geeksforgeeks.org/dynamic-memory-allocation-in-c-using-malloc-calloc-free-and-realloc/)

In C, variables defined inside functions are stored in stack memory with a fixed size (defined by compile time)
Several functions that can be used within stdlib.h library are : 
- malloc() to allocate a specified amount of uninitialized memory, returning a void pointer (must be cast)
As an example, the code below allocates memory to store 5 integers 

```int *ptr = (int *)malloc(sizeof(int) * 5); ```

-> However, values inside ptr need to be allocated by populating the array of 5 integers

- calloc() to allocate memory and initialize as zero

```int *ptr = (int *)calloc(5, sizeof(int));```

-> same function as malloc but array of integers is initialized to 0

- free() releases or frees allocated memory back to system (followed by setting pointer to NULL)

```free(ptr); ```

- realloc() resizes allocated memory block

```ptr = (int *)malloc(5* sizeof(int)); ```

```ptr = (int *)realloc(ptr, 10 * sizeof(int)); ```

-> memory allocated in pointer is resized

These memory allocation are useful in some scenarios, but might also prove to be prone to problems originating from memory leaks, dangling pointers, fragmentation, and allocation failure. Hence, it's important to make sure that pointers are set to a known address at all times and not overlap between memory allocation happen. 

## Topic 3 : File Handling
Reference : [Basics of File Handling in C | GeeksforGeeks](https://www.geeksforgeeks.org/basics-file-handling-c/) 

### Basic functions
Opening a file in C

```FILE* fopen(*file_name, *access_mode)```

file_name is a pointer that points to the name of the file specified
There are several access_mode that are used in programs, the most common ones include : 
- r : read mode, only able to read the contents of the file without modifying it
- w : write mode, all contents in the file are overwritten then user can "write" in the file
- a : append mode, read the contents of a file then enables user to "append" or write new contents that will later be added to the file
if file is not found, 'r' will return a NULL but 'a' and 'w' will create a new file

Reading from a file can be performed using these functions :
- fscanf() : use formatted string and variable arguments to take input from a file
- fgets() : reads whole line from file
- fgetc() : reads a single character from file
- fgetw() : reads a number from file
- fread() : reads specified bytes from binary file (needs to be read with different mode such as 'rb')

Closing a file can be done with the fclose() function. It's done to remove the memory allocated to the pointer to avoid bugs and faults.

Ex : 
``` 
FILE* fptr;
fptr = fopen("filename.txt", "r");

char data[50];

while(fgets(data,50,fptr) != NULL) {
  printf("%s", data);
}
fclose(fptr);
```

Writing in a file can be oerformed with these functions :
- fprintf() : uses formatted string and variable arguments to print output to a file
- fputs() : prints whole line into a file with a newline at the end
- fputc() : prints a single character into a file
- fputw() : prints a number into a file
- fwrite() : writes a specified number of bytes to binary file (needs to be accessed using access mode wb or ab)

Ex : 
``` 
FILE* fptr;
fptr = fopen("filename.txt", "w");

char data[50] = "String to be written within file ";

fputs(data, fptr); // new text file with data written in it

fclose(fptr);
```

### Processing files
In C, there is a constant macro defined as "EOF" which marks the end of file being handled
When reading a file, for example using getc(fptr) to read characters that fptr is pointing to, it will return the character being read from the file until an error occurs or the end of file is reached, where it will return the constant EOF.

Another useful function is feof(fptr) that checks whether fptr has reached EOF or not by returning a value 0 when pointer doesn't point to EOF, but returns non-zero value when pointer reaches EOF.

To read a file, the most common function used is fgets(). 
```
fgets(buffer, n, stream)
```
buffer acts as a pointer to a string buffer to store the read data
n acts as the max number of characters to read (including null terminator)
stream acts as the input stream
Ex : 
```
FILE *fptr = fopen("filename.txt", "r");
char data[50];
fgets(data, sizeof(data), fptr); // fptr will be stored into data buffer
fclose(fptr); 
```

To write content into a file, one of the common functions used is fprintf().
```
fprintf(FILE* fptr, const char *format, ...); 
```
fptr acts as a stream or a pointer to the file's location where the output will be written
format acts as a string that specifies the format of the output
"..." marks additional arguments that correspond to format specifiers
Ex : 
```
int a = 1;
int b = 2;
FILE *fptr = fopen("filename.txt", "w");
fprintf(fptr, "%d, %d\n", a, b); // write 1, 2 in the file
fclose(fptr); 
```

### Parsing data 
stdin can be read commonly with scanf() function which reads the given input from user according to the format specifier given. 
Ex : 
```
int a;
scanf("%d", &a); // stores stdin of an integer in the address of a
```

For file processing, the fscanf() function can also read and "extract" values from the file according to the format specifier.
Ex : 
```
FILE *ptr = fopen("filename.txt", "r");
char buffer[50];
/* Contents of filename.txt
   NAME    AGE   CITY
   abc     12    hyderabad
   bef     25    delhi
   cce     65    bangalore */
while(fscanf(ptr, "%*s %*s %s ", buffer) == 1){ // extracts only the last column as a string
  printf("%s\n", buffer); // prints the last column values
} 
```

One of the methods to parse data is to use tokens from the function strtok()
```
strtok(char *str, const char *delimiter);
```
str is the string that is being "parsed" which can be extracted using fgets if applied to an external file
delimiter is the separator which we use to tokenize the string
Ex : 
```
char str[] = "apples.pies.bananas";
char delimiter[] = ".";
char* token;
token = strtok(str,delimiter);
while (token) {
  printf("%s\n", token); // prints segmented parts of the initial string
  token = strtok(NULL, delimiter); // search from last point of token to a new delimiter
}
```
Hence, when working with csv or similar files, such methods can be used to separate between lines and columns by adjusting the delimiters and boundaries of the token extraction.

## Topic 4 : Structures
Reference : [C Structures | GeeksforGeeks](https://www.geeksforgeeks.org/structures-c/)

In C, a structure is a user-defined data type that can be used to group items of different types into one "struct". 
To point to a specific member of a struct, it can be called with '.' on a defined and declared struct.
```
struct  A { // struct definition
  int x;
  char c;
};
int main() {
  struct A a; // declaration of struct
  a.x = 5; // stores value of integer 5 within x of A
  return 0;
}
```

Structs function the way most other variables and data types would as it can also be copied into other structs (of same type) and passed into a function as well.
Another syntax to define a struct is with the typedef that sets an alias for an existing data type.
```
typedef struct {
  int a;
} str1;
int main() {
  str1 var1 = {10}; // does not need the "struct" data type attached to it
  return 0;
}
```

Struct pointer is a pointer that allows access to struct members using '->' instead of '.' 
```
struct Point {
  int x, y;
};
int main() {
  struct Point p = {1,2};
  struct Point* ptr = &p;
  printf("%d %d", ptr->x, ptr->y); 
  return 0;
}
```
This concept can be implemented for advanced and complex data structures such as linked lists, stacks, etc. Since a struct can contain a self-referring member : 
```
struct str {
  int mem1;
  struct str* next;
};
```
