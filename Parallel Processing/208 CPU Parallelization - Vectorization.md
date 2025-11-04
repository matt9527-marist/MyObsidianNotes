**Vectorization and single instruction, multiple data (SIMD) overview**
• Vectorization means doing multiple operations at once, using special  
vector units inside the CPU (like SIMD – Single Instruction, Multiple Data).

**Why is Vectorization Important?**
• Modern CPUs have hardware (like AVX, SVE, NEON) that can operate on  
2, 4, 8 or more numbers in parallel.  
• This is faster than doing one number at a time.  
• To get peak performance, vectorization is often necessary.
**AVX (Advanced Vector Extensions) – Intel/AMD**
• Used on x86-64 processors.  
• Works on 128-bit, 256-bit, or 512-bit wide registers (AVX, AVX2, AVX-512).  
• Can process 4 or 8 doubles / 8 or 16 floats at once.  
• Very common in high-performance computing, scientific applications,  
image processing.
**SVE (Scalable Vector Extension) – ARM**
• Introduced by ARM for servers and HPC (used in processors like Fujitsu  
A64FX, Amazon Graviton3).  
• Vector length is variable: 128 to 2048 bits! (hence scalable).  
• Lets compilers generate portable code that works on different SVE CPUs.  
• Designed for performance + energy efficiency in vector workloads.
**NEON – ARM**
• Older and more common than SVE.  
• Found in smartphones, tablets, Raspberry Pi, etc.  
• Fixed width: 128 bits  
• Good for mobile multimedia, gaming, low-power SIMD tasks.

**SIMD Architecture in Parallel Computing**
• SIMD = Single Instruction, Multiple Data  
• Part of *Flynn’s Taxonomy* (Section 1.4)  
• One instruction operates on multiple data elements  
• Example:  
	• 1 vector add = 8 scalar adds  
	• Reduces pressure on instruction queue and cache  
• Power Efficiency:  
	• Performing 8 vector additions uses about the same power as 1 scalar addition
![[Pasted image 20251103201210.png]]

**Vectorization Terminology**
• Vector (SIMD) lane  
	• Path for one data element in a vector operation  
	• A 512-bit vector with 8 lanes for 8 double-precision values  
• Vector width  
	• Bit width of the vector unit  
	• 256-bit (AVX), 512-bit (AVX-512)  
• Vector length  
	• Number of elements processed at once  
	• 512-bit width -> 8 × 64-bit doubles or 16 × 32-bit floats  
• Vector (SIMD) instruction sets  
	• Instructions for parallel processing on vector units  
	• SSE, AVX, AVX2, AVX-512 (Intel); NEON (ARM)
**Vectorization Requirements & Best Practices**
• Vectorization involves both software and hardware:  
	• Generate Instructions  
	• By compiler, intrinsics, or assembly  
	• `#pragma omp simd` or Intel intrinsics like `_mm256_add_pd`  
• Match Instructions to Hardware  
	• New CPUs support older instructions  
	• But: old CPUs cannot run newer vector instructions (e.g., AVX fails on 10+ year-old chips)  
• No Automatic Scalar -> Vector Conversion  
	• Old compilers do not support the latest instruction sets  
	• Compiler support for new hardware often lags  
• Takeaway:  
	• Use the latest compiler version with current hardware

**Specifying Vector Instruction Sets**
• Default (safe): SSE2 -> 2 double ops at once  
• Better options for performance:  
	• Compile for current architecture  
	• Use AVX -> 256-bit  
	• Use AVX-512 -> 512-bit (modern Intel chips)  
	• Ask the compiler to emit multiple versions and pick at runtime  
• Takeaway  
	• Explicitly set compiler flags to target the most advanced instruction set your hardware  
	supports

## Hardware Trends for Vectorization 
**History of Vector Instruction Sets**  
• Vector units appeared in commodity CPUs ~1997  
• Over 20+ years:  
• Increased vector width  
• More operation types supported
![[Pasted image 20251103202508.png]]

**Vector Instruction Set Evolution**
![[Pasted image 20251103202518.png]]Vectorization Methods  
(Least to Most Effort)  
• 1. Optimized Libraries  
• Use pre-built, vectorized libraries (e.g., BLAS, Eigen, Intel MKL)  
• No code changes needed  
• . Auto-Vectorization  
• Let the compiler identify and apply SIMD automatically  
• Requires no explicit instructions  
• Compiler Hints (Pragmas)  
• Guide the compiler with directives like:  
	• `#pragma omp simd`  
	• `#pragma ivdep`  
• Minimal code changes  
• Vector Intrinsics  
• Use C/C++ functions that map directly to SIMD instructions  
• Example: mm256_add_pd() for AVX  
• Assembler Instructions  
• Manually write SIMD code in assembly language  
• Maximum control, but highest complexity