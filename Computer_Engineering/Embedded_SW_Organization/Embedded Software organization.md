# Factors that influence Embedded systems development

- Complex and demanding requirements
- Cost
- Short Time to market (Reduces development time)
- Hardware complexity
- Human ressources (Developper experience)

# Advantages of software organization

- Optimize and speed-up software development without compromissing safety, robustness and  Quality of the software component
- Increase the software portability to different  hardware platforms

# Definitions

- Software Architecture
	Is a collection of software components that follows an organized structure, and describes the overall system and it components behavior from a high-level design perspective
-  Embedded Software Architecture 
	Is the structure and organization of multiple software components through different abstraction layers that intend to provide hardware independence and maximize code reusability.
-  Abstraction
	 Simplified view of a system containing only the details important for a particular purpose
- Embedded Software Abstraction
	 Design methodology used to hide hardware architecture details from the application software domain by the isolation and encapsulation of relevant parameters that describe the behavior of an specific hardware entity, in order to facilitate software component reusability and portability.
- Software Component
    dfIs an entity well defined behavior and interacts with other components and modules within the system.
- Software interface
	 Is a mechanism used by a software component or module to interact with the external world (i.e., analog/digital signals, RF) and other software components.
- Coupling
	 Degree of dependency between different software components within a system.
- Cohesion
	 Measures the degree of relationship between elements within a software component

*All architecture is design, but not all design is architecture. Architecture represents the significant design decisions that shape a syste, where significant is measured by ==cost of change==*

# Layered architecture exemple

![[Pasted image 20240808142149.png]]

1. MCU Peripheral drivers layer
	- Internal device driver
	- Hardware access to MCU peripherals
	- Provide MCU low-level abstraction
	- High hardware dependency, therefore, reuse is limited at this level
	- Provide standard interfaces used by HAL, Os and external driver layers 
2. Hardware abstraction layer (HAL)
	* Provides access to MCU hardware feature through periperal driver layer
	* Hide hardware details not relevant to upper software layers
	* Interfaces with MCU and external drivers in the low level side, and with HAL signal interface at the upper side
3. Middleware
	* Facilitates the interaction between application components and other modules and/or components within the system:
		* Graphics Library
		* Networking
		* File systems
		* Databases
	* Provides system management
	  * Power Management
	  * Memory management
	  * Diagnostics
	*==Due to overhead, it is an optional layer==*  
4. External drivers
	* Implements direct hardware access to external devices through MCU peripherals
	* Meet all functional and timing requirements of the external devices
	* Examples:
		* EEPROM (I2C, SPI, etc)
		* External ADCs (Delta-Sigma high-resolution converters)
		* Sensors and Actuators
		* I/O Driver ICs
5. Embedded Infrastructure SW interface
	* Provide to the applicationn one more level of abstraction and hardware independence
	* Translates logical signals into a meaningful format for the application
	* facilitates the communication between application software components and/or lower layer modules
	 *==Due to overhead, it is an optional layer==*
6. Application layer
	 * Product specific functions
	 * Contains the software components that implements the desired functionality (unique) for a specific embedded computer system
	 * A high-level design methodology ignores the details of the hardware
	 * Reusability of application components strongly depends in the availability and efficiency of lower layers
7. OS
	* Provides support for multi-tasking
	* Task scheduling and synchronization
	* If real-time OS (RTOS)
		-  Context-switsching
		- Task preemption
		- Interrupt management
## Software layered architecture advantages

- [-] Organized and modular design
- [-] If properly applied, an architectureal approach allows and facilitate distributed development; software components being developed by different teams
- [-] Once a software architecture has evolved reaching an optimal level of maturity, the development process can be benefited by reducing development time and cost
- [-] Well defined architectures facilitates the usage of more advanced development techniques and tools, i.e., Model Based and Code Generation 
## Software layered architecture disadvantages

- [?] Modular layered software architecture and abstraction can consume significant resources in an embedded system in terns of memory and performance
	- From few kBytes of ROM/RAM to the order of several MBytes
	- From tenths of MHz to hundreds of MHz (even GHz)
- [-] Transitioning from traditional embedded software development into a layered software architechture, can result in a large learning curve:
	- Adopting a new design and implementation methodology
	- learning new tools
- [-] Initially, the adoption of software layered architectures may result in a spike in cost and development time, making diffcult its acceptance

## Directory structure exemple

![[Pasted image 20240808153237.png]]

## Example - Dome Light Control

![[Pasted image 20240808153440.png]]

![[Pasted image 20240808160347.png]]



![[Pasted image 20240808160420.png]]



![[Pasted image 20240808160636.png]]

![[Pasted image 20240808160652.png]]

![[Pasted image 20240808160710.png]]

![[Pasted image 20240808160731.png]]


![[Pasted image 20240808160754.png]]

![[Pasted image 20240808160807.png]]


![[Pasted image 20240808160909.png]]


![[Pasted image 20240808160934.png]]


![[Pasted image 20240808160952.png]]


![[Pasted image 20240808161004.png]]


![[Pasted image 20240808161027.png]]

![[Pasted image 20240808161046.png]]


![[Pasted image 20240808161102.png]]

![[Pasted image 20240808161124.png]]


![[Pasted image 20240808161140.png]]


![[Pasted image 20240808161157.png]]


![[Pasted image 20240808161211.png]]


![[Pasted image 20240808161226.png]]

# Conclusion


- The Embedded world requires more sophisticated design methodologies that can satisfy market demands, it is important to develop robust architechtures that allow more efficient and low cost implementations
- The even more exigent and complex requirements trigger the advances of semiconductor industry, providing more powerful processors; therefore, software development becomes a more complex task
- The evolvement of software requires the application of more advanced software engineering concepts
- Embedded software development is not a trivial task; a ner culture of development is emerging and requires immediate attention
- The embeddded Software development is not the task of electrical engineers anymore; neither pure software engineers; new culture of development is emerging 


Source: Vector https://ewh.ieee.org/r4/se_michigan/cs/20131019/Embedded%20Software%20Organization%20-%20Architecture%20and%20Design.pdf