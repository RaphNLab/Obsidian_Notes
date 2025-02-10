# **Introduction**

Basically there are two different running design possible (No RTOS):
+ Super Loop design: The processor do the same task or set of task for ever
+ Foreground-Background design: The processor run a super Loop with interrupt. The CPU interrupts it's background activities to handle the interrupt (Foreground) and go to the background once interrupt is handled.

![[Pasted image 20250112102803.png]]

The disadvantage of this is the "Determinism". If a bug cause that the software come into an infinite loop or the software is not reachable anymore, the is no other way to communicate instead of restarting the system (Turn on, Turn off).

In such design a watch-dog is used to prevent parts of code to be blocked by resetting the system. If instead of a watch-Dog a normal timer is used, we can allow a period of time to a code piece to execute. Once the time elapsed a Timer-ISR is called and in this timer-ISR necessary code is executed to pass the control of the execution to another piece of code. This mechanism is the basic of RTOS. 
+ Determinism is guarantied: We know in advance the amount of time a specific piece of code will be executed
+ The computational power of the CPU is shared.

# **The scheduler** 
The scheduler is similar to the timer ISR that decides what piece of code should be executed at what time. It decides who get the ownership of the CPU and other system resources.

Unspecified code pieces are not allow to get ownership of the CPU. The Scheduler requires minimum criteria to allow a specific piece of code to run.
+ It shall have a name
+ It shall have its own activity to accomplish
+ There should be a mechanism to save its state before releasing the CPU
+ What is his rank among the other pieces of code
The name given to this is **Task**.

==To say in other way, the scheduler keeps on “scheduling” the task with the highest “priority” among the various other tasks that want to get CPU ownership.==


# Queue
A queue is an abstract linear data structure serving as a collection of the elements that are inserted (enqueued operation) and removed (dequeued operation) according to the FIFO principle.
Queues are the channel used by the task to communicate.