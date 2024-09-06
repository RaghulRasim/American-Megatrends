
---

### **1. Mergesort in C**
Mergesort is a divide-and-conquer algorithm that divides the array into two halves, sorts them, and then merges them.

```c
#include <stdio.h>

void merge(int arr[], int l, int m, int r) {
    int i, j, k;
    int n1 = m - l + 1;
    int n2 = r - m;
    int L[n1], R[n2];  // Temp arrays

    for (i = 0; i < n1; i++) L[i] = arr[l + i];
    for (j = 0; j < n2; j++) R[j] = arr[m + 1 + j];

    i = 0;  // Initial index of first subarray
    j = 0;  // Initial index of second subarray
    k = l;  // Initial index of merged subarray
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }

    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

void mergeSort(int arr[], int l, int r) {
    if (l < r) {
        int m = l + (r - l) / 2;

        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);

        merge(arr, l, m, r);
    }
}

void printArray(int A[], int size) {
    for (int i = 0; i < size; i++) printf("%d ", A[i]);
    printf("\n");
}

int main() {
    int arr[] = {12, 11, 13, 5, 6, 7};
    int arr_size = sizeof(arr) / sizeof(arr[0]);

    printf("Given array is \n");
    printArray(arr, arr_size);

    mergeSort(arr, 0, arr_size - 1);

    printf("\nSorted array is \n");
    printArray(arr, arr_size);
    return 0;
}
```

---

### **2. Reverse a Linked List Using Recursion**

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

struct Node* reverse(struct Node* head) {
    if (head == NULL || head->next == NULL)
        return head;

    struct Node* rest = reverse(head->next);
    head->next->next = head;
    head->next = NULL;
    
    return rest;
}

void push(struct Node** head_ref, int new_data) {
    struct Node* new_node = (struct Node*) malloc(sizeof(struct Node));
    new_node->data = new_data;
    new_node->next = (*head_ref);
    (*head_ref) = new_node;
}

void printList(struct Node *node) {
    while (node != NULL) {
        printf("%d ", node->data);
        node = node->next;
    }
}

int main() {
    struct Node* head = NULL;

    push(&head, 20);
    push(&head, 4);
    push(&head, 15);
    push(&head, 85);

    printf("Given linked list\n");
    printList(head);

    head = reverse(head);

    printf("\nReversed Linked list \n");
    printList(head);
    return 0;
}
```

---

### **3. Replace a Word in a Paragraph**

```c
#include <stdio.h>
#include <string.h>

void replaceWord(const char *str, const char *oldWord, const char *newWord) {
    char result[1000];
    int i = 0, cnt = 0;
    int newWlen = strlen(newWord);
    int oldWlen = strlen(oldWord);

    for (i = 0; str[i] != '\0'; i++) {
        if (strstr(&str[i], oldWord) == &str[i]) {
            strcpy(&result[cnt], newWord);
            cnt += newWlen;
            i += oldWlen - 1;
        } else
            result[cnt++] = str[i];
    }
    result[cnt] = '\0';
    printf("Modified String: %s\n", result);
}

int main() {
    char str[1000] = "The quick brown fox jumps over the lazy dog";
    char oldWord[] = "fox";
    char newWord[] = "cat";

    printf("Original String: %s\n", str);
    replaceWord(str, oldWord, newWord);

    return 0;
}
```

---

### **4. Create a Linked List in C**

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

void push(struct Node** head_ref, int new_data) {
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));
    new_node->data = new_data;
    new_node->next = (*head_ref);
    (*head_ref) = new_node;
}

void printList(struct Node* n) {
    while (n != NULL) {
        printf("%d ", n->data);
        n = n->next;
    }
}

int main() {
    struct Node* head = NULL;

    push(&head, 10);
    push(&head, 20);
    push(&head, 30);

    printList(head);
    return 0;
}
```

---

### **5. String and Array Concept (Pointers and Structs)**

- **Pointer to an Array:**

```c
#include <stdio.h>

int main() {
    int arr[] = {10, 20, 30, 40};
    int *ptr = arr;

    for (int i = 0; i < 4; i++) {
        printf("%d ", *(ptr + i));
    }

    return 0;
}
```

---

Let's continue with the next set of C programs and topics:

---

### **6. Swap Two Variables Without Using a Third Variable**

You can use either arithmetic operations or bitwise XOR to swap two variables without a third variable.

#### **Using Arithmetic Operations:**
```c
#include <stdio.h>

int main() {
    int a = 10, b = 20;
    printf("Before Swap: a = %d, b = %d\n", a, b);

    a = a + b;  // a becomes 30
    b = a - b;  // b becomes 10
    a = a - b;  // a becomes 20

    printf("After Swap: a = %d, b = %d\n", a, b);
    return 0;
}
```

