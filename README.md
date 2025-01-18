# vsd_asic
## **Task 1**
### **C program to calculate all numbers from 1 to n**
![image](https://github.com/user-attachments/assets/2ee593a4-10f3-4479-8817-a2a3c28b446d)
- ```
  gcc sum.c
  ```
  to compile the c code
- ```
  ./a.out
  ```
  to see the output
![image](https://github.com/user-attachments/assets/6a1313bf-d4a7-4a52-9c63-378629ac78a5)

![image](https://github.com/user-attachments/assets/b5cf698d-1d73-4875-adcf-bdad7a47a07d)
- now create a object file sum.o using the command
  ```
   riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum.o sum.c
  ```
- to look into the object file for instruction sets
  ```
  riscv64-unknown-elf-objdump -d sum.o  | less
  ```
- now go to the main section in the file to check the number of instructions
![image](https://github.com/user-attachments/assets/bb5ad334-dbb2-4530-9be8-a02246696602)
![image](https://github.com/user-attachments/assets/96d2163e-17c9-42c5-9bde-f792d1db8b32)
![image](https://github.com/user-attachments/assets/e667340b-0811-4693-9f2a-28672a105ce6)
![image](https://github.com/user-attachments/assets/e5fd0933-5b23-43e0-88b8-a49f0f5e4b3d)
- For the "main" section, we can determine the number of instructions by subtracting the address of the first instruction in the next section from the address of the first instruction in the main section, then dividing the difference by 4 (since each instruction is 4 bytes).
- so total number of instructions is 25

- now compile the code using the riscv compiler using ofast optimisation
```
  riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum.o sum.c
```
   ![image](https://github.com/user-attachments/assets/8609ecff-5519-4fe6-a3ca-3da391c0269e)
   ![image](https://github.com/user-attachments/assets/f56ae57e-72ac-4980-90fe-fb7495f6940e)
  ![image](https://github.com/user-attachments/assets/9f128639-0657-43f8-9cbb-98343eafdb73)
  ![image](https://github.com/user-attachments/assets/a26b5713-3780-44ce-8113-45b10ee3c3f3)

- There are a total of 25 instructions using O1 and a total of 24 instructions using Ofast. O1 provides a balanced optimization, resulting in more instructions, whereas Ofast prioritizes faster compilation time, leading to fewer instructions.

## **Task 2**
![image](https://github.com/user-attachments/assets/eacf00e1-9a24-4ff0-9f51-a32e5a9aa8cb)
![image](https://github.com/user-attachments/assets/4ca1ac17-4c6f-487b-81f8-8687f0b2d562)
![image](https://github.com/user-attachments/assets/f7fc7886-d620-4871-9fcd-b38b4d71fa1b)

## **Task 3**
Below is a description of each instruction included in the hardcoded implementation:

---

### **1. add r6, r1, r2**
- **Operation**: Performs an arithmetic addition of the values in registers `r1` and `r2`, and stores the result in register `r6`.
- **Syntax**: `add rd, rs1, rs2`
- **Use Case**: Commonly used for simple arithmetic operations.

---

### **2. sub r7, r1, r2**
- **Operation**: Subtracts the value in register `r2` from the value in register `r1`, and stores the result in register `r7`.
- **Syntax**: `sub rd, rs1, rs2`
- **Use Case**: Used for subtraction operations.

---

### **3. and r8, r1, r3**
- **Operation**: Performs a bitwise AND operation between the values in registers `r1` and `r3`, and stores the result in register `r8`.
- **Syntax**: `and rd, rs1, rs2`
- **Use Case**: Useful for masking specific bits.

---

### **4. or r9, r2, r5**
- **Operation**: Performs a bitwise OR operation between the values in registers `r2` and `r5`, and stores the result in register `r9`.
- **Syntax**: `or rd, rs1, rs2`
- **Use Case**: Commonly used for setting specific bits in a value.

---

### **5. xor r10, r1, r4**
- **Operation**: Performs a bitwise XOR operation between the values in registers `r1` and `r4`, and stores the result in register `r10`.
- **Syntax**: `xor rd, rs1, rs2`
- **Use Case**: Used in generating parity bits or toggling specific bits.

---

### **6. slt r11, r2, r4**
- **Operation**: Sets `r11` to `1` if the value in register `r2` is less than the value in register `r4`, otherwise sets `r11` to `0`.
- **Syntax**: `slt rd, rs1, rs2`
- **Use Case**: Used for conditional operations and comparisons.

---

### **7. addi r12, r4, 5**
- **Operation**: Adds the immediate value `5` to the value in register `r4`, and stores the result in register `r12`.
- **Syntax**: `addi rd, rs1, imm`
- **Use Case**: Frequently used to load small constants or perform offset calculations.

---

### **8. sw r3, r1, 2**
- **Operation**: Stores the value in register `r3` into the memory location at address `r1 + 2`.
- **Syntax**: `sw rs2, imm(rs1)`
- **Use Case**: Used to store data in memory, such as saving temporary results or variables.

---

### **9. lw r13, r1, 2**
- **Operation**: Loads a 32-bit value from the memory address `r1 + 2` into register `r13`.
- **Syntax**: `lw rd, imm(rs1)`
- **Use Case**: Used to retrieve data from memory into a register.

---

### **10. bne r0, r1, 20**
- **Operation**: Compares the values in registers `r0` and `r1`. If they are not equal, the program counter is updated to `PC + 20`, effectively performing a branch.
- **Syntax**: `bne rs1, rs2, offset`
- **Use Case**: Useful for implementing loops or conditional jumps.

---
- **Instruction Categories**:
  - **Arithmetic Operations**: `add`, `sub`, `addi`
  - **Logical Operations**: `and`, `or`, `xor`
  - **Comparison**: `slt`
  - **Memory Access**: `lw`, `sw`
  - **Control Flow**: `bne`
- **Registers**:
  - `rs1` and `rs2`: Source registers
  - `rd`: Destination register
  - `imm`: Immediate value
  
hardcoded all the instructions
![image](https://github.com/user-attachments/assets/158c7635-a2c2-42a4-b958-bc71a3b3e40c)


hardcoded add instruction updated verilog code
```
always @(posedge RN) begin
    NPC <= 32'd0;

    // Initialize instruction memory with the hardcoded instruction
    MEM[0] <= 32'h02208333;  // add r6, r1, r2
    MEM[1] <= 32'h00000000;  // NOP or empty instruction for simplicity
    // Other instructions can follow here...

    // Initialize registers for testing
    REG[0] <= 32'h00000000;
    REG[1] <= 32'd10;  // r1 = 10
    REG[2] <= 32'd20;  // r2 = 20
    REG[6] <= 32'd0;   // r6 = 0 (will hold result)
end
```
![image](https://github.com/user-attachments/assets/fe12f7b0-3b11-4e6b-a2b6-8831a1e4e14b)
hardcoded sub  r7, r1, r2
```
always @(posedge RN) begin
    NPC <= 32'd0;

    // Initialize instruction memory with the hardcoded instruction
    MEM[0] <= 32'h02209380;
    MEM[1] <= 32'h00000000;  // NOP or empty instruction for simplicity
    // Other instructions can follow here...

    // Initialize registers for testing
    REG[0] <= 32'h00000000;
    REG[1] <= 32'd10;  // r1 = 10
    REG[2] <= 32'd20;  // r2 = 20
    REG[7] <= 32'd0;   
end
```
![image](https://github.com/user-attachments/assets/eaac884a-ba11-4821-86fb-0322d35ab006)
Hardcoded Instruction: and r8, r1, r3
![image](https://github.com/user-attachments/assets/812ab672-82bf-46d7-99f9-4a5b86636be6)
Hardcoded Instruction: or r9, r2, r5
![image](https://github.com/user-attachments/assets/8dcbd77f-cd14-4c78-9a9b-9d66c3093fca)
Hardcoded Instruction: xor r10, r1, r4
![image](https://github.com/user-attachments/assets/c075bd5e-6a05-4d01-8a8f-15439d18a251)
Hardcoded Instruction: slt r11, r2, r4
![image](https://github.com/user-attachments/assets/e3b27ede-cc82-4fa9-b1d7-2b81c7fe8dc3)
Hardcoded Instruction: addi r12, r4, 5
![image](https://github.com/user-attachments/assets/470f7f85-e2fb-4e4c-9b94-e36eb709753b)
Hardcoded Instruction: sw r3, r1, 2
![image](https://github.com/user-attachments/assets/7085ddf7-dd1e-42b4-8576-36b2a592e4af)
Hardcoded Instruction: lw r13, r1, 2
![image](https://github.com/user-attachments/assets/1192b4d4-7877-4553-a218-9a56f4a5421a)
Hardcoded Instruction: beq r0, r0, 15
![image](https://github.com/user-attachments/assets/5afd6ac0-3a2a-4d9f-b001-fa3560f572ab)
Hardcoded Instruction: add r14, r2, r2
![image](https://github.com/user-attachments/assets/61a13600-dd5c-475d-9524-b6af528d8472)
Hardcoded Instruction: bne r0, r1, 20
![image](https://github.com/user-attachments/assets/1da33d73-7b74-4fad-9940-7fff051051e5)

## **Task 4**
write a c program to do a binary search on a sorted array
```
#include <stdio.h>

// Function to perform binary search
int binarySearch(int arr[], int size, int target) {
    int low = 0;
    int high = size - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2; // Avoids potential overflow
        if (arr[mid] == target) {
            return mid; // Target found
        } else if (arr[mid] < target) {
            low = mid + 1; // Search in the right half
        } else {
            high = mid - 1; // Search in the left half
        }
    }

    return -1; // Target not found
}

int main() {
    int sortedArray[] = {1, 3, 5, 7, 9, 11};
    int size = sizeof(sortedArray) / sizeof(sortedArray[0]);
    int target = 7;

    int result = binarySearch(sortedArray, size, target);

    if (result != -1) {
        printf("Element %d found at index %d.\n", target, result);
    } else {
        printf("Element %d not found in the array.\n", target);
    }

    return 0;
}
```
![image](https://github.com/user-attachments/assets/fd85092f-557e-45ab-a768-2eb4cc6dfcfe)
compile using riscv compiler and create bin.o file and see the number of instructions
![image](https://github.com/user-attachments/assets/e882e6c5-1f44-42a7-92bc-f4c9dc62cb86)

now compile the c program with ricv compiler with Ofast optimisation
![image](https://github.com/user-attachments/assets/0a7d8768-1e0a-4972-8b98-7816edd6f920)
now create object file
![image](https://github.com/user-attachments/assets/9e82fb65-b471-4dd6-98d2-389f53905c35)
there are 48 instructions
mow run the spike simulation
![image](https://github.com/user-attachments/assets/d4879fa4-3ff2-4f32-9269-a1285c133a6b)
We now bring the PC (program counter) to the start of the main function using the command 'until pc 0 100b0'. We then check the contents of register 'a5' before and after running the instructions. After executing the commands, we observe that the registers 'a5' is properly loaded with appropriate values.
![image](https://github.com/user-attachments/assets/12fde7ae-913f-4d75-8ec1-9c00f1135f5c)




