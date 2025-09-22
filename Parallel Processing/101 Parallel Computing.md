---
aliases:
---
Parallel computing means large-scale computing for big problems
## Demands of Large-Scale Computing
• Examples of Applications:
	• Megafire modeling for emergency response
	• Tsunami & hurricane surge simulations
	• Climate modeling over decades
	• Voice & image recognition (e.g., autonomous vehicles)
• *AI & machine learning* now drive large-scale compute demand

**Why Parallel Computing?**
Why is it large-scale computing? We have done many programming languages at this point tackling small problems. Perhaps we need to try solving much greater problems. Parallel programming helps us solve large problems or simply solve problems much faster.
• Enables solving larger problems & faster simulations  
• Essential to unlock unused compute potential  
• Can speed up applications 10x, 100x, or 1000x  
• What is Parallel Computing?  
	• Performing many operations at the same time  
	• Requires:  
		• Identifying safe-to-parallelize tasks  
		• Executing them concurrently using available resources

Not all problems parallelization is possible, and therefore we need to identify the aspects of solving a problem where we can use it. This also means it;s not always safe to parallelize. 

• Definition:  
	• Parallel computing is the practice of:  
		• Identifying & exposing parallelism in algorithms  
		• Expressing it clearly in software  
		• Understanding costs, benefits, and limitations of implementation

**Parallelism in Algorithms**
• *Algorithms* -> step-by-step instructions to solve a problem  
• Some steps are inherently serial (must follow order)  
• But many tasks can run in parallel if no dependencies exist  
• Key Idea->  
	• Exposing parallelism helps scale performance, but trade-offs exist in  
	efficiency, cost, and complexity

One of the most critical issues in parallel computing is *communication*. 
- We need to ensure that all processing synchronizes at the end. 
- Suppose we have a set of cores that are summing numbers, and the numbers are divided individually among the cores. The cores need some way to communicate their sums in the end. 

Modern Hardware is Parallel:
![[Pasted image 20250922190358.png]]
Consumer devices are multi-core *CPUs* and *GPUs*.
They also support **hyperthreading**:
- Hardware can identify when parallelism is possible with a process. 
- Hyperthreading allows more than one thread to run a task. 
1 physical core -> 2 virtual threads  
(via instruction interleaving)

![[Pasted image 20250922190612.png]]
![[Pasted image 20250922190619.png]]
**Vector Units**: wide execution of multiple instructions (e.g. 256-bit -> 4 doubles or 8 floats at once)![[Pasted image 20250922190710.png]]
The compiler for our smaller programs can recognize when certain processes can be parallel.
*Vectorization*: When we are summing 4 vectors for example, this instruction can run in one clock cycle if vectorization is available. 

**Serial Code Wastes Modern CPU Power**
• Example: 16-core CPU with:  
	• 2 hyperthreads/core  
	• 256-bit vector unit
Parallelism capacity: $$16 \times 2 \times \frac{256 \space bits}{64 \space bits} = 128 \space ways$$ Serial usage: $$= \frac{1}{128} = 0.8\%$$
A serial program only taps 0.8% of CPU’s potential!

**Instead, we save energy with Parallelism**
![[Pasted image 20250922191510.png]]
We can also *reduce monetary costs*:
• Power costs are rising->often exceed hardware cost  
• Cloud billing -> time × resources  
• GPU acceleration can cut both runtime and total cost  
• Effective parallelism -> cost savings in both cloud and on-premise systems

**Cautions in Parallel Computing**
• Not all applications need or benefit from parallelism  
• Some may lack enough inherent parallelism  
• Transitioning to parallel can divert focus from core goals  
• Always ensure the application *works correctly* first