#### **Using Bitwise XOR:**
```c
#include <stdio.h>

int main() {
    int a = 10, b = 20;
    printf("Before Swap: a = %d, b = %d\n", a, b);

    a = a ^ b;
    b = a ^ b;
    a = a ^ b;

    printf("After Swap: a = %d, b = %d\n", a, b);
    return 0;
}
```

---

### **7. Automorphic Number Using Pointer in C**

An automorphic number is a number whose square ends in the same digits as the number itself.

```c
#include <stdio.h>

int isAutomorphic(int *num) {
    int square = (*num) * (*num);

    while (*num > 0) {
        if (*num % 10 != square % 10)
            return 0;

        *num /= 10;
        square /= 10;
    }
    return 1;
}

int main() {
    int num = 25;
    if (isAutomorphic(&num))
        printf("Automorphic Number\n");
    else
        printf("Not an Automorphic Number\n");

    return 0;
}
```

---

### **8. Reverse a String in C**

```c
#include <stdio.h>
#include <string.h>

void reverseString(char *str) {
    int len = strlen(str);
    for (int i = 0; i < len / 2; i++) {
        char temp = str[i];
        str[i] = str[len - i - 1];
        str[len - i - 1] = temp;
    }
}

int main() {
    char str[100] = "HelloWorld";
    printf("Original String: %s\n", str);

    reverseString(str);
    printf("Reversed String: %s\n", str);

    return 0;
}
```

---

### **9. Assembly Language Program: Multiplication and Division**

Since Assembly code varies by processor, here’s a general concept using x86 Assembly.

#### **Multiplication Example in Assembly (x86):**
```asm
section .data
    num1 db 5
    num2 db 4
    result dw 0

section .text
    global _start

_start:
    mov al, [num1]     ; Load num1 into AL
    mov bl, [num2]     ; Load num2 into BL
    mul bl             ; Multiply AL by BL (result stored in AX)
    mov [result], ax   ; Store result
```

#### **Division Example in Assembly (x86):**
```asm
section .data
    dividend db 10
    divisor  db 2
    quotient dw 0

section .text
    global _start

_start:
    mov al, [dividend] ; Load dividend into AL
    mov bl, [divisor]  ; Load divisor into BL
    div bl            ; Divide AL by BL (quotient stored in AL)
    mov [quotient], al ; Store result
```

---

### **10. Decimal to Binary Conversion in C**

```c
#include <stdio.h>

void decimalToBinary(int n) {
    if (n == 0)
        return;
    decimalToBinary(n / 2);
    printf("%d", n % 2);
}

int main() {
    int n = 10;
    printf("Binary of %d is: ", n);
    decimalToBinary(n);
    return 0;
}
```

---

### **11. Hexadecimal to Binary Conversion in C**

```c
#include <stdio.h>

void hexToBinary(char hex[]) {
    int i = 0;
    while (hex[i]) {
        switch (hex[i]) {
        case '0': printf("0000"); break;
        case '1': printf("0001"); break;
        case '2': printf("0010"); break;
        case '3': printf("0011"); break;
        case '4': printf("0100"); break;
        case '5': printf("0101"); break;
        case '6': printf("0110"); break;
        case '7': printf("0111"); break;
        case '8': printf("1000"); break;
        case '9': printf("1001"); break;
        case 'A': case 'a': printf("1010"); break;
        case 'B': case 'b': printf("1011"); break;
        case 'C': case 'c': printf("1100"); break;
        case 'D': case 'd': printf("1101"); break;
        case 'E': case 'e': printf("1110"); break;
        case 'F': case 'f': printf("1111"); break;
        default:  printf("\nInvalid hexadecimal digit %c ", hex[i]);
        }
        i++;
    }
}

int main() {
    char hex[100] = "1A3";
    printf("Binary equivalent of %s is: ", hex);
    hexToBinary(hex);
    return 0;
}
```

---

### **12. What is a Compiler? Where is it Present?**

A **compiler** is a software program that translates source code written in a high-level programming language (like C, C++, or Java) into machine code that can be executed by the computer's CPU.

- **Where is it present?**
  The compiler is present on your development machine as part of your software development environment. For example:
  - **For C/C++:** You might use **GCC** (GNU Compiler Collection) on Linux/Windows.
  - **For Java:** You use the **Java Compiler (javac)**.
  
---

### **13. Prime Number Code in C**

```c
#include <stdio.h>

int isPrime(int n) {
    if (n <= 1) return 0;
    for (int i = 2; i <= n / 2; i++) {
        if (n % i == 0)
            return 0;
    }
    return 1;
}

int main() {
    int num = 29;
    if (isPrime(num))
        printf("%d is a prime number.\n", num);
    else
        printf("%d is not a prime number.\n", num);
    return 0;
}
```

