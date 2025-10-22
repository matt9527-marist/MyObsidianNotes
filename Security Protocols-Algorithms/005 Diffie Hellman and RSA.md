**Asymmetric Encryption**
Aspects of our full cryptosystem:
- We can encrypt and auth data 
- We cannot negotiate a shared secret key between two individuals 
- Management of keys to identify other parties over the Internet

**Initial Key Server**
Setting up one key server that maintains state 
Steps of this Alternative Method 
1. The client and the key server set up a secure channel 
2. The client requests to set up authentication with a service servers
3. The key server sends K(AB) to both the client and the service server.
Risks:
4. One computer with all keys is an attractive target to attackers  
5. The key server must be running at all times  
6. All members of the service must first authenticate with the key server

**The Key Server**
![[Pasted image 20251022154411.png]]
How does Bob trust that Alice is indeed Alice? (know that this is a legitimate ticket?)
- Because the only other person that shou