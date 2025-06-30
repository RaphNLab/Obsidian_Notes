
# Sections

![[Sections.png]]


![[Sections_1.png]]


![[Pasted image 20250629194717.png]]

At the linker stage you receive "Unresolved symbol" if glob_ext or func_ext is not known. We first assume that it exist and reserve space for it.

This picture shows how the compiler name is composed.

![[Pasted image 20250629195150.png]]


## Build process

![[Pasted image 20250629195226.png]]

## How to save space during compiling

![[Pasted image 20250629200023.png]]


* **Solution Part 1**: Functions use different sections wich is the key here. By adding solution part 1 it becomes helpful
* **Solution part 2**: We take advantage of the linker garbage collector. The linker will not include sections from with no symbol is needed in the code. Sections that are not needed are simply removed
After compiling some files are generated, these files give information about:


### project_name.map (Linker map file)
* This file is generally used by the debugger 
* From which library a specific function comes
* What is the address (In the flash) of a particular function or variable
* What archive library (archive name.a) does the linker pull to satisfy unresolved bimbos
### The list-file 
* Can be used for debugging purpose
* With the program counter value, it is possible to find out what line of code causes the program to crash
* By analyzing the assembly it's possible to solve the problem