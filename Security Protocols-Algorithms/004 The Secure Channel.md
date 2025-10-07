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

**Designing a Secure Channel**
Consists of:
1) Message Numbering (i): Must be accurate and tracked. They identify our IVs and allow us to identify any replay of messages. We will encode a 32-bit message number for our system starting at 1. If we run out of numbers, we will NOT wrap back to 0 since it will create repeated IVs. We will generate a new key and a new session. 
2) Authentication: Using HMAC-256, ensuring that we can parse the protocol information and x correctly. We will feed into the MAC algorithm the message number `i` and the length of additional information `x` and the message itself. 
3) Encryption: AES-CTR. Important with CTR mode that the nonce/IV that we use is only used once. This is why we are using message numbers and recreate the session when we run out. 

Function 1: **Initializing the Secure Channel**
![[Pasted image 20251006222800.png]]
Params: input key (K) and the roles (R)
First compute the 4 encryption keys using SHA256. All of these are subkeys derived from the original key `K`. All of these are first created for Alice. 
If the party is Bob, just swap the sending subkey to the receiving key.

