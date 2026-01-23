## Biological Neuron vs. Artificial Network 
![[Pasted image 20260122190546.png]]
Simplest element of artifical neural network is the *artificial neuron*, mathematically represented as a signal (inputs) into a specific function generating an output. 

> Perceptron - mathematical model of neurons in our mind. The most basic element in deep artificial neural networks 

![[Pasted image 20260122193847.png]]

AI is a large umbrella term. The hardware of AI includes machine learning, which is the "brain" that drives the AI. 
Deep Learning is a part of "representative learning" which attempts to learn from raw data. 

**Terminology**
AI definitions: (by the "fathers of AI")
1) John McCarthy: It is the science and engineering of making intelligent machines, especially *intelligent computer programs*. It is related to the similar task of *using computers to understand human intelligence*, but AI does not have to confine itself to methods that are biologically observable.
2) "Can machines think?" - defined by a question, offered by the famous *Turing Test*. 
	- Turing Test: Can the human, through sending and receiving messages from the robot, be convinced that the robot is human? 
3) We have 4 different definitions and goals for AI based on what we want to do:
	- Human Approach:
		- System that thinks like human 
		- System that acts like human 
	- Ideal approach: 
		- Systems that think rationally 
		- Systems that act rationally 
			- Why differentiate? For some tasks, we cannot define, clear-cut rational rules to provide the answer? For example, determine cat vs. dog given an image, and separate them. Such a simple task is still impossible to define a set of permanent rules for. The ideal approach may not be feasible, so we must go with the human approach. Then again, some tasks require a rational approach (factoring numbers)

## Early Successes of AI 
- IBM's Deep Blue chess-playing system defeated world champions in 1997. 
- Relatively sterile and formal environment- nothing they did not expect, a controlled environment. 
- Have to sought hard-code knowledge about the world in formal languages. 
	- A formal language is a set of strings of symbols drawn from a fnite alphabet in automata theory. 
	- Easier for a computer to understand, hard for a human to understand 
	- *Formal Language* is the understandable in-between, usually math and logic. 
	- *Hard-coding* means embedding data directly into the source code of the program as opposed to obtaining he data from external sources or generating it at runtime. If our chess opponent plays a certain position C11, for example, the system will play D11, placing action and effect together. 
- Abstract and formal tasks are among the hardest for humans to solve, but the among the easiest for computers to solve. 

![[Pasted image 20260122195918.png]]

## Why Machine Learning? 
• Moving from hard-coded knowledge to acquiring knowledge from raw data
• Accessing subjective and intuitive knowledge that are hard or impossible to
explain in formal language
• Capturing patterns through big, diverse, noisy, and missing data
![[Pasted image 20260122200329.png]]

**Definition for Machine Learning**
Arthur L. Samuel "Father of Machine Learning":
- Machine learning is the field of study that gives computers the ability to learn *without being explicitly programmed*.
Tom M. Mitchell
- *A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P if its performance at tasks in T, as measured by P, improves with experience E.*
- Experience E is basically data. Tasks T represent whatever objective we want with the data. Performance P can be measured in different ways (recall cost function/reward-punishments). Most deep learning algorithms will improve with more experience. 

**Types of Machine Learning Tasks:**
![[Pasted image 20260122201208.png]]

**Supervised Learning**