---


### **14. BMC in Servers**

**BMC (Baseboard Management Controller)** is a specialized microcontroller embedded in servers that monitors and manages the physical state of the hardware (e.g., temperature, power, fans, and memory). It works independently of the server's CPU, allowing remote management even if the server is powered down.

---
Let's continue with additional topics and explanations:

---

### **15. Network Layers (OSI Model)**

The OSI (Open Systems Interconnection) model divides the communication system into seven distinct layers:

1. **Physical Layer**: Deals with the physical connection between devices, such as cables, switches, and network interface cards (NICs). It includes electrical signals, bit transmission, and hardware transmission media.
   
2. **Data Link Layer**: Responsible for node-to-node data transfer and error detection/correction (e.g., Ethernet). It is divided into two sub-layers:
   - **Logical Link Control (LLC)**
   - **Media Access Control (MAC)**

3. **Network Layer**: Manages data routing, switching, and addressing. It decides the physical path the data takes. Protocols include IP (Internet Protocol) and ICMP.

4. **Transport Layer**: Ensures reliable data transfer between host systems (e.g., TCP, UDP). It handles flow control, error handling, and re-transmissions.

5. **Session Layer**: Manages and controls the connections between computers. It establishes, maintains, and terminates communication sessions (e.g., APIs, Socket programming).

6. **Presentation Layer**: Translates, encrypts, and compresses data. For instance, translating from EBCDIC to ASCII.

7. **Application Layer**: Closest to the end user, this layer enables applications to access network services (e.g., HTTP, FTP, SMTP).

---

### **16. Sorting a List in C**

Here is an implementation of **Bubble Sort** to sort a list in C:

```c
#include <stdio.h>

void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n-1; i++) {
        for (int j = 0; j < n-i-1; j++) {
            if (arr[j] > arr[j+1]) {
                int temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}

void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr)/sizeof(arr[0]);

    printf("Unsorted array: ");
    printArray(arr, n);

    bubbleSort(arr, n);

    printf("Sorted array: ");
    printArray(arr, n);
    return 0;
}
```

---

### **17. Microprocessor Architecture Overview**

A microprocessor is the brain of a computer system. It is a programmable, multipurpose, clock-driven, register-based electronic device that performs arithmetic and logical operations. Here are the main components of a microprocessor:

1. **Arithmetic Logic Unit (ALU)**: Performs arithmetic and logical operations.
2. **Control Unit (CU)**: Directs operations of the processor, fetching and decoding instructions.
3. **Registers**: Small, fast storage locations for holding temporary data and instructions.
4. **Bus**: Set of electrical paths used for communication between components.
   - **Address Bus**: Carries the address of memory locations.
   - **Data Bus**: Carries actual data between memory and processor.
   - **Control Bus**: Sends control signals to ensure proper data flow.

### **18. SPI (Serial Peripheral Interface) vs I2C (Inter-Integrated Circuit)**

| Feature                | **SPI**                          | **I2C**                             |
|------------------------|----------------------------------|-------------------------------------|
| **Number of Wires**     | 4 (MOSI, MISO, SCK, SS)          | 2 (SDA, SCL)                        |
| **Speed**               | Faster (up to 10 Mbps or more)   | Slower (up to 3.4 Mbps)             |
| **Data Transfer**       | Full-Duplex                      | Half-Duplex                         |
| **Slave Selection**     | Requires separate SS per slave   | Uses addressing for multiple slaves |
| **Complexity**          | Simpler                          | More complex                        |
| **Use Case**            | Short-distance communication     | Short-to-medium distance            |
| **Typical Devices**     | Sensors, displays, flash memory  | EEPROMs, RTCs, sensors              |

---

### **19. Structure vs Union in C**

#### **Structure**:
- A structure is a collection of variables of different types stored at different memory locations.
- Each member has its own memory location.
  
Example:
```c
#include <stdio.h>

struct Person {
    char name[50];
    int age;
    float salary;
};

int main() {
    struct Person p1 = {"John", 30, 5000.50};
    printf("Name: %s, Age: %d, Salary: %.2f\n", p1.name, p1.age, p1.salary);
    return 0;
}
```

#### **Union**:
- A union is similar to a structure but stores all variables in the same memory location, meaning only one member can hold a value at any given time.
  
Example:
```c
#include <stdio.h>

union Data {
    int i;
    float f;
    char str[20];
};

int main() {
    union Data data;
    data.i = 10;
    printf("i: %d\n", data.i);
    
    data.f = 220.5;
    printf("f: %.1f\n", data.f);
    
    return 0;
}
```

#### **Key Differences**:
- **Memory Usage**: Structure allocates memory for each member, union shares memory among all members.
- **Usage**: Structure is used when all members are needed at the same time. Union is useful when only one of the members is used at a time.

