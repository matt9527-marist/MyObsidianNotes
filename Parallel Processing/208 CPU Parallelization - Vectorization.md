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