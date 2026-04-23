![[Pasted image 20260416192537.png|548]]
![[Pasted image 20260416192547.png|548]]

**New Problem**
What is *reinforcement learning*?
- This is such a large topic that it can be contained within its own course. 
- Examples: 
![[Pasted image 20260416192739.png]]
The game Go might appear simple, but considering all of the possible decision trees for a single game, it can be a massive task. 
- Reinforcement learning: when do we use it? *When we know the solution, but the decision space is very large*. We call this decision space a namespace. 
- It is not like supervised learning where a set of actions can be performed correctly and then the job is complete. This is a continuing sequence of actions, done in this case to win a game. 
- We also need reinforcement learning for games, robotics, and marketing. 

## Reinforcement Learning 
#ReinforcementLearning 
![[Pasted image 20260416193120.png]]

![[Pasted image 20260416193149.png|415]]
![[Pasted image 20260416193158.png|415]]![[Pasted image 20260416193213.png|414]]
![[Pasted image 20260416193225.png|414]]
![[Pasted image 20260416193248.png|416]]
![[Pasted image 20260416193304.png|418]]
*State* - current situation or observation of the environment 
*Action* - decision taken by the agent based on the state
*Observation* - what the agent observes from the environment to inform the next action 
*Reward* - what the agent receives from acting upon the environment (correctly), which the agent wants to maximize

**Introductory Example to RL**
![[Pasted image 20260416193523.png]]
By what policy do we make a decision? 
Many ways to think about it:
- One way is called *Discounted Return*, which is one policy we can follow:
$$R = \sum^{\inf}_{t = 0} \gamma^tr_{t} = r_{0} + \gamma r_{1} + \gamma^2r_{2}$$
- We must first understand the name of the space. 
- We do this in operational analysis through a **Q-Table**
![[Pasted image 20260416193848.png]]
What is a **Q-Table?**
- We have actions and the states. 
- Computes all of the situations. 
- "I am in x state and I have y possible actions. What's the best action to take from y?"
How do we select `gamma`?
What is the optimal Q value with consideration of discount return?
![[Pasted image 20260416194054.png]]

Now we have this Q-Table of possible actions to perform, but how do we choose the action? 
- Use the *Bellman Equation*. 
- If we go with this action, we will have the highest reward outcome. 

**Review So Far**
Variables:
- environment
- agent
- state 
- action 
- reward
- total return 
- discount factor 
Q-Table:
- matrix of entries 
- representing how good it is to take a certain action at a state `s`
Policy:
- Function that tells us what is the best strategy to adapt 
Bellman equation satisfied by the optimal Q-Table. 
(Why is Bellman the most optimal? Independent research question)

**Markov Decision Process**
- mathematical formulation of the RL problem 
- *Markov Property*: current state completely characterizes the state of the world. 
![[Pasted image 20260416194856.png|584]]

- At time step 0, the environment samples initial state `s0 ~ p(s0)` (we are not certain where we are)
- For `t=0` until done:
	- Agent selections action `a_t`
	- Environment samples reward `r_t ~ R(.|s_t, a_t)`
	- Environment samples next state `s_t+1 ~ P (.|s_t, a_t)`
	- Agent receives reward `r_t` and next state `s_t+1`
A policy `pi` is a function from S to A that specifies what action to take in each state. 
Objective: Find policy `pi` that maximizes cumulative discount reward: `sum(t>0) gamma^(t)r_t`

Through this problem, we have our Q-table telling us what actions are available for each state, and what rewards will result from those actions, and we have the Bellman equation telling us the best policy to have. 
One question: If we have such a small environment that we have only 5 stages with only 2 actions, as in the case with the recycling problem, we end up with Q-table that is 10 different states each time. Consider what happens when we have more states and more actions. This Q-table can expontentially explode. 

**Deep Q-Learning**
We want to find a Q-function to replace the Q-table.
![[Pasted image 20260416195415.png|549]]
Use a network to determine what the best action is. Have it learn the action that gives the most reward through backpropagation.
But how do we compute the loss?

![[Pasted image 20260416195517.png|605]]
![[Pasted image 20260416195701.png|605]]
How should we do the backpropagation? We can use simple SGD, but there are many options. 

**Initial Pseudocode**
![[Pasted image 20260416195802.png|560]]

**Deep Q-Learning Application: Atari Breakout**
![[Pasted image 20260416200043.png|576]]
How will our network work? 
- Instead of giving one state, we will give several states based on several timeframes. Why?
	- For preprocessing, we need a sequence of pictures because for the game, we need to know which way to move the bracket to know where to bounce the ball. The direction that the ball is going is critical information to observe. With just one input it will fail. 
![[Pasted image 20260416200241.png|581]]
We also do preprocessing to improve the input that we have. Instead of needing a 3D CNN, we can just use 1D. 
![[Pasted image 20260416200322.png|583]]
Implementation:
![[Pasted image 20260416200344.png|583]]
We most add a check in this implementation to check if we are at the last action.
- In Atari Breakout, that's when we have successfully cleared the last block. 
![[Pasted image 20260416200628.png]]

**Training Challenges**
![[Pasted image 20260416200639.png|524]]
Consider *Dynamic Programming*:
- For a specific state, we perform a specific action, we get a specific reward, and then we continue. 
- The decisions we make in the game, however, are not isolated from each other. 
- We need to keep a memory of actions stored because these actions can affect each other sequentially (Consider chess).
- Dynamic programming stores computations made to make it more efficient, so that if we encounter the same problem again in the code, we already have the solution. 

**Exploration vs. Exploitation**
*Exploration*: When we are simply searching or trying new actions to find better rewards
*Exploitation*: When we know a certain action and want to maximize rewards with it
Recall adaptive learning: At the beginning, we set the learning parameter to be high, which let the weights in our network change a lot. As we progress, we want the learning rate to become smaller, which means that the future adjustment and weights that we have already learned to become weaker. This means that at the start, we want to explore for new values, and then once we find good values, we want to exploit them and maximize the benefit. 

Consider the Discounted Reward function: the value of gamma increases as the time passes. It is a similar idea as adaptive learning, where the reward changes depending on our position. 

*Problem*: Q is just an estimate. We want to explore and exploit because the environment is probabilistic, and we cannot always be certain. 

**Completed Pseudocode**
![[Pasted image 20260416201820.png]]
![[Pasted image 20260416201918.png]]

```Pseudocode
Init replay memory and Q-network

Play M episodes (full games)
	Initialize state (starting game pixels) at beginning of each stage
	
	At each timestep t of the game... 
		Explore at random, select a random action
		otherwise select greedy action from policy 
		
		Take the action a_t, and observe reward r_t and states s_t+1
		
		Store the transition in replay memory 
		
		Sample a random minibatch of transitions from replay memory
		and perform a gradient descent step (experience replays)
```

### Review 
**What is the state space of Go?**
The possible legal configurations of a game of Go. State space is how many possible options can happen in this environment. For Go, it is 10^170. The board of Go is 19x19, and for each of the cells, we have 3 options. This is 3^(19x19).
**What are the elements of RL?**
Agent, state, action, reward, environment, policy, discount factor, and t
**What is discounted return? What happens when we adjust gamma, the discounted return parameter?**

**What is the Q-Table**
**When do we need depe learning to assist in RL programming?**
**What is the Bellman Equation?**
**What is the number of output and input layers in a perceptron of deep reinforcement learning?**