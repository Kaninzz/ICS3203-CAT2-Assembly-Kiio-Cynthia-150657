
## **ICS3203-CAT2-Assembly-Kiio-Cynthia-150657**

### **Task 1: Control Flow and Conditional Logic (6 Marks)**

**Overview:**
This program classifies user input as either **POSITIVE**, **NEGATIVE**, or **ZERO** based on the value entered by the user. It uses conditional logic with jump instructions to handle different cases.

**Commands:**
```
cd Task1_controFlow
nasm -f elf32 task1.asm -o task1.o -g
ld -m elf_i386 task1.o -o task1
./task1
```

**Flow:**
- Upon running the above commands, the program prompts you to enter a number.
- Based on the input:
  - If the number is negative, the program prints **NEGATIVE**.
  - If the number is positive (greater than zero), it prints **POSITIVE**.
  - If the number is zero, it prints **ZERO**.

### **Documentation Requirement: Jump Instructions Explanation**

1. **`jne parse_digits`**
   - This instruction checks if the input is negative by verifying the first character. If it's not a `-`, it jumps to parse the digits directly.
   
2. **`je finalize_conversion`**
   - If the end of the string is reached (null terminator), this instruction jumps to finalize the number stored in `eax`.

3. **`jmp parse_loop`**
   - This jump ensures the program continues parsing the digits of the input string until the entire string is processed.

4. **`je zero_case`**
   - If the final value in `eax` is zero, this jump directs the program to display the "ZERO" message.

5. **`jl negative_case`**
   - If the value in `eax` is less than 0, the program jumps to the "NEGATIVE" case to print the relevant message.

6. **`jmp positive_case`**
   - If the number is positive (greater than 0), the program jumps to display the "POSITIVE" message.

---

### **Task 2: Array Manipulation with Looping and Reversal (6 Marks)**

**Overview:**
This program demonstrates array manipulation by reversing an array of integers using a loop and prints the reversed array.

**Commands:**
```
cd Task2_ArrayManipulation
nasm -f elf64 task2.asm -o task2.o -g
ld -m task2.o -o task2
./task2
```

**Array Manipulation:**
- The original array `array db 5, 10, 15, 20, 25` is reversed, resulting in `50, 40, 30, 20, 10`.
- The program performs the reversal using memory manipulation techniques and prints the reversed array to the console.

---

### **Documentation Requirement**

#### **1. Reversing the Array:**

- **Step-by-Step:**
  - `mov rsi, array`: Points `rsi` to the start of the array.
  - `mov rcx, [size]`: Loads the size of the array into `rcx`.
  - `xor rdi, rdi`: Initializes `rdi` to 0, used as the index for the start of the array.
  - `dec rcx`: Decrements `rcx` to point to the last element of the array.
  - **Loop:**
    - The loop `reverse_loop` continues swapping elements starting from the ends of the array.
    - `mov al, [rsi + rdi]` and `mov bl, [rsi + rcx]`: Load elements at `rdi` and `rcx` into registers.
    - `mov [rsi + rdi], bl` and `mov [rsi + rcx], al`: Swap the elements.
    - `inc rdi` and `dec rcx`: Move indices towards the center of the array.

#### **2. Printing the Reversed Array:**

- **Step-by-Step:**
  - `mov rbx, array`: Points `rbx` to the start of the reversed array.
  - `mov rcx, [size]`: Loads the array size to iterate through.
  - **Printing:**
    - Convert each array element to ASCII using the subroutine `int_to_ascii`.
    - Use `mov eax, 1` and `syscall` to print the array elements.

#### **3. Subroutine (`int_to_ascii`):**

- **Converts integer to ASCII:**
  - `div r8`: Divides the number by 10 to get digits.
  - `add dl, '0'`: Converts the digits to ASCII characters.
  - Store the digits in a buffer and reverse the string to ensure the correct order of digits.

---

### **Task 3: Modular Program with Subroutines for Factorial Calculation (4 Marks)**

**Overview:**
This program calculates the factorial of the user input using recursive subroutines.

**Commands:**
```
cd Task3_Factorial
nasm -f elf32 task3.asm -o task3.o -g
ld -m elf_i386 task3.o -o task3
./task3
```

**Flow:**
- The program prompts for a number and computes its factorial recursively.
- The result is printed on the terminal.

---

### **Documentation Requirement**

#### **1. Register Management:**

- **`eax`**: Holds the result of operations (e.g., user input, factorial calculation).
- **`ebx`**: Used for file descriptors in system calls.
- **`ecx`**: Used for loop counters and system call parameters.
- **`edx`**: Used for division and number printing.
- **`esi`**: Manages the position during string conversion.
- **`ebp`**: Manages the stack frame during function calls.

#### **2. Preserving and Restoring Values on Stack:**

- **Before recursion**: `eax` (input number) is pushed onto the stack.
- **After recursion**: The stack pointer is adjusted using `add esp, 4` to restore register values.

#### **3. Subroutines:**

- **`factorial_calc`**: Computes the factorial recursively.
- **`print_number`**: Converts the result into a string and prints it.

---

### **Task 4: Data Monitoring and Control Using Port-Based Simulation (4 Marks)**

**Overview:**
The program simulates monitoring sensor values and controls motor and alarm states based on the thresholds provided.

**Commands:**
```
cd Task4_DataMonitoring
nasm -f elf32 task4.asm -o task4.o -g
ld -m elf_i386 task4.o -o task4
./task4
```

**Flow:**
- The program reads a sensor value, processes it, and performs actions based on the value:
  - If the sensor value is greater than 100, it triggers the alarm.
  - If it is between 51 and 100, the motor is turned on.
  - If it is 50 or below, the motor is turned off.

---

### **Documentation Requirement**

#### **1. Prompt & Input:**

- The program prompts the user to enter a sensor value as a string and converts it into an integer for processing.

#### **2. Conversion:**

- The input string is converted to an integer using a loop.

#### **3. Decision Making:**

- **Comparison logic:**
  - `If greater than 100`: The alarm is triggered.
  - `If between 51 and 100`: The motor is turned on.
  - `If 50 or less`: The motor is turned off.

#### **4. Registers and System Calls:**

- **`eax`**: Holds the converted sensor value and results of comparisons.
- **`ecx`, `ebx`, `edx`**: Used for system calls (printing messages).
