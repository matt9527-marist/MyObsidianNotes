## What is Cryptography
**Art and science of encryption**
Can also be defined as the process of converting human readable information into cyphertext specifically for the goal of preventing unauthorized access. 
The main goals surrounding cybersecurity are centered on access. We do not want unauthorized agents to be able to read or write to private data. 

**Role of Cryptography**
This is not the only thing we need to be focused on. The security of our systems are dependent on strongest vs. weakest link.
1. Cryptography is useless without security mechanisms that go along with it.
	- Cryptography can be deployed within a larger ecosystem, not just by itself.
	- Many organizations implement cryptography, but fail in incorporating other security strategies with it. 
2. Access Management
3. Why is the major focus on it?
	- From an app development standpoint, it is one of the most important aspects as one of the most natural points of access for an attacker. 
	- If an attacker gets around encryption, the risk is very high, as it is extremely easy to impersonate actors when in possession of their encryption keys. 

**Threat Models**
*A security system is only as strong as its weakest link.*
Looking at a threat model of breaking into a bank vault:
![[Pasted image 20250903141327.png]]
Solution:
1. Risk Management
2. Attack Trees 
3. Defense-in-Depth 
*Defense-in-Depth* - Adding layers of security to protect against certain attack methods, the idea of layered security measures and additional steps to minimize potential damages. 

There is also the question of who is beyond attack vectors. This brings us to risk assessment. 

What is a "proper" level of security?
1. Focus on threats and assets
2. Match security controls to risks
![[Pasted image 20250903143055.png]]
Prioritize and determine the level of security that we want to use. 

**Encryption is not the answer**
- It can make things worse.
- There is no one solution. 
- Cryptography itself is hard. Implementation is easy. 
- There exists more generic attacks.

This is why we **balance security** with efficiency and performance in mind. 
- Complexity is our worst enemy. 
- The evolution of tehcnology adds to this complexity. 
- Performance is often the primary objective (especially for application developers)
No conversation should prioritize EVERYTHING, especially in a business environment where we want to minimize costs.


---


![[Pasted image 20250903145844.png]]
Key:
*m* => message in cleartext
*c* => encrypted text, cyphertext
- Created utilizing an **encryption function** *E*(K<sub>e</sub>, m)
- *K*<sub>e</sub> => encryption key 
Actors Alice and Bob, bad actor Eve. 
Bob will receive *c* and feed it into a **decryption function** *D*(K<sub>e</sub>, c)
- Bob will get the plaintext message *m* decrypted by the function with the shared key. 

What are some major weaknesses in our encryption model?
- Add noise to confuse the recipient
- Repeat *c* 
- Insert new message
- Change the order of messages
- Intercept and delay the message

**Kirchhoffs Principle**
1. Security depends on the security of the encryption key, not the encryption algorithm. 
	- The encryption algorithms used by Alice and Bob are NOT secret. It is public information how they work. 
	- The key input needs to remain secret. 
	- This is important because this allows us to do public peer reviews on the algorithms that we are using. Secure algorithms are not only difficult to create, but they are also difficult to implement in existing systems. 
2. Algorithms are embedded in the system.

**Authentication**
![[Pasted image 20250903152940.png]]
This is the process for the recipient to verify whether or not a message is legitimate. 
This is how **hashing** works, maintaining the integrity of the message *m* by checking it with an authenticating function H(K<sub>a</sub>, m). This is not secrecy of the message, but rather authentication of the message. This does not protect against sequencing of messages. Usually to fix that, we add sequencing numbers to messages. 

> **Public Key Encryption**
> Also known as **asymmetric Encryption,** where two keys are being used.![[Pasted image 20250903153331.png]]
1. Bob generates a pair of keys (*Sbob, Pbob*) which are his private and  
public key.  
2. He publishes his public key  
3. Alice obtains public key from a website, etc. and uses it to encrypt her  
message and send it to Bob
4. Bob uses his secret key to decrypt the message

	This allows scalability of encrypted messaging. 