---

### **20. Dynamic Memory Allocation in C**

Dynamic memory allocation allows you to allocate memory during runtime using functions like `malloc()`, `calloc()`, `realloc()`, and `free()`.

Example using `malloc()`:

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *ptr;
    ptr = (int*)malloc(5 * sizeof(int));  // Allocating memory for 5 integers

    if (ptr == NULL) {
        printf("Memory allocation failed!\n");
        return 1;
    }

    // Assigning values
    for (int i = 0; i < 5; i++) {
        ptr[i] = i + 1;
    }

    // Printing values
    for (int i = 0; i < 5; i++) {
        printf("%d ", ptr[i]);
    }

    free(ptr);  // Deallocating memory
    return 0;
}
```

---

### **21. DMA (Direct Memory Access)**

**Direct Memory Access (DMA)** is a feature that allows hardware subsystems within a computer to access the main system memory (RAM) independently of the CPU. This is useful in embedded systems, where it helps with tasks like transferring data from peripherals (e.g., ADC, UART) to memory without burdening the CPU.

#### **How it works**:
- The DMA controller handles data transfer from memory to I/O devices (or vice versa), freeing up the CPU for other tasks.
  
---

### **22. Shallow Copy vs Deep Copy (Python)**

#### **Shallow Copy**:
- A shallow copy creates a new object but inserts references into it to the objects found in the original.
  
Example:
```python
import copy
lst1 = [1, 2, [3, 4]]
lst2 = copy.copy(lst1)
lst2[2][0] = 7
print(lst1)  # Output: [1, 2, [7, 4]] (the inner list is shared)
```

#### **Deep Copy**:
- A deep copy creates a new object and recursively copies all objects found in the original.

Example:
```python
import copy
lst1 = [1, 2, [3, 4]]
lst2 = copy.deepcopy(lst1)
lst2[2][0] = 7
print(lst1)  # Output: [1, 2, [3, 4]] (completely independent copy)
```

---

---

### **23. Register Writing and Reading in Embedded C**

In embedded systems, registers are used to configure and control peripherals and processor functionality. Writing to and reading from registers involves accessing specific memory-mapped addresses.

#### **Example**: Writing and reading from a GPIO register on a microcontroller (e.g., ARM Cortex-M).

Assuming `GPIO_PORTA` is mapped at address `0x40004000`:

```c
#define GPIO_PORTA_DATA  (*((volatile unsigned long *) 0x40004000))
#define GPIO_PORTA_DIR   (*((volatile unsigned long *) 0x40004400))

int main() {
    // Set PORTA pin 0 as output
    GPIO_PORTA_DIR |= 0x01;  
    
    // Write to GPIO register: Set pin 0 high
    GPIO_PORTA_DATA |= 0x01;  
    
    // Read the state of GPIO pin 0
    unsigned long pin_state = GPIO_PORTA_DATA & 0x01;
    
    return 0;
}
```

- **volatile** is used because the register's value may change outside the program's control (e.g., hardware).

---

### **24. Dangling Pointer and Memory Leak in C**

#### **Dangling Pointer**:
A **dangling pointer** is a pointer that points to a memory location that has already been freed or released. Accessing such memory leads to undefined behavior.

Example:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *ptr = (int *)malloc(sizeof(int));  // Allocate memory
    *ptr = 10;

    free(ptr);  // Free memory
    // ptr is now a dangling pointer, accessing it is dangerous
    printf("%d\n", *ptr);  // Undefined behavior

    return 0;
}
```

#### **Memory Leak**:
A **memory leak** occurs when a program allocates memory but fails to release it, leading to wasted memory.

Example:
```c
#include <stdlib.h>

int main() {
    int *ptr = (int *)malloc(sizeof(int));
    // Forgot to free the allocated memory - Memory Leak

    return 0;
}
```

---

### **25. Little Endian vs Big Endian**

**Endianness** refers to the byte order used to store data in memory. 

- **Little Endian**: The least significant byte (LSB) is stored first (at the lowest address).
  - Example: `0x12345678` is stored as `78 56 34 12` in memory.
  
- **Big Endian**: The most significant byte (MSB) is stored first (at the lowest address).
  - Example: `0x12345678` is stored as `12 34 56 78` in memory.

#### **Detecting Endianness in C**:

```c
#include <stdio.h>

int checkEndianness() {
    unsigned int num = 1;
    char *ptr = (char *)&num;
    return (*ptr == 1) ? 1 : 0;  // 1 for Little Endian, 0 for Big Endian
}

int main() {
    if (checkEndianness())
        printf("Little Endian\n");
    else
        printf("Big Endian\n");

    return 0;
}
```

---

### **26. C Program to Print a to z Skipping Certain Letters**

This program prints all letters from 'a' to 'z' but skips specific ones (e.g., 'e' and 'o').

```c
#include <stdio.h>

void printAlphabetSkipping(char skip[], int size) {
    for (char ch = 'a'; ch <= 'z'; ch++) {
        int skipFlag = 0;
        for (int i = 0; i < size; i++) {
            if (ch == skip[i]) {
                skipFlag = 1;
                break;
            }
        }
        if (!skipFlag) {
            printf("%c ", ch);
        }
    }
    printf("\n");
}

int main() {
    char skip[] = {'e', 'o'};
    int size = sizeof(skip) / sizeof(skip[0]);

    printAlphabetSkipping(skip, size);
    return 0;
}
```

---

### **27. Use of `#` in C Program**

The `#` symbol in C is used for **preprocessor directives**, which are commands that are processed before the compilation of the program. Some common preprocessor directives:

- **`#include`**: Includes a header file into your program.
  ```c
  #include <stdio.h>
  ```

- **`#define`**: Defines a macro or constant.
  ```c
  #define PI 3.14159
  ```

- **`#ifdef` / `#ifndef`**: Conditional compilation.
  ```c
  #ifdef DEBUG
  printf("Debugging mode\n");
  #endif
  ```

---

### **28. Power of 2 Check in Assembly Language (x86)**

To check if a number is a power of 2, we use the condition `n & (n - 1) == 0` and `n > 0`.

```asm
section .data
    num db 16
    result db 0

section .text
    global _start

_start:
    mov al, [num]     ; Load num into AL
    dec al            ; Decrement AL by 1
    and al, [num]     ; Perform bitwise AND with original num
    jnz not_power_of_2

    mov byte [result], 1  ; num is a power of 2
    jmp done

not_power_of_2:
    mov byte [result], 0  ; num is not a power of 2

done:
    ; Exit
    mov eax, 60        ; syscall: exit
    xor edi, edi       ; status: 0
    syscall
```

---

### **29. I/O (Input/Output) in Java and C**

I/O operations in **C** are performed using `printf`/`scanf` (console I/O) and `fopen`/`fread`/`fwrite` (file I/O).

Example:
```c
#include <stdio.h>

int main() {
    FILE *fptr = fopen("file.txt", "w");
    if (fptr == NULL) {
        printf("Error opening file!\n");
        return 1;
    }
    fprintf(fptr, "Writing to a file.\n");
    fclose(fptr);

    return 0;
}
```

In **Java**, I/O operations are handled using classes like `Scanner`, `File`, `BufferedReader`, etc.

Example:
```java
import java.io.*;

public class FileWriteExample {
    public static void main(String[] args) {
        try {
            FileWriter fw = new FileWriter("file.txt");
            fw.write("Writing to a file.");
            fw.close();
        } catch (IOException e) {
            System.out.println("Error occurred: " + e.getMessage());
        }
    }
}
```

---

### **30. Project Explanation for Interview**

When explaining a project in an interview, structure it as follows:

1. **Introduction**: Briefly introduce the project, its purpose, and the problem it solves.
2. **Technology Stack**: Discuss the tools, technologies, and programming languages used.
3. **Implementation**: Describe the architecture, main features, and challenges faced during implementation.
4. **Your Role**: Focus on your contributions and key tasks you handled.
5. **Outcome**: Share the result or impact of the project.

---

### **31. Function Pointers in C**

A **function pointer** is a pointer that points to the address of a function.

Example:
```c
#include <stdio.h>

int add(int a, int b) {
    return a + b;
}

int main() {
    int (*func_ptr)(int, int) = &add;  // Function pointer
    printf("Sum: %d\n", func_ptr(2, 3));  // Call the function using pointer

    return 0;
}
```

---
Let's continue with the remaining topics.

---

### **32. Shell Basic Commands**

In **Linux**, shell commands are used to interact with the operating system. Some basic commands include:

1. **`ls`**: Lists the contents of a directory.
   ```bash
   ls
   ```

2. **`cd`**: Changes the current directory.
   ```bash
   cd /path/to/directory
   ```

3. **`mkdir`**: Creates a new directory.
   ```bash
   mkdir new_directory
   ```

4. **`rm`**: Removes files or directories.
   ```bash
   rm file.txt   # Remove a file
   rm -r folder  # Remove a folder
   ```

5. **`cp`**: Copies files or directories.
   ```bash
   cp source.txt destination.txt
   ```

6. **`mv`**: Moves or renames files or directories.
   ```bash
   mv old_name.txt new_name.txt
   ```

7. **`chmod`**: Changes file permissions.
   ```bash
   chmod 755 script.sh
   ```

8. **`grep`**: Searches for patterns in files.
   ```bash
   grep "text" file.txt
   ```

