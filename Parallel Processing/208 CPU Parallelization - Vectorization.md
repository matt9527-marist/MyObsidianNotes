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
![[Pasted image 20251103202518.png]]**Vectorization Methods**  
**(Least to Most Effort)**  
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

**Optimized Libraries for Easy Vectorization**
• Least-effort vectorization method:  
	• Use pre-built, highly optimized libraries  
	• Offers excellent performance with minimal coding  
• Common Libraries:  
	• BLAS – Basic Linear Algebra Subprograms  
	• LAPACK – Linear algebra computations  
	• SCALAPACK – Scalable version of LAPACK  
	• FFT Libraries – Fast Fourier Transform implementations  
	• Sparse Solvers – Specialized for sparse matrices

**Example: Intel® Math Kernel Library (MKL)**
• Optimized BLAS, LAPACK, SCALAPACK, FFT, sparse solvers  
• Free to use; tuned for Intel CPUs  
• Available in both commercial and open distributions

**Auto-Vectorization – Easy SIMD Speedup**
• Auto-vectorization = automatic vectorization by the compiler from  
standard C/C++/Fortran source code

**Why Use It?**
• Minimal effort for significant speedup  
• Compiler handles SIMD instruction generation  
• Improves with newer compilers and CPUs  
• Example Use Case:  
	• STREAM Triad loop — auto-vectorized for performance  
	(From STREAM Benchmark, Section 3.2.4)

• Make Your Code Vector-Friendly:  
	• Use restrict in C or `__restrict, __restrict__` in C++  
	• Avoid complex control flow in loops  
	• Use simple, stride-1 loops over arrays  
• Enable with compiler flags (e.g., -O3, -ftree-vectorize, /O2)  
• Check compiler reports to confirm vectorization  
• Auto-vectorization is the recommended starting point for SIMD — just write clean  
loops and let the compiler do the rest!

**STREAM Triad Loop - Auto-vectorized for performance**
![[Pasted image 20251103203034.png]]

**Optimizing Vector Width in GCC**
• GCC 8.2 defaults to 256-bit vectors on Skylake  
	• Use flag -mprefer-vector-width=512 to force 512-bit AVX512  
• Before flag:  
	• 256B ops: 640M, 512B ops: 0  
• After flag:  
	• 256B ops: 0, 512B ops: 320M  
• Example:  
	• Function with stream triad loop is auto-vectorized when compiled properly.

Verify with *Likwid*
• likwid-perfctr -C 0 -f -g MEM_DP ./stream_triad  
• Key output:  
	• 256B vector ops: 640,000,000  
	• 512B vector ops: 0

**What Is Aliasing?**
• Aliasing occurs when two or more pointers refer to overlapping memory  
• Prevents the compiler from safely optimizing or vectorizing code  
```c++
void example(double *a, double *b) {  
	a[0] = b[0] + 1; // If a and b alias, reordering or vectorizing is unsafe 
}
```
• Compiler can't assume a[0] and b[0] are separate  
• Disables aggressive optimizations like loop vectorization  
• Solution: Use restrict if you guarantee no aliasing  
• void example(double * restrict a, double * restrict b);

Use with compiler optimizations:
• -fstrict-aliasing: assumes no aliasing between pointers  
• Default in -O2 and -O3 optimizations  
• Caused issues with legacy code relying on aliasing  
• Fewer function versions are generated due to compiler caution. Compilers now optimize more conservatively  
• Use both:  
	• restrict keyword: portable aliasing promise to the compiler  
	• -fstrict-aliasing: enforces this behavior in compilation  
• Note: Compiler behavior varies with versions  
• Programmer hints are often needed for complex loop vectorization

We can try all of the possible optimization flags if we find that we are not vectorizing. 
