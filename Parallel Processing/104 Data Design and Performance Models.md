**Performance is about Data**
• Performance models — ways to predict how fast your code runs.  
• Data structure and layout — how your data is arranged in memory.  
	• Even though code seems like the heart of programming, for  
	performance, the most important part is how data is organized and  
	accessed.

**Why Data Layout Matters**
• The way you store data decides how fast your code runs.  
• This is because data movement (memory bandwidth) is now the main  
bottleneck, not computation (flops).  
• If your code is slow, it’s probably spending time waiting on data, not doing  
math.

**Data-Oriented Design (DoD)**
• Think about data usage patterns first  
• Organize data to fit those patterns  
• Prioritize:  
	• Memory bandwidth  
	• Cache efficiency  
	• Operations on data already in cache  
• Steps:  
	• Estimate performance  
	• Predict whether a code change is worth it  
	• Identify bottlenecks