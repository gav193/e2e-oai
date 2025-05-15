# Study Notes

## Topic 1 : Pointers review
Reference : [C Pointers | GeeksforGeeks](https://www.geeksforgeeks.org/c-pointers/)
### Overview
A pointer is a variable that stores the **memory address** of another variable.
In a sense, pointers **point** towards the said variable and creates a reference that can be especially useful in functions or other scenarios that needs indirect access of the variable itself. 

Declaring a pointer (data_type* name)
```int *ptr;/n```

To initialize a pointer or to assign a value to the pointer, use the "&" operator to get the memory address of a variable (in this case 'var')
```int *ptr = &var;\n```

Size of pointers on a 32-bit system occupy 4 bytes. Meanwhile, on a 64-bit system occupies 8 bytes. (this value stays constant regardless of the data type)

Pointers allow for dynamic memory allocation/deallocation and allows for complex data structures such as linked lists, stacks, trees, etc. 
However, problems might arise from the use of pointers such as memory corruption, special cases of memory allocation faults, and the complexity itself causing it to be hard to understood.

### Special cases:
- NULL pointers do not point to any memory. It represents the absence of address and allows us to check whether the pointer is pointing to a valid memory.
```int *ptr = NULL;\n```

- Void type pointers do not have any associated data type, it's used as a generic pointer that can point to any type.
```void *ptr;\n```

- Wild pointers are pointers that are declared, but not initialized to any value or memory. Wild pointers can cause problems within the program and eventually cause it to crash or corrupt.

- Dangling Pointers are pointers that point**ed** to a location that has been deleted or freed. Dangling pointers can lead to bugs and unexpected behaviors within the program. Can usually be resolved by re-assigning the pointer to a new memory location or to set it as NULL.

### Relation to array
The name of an array acts like a pointer constant. Ex : array named val has the same address as val[0]
A concept called constant pointers can be used to store a memory address within a pointer that cannot be modified (as a reference of sorts).
```int* const ptr = &a;\n``` -> ptr will not change values when reassigned

### Relation to Function
Pointers can be used for callback or event-driven programs where functions can be passed as arguments and invoked dynamically. 
Ex : we have an "add" function as such
``` int add(int a, int b) \n{return a + b;} \n```
and we want to call it dynamically through a pointer (within main)
``` int (*fptr)(int,int); #pointer declaration\n```
``` fptr = &add;\n ```
-> Whenever fptr is called, "add" function will be called dynamically

### Multilevel Pointers
Basically stages of pointers, or "pointers of pointers of .... and so on" 
It stores the memory location of another pointer in another address. 
Ex : 
```int *ptr1 = &var\n```
```int **ptr2 = &ptr1\n```

## Topic 2

## Topic 3
