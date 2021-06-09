# riscv
### when we use this riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
when we type /main then it will show the main section and the address of main section is 10184 and the byte address it is incremented by four
-10184 + 4 =10188
-10188 + 4 =1018c
-1018c + 4 =1019c.....and so on , everytime the address will be incremented by four
### To count the number of instructions -->> I= 101c0-10184=3c;{next block addresss -  main block address}
### total number of instructions = I/4 --> 3c/4=F  {therefore the total number of instructions are 15}
total 15 instructions that came out when we use options O1
### riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c {we are using Ofast instead of O1}
when we type /main then it will show the main section and the address of main section is 100b0 and the byte address it is incremented by four
### To count the number of instructions -->> I = 100e0-100b0=30;{next block addresss -  main block address}
### total number of instructions = I/4 --> 30/4=c  {therefore the total number of instructions are 12}
### Therefore we aboserved that the total number of instructions are decreased from 15 to 12 by changing the options from O1 to Ofast
when we written c code for sum of 1 to n natural numbers and compiled using the gcc compiler we got the below output
- 
![gcc1](https://user-images.githubusercontent.com/84865915/121396975-897ba000-c971-11eb-98f8-e2f91ab9fb99.JPG)

when we want to execute the same program using the riscv compiler
### command used to execute the same program using the riscv compiler
spike pk object file
![spike](https://user-images.githubusercontent.com/84865915/121397056-a021f700-c971-11eb-8f46-3293221e77d4.JPG)
- therefore from the above screenshot we can clearly see that the normal execution and the execution using riscv compiler both giving the same output.
- when we open the object dumb of the above file by using the command **riscv64-unknown-elf-objdump -d sum1ton.o | less**
![instrct](https://user-images.githubusercontent.com/84865915/121397136-b465f400-c971-11eb-96f7-acf61c2585ac.JPG)
- to debug all the above instructions we must use the Debuger **command used is-->spike -d pk sum1ton.o**
- to run the program counter manually step by step we use below command
![pc](https://user-images.githubusercontent.com/84865915/121397183-bf208900-c971-11eb-8558-616e500237f0.JPG)
- to read the contents of particular register we use the below command


![reg](https://user-images.githubusercontent.com/84865915/121397244-c9428780-c971-11eb-97dc-3144ee42a94d.JPG)
and we press enter then we can see the next instruction and also we can see that the after execution of the instruction the contents of the a2 register will be modified as shown in the below screenshot
![register](https://user-images.githubusercontent.com/84865915/121397293-d3648600-c971-11eb-9dff-f93f47835184.JPG)

![stack](https://user-images.githubusercontent.com/84865915/121397362-e2e3cf00-c971-11eb-82b0-032dbba6645b.JPG)
- lui stands for load upper immediate
# when iam taking the value of n=100
![100](https://user-images.githubusercontent.com/84865915/121394624-2983fa00-c96f-11eb-8f41-49e80747d3c6.JPG)

![ofast 100](https://user-images.githubusercontent.com/84865915/121396868-6c46d180-c971-11eb-8e14-286ebbb76d60.JPG)


![main100](https://user-images.githubusercontent.com/84865915/121396550-1eca6480-c971-11eb-8c90-b7d98f6d6f65.JPG)

![fasto main100](https://user-images.githubusercontent.com/84865915/121396611-2d188080-c971-11eb-9f3b-c76e221118eb.JPG)

![each instruc100](https://user-images.githubusercontent.com/84865915/121396682-3d306000-c971-11eb-9794-761560598ba7.JPG)