9. **`ps`**: Lists running processes.
   ```bash
   ps aux
   ```

10. **`kill`**: Kills a process by its PID.
    ```bash
    kill 1234
    ```

---

### **33. OOP Concepts in Detail (Object-Oriented Programming)**

1. **Encapsulation**: Bundling data (variables) and methods (functions) that operate on the data into a single unit or class. It hides the internal state of objects.
   - Example: A class in Java or C++.
   ```java
   class Car {
       private String model;
       public void setModel(String model) {
           this.model = model;
       }
       public String getModel() {
           return model;
       }
   }
   ```

2. **Abstraction**: Hiding the complex implementation details and showing only the essential features of an object.
   - Example: Abstract classes and interfaces in Java.
   ```java
   abstract class Vehicle {
       abstract void start();
   }
   ```

3. **Inheritance**: Acquiring properties and behavior from a parent class. It allows for code reuse.
   - Example: Class inheritance in Java or C++.
   ```java
   class Car extends Vehicle {
       void start() {
           System.out.println("Car starting...");
       }
   }
   ```

4. **Polymorphism**: Ability to take many forms. It allows the same method to do different things based on the object that it is acting upon.
   - Example: Method overloading and overriding in Java.
   ```java
   class Animal {
       void sound() {
           System.out.println("Animal makes sound");
       }
   }
   class Dog extends Animal {
       void sound() {
           System.out.println("Dog barks");
       }
   }
   ```

---

### **34. Differences between ARM and x86 (Paper Exam)**

#### **ARM Architecture**:
- **Type**: RISC (Reduced Instruction Set Computing)
- **Registers**: More general-purpose registers, allowing for more efficient computation.
- **Power Consumption**: Low power, designed for mobile and embedded devices.
- **Performance**: Performs better for tasks that require simple instructions executed in sequence.
- **Commonly Used In**: Smartphones, tablets, embedded systems.
  
#### **x86 Architecture**:
- **Type**: CISC (Complex Instruction Set Computing)
- **Registers**: Fewer registers but more complex instructions.
- **Power Consumption**: Higher power usage, generally used in desktops and servers.
- **Performance**: Performs better for tasks that benefit from complex instructions.
- **Commonly Used In**: PCs, laptops, and servers.

---

### **35. Header Files, Preprocessor Questions, and Function Calling**

#### **Header Files**:
In C, **header files** are used to include declarations and macro definitions. Common header files include:
- `stdio.h` (for I/O operations)
- `stdlib.h` (for memory allocation, conversion)
- `string.h` (for string manipulation)
  
Example:
```c
#include <stdio.h>  // Includes the standard I/O library

int main() {
    printf("Hello, World!\n");
    return 0;
}
```

#### **Preprocessor Directives**:
Preprocessor directives are commands that are executed before the actual compilation of code. Examples include `#define`, `#include`, and conditional compilation using `#ifdef` and `#ifndef`.

Example:
```c
#define PI 3.14159  // Macro definition
```

#### **Function Calling**:
Function calling is the process of invoking a function in C. It can either be:
- **Call by Value**: Passing a copy of the argument.
- **Call by Reference**: Passing the actual address of the argument (using pointers).

Example:
```c
void add(int a, int b) {
    printf("Sum: %d\n", a + b);
}

int main() {
    add(5, 3);  // Call by value
    return 0;
}
```

---

### **36. IPC (Inter-Process Communication)**

**IPC** is a mechanism that allows processes to communicate and synchronize with each other. There are several IPC mechanisms:

1. **Pipes**: Unidirectional communication between processes. It can only be used between parent and child processes.
   ```c
   pipe(int fds[2]);  // fds[0] for reading, fds[1] for writing
   ```

2. **Message Queues**: Allows multiple processes to send and receive messages.
   ```c
   msgget(), msgsnd(), msgrcv()
   ```

3. **Shared Memory**: Multiple processes can access the same segment of memory.
   ```c
   shmget(), shmat(), shmdt()
   ```

4. **Semaphores**: Used for synchronization between processes.
   ```c
   semget(), semop(), semctl()
   ```

5. **Sockets**: Used for communication between processes over a network.

---

### **37. Binary Tree Program (Add Nodes a to z)**

Here’s a simple program to add nodes to a binary tree and retrieve the parent node of a specific value:

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    char data;
    struct Node* left;
    struct Node* right;
};

struct Node* createNode(char data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return newNode;
}

struct Node* insertNode(struct Node* root, char data) {
    if (root == NULL) {
        return createNode(data);
    }
    if (data < root->data) {
        root->left = insertNode(root->left, data);
    } else if (data > root->data) {
        root->right = insertNode(root->right, data);
    }
    return root;
}

