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
  riscv64-unknown-elf-gcc- -O1 -mabi=lp64 -marchrv64i -o sum.o sum.c
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
  riscv64-unknown-elf-gcc- -Ofast -mabi=lp64 -marchrv64i -o sum.o sum.c
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
