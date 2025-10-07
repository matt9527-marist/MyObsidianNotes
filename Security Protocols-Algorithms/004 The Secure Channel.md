Putting everything together. 
**Secure Channel** - Secure session created for a user or client in order to communicate with your app. 

**Properties of the Secure Channel**
1. Roles to be set:
2. The Key needs to be set - currently exists, and only Alice and Bob know it. 
   Known as the session key
   256-bit value to achieve a proper security level
3. Messages or information stream?
   Think UDP vs. TCP- TCP using discrete messages vs. UDP's info stream. At the cryptographic layer, we want to keep things in terms of discrete messages
4. Security Properties
   Eve only knows the timing and the size
   Bob (or Alice) can tell when Eve manipulates message sequencing

**Authentication and Encryption: Which comes first?**
Three Approaches: 
1. Encrypt-Then-Authenticate
   The intuition of encryption first being secure is a bit flawed because we shouldn't rely on authentication to make encryption itself secure. 
   But this does us validate the authentication before decrypting. 
2. Authenticate-Then-Encrypt*
   Create a tag and then encrypt the tag and the message together. 
   *Horton Principle*: "Authenticate what is being meant, not what is being said"
3. Encrypt-And-Authenticate
   Implement the processes in parallel. One issue: the first MAC created will not be encrypted, and will therefore be vulnerable. 

* 