struct Node* findParent(struct Node* root, char child) {
    if (root == NULL || (root->left != NULL && root->left->data == child) || 
        (root->right != NULL && root->right->data == child)) {
        return root;
    }
    if (child < root->data) {
        return findParent(root->left, child);
    } else {
        return findParent(root->right, child);
    }
}

int main() {
    struct Node* root = NULL;
    char nodes[] = {'m', 'b', 'a', 'z', 'h', 'p', 's', 'x'};
    
    for (int i = 0; i < 8; i++) {
        root = insertNode(root, nodes[i]);
    }

    char findNode = 's';
    struct Node* parent = findParent(root, findNode);

    if (parent != NULL) {
        printf("Parent of %c is %c\n", findNode, parent->data);
    } else {
        printf("%c has no parent\n", findNode);
    }

    return 0;
}
```

---

### **38. Return Series of Variables of Different Types**

In C, returning multiple types can be done using **structures**.

Example:

```c
#include <stdio.h>

struct Result {
    int integer;
    float decimal;
    char character;
};

struct Result returnMultiple() {
    struct Result res;
    res.integer = 10;
    res.decimal = 3.14;
    res.character = 'A';
    return res;
}

int main() {
    struct Result res = returnMultiple();
    printf("Integer: %d, Float: %.2f, Character: %c\n", res.integer, res.decimal, res.character);
    return 0;
}
```

---

### **39. Multithreading and Synchronization in C#**

Multithreading in C# can be achieved using the `Thread` class or `Task` class. Synchronization is done using locks, `Mutex`, `Semaphore`, etc.

Example of a simple multithreaded program in C#:

```csharp
using System;
using System.Threading;

class Program {
    static void PrintNumbers() {
        for (int i = 1; i <= 5; i++) {
            Console.WriteLine(i);
            Thread.Sleep(100);
        }
    }

    static void

 Main() {
        Thread t1 = new Thread(PrintNumbers);
        Thread t2 = new Thread(PrintNumbers);
        
        t1.Start();
        t2.Start();

        t1.Join();
        t2.Join();
    }
}
```

---
Here are the remaining topics you mentioned:

---

### **40. Automorphic Number Using Pointer in C**

An **automorphic number** is a number whose square ends with the number itself. For example, 25 is an automorphic number because \(25^2 = 625\), and 625 ends with 25.

Here’s a C program to check if a number is automorphic using pointers:

```c
#include <stdio.h>
#include <math.h>

// Function to check if a number is automorphic
int isAutomorphic(int num) {
    int square = num * num;
    int temp = num;
    int power = 1;

    // Calculate the number of digits in num
    while (temp > 0) {
        temp /= 10;
        power *= 10;
    }

    // Check if the square ends with num
    return (square % power == num);
}

