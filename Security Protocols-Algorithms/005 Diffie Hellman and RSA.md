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
- Because the only other person that should have K(B) is the Key Server. 
- Almost acts like a signature from the key server. 

**Kerberos**
![[Pasted image 20251022155006.png]]
One of the main methods used for validation within an environment. The above is the same previous model but expanded. 
- 4 Entities (Client `C`, Authentication Server `AS`, Ticket Granting Server `TGS`, and Service Server `SS`). 4 differeny keys color-coded. The Authentication Server is meant to auth the user. The ticket granting server is meant to manage access to different services within the environment. Each service server will host a different application that the end user will want to use. Kerberos is normally deployed in a corporate environment. 
1. `C` wants to auth. `AS` agrees. Auth the user to the ticket granting server: Message B (a ticket), and Message A (session key) encrypted with the client key. 
2. `C` forwards ticket to `TGS` as Message C. (Message B and Message C are the same ticket), alongside Message D, which is a server request for a certain service. Message C also has the red key, the session key, encrypted with it. 
3. `TGS` must decrypt the ticket using a shared key with `AS` (yellow key). Sends back the client-service exchange key (blue) to `C`, along with encrypted new ticket in Message E. `C` will not have the black key. 
4. `C` sends over the ticket (the same Message E) and the requested service to `SS`. `SS` has the service key to decrypt this ticket (black key). Validates `C` for the service. 
5. Return a timestamp to `C`. 

**Advantages of Kerberos**
1. The TGS does not track the tickets it shares with users 
2. Kerberos has been heavily scrutinized 
3. Maintained and updated constantly

**Limitations of Kerberos**
