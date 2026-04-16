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
