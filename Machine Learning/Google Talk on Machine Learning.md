## Where does knowledge come from?
4 forms of knowledge discovery:
1) Evolution
2) Experience
3) Culture
4) Computers
Each form of knowledge discovery is orders of magnitude faster than the previous, discovering orders of magnitude more knowledge. 

Most of the knowledge in the world in the future may be extracted by machines.

**How do computers discover new knowledge?**
1) Filling gaps in existing knowledge
	- We make observations and then find ways to adapt them and explain them
2) Simulating the brain
3) Simulating evolution
	- By some standards, evolution is even greater learning algorithm 
4) Systematically reduce uncertainty
	- Realize that all knowledge learned is necessarily uncertain.
5) Reason by analogy
	- Transfer situations that we know to situations we are faced with

Five Tribes of Machine Learning:
![[Pasted image 20250826170819.png]]
Each of these master algorithms has a mathematical proof claiming that, given enough data, the machine can learn anything. 

### Symbolists
Think of learning as being the inverse of deduction. Learning is *induction* of knowledge. *Deduction* is going from general rules to specific facts. 
In this same manner, we can approach this idea with mathematics, in the same way that subtraction is the inverse of addition. 

![[Pasted image 20250826171044.png]]
Of course, we will use many more examples than just one data point (Socrates).
Also, this is in English, but we can extend this principle to logic or other natural languages. 
This is the closest to the studies of computer scientists. 

### Connectionists 
Simulating the brain, founded ideas with neuroscience. 

Build a mathematical model of how a single neuron works. The strength of human learning is encoded in the synpases between the neurons. 

With artificial neurons, we will use a weighted combination of inputs. Depending on how strong the synpase is for that input, the neuron will "fire" as 1, and otherwise it will be 0.

What problem is there here? Suppose we have a very large, messy network. Think of one neuron in one area of the network leading to a network. This is the **Error-Assignment Problem**

This is solved using **Backpropagation**

Consider the difference between the actual output and our desired output. How do we know what to tweak in the weights to reduce the cumulative error. 
To do this *we compute the derivative of each neuron going backwards in the network to the input*. We are propagating back the errors and then progressively changing the weights to get the desired output. 

### Evolutionaries 
If we want to learn very powerful things, we want to understand evolution and apply it to the computer. 
This is **Genetic Algorithms**

Consider a population of individuals, each of which is described by its **genome**. In the computer this will be base pairs, 0 and 1. Each individual will go out in the world and be evaluated in the task that it is meant to complete. Individuals that do better will have a higher fitness and have a higher chance at being parents of the next generation. 

We will have random mutation on the base pairs. 

Once we have enough generations of this, the machine can be observed to perform certain tasks a lot better. 

### Bayesians
Root computer learning in statistics. Everything that we learn is uncertain, so we have to compute the probability of each one of our hypotheses and update it as new evidence comes on. 

**Bayes' Theorem**
$$
P(A|B) = \frac{P(B|A) P(A)}{P(B)}
$$
How does this work?
![[Pasted image 20250826175852.png]]
Suppose we have all of our hypotheses.
1) We have a prior probability - how much we beli