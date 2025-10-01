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
They also support **hyperthreading**: #hyperthreading
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

**Plan Before Parallelizing**
How much speedup we get depends on how many cores we can use to solve the problem. 
• Begin with a clear plan  
• Evaluate:  
	• Available acceleration options  
	• Effort vs. potential payoff (speed, cost, energy, scalability)  
	• Assess if the investment is worthwhile  
• Key Advice:  
	• Make sound decisions before diving into parallel implementation

## Fundamental Laws of Parallel Computing 
**Amdahl's Law** #AmdahlsLaw
![[Pasted image 20250922192114.png]]
• #Speedup limited by serial portion of code  
• Applies to fixed-size problems (strong scaling)  
$$Speedup = \frac{1}{S + \frac{P}{N}}$$ where P + S = 1 or (100%)
(S: Serial function, P: Parallel function, N: Number of processors)
• Key Insight:  
	• Even with many processors, serial code limits total speedup  
This is called strong scaling, which takes a singular problem and continuously adds processors to make speedup.

**Gustafson-Barsis’s Law** #Gustafson-Barsis
![[Pasted image 20250922192606.png]]
• Increase problem size with *processor count*  
• More realistic for real-world applications
$$Speedup = N - S \times (N - 1)$$
(S: Serial function, N: Number of processors)

Solves larger problems in the same time .
This is weak scaling. 

**Strong vs. Weak Scaling**
![[Pasted image 20250922192809.png]]
![[Pasted image 20250922192833.png]]

**Replicated vs. Distributed Arrays**
![[Pasted image 20250922193321.png]]
With the distributed approach, we grow farther, but it is not preferred for all situations. 

## How Parallel Computing Works 
**Sample Application** - Suppose we need to simulate volcano eruption or tsunami forecasting. 
• A common strategy in parallel computing  
• Applies the same operation to many data elements  
• Example domain: 2D spatial mesh  
• Steps:  
	• Discretize the problem -> break into 2D grid cells  
	• Define *kernel* -> operation for each cell  
	• Apply parallel layers for acceleration

**Real-World Example: Krakatau Simulation**
• Input: 2D image of Krakatau volcano  
![[Pasted image 20250922193813.png]]
	• Possible applications:  
	• Volcanic plume modeling  
	• Tsunami simulation  
	• Machine learning for early eruption detection  
• Why Parallelism?  
	• Achieve real-time results for faster, data-driven decisions

**Step-by-Step Parallelization Strategy**
*Step 1: Discretize the Problem*: 
• Divide domain into 2D grid of cells/elements  
![[Pasted image 20250922194511.png]]
• Forms a computational mesh  
• Each cell holds values like wave height, velocity, eruption debris mass, or color
We want to do computations on each of these cells. 
*Step 2: Define the Computational Kernel*:
Use a **stencil** operation:  
	• Applies a pattern (e.g., 5-point cross) to  
	update each cell  
	![[Pasted image 20250922194438.png]]
	Q: Will there be any communication between the processors above? 
	- Each red dot (a grid point being updated) depends on the values of its neighbors: left, right, up, down, and itself.
    - In parallel execution (e.g., domain decomposition across processors), the values at the boundaries of each processor’s subdomain must be communicated to neighboring processors, because they are required for the update.
• Example:  
	• Apply a blur separately to R, G, B channels  
	of an image
*Step 3: Vectorization*:
Perform multiple operations in one clock cycle  
(when available)
• Example:  
	• 256-bit vector unit = 4 doubles per instruction  
	• Achieves speedup with low energy cost
![[Pasted image 20250922194454.png]]
*Step 4 – Thread-Based Parallelization*
• Utilize multiple CPU cores via threads  
- Recall thread memory is shared, and process memory is individual. 
- If the memory is shared among threads, we can spawn 4 threads, each adding 4 units. 
![[Pasted image 20250922194643.png]]
• Example:  
	• 4 cores process 4 rows of the mesh simultaneously
OR
*Step 5 – Process-Based Parallelization*
![[Pasted image 20250922194732.png]]
• Distribute computation across separate memory spaces  
• Used across nodes in a cluster  
• Example:  
	• 2 desktops × 4 cores × 4-wide vector = 32x speedup  
• Cluster Example:  
	• 16 nodes × 36 cores × 8-wide vector = 4,608x speedup
*Step 6 – GPU Offloading*
• Divide work into tiles (e.g., 8×8 blocks)  
![[Pasted image 20250922195115.png]]
• Leverage thousands of GPU cores (e.g., NVIDIA Volta)  
• Example:  
	• 1 GPU -> 32x84=2,688 double-precision cores  
	• 16 GPUs -> 43,008-way parallelism  

Notes:
Theoretical speedup is rarely achieved in full  
	• Success depends on how well layers are organized and combined  
	• Key Takeaway:  
		• Mastering parallel strategies requires both hardware awareness and  
		software design skill

![[Pasted image 20250922200414.png]]
S = 1 / (S+ P/N).
N can be any number in this case. Assume 1 / S, and if S = 0.05, then the answer here is 20x, and no more. 

**Distributed Memory Architecture**
![[Pasted image 20250922200544.png]]
• Distributed Memory Architecture  
	• Each CPU has its own *DRAM*  
	• Nodes are connected by a communication network  
	• Used in clusters and supercomputers  
• Advantages:  
	• Scales well->just add more nodes  
	• Clear memory locality (on-node vs. off-node access)  
• Disadvantages:  
	• Programmer must *manually partition* memory  
	• Explicitly manage cross-node communication

Suppose have the computational kernel taking averages across the unit. 

**Shared Memory Architecture**
![[Pasted image 20250922201508.png]]
• Multiple CPUs or cores share the same memory space  
• Easier programming: single address space  
• Used in multi-core CPUs or multi-CPU systems
- All communication here will be shared. We need to take care with our programming to ensure that ONLY one thread is writing at a time. If more than one thread writes at the same time, this is where errors occur. 
*Pros and Cons of Shared Memory*
• Advantages:  
	• Simplified memory access (no explicit partitioning)  
	• Good for within-node parallelization  
• Disadvantages:  
	• Memory conflicts possible  
	• Synchronization is complex and costly  
	• **Limited scalability**: More cores ≠ more memory  
• Performance degrades with increased contention  
• Conclusion:  
	• Ideal for small-scale parallelism within a node, but not for scaling across many nodes.

**Why Not Just Increase Clock Speed?**
Vectorization in one clock cycle, we can increase the number of operations, so why not increase the clock speed? Why not run more cycles? 
We will reach a power wall:
*• Higher clock -> more power + more heat*  
• Power wall: physical limits on power and cooling  
	• Affects supercomputers and mobile devices alike  
• Leads to diminishing returns with higher frequencies

Vectorization as the Solution:
- Simply, 4 additions in 1. 
- Instead of increasing the speed of one lane, we just have 4 lanes. 
Vectorization -> perform multiple operations per clock  
cycle  
• More efficient than increasing clock speed  
• Reduces execution time with little extra power  
• Like a 4-lane freeway vs. a single-lane road  
• 256-bit vector unit -> 4 lanes, each lane operates on one  
64-bit double simultaneously

**What Is an Accelerator Device?**
![[Pasted image 20250922202123.png]]
- Discrete GPUs means that there is one bus (PCI) connecting the GPU and CPU. When running on discrete GPU, we need to send data over throug this bus.  
• GPU Structure:  
	• Composed of many small cores called Streaming Multiprocessors (SMs)  
	• SMs are simpler than CPU cores but enable massive parallelism  
	• Specialized hardware for fast execution of specific tasks  
	• Most common: GPU (Graphics Processing Unit)  
	• When used for computation: GPGPU (General-Purpose GPU)
General Heterogeneous Parallel Architecture Model
![[Pasted image 20250922202347.png]]
• Integrated GPUs: lower power, part of CPU  
• Discrete GPUs: higher performance, connected via PCI  
• Cache memory: fast, close to the core (details in Chapter 3)  
• Heterogeneous components -> greater parallel opportunities

*Why this model matters*: we need the right parallel strategy:
• Where computation should run  
• What memory regions to use  
• How to minimize data transfer costs  
• Choosing the right parallel strategy depends on understanding your  
hardware layout and memory hierarchy.

**Process-Based Parallelization**
• Used in distributed memory systems  
• App spawns independent processes (ranks)  
• Each process has:  
	• Its own memory space  
	• Independent instruction stream  
	• Processes handed to OS -> mapped to processors  
	• User space -> Application code runs  
	• Kernel space:->Protected OS operations  
• Explicit messaging is used to move data between processes across nodes.![[Pasted image 20250922203130.png]]
*Processes vs. Processing Cores*
• You can *spawn more processes than cores*  
• OS schedules processes to run on available cores  
• Example: 8 processes on a 4-core laptop -> cores time-share
- Programs will show the best output when `P` processes = `N` cores.

**Message Passing with MPI**
• Processes don’t share memory -> must communicate explicitly  
• **MPI (Message Passing Interface):**  #MPI
	• Became the standard in 1992  
	• Dominates in multi-node parallel applications  
	• Many implementations exist (e.g., OpenMPI, MPICH)  
• Process-based parallelism needs both explicit data movement and awareness of  
how processes are mapped to cores.

**Distributed vs. Parallel Computing**
We will be doing parallel computing on our laptops, which feature multi-core configurations. We will be doing multi-core processing, where each process runs on a core, having its own memory. 
When accessing webpages, however, it will involve distributed computing over a network (or over a set of supercomputers)
• Parallel Computing:  
	• Multiple tasks run simultaneously to solve a problem  
• Distributed Computing:  
	• A type of parallel computing using loosely coupled processes  
	that communicate via OS-level calls
![[Pasted image 20250922203757.png]]
Note: MPI framework is also distributed, but it specifically deals with parallel computing. 
- Distributed means many nodes are out there. 
	- If connected via internal network, it is parallel computing. 
	- If connected over the Internet (HTTP), it is distributed computing. 