int main() {
    int num;
    printf("Enter a number: ");
    scanf("%d", &num);

    if (isAutomorphic(num)) {
        printf("%d is an automorphic number.\n", num);
    } else {
        printf("%d is not an automorphic number.\n", num);
    }

    return 0;
}
```

---

### **41. Time-Speed-Distance and Time-Work Problems**

#### **Time-Speed-Distance Problems**:

1. **Speed**: Distance/Time
   - Example: A car travels 100 km in 2 hours. Speed = 100 km / 2 hr = 50 km/hr.

2. **Time**: Distance/Speed
   - Example: A cyclist covers 60 km at a speed of 20 km/hr. Time = 60 km / 20 km/hr = 3 hours.

3. **Distance**: Speed * Time
   - Example: A train travels at 80 km/hr for 4 hours. Distance = 80 km/hr * 4 hr = 320 km.

#### **Time-Work Problems**:

1. **Work Done**: Work = Rate * Time
   - Example: If 3 workers can complete a task in 6 days, then 1 worker will complete the task in 18 days.

2. **Combined Work Rate**:
   - If A can complete a task in 10 days and B in 15 days, their combined rate is:
     \[
     \text{Combined Rate} = \frac{1}{10} + \frac{1}{15} = \frac{3+2}{30} = \frac{5}{30} = \frac{1}{6}
     \]
   - They will complete the task together in 6 days.

---

### **42. Shell Basic Commands**

Some additional shell commands:

1. **`find`**: Searches for files in a directory hierarchy.
   ```bash
   find /path -name filename
   ```

2. **`echo`**: Displays a line of text.
   ```bash
   echo "Hello, World!"
   ```

3. **`cat`**: Concatenates and displays file content.
   ```bash
   cat file.txt
   ```

4. **`head`**: Displays the first part of files.
   ```bash
   head file.txt
   ```

5. **`tail`**: Displays the last part of files.
   ```bash
   tail file.txt
   ```

6. **`history`**: Shows command history.
   ```bash
   history
   ```

---

### **43. Basic Questions About Data Science**

**Data Science** involves statistical analysis, machine learning, and data processing to extract insights from data. Key components include:

1. **Data Collection**: Gathering raw data from various sources.
2. **Data Cleaning**: Removing or correcting errors and inconsistencies in the data.
3. **Exploratory Data Analysis (EDA)**: Summarizing and visualizing data to understand its structure and patterns.
4. **Feature Engineering**: Creating new features or variables from existing data to improve model performance.
5. **Modeling**: Applying statistical or machine learning models to make predictions or inferences from data.
6. **Evaluation**: Assessing the performance of models using metrics like accuracy, precision, recall, etc.
7. **Deployment**: Implementing the model in a production environment where it can be used to make decisions based on new data.

**Popular Tools**:
- Programming languages: Python, R
- Libraries: pandas, NumPy, scikit-learn, TensorFlow, Keras
- Visualization tools: Matplotlib, Seaborn, Tableau

---

### **44. Shallow Copy vs Deep Copy in Python**

1. **Shallow Copy**:
   - Copies the reference pointers of objects. Changes to mutable objects in the copied instance will reflect in the original instance.
   - Example: Using `copy.copy()`
     ```python
     import copy
     original = [1, [2, 3]]
     shallow_copy = copy.copy(original)
     shallow_copy[1][0] = 99
     print(original)  # Output: [1, [99, 3]]
     ```

2. **Deep Copy**:
   - Copies the objects recursively, meaning changes to nested objects do not affect the original.
   - Example: Using `copy.deepcopy()`
     ```python
     import copy
     original = [1, [2, 3]]
     deep_copy = copy.deepcopy(original)
     deep_copy[1][0] = 99
     print(original)  # Output: [1, [2, 3]]
     ```

---

### **45. Differences Between ARM and x86**

Already covered above. (Refer to point 34)

---

### **46. C Programming Basics in Depth**

For a comprehensive understanding of **C programming basics**, consider focusing on:

1. **Syntax and Structure**: Data types, operators, control flow (if, for, while).
2. **Functions**: Declaration, definition, and calling of functions.
3. **Pointers**: Pointer arithmetic, pointers to functions.
4. **Memory Management**: Dynamic allocation (malloc, free), stack vs heap.
5. **Data Structures**: Arrays, linked lists, stacks, queues.
6. **File I/O**: Reading from and writing to files using `fopen`, `fread`, `fwrite`.

---

### **47. C Programs for Specific Tasks**

1. **Prime Number Check**:
   ```c
   #include <stdio.h>
   int isPrime(int num) {
       if (num <= 1) return 0;
       for (int i = 2; i * i <= num; i++) {
           if (num % i == 0) return 0;
       }
       return 1;
   }
   int main() {
       int num;
       printf("Enter a number: ");
       scanf("%d", &num);
       if (isPrime(num)) {
           printf("%d is a prime number.\n", num);
       } else {
           printf("%d is not a prime number.\n", num);
       }
       return 0;
   }
   ```

2. **Reverse a String**:
   ```c
   #include <stdio.h>
   #include <string.h>

   void reverseString(char *str) {
       int n = strlen(str);
       for (int i = 0; i < n / 2; i++) {
           char temp = str[i];
           str[i] = str[n - i - 1];
           str[n - i - 1] = temp;
       }
   }

   int main() {
       char str[100];
       printf("Enter a string: ");
       fgets(str, sizeof(str), stdin);
       str[strcspn(str, "\n")] = '\0';  // Remove newline character
       reverseString(str);
       printf("Reversed string: %s\n", str);
       return 0;
   }
   ```

---

### **48. BMC in Server**

**BMC (Baseboard Management Controller)** is a specialized microcontroller on a server motherboard that manages the interface between the system management software and the hardware. It is used for:
- Remote management of servers.
- Monitoring system health (e.g., temperature, voltage).
- Power cycling the server.

---

### **49. Network Layers**

In the **OSI (Open Systems Interconnection) model**, there are 7 layers:

1. **Physical**: Transmits raw bitstream over the physical medium.
2. **Data Link**: Provides node-to-node data transfer and error detection.
3. **Network**: Manages addressing and routing of data.
4. **Transport**: Ensures end-to-end communication and error recovery.
5. **Session**: Manages sessions between applications.
6. **Presentation**: Translates data between the application layer and network formats.
7. **Application**: Interfaces with end-user applications.

---

### **50. Combine Two Strings**

In C:

```c
#include <stdio.h>
#include <string.h>

int main() {
    char str1[100] = "Hello, ";
    char str2[] = "World!";
    
    strcat(str1, str2);  // Concatenate str2 to str1
    printf("%s\n", str1);
    
    return 0;
}
```

---
