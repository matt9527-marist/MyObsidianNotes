**Targeting Performance: Where to Focus Developer Effort**
• Goal: Use developer time where it brings the most performance gain  
	• Requires understanding:  
• Limiting aspect of performance  
	• E.g., memory bandwidth, CPU flops, I/O  
• Hardware capabilities  
	• Measure theoretical & achievable limits  
• Application’s current performance  
	• Use profiling tools to identify bottlenecks  
• Without this knowledge, optimization efforts may miss the mark

## Knowing our application's potential performance limits 
• Most apps are limited by bandwidth or latency  
	• *Speeds -> Rate of operations (e.g., flops)*  
	• Feeds -> Data delivery (memory, network, disk)  
• Memory Latency vs. Bandwidth  
	• Latency -> time to fetch first byte  
	• *Bandwidth -> rate for streaming data*  
• Efficient use: access contiguous data to stay in cache  
	• Possible performance limits:  
	*• Flops / All Ops (arithmetic & logic)*  
	*• Memory bandwidth/latency*  
		We will be mostly concerning ourselves with FLOPs and memory bandwidth in this course. We will also be concerned with memory and compute bounding. 
	• Instruction cache  
	• Network bandwidth/latency  
	• Disk bandwidth/latency  
• Good programming can shift an app from latency-bound to bandwidth-bound

Example Roofline Plot for a given system:
![[Pasted image 20250929202035.png]]
This tool works on Linux, but can be iffy on Windows/Mac, mostly because profiling to this level concerns supercomputers and servers, which all run Linux. 

**Computation Speed vs. Memory Access**
• Modern CPUs are fast at flops, helped by cache layers  
• L1 cache is fastest but very small (~32 KiB)  
• Large data (ML, scientific computing) lives in slower DRAM or disk  
• *CPUs often wait on memory* — not flops
• Most apps: ~1 flop per word loaded  
• Some apps: much higher arithmetic intensity

**High-AI Example: Dense Matrix Solvers**
To solve a dense matrix, you need to solve a system of equations.
• Solve systems of equations  
• Classic case: *Linpack benchmark*  
• Linpack AI: 62.5 flops/word (Peise, 2017, p. 201, appendix)  
	• High enough to saturate most CPUs  
• Impact on System Design  
	• Linpack drives Top 500 supercomputer rankings  
	• Leads to designs optimized for high flop/memory ratios

Efficient memory access therefore matters a lot. 
	• CPU uses a memory hierarchy: cache -> DRAM  
	• Data is loaded in cache lines (usually 64 bytes)  
	• Wasted cache if memory access is *non-contiguous*
If memory is not in L1 cache, the program will be faster.

Example: 2D Array Access
• Row-major storage: rows next to each other in memory  
• Column access -> strided pattern  
• Loads full cache line but uses 1 of 8 values  
• Results in low memory efficiency  

**I/O Limits & Application Bottlenecks**
• Network & disk can dominate performance in:  
• Big data, distributed computing, message passing  
• Rule of thumb:  
	• Time for 1st network byte ≈ 1,000 flops  
	• Mechanical disks are even slower  
• This reinforces the idea that in modern systems, *data access* —> not  
computation —> is usually the *bottleneck*.  
I/O Limits & Application Bottlenecks

## Benchmarking to determine hardware capabilities 
**Characterizing Hardware Performance**
• After setup, begin analyzing target hardware  
• Build a conceptual model to estimate peak performance  
• Core Metrics  
	• FLOPs/s – Floating-point compute rate  
	• GB/s – Data transfer speed across memory levels  
	• Watts – Energy consumption rate  
• Why It Matters  
	• Helps estimate theoretical performance limits  
	• Focus depends on your app's performance goals
Example: *Hardware Inspection Tool*: *lstopo* (via hwloc)
• Visual/text system layout  
	• Full graphics needs:  
		• hwloc + cairo with X11  
• Other CLI tools:  
	• Linux: lscpu, /proc/cpuinfo, lspci  
	• Windows: wmic  
	• macOS: sysctl, system_profile
System Profile Inspection Example:
![[Pasted image 20250929204606.png]]

**Memory Inspection Tool**
![[Pasted image 20250929204658.png]]

• *lscpu*  
	• A command-line utility (part of util-linux) that displays basic CPU information.  
	• Uses /proc/cpuinfo and sysfs to report architecture, core counts, threads, etc.  
• *hwloc*  
	• A library + toolset to programmatically query and manipulate system topology (CPU cores,  
	sockets, NUMA nodes, caches, I/O devices).  
	• lstopo is a tool provided by hwloc to visualize this hierarchy.  
• *cairo*  
	• A 2D graphics library. Often used by hwloc to render graphical topologies via lstopo.

**Theoretical FLOP Rate** for a given system:
$$F_{T} = C_{v} \times f_{c} \times I_{c}$$
Where C_v = Virtual Cores
f_c: Clock Rate
I_c Flops/Cycle
$$I_{c} = \frac{VW}{W_{bits}} \times Fops $$
VW = Vector width = 256 bits 
W_bits = word size 
Fops = Fused multiply-add (FMA) (typicall = 2)

![[Pasted image 20251006185303.png]]

**Memory Bandwidth and Hierarchy**
• Large arrays must load from main memory -> caches  
• Memory hierarchy deepens as CPU speeds outpace memory  
• Data moves in cache lines, reused at each cache level  
• Theoretical Memory Bandwidth
$$B_{T} = MTR \times M_{c} \times T_{W} \times N_{S}$$
- MTR: Data Transfer Rate (MT/s)
- M_c: Memory Channels 
- T_w: Bytes per transfer (8 bytes)
- N_s: Sockets (CPUs)

**Measuring Memory Bandwidth Empirically**
• Two Key Methods:  
	• STREAM Benchmark  
		• Created by John McCalpin (1995)  
		• Emphasizes memory bandwidth -> peak flops  
	• Empirical Roofline Toolkit  
		• From LBNL (Lawrence Berkeley National Laboratory)  
		• Plots memory bandwidth + flop rate in one model
![[Pasted image 20251006190241.png]]

**Stream Benchmark**
![[Pasted image 20251006190931.png]]
• Measures time to read/write large arrays  
• Four variants:  
	• Copy – no floating-point  
	• Scale, Add – 1 flop  
	• Triad – 2 flops  
	• Shows max bandwidth when data is used only once  
• Insight  
	• In STREAM regime, flop rate is bounded by memory speed  
	• Roofline plots help visualize bottlenecks and ceilings

