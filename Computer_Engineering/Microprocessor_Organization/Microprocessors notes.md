A bus is use to carry data and instructions around the CPU. The CPU has a clock inside it, which is used to synchronize the whole system. In simple systems an instruction is executed each tick. 
Higher clock rate = More instruction cycles in a period of time. A single core CPU can carry out one instruction per tick (At a time) a multicore CPU can execute mutiple instrictions in parallel. 
More CPU cores = Multiple instructions carried out in parallel

When carrying out these instructions, the CPU often need to store and read data from memories like Random Access Memory (RAM). 
Random dans (RAM) signifie que n'importe quelle partie de la memoire peut etre accedee, sans avoir besoin de commencer au premier element de la memoire et naviguer tout le long de la memoire jusqu'a ce que l'element rechercher soit trouve.

## SRAM (Static RAM) 
Data are store as voltage in transistors and need a constant power supply. SRAM is called static because no action is needed to keep data intact. It is used to implement cache memory.
### Advantage of SRAM 
+ lower power needs 
+ higher speed
+ Used in Cache memory
### Disadvantages of SRAM
+ Low store capacity
+ Cost more than DRAM
+ Used for complex design

## DRAM (Dynamic RAM)
Data is stored in capacitors. Capacitors that store data in DRAM gradually discharge energy, no energy means the data has beed lost. DRAM is called dynamic as constant action i.e. refreshing is needed to keep the data intact. It is used to implement the main memory.
### Advantages of DRAM
+ Large storage capacity.
+ Cost less than SRAM

### Disadvantages of DRAM
+ Slower than SRAM
+ Consumes more power

When a computer turns on it doesn't know how to use any component, A piece of ROM holds the most basic instructions and is run automatically when the power is turned on. This instructs the CPU how to use the RAM, Hard drive and so on. 

# Components of a simple CPU

![[Pasted image 20240813130722.png]]

## The control unit
+ Sends control signals to the other parts of the computer system
+ Decode instructions
+ Apply instructions set to identify what routines need to be carries out
## The Arithmetic and Logical Unit (ALU)
The ALU was first proposed by *John von Neumann*. It carries out the majority of the instructions; These are commonly mathematical i.e. ADD, SUBTRACT or logical like AND, OR and logical shifts.

## Registers
+ PC: The program counter stores the memory address of the current or next instruction to be executed.
+ CIR: The current instruction register stores the contents of the memory location that is to be executed, ready to be decoded by the control unit.
+ MAR: The memory address register stred the address of the memory location from which data may be fetched, and when it is fetched, the data are buffered. 
+ MDR: the Memory data register stores the fetched data.
+ ACC: The accumulator is used as a *go to* register for input and result of instructions. For exemple: , the instruction ADD 10 may be implemented to take whatever is in the accumulator, add 10 to it, and put the result back into the accumulator.
There are many different types of CPU:
+ Genera-purpose CPUs: Used in PC and Laptops
+ Embedded processors: Used in Washing machines, cars, fridges, airplanes, IoT-Devices. 
A washing machine CPU is designed to be low power and cheap to produce.
The CPU in a car is  more likely to be as reliable as possible and to be able to produce results within a given very shot time.

These differences will involve differing designs, differing amounts and types of registers, and may even involve the addition (or removal) of certain parts of the processor— if a special-purpose CPU only works with integers then there's no need for a floating point unit, an FPU, for example.

# The System Bus

![[Pasted image 20240813142206.png]]

The CPU contains 3 main busses:
+ The control bus: Is used to transfer control instructions like "*give me data*" back and forth betwenn CPU, Memory and Input/Output controllers
+ The address bus: Carries memory addresses. so while the control bus might say "Give me data from the address I'm sending you", the address bus might carry the address "312" 
+ The data bus: carries data that is to be written or read between the CPU, main memory, and the input/output controllers. So, after the memory unit receives the "Give me data" request and the address "312", it goes to get the data from the memory address 312 and sends it back to the CPU on the data bus.

# How to interpret instructions

![[Pasted image 20240813154738.png]]
Each processor has a instruction set and the programmer can look up the code for indicidual instructions. The first part of the instruction (here 0110) represents the opcode (or operation code). The rest of the instruction is one or more operands. 