**Threading Systems Overview**
• Thread types:  
	• Heavyweight (managed by OS)  
	• Lightweight (managed in user space)  
• Threading tools:  
	• OpenMP (C/C++/Fortran)  
	• pthreads, Intel® oneAPI Threading Building Blocks (TBB), others  
• Threading is a powerful tool for intra-node parallelism, but it requires careful  
design to avoid bugs and maximize performance.

**Thread-Based Parallelization**
• Spawns *multiple instruction pointers* within the same  
process  
• Threads share memory space -> efficient  
communication  
• Used for parallelism within a single node
![[Pasted image 20250922204204.png]]
GPUs also use thread-based frameworks. We will be mostly using thread-based frameworks. 
*Advantages & Challenges of Threads*
• Advantages:  
	• Low overhead for sharing data  
	• Efficient for modest speedup on multi-core CPUs  
	• Supported by libraries like OpenMP  
• Challenges:  
	• Programmer must ensure correctness (no *data races*)  
	• Memory access conflicts affect performance  
	• Limited by single-node memory

**Vectorization: SIMD Parallelism**
• #SIMD -> Single Instruction, Multiple Data  
	• Executes the same operation on multiple data points at once  
	• Key principle in machine learning with GPUs
	• Typical vector width: 2–16 elements per instruction  
• Why Use It?  
	• More cost-effective than adding cores/nodes  
	• Essential on power-constrained devices (e.g., phones)
*Key Considerations for Vectorization:*
• Vectorization is a lightweight, high-reward form of parallelism—especially useful when  
power or hardware is limited.  
We need to give the compiler the relevant flags for when we want to use vectorization. It can vary depending on the compiler, and whether or not vectorization is possible. 
• Pros:  
	• Efficient for numerical workloads  
	• Reduces loop overhead  
	• Saves energy through faster execution  
• Cons:  
	• Dependent on compiler capabilities  
	• Requires specific flags for full performance
![[Pasted image 20250922204640.png]]

**Offloading to the GPU**
• Data & compute kernel sent over PCI bus to GPU  
• GPU uses Streaming Multiprocessors (SMs) for parallel processing  
• Output is returned to CPU for further use (e.g., file I/O)  
• Figure : shows data offload, GPU execution, and return path
*Stream Processing Pros & Cons*
• Advantages:  
	• High throughput on parallel data  
	• Lower power use vs. general CPUs  
	• Ideal for large, regular workloads (e.g., images, meshes)  
• Limitations:  
	• GPUs have restricted functionality compared to CPUs  
	• PCI transfer cost can be significant  
	• Not suited for all types of computation  
• When used correctly, stream processing—>especially with GPUs—>offers massive speedup for  
structured, data-parallel tasks.

## Categorizing Parallel Approaches 
**Flynn's Taxonomy of Parallel Architectures**
![[Pasted image 20250922205025.png]]
**Variants of SIMD**
• *SIMD* -> One instruction, multiple data items  
	• Example: Vector units processing 4 or 8 values at once  
	• Vectorization
• *SIMT* -> Single instruction, multiple threads  
	• Common in GPU workgroups  
	• Same thing but in a GPU environment 
• Challenge:  
	• Conditionals complicate SIMD/SIMT  
	• All threads must follow the same instruction path  
• *MISD*-> redundant computation on the same data-> Fault-tolerant systems

**MIMD – The Dominant Model**
• Multiple instructions across multiple data streams  
• Describes:  
	*• Multi-core CPUs*  
	*• Distributed clusters*  
	• Supports independent thread/process execution  
• Flynn’s Taxonomy helps identify parallelism patterns and choose  
architectures suited to specific algorithm structures.
![[Pasted image 20250929185309.png]]

## Parallel Strategies 
**Task Parallelism Approaches**
• Focuses on different tasks, not just data split  
• **Main–Worker Model**  
	• One controller assigns tasks to worker threads/processes  
	• Workers fetch next task after completion  
	Thread-based and process-based
• **Pipeline Parallelism**  
	• Data flows through stages (like an assembly line)  
	• Used in superscalar processors for parallel instruction execution  
	Serial-kind of machine, recall organization and architecture
• **Bucket-Brigade**  
	• Each processor transforms data in sequence  
	• Output of one becomes input for the next

**Data Parallelism – The Most Common Strategy**  
• Each process/thread operates on a subset of data  
• All execute the same program logic  
• Works well for-> Cells, Pixels, Particles, Objects  
	Example could be using machine learning to determine if an image is a cat or a dog. 
• Advantages:  
	• Scales efficiently with problem size and processor count  
	• Simple and consistent to implement  
• Each worker handles a partitioned block of data

## Speedup Metrics 
Comparing weak vs. strong speedup. 
• **Parallel Speedup**  
	• Also called serial-to-parallel speedup  
	• Compares parallel run to a serial baseline (e.g., 1 CPU core)  
	• Shows *benefit of parallelization*  
• **Comparative Speedup**  
	• Compares two parallel implementations  
	• Example: MPI on CPU vs. CUDA on GPU  
	• Used to *compare architectures or technologies*