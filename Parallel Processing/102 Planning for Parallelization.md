**Approaching a New Project Preparation**:
• Prepare application and team  
• Profile and benchmark  
	What do we mean by benchmark?
	We are roofline plotting a system according to its maximum hardware capabilities. When we are benchmarking, we are testing a parallel application's performance against this roofline plot. 
• Parallelize key kernels  
• Test for correctness and portability  
• Commit changes and repeat

**Test for Correctness and Portability**
*Acceptable Variations in Simulation Results*
• Output differences may be caused by:  
	• Compiler or compiler version changes  
	• Hardware differences  
	• Compiler optimizations  
	• Order of operations (especially with parallelism)  
• Determining acceptability:  
	• Requires context and validation data  
	• Need to know what is within the expected tolerance  
• Challenge:  
	• Hard to judge correctness without additional information
Serial and Parallel output needs to both be correct, needs to both be the same. 
In order to ensure that it is correct, we may use Main-Worker thread setup and choose some method of communication. 

**Importance of Test Suites in Simulation Applications**
• Test suite: Set of problems that verify code integrity after changes  
• Essential for all but the simplest codebases  
• Ensures results remain consistent after modifications  
• Results may vary by compiler or processor count
*Example*: Krakatau Ocean Wave Simulation 
Validated results: Match real-world or experimental data  
• Used GCC (open-source) and Intel C (commercial) compilers  
• Parallelization introduced slight variations in:  
• Predicted wave height  
• Total mass

In the GCC Compiler, there is a tool called *GCoverage*, or `gcov`, which can help generate coverage statistics. 
**Code Coverage** - We have a test case. While executing the program, code coverages measure how many lines of the code actually executed? 
• Measure how much of your program’s code is actually run when you  
execute your test suite  
• Expressed as a percentage of lines tested vs total lines in the source  
code  
• The *more coverage* you have, the more confident you can be that  
your code is tested  
• 100% coverage doesn’t guarantee bug-free code—it just means all  
lines were executed at least once

**Understanding the Different Kinds of Code Tests**
• Use multiple test types together for strong coverage especially critical for parallel applications  
• Types of tests:  
	• *Regression Tests*  
		• Catch regressions by running nightly/weekly (e.g., via cron)  
	• *Unit Tests*  
		• Check individual functions/subroutines during development  
	• *Continuous Integration (CI) Tests*  
		• Run automatically on commits  
		• Common in modern workflows  
	• *Commit Tests*  
		• Fast, local tests run before committing changes

**Unit Tests & test-driven development (TDD)**
• Create unit tests during code development  
• TDD: Write tests first, then code to pass them  
• In parallel programming: test in both parallel language &  
implementation  
• Early problem detection = easier fixes  
• Example: In TDD, write a test for a function before implementing  
it

All of these tools help us to verify whether or not code is written correctly. 

**Fixing Memory Issues with Valgrind**
*Catches memory leakage*
• Parallelization exposes bugs like:  
	• Uninitialized memory -> unpredictable values  
	• Memory overwrites -> e.g., writing past array bounds  
• Use memory correctness tools:  
	• Valgrind (best with GCC)
Code example:
![[Pasted image 20250929194217.png]]![[Pasted image 20250929194250.png]]
• Valgrind reports the error when a decision was made with an  
uninitialized value  
• The error is actually on line 4, where iarray is set to ipos, which was  
not given a value  
• It can take careful analysis in a more complex program to determine  
the source of the error  
• Example  
	• Line 4: iarray = ipos (ipos uninitialized)
	• Also, the array is being initialized for a size of 10 ints, but we are trying to access i = 10, which is the 11th position. Invalid write size. 
	• We also need to use `free()`

**Improving Code Portability Across Compilers & Systems**  
• Portability -> Wider support for tools, compilers, and platforms  
• Compiling with multiple compilers reveals errors and edge-case issues  
• Why it matters:  
	• Tools have compiler preferences (e.g., Valgrind -> GCC, Intel Inspector  
	-> Intel)  
	• GPU language support varies:  
		• CUDA Fortran -> PGI only  
	• OpenACC/OpenMP (target) -> limited compiler support

## Profiling: Probing the gap between system capabilities and application performance 

**Profiling - Finding Performance Bottlenecks**
• Goal: Compare hardware capabilities with application performance  
• Gap = Potential for improvement  
• Profiling process:  
	• Identify the limiting factor in performance  
	• Often memory bandwidth  
	• Sometimes floating-point operations (FLOPS)  
	• Estimate theoretical performance limits (see Sec. 3.2)  
	• Use profiling tools (see Sec. 3.3) to measure actual performance  
• Outcome:  
	• Pinpoint bottlenecks for optimization  
	• Guides the parallelization strategy

## Planning: A foundation for success 
• Use gathered application and platform info to build a detailed  
plan  
• Explore:  
	• parallelism techniques  
	• Benchmarks and mini-apps: Offer both insight and source code  
		• Mini-apps combine research ideas with working code
Exploring with Benchmarks and Mini-Apps:
• Use to evaluate hardware and guide algorithm design  
• Benchmarks test specific hardware traits  
	• E.g., STREAM -> memory bandwidth  
	• High Performance Conjugate Gradient (HPCG) -> iterative  
	matrix solver as your kernel  
	• Mini-apps simulate common patterns in scientific apps  
		• Offer code examples, performance tuning, and porting  
		insights
We will be using the application **CloverLeaf** as an example for how to profile. 

**Algorithms Resdesigned for Parallel Execution**
• Assess algorithms for parallel suitability and scalability  
• Look beyond current runtime -> evaluate scaling trends  
• A small part (e.g., 5%) can grow to dominate with poor scaling  
• Research into parallel styles and algorithm alternatives  
	• Difficult routines may require new algorithms for efficiency

## Implementation 
**Turning Strategy into Parallel Code**
• Hands-on phase: transform code line-by-line, loop-by-loop  
• Initial direction depends on goals:  
	• Modest speedup ->Vectorization, OpenMP (Ch. 6–7)  
	• Need more memory -> Distributed memory (MPI, Ch. 8)  
	• Large speedup -> GPU programming (Ch. 9–13)  
• Break down work, collaborate, and iterate

**Commit** 
• Focus on quality checks, portability, and stability  
• Key actions:  
	• Tailor tests to the application’s scale and use  
	• Catch issues early, before they scale (e.g., on 1000+  
	processors)  
	• Team must agree on and follow a shared commit process  
	• Review and adapt the process as the project evolves  
	• Early detection beats deep-debugging long runs
- Potential Issues:
	• Example: Race Condition in Wave Simulation  
	• After adding OpenMP, app crashes intermittently  
	• Team suspects thread race conditions  
	• Adds race-checking step to the commit process

![[Pasted image 20250929201252.png]]
Step-by-step calculation:
1) The Grid Size is given: $$15660 \times 15660 = 245763600 \text{ cells}$$
2) Since each cell is a double = 8 bytes, one array $$245763600 \times 8 = 1,966,108,800 \text{ bytes} = 1.83 \text{ GiB}$$
3) Total memory accessed per iteration: $$25 \times 1.83 \times 2 = 91.5 \text{ GiB per iteration}$$
4) Bandwidth if one iteration takes 0.5s: $$\frac{91.5}{0.5} = 183 \text{ GiB/s}$$
