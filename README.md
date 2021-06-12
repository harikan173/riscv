# RISC-V based Microprocessor
![riscimage](https://user-images.githubusercontent.com/84865915/121753478-12d8d100-cb30-11eb-9632-421dfff5950d.JPG)

RISC-V is a free and open ISA enabling a new era of processor innovation through open standard collaboration. Born in academia and research, RISC-V ISA delivers a new level of free, extensible software and hardware freedom on architecture, paving the way for the next 50 years of computing design and innovation. A number of companies are offering or have already announced RISC-V hardware, open source operating systems with RISC-V support are available and the instruction set is supported in several popular software toolchains.

This repository contains all the information needed to build your RISC-V pipelined core, which has support of base interger RV32I instruction format and testing it with a simple C code using TL-Verilog on [Makerchip IDE platform](https://www.makerchip.com/).


Introduction to RISC-V basic keywords
Labwork for RISC-V software toolchain
Integer number representation
Signed and unsigned arithmetic operations
Day 2: Introduction to ABI and basic verification flow
Application Binary interface (ABI)
Lab work using ABI function calls
Basic verification flow using iverilog
Day 3: Digital Logic with TL-Verilog and Makerchip

Combinational logic in TL-Verilog using Makerchip
Sequential and pipelined logic
Validity
Hierarchy
Day 4: Basic RISC-V CPU micro-architecture

Microarchitecture and testbench for a simple RISC-V CPU
Fetch, decode, and execute logic
RISC-V control logic
Day 5: Complete Pipelined RISC-V CPU micro-architecture/store

Pipelining the CPU
Load and store instructions and memory
Completing the RISC-V CPU
Wrap-up and future opportunities
# RISC-V based Microprocessor

RISC-V is a free and open ISA enabling a new era of processor innovation through open standard collaboration. Born in academia and research, RISC-V ISA delivers a new level of free, extensible software and hardware freedom on architecture, paving the way for the next 50 years of computing design and innovation. A number of companies are offering or have already announced RISC-V hardware, open source operating systems with RISC-V support are available and the instruction set is supported in several popular software toolchains.

This repository contains all the information needed to build your RISC-V pipelined core, which has support of base interger RV32I instruction format and testing it with a simple C code using TL-Verilog on Makerchip IDE platform.
  This repository contains all the information studied and created during the [Advanced Physical Design Using OpenLANE / SKY130](https://www.vlsisystemdesign.com/advanced-physical-design-using-openlane-sky130/) workshop. It is primarily foucused on a complete RTL2GDS flow using the open-soucre flow named OpenLANE. [PICORV32A](https://github.com/cliffordwolf/picorv32) RISC-V core design is used for the purpose.

# Table of Contents

  - [Day 1  Introduction to RISC V ISA and GNU compiler toolchain](#day-1--introduction-to-risc-v-isa-and-gnu-compiler-toolchain)
    - [Basic IC Design Terminologies](#basic-ic-design-terminologies)
    - [Introduction To RISC-V](#introduction-to-risc-v)
    - [SoC Design and OpenLANE](#soc-design-and-openlane)
      - [Open-Source PDK Directory Structure](#open-source-pdk-directory-structure)
      - [What is OpenLANE](#what-is-openlane)
    - [Open-Source EDA Tools](#open-source-eda-tools)
      - [OpenLANE Initialization](#openlane-initialization)
      - [Design Preparation](#design-preparation)
      - [Design Synthesis and Results](#design-synthesis-and-results)
  - [Day 2 Introduction to ABI and basic verification flow](#day-2-introduction-to-abi-and-basic-verification-flow)
    - [Application Binary interface (ABI)](#Application-binary-interface-(ABI))
      - [Utilization Factor and Aspect Ratio](#utilization-factor-and-aspect-ratio)
      - [Power Planning](#power-planning)
      - [Pin Placement](#pin-placement)
      - [Floorplan using OpenLANE](#floorplan-using-openlane)
      - [Review Floorplan Layout in Magic](#review-floorplan-layout-in-magic)
    - [Placement](#placement)
      - [Placement and Optimization](#placement-and-optimization)
      - [Placement using OpenLANE](#placement-using-openlane)
    - [Cell Design and Characterization Flows](#cell-design-and-characterization-flows)
      - [Cell Design Flow](#cell-design-flow)
      - [Characterization Flow](#characterization-flow)
  - [Day 3 - Design library cell using Magic Layout and ngspice characterization](#day-3---design-library-cell-using-magic-layout-and-ngspice-characterization)
    - [CMOS Inverter Design using Magic](#cmos-inverter-design-using-magic)
    - [Extract SPICE Netlist from Standard Cell Layout](#extract-spice-netlist-from-standard-cell-layout)
    - [Transient Analysis using NGSPICE](#transient-analysis-using-ngspice)
  - [Day 4 - Pre-layout timing analysis and importance of good clock tree](#day-4---pre-layout-timing-analysis-and-importance-of-good-clock-tree)
    - [Magic Layout to Standard Cell LEF](#magic-layout-to-standard-cell-lef)
    - [Timing Analysis using OpenSTA](#timing-analysis-using-opensta)
    - [Clock Tree Synthesis using TritonCTS](#clock-tree-synthesis-using-tritoncts)
  - [Day 5 - Final steps for RTL2GDS](#day-5---final-steps-for-rtl2gds)
    - [Generation of Power Distribution Network](#generation-of-power-distribution-network)
    - [Routing using TritonRoute](#routing-using-tritonroute)
    - [SPEF File Generation](#spef-file-generation)
  - [References](#references)
  - [Acknowledgement](#acknowledgement)
# Day 1  Introduction to RISC-V ISA and GNU compiler toolchain 
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
# day2
## algorithm to rewrite c program using ASM language
intially from the main program we will pass intial number and the final number
# initialize
![main program](https://user-images.githubusercontent.com/84865915/121748068-018ac700-cb26-11eb-8600-23add644e1d8.JPG)
![load1](https://user-images.githubusercontent.com/84865915/121748110-12d3d380-cb26-11eb-874b-dab11710d5cd.JPG)
![risc1](https://user-images.githubusercontent.com/84865915/121748149-22531c80-cb26-11eb-93bb-b06af89ff2b9.JPG)
![risc2](https://user-images.githubusercontent.com/84865915/121748163-2717d080-cb26-11eb-9dca-e9e715cabb11.JPG)
![gitclone](https://user-images.githubusercontent.com/84865915/121748247-44e53580-cb26-11eb-8c21-ece6a6e29d53.JPG)
![directory](https://user-images.githubusercontent.com/84865915/121748263-4ca4da00-cb26-11eb-84ea-a71ad40a14b7.JPG)
![direct1](https://user-images.githubusercontent.com/84865915/121748275-50d0f780-cb26-11eb-8eaa-4e4de39d87c2.JPG) 
- we can see picorv32.v file which is one of the riscv cpu and we can run it by using the command vim picorv32 or less picorv32
![pico](https://user-images.githubusercontent.com/84865915/121748327-634b3100-cb26-11eb-8e97-51228952ce6c.JPG)
- If we open that particular riscv cpu then we can see that the top level module name as picorv32
![pico1](https://user-images.githubusercontent.com/84865915/121748398-7cec7880-cb26-11eb-92e9-b05baeaeb7c9.JPG)
- this is the test bench used used for verification purpose 
- And also we can see that picorv32 is under uut
![pico2](https://user-images.githubusercontent.com/84865915/121748416-84138680-cb26-11eb-91f8-96625380b5c4.JPG)
- below sccreenshot we are reading the hex fileinto the memory
- command used for reading the hex file is readmemh
![pico3](https://user-images.githubusercontent.com/84865915/121748421-883fa400-cb26-11eb-865c-fce1719dc475.JPG)
- immage shows the standard scripts of how do we create the hex file
- script over here is vimrv32im.h
- in that image we can also see the set of scripts that are needed to covert into hex file
![pico4](https://user-images.githubusercontent.com/84865915/121748426-8b3a9480-cb26-11eb-91ee-16442d09f37e.JPG)
- to run the above scripts the command used are:
- chmod 777 rv32im.sh
- ./rv32ikm.sh
![pico6](https://user-images.githubusercontent.com/84865915/121748433-8fff4880-cb26-11eb-8fde-68d07652a3c2.JPG)
- above figure shows the sum os numbers from 1 to 2 is 3
![pico7](https://user-images.githubusercontent.com/84865915/121748437-942b6600-cb26-11eb-990d-95a83d943deb.JPG)
- these above scripts can create the hex file
- commands to see the hex files are:
- -vimfirmware.hex
- and we can clearly see that application software is getting converted into bits patterns or bits stream
![pico8](https://user-images.githubusercontent.com/84865915/121748448-9a214700-cb26-11eb-8e6f-2d518c660a7e.JPG)
- the above figure shows how the bitstream file looks like 
- to veiw this we must use the command firmware 32.hex
- then next this bitstream file is loaded into the memory through the test bench
![pico10](https://user-images.githubusercontent.com/84865915/121748452-9db4ce00-cb26-11eb-8902-01811da5e517.JPG)
- Now that bitstream file is being used by the picorv32 unit under test and then hex file is processed by the testbench code
- finally we displays the output.
# day 3
- Now that bitstream file is being used by the picorv32 unit under test and then hex file is processed by the testbench code
- finally we displays the output.

### RTL Design Using TL-Verilog and Makerchip
Makerchip is a free online environment for developing high-quality integrated circuits. You can code, compile, simulate, and debug Verilog designs, all from your browser. Your code, block diagrams, and waveforms are tightly integrated.

Following are some unique features of TL-Verilog:

Supports 
- "Timing Abstraction"

- Easy Pipelining

- TL-Verilog removes the need always blocks, flip-flops.

- Compiler available converts TL-Verilog to Verilog, which can be easily synthesized
![mk1](https://user-images.githubusercontent.com/84865915/121682845-37a25980-cada-11eb-89ec-684c449dd917.JPG)
### eg:fpga multiplier
```
  \m4_TLV_version 1d: tl-x.org
\SV
   // Based on the design from: http://surf-vhdl.com/how-to-implement-pipeline-multiplier-vhdl/?utm_source=mult-pipe&utm_medium=LK2&utm_campaign=ACLEAD
   // Converted to TL-Verilog with validity added, as well as inline stimulus and checking.
   
   // The logic diagram for this example, from Surf VHDL is (originally) here:
   //   http://surf-vhdl.com/wp/wp-content/uploads/2016/12/Mult-35x35_break_PIPE2.jpg

   m4_makerchip_module
 
\TLV
   |mul
      ?$valid
         
         // Random stimulus
         @0
            m4_rand($aa, 34, 0)
            m4_rand($bb, 34, 0)
         
         
         // 1. A.lower * B.lower (green rectangle in surf-vhdl diagram)
         @1
            $pp1[33:0] = $aa[16:0] * $bb[16:0];
         @2
            $mm1[16:0] = $pp1[16:0];
         
         // 2. A.lower * B.upper (lower purple rectangle in surf-vhdl diagram)
         @2
            $pp2[51:17] = $aa[16:0] * $bb[34:17];
         @3
            $mm2[52:17] = $pp2[51:17] + $pp1[33:17];
         
         // 3. A.upper * B.lower (upper purple rectangle in surf-vhdl diagram)
         @3
            $pp3[51:17] = $aa[34:17] * $bb[16:0];
         @4
            $mm3[52:17] = $pp3[51:17] + $mm2[52:17];
         
         // 4. A.upper * B.upper (orange rectangle in surf-vhdl diagram)
         @4
            $pp4[69:34] = $aa[34:17] * $bb[34:17];
         @5
            $mm4[69:34] = $pp4[69:34] + $mm3[52:34];
         
         // Output
         @6
            $mm[69:0] = {$mm4[69:34], $mm3[33:17], $mm1[16:0]};
         
         
         //---------------------
         // Testbench (inlined)
         
         // Perform full width multiplication and compare with DUT result.
         @7
            $mm_full[69:0] = $aa * $bb;
            // Sticky error flag.
            $Error <= *reset ? 0 : $Error || ($mm_full != $mm);
            
            
            // Assert these to end simulation (before Makerchip cycle limit).
            *passed = *cyc_cnt > 40;
            *failed = $Error;
 
\SV
   endmodule
 
```

![mk2](https://user-images.githubusercontent.com/84865915/121682860-3cffa400-cada-11eb-98ac-21b86ba23064.JPG)

![mk3](https://user-images.githubusercontent.com/84865915/121682888-4557df00-cada-11eb-9b40-4f5200edafb4.JPG)

### eg:pythagorean
```
 \m4_TLV_version 1d: tl-x.org
\SV
   `include "sqrt32.v";
   
   m4_makerchip_module
\TLV
   
   // Stimulus
   |calc
      @0
         $valid = & $rand_valid[1:0];  // Valid with 1/4 probability
                                       // (& over two random bits).
   
   // DUT (Design Under Test)
   |calc
      // [+] ?$valid
      @1                                  // [>>>]
         $aa_sq[7:0] = $aa[3:0] ** 2;     // [>>>]
         $bb_sq[7:0] = $bb[3:0] ** 2;     // [>>>]
      @2                                  // [>>>]
         $cc_sq[8:0] = $aa_sq + $bb_sq;   // [>>>]
      @3                                  // [>>>]
         $cc[4:0] = sqrt($cc_sq);         // [>>>]


   // Print
   |calc
      @3
         \SV_plus
            always_ff @(posedge clk) begin
               // [+] if ($valid)
                  \$display("sqrt((\%2d ^ 2) + (\%2d ^ 2)) = \%2d", $aa, $bb, $cc);
            end

\SV
   endmodule
  
```
![pk1](https://user-images.githubusercontent.com/84865915/121683793-7dabed00-cadb-11eb-9488-21a3508aa444.JPG)
![pk2](https://user-images.githubusercontent.com/84865915/121683823-88668200-cadb-11eb-9c28-013476f38355.JPG)

### eg:inverter
```
 \TLV
   $reset = *reset;

   $out = ! $in1;

   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
  
```
![invert](https://user-images.githubusercontent.com/84865915/121688421-0f6a2900-cae1-11eb-91f0-cb725030b4ba.JPG)
### eg: and
```
 \TLV
   $reset = *reset;

   $out =  $in1 && $in2;

   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV  
```

![qand](https://user-images.githubusercontent.com/84865915/121689083-d54d5700-cae1-11eb-907f-91270bce83f4.JPG)
### eg:or gate
```
  \TLV
   $reset = *reset;

   $out =  $in1 || $in2;

   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
 
```
![qor](https://user-images.githubusercontent.com/84865915/121689474-43921980-cae2-11eb-8a9f-306a3976d939.JPG)
### eg:exor gate
```
  \TLV
   $reset = *reset;

   $out =  $in1 ^ $in2;

   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule 
```

![qexor](https://user-images.githubusercontent.com/84865915/121691067-3544fd00-cae4-11eb-98af-808045fcb126.JPG)
### eg:vectors
```
  \TLV
   $reset = *reset;

   $out[4:0] =  $in1[3:0] + $in2[3:0];

   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
 
```
![vect](https://user-images.githubusercontent.com/84865915/121709018-bbb60a80-caf5-11eb-86e2-ba99436de690.JPG)
## Designing of calculator
### cobinational calculator
```
 \TLV
   $reset = *reset;

   $val1[31:0] =  $rand1[3:0]; 
   $val2[31:0] =  $rand2[3:0];
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
  
```
![calcul](https://user-images.githubusercontent.com/84865915/121710812-90ccb600-caf7-11eb-895d-d1c8b4bdc8ce.JPG)
### fibonacci sereis
```
\TLV
   $reset = *reset;

   $num[31:0] =  $reset ? 1 : (>>1$num + >>2$num);

   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule   
```
![fibonac](https://user-images.githubusercontent.com/84865915/121710194-f9676300-caf6-11eb-8154-785dc4feed90.JPG)
### single stage pipeline
![pipelinedesin](https://user-images.githubusercontent.com/84865915/121765009-a7115b00-cb65-11eb-88f3-5abe533d1b1e.JPG)
### pipelined design
- In this we are distributing the computational time
- In this pipelined design we can see that c value is two stages later in the pipeline
- there are two stages of flops,the values we are looking at stage one signals effect the stage three signals two cycles later.
![singlesatgepipeline](https://user-images.githubusercontent.com/84865915/121765018-b1cbf000-cb65-11eb-8f15-9a1cf9b7eeaf.JPG)
### retiming 
- By retiming we can see the number of flipflops present 
![retiming](https://user-images.githubusercontent.com/84865915/121765386-17b97700-cb68-11eb-8e95-19d94650ac79.JPG)





