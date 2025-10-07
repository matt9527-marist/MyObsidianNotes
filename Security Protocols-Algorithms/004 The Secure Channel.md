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
Params: input key (K) and the roles (R), Return: state of the secure channel (S)
First compute the 4 encryption keys using SHA256. All of these are subkeys derived from the original key `K`. All of these are first created for Alice. 
If the party is Bob, just swap the sending subkey to the receiving key.
Next, handle message counting: set two counters (`MSGCNTSEND`, `MSGCNTRECEIVE`) to 0. 
Package the state into `S`, return `S`

Function 2: **Send Message**
![[Pasted image 20251006223424.png]]
Params: the secure session state (S), message to be sent (m), additional data to be authenticated (x)
Return: Data to be transmitted to the receiver (t)
Check that `MSGCNTSEND` is still less than 32 bits. If it is not maxed out,  increment `MSGCNTSEND`.  Create a variable `i` using `MSGCNTSEND`
Then compute the authentication `a` using HMAC-SHA-256, using inputs `i`, `len(x)` (so when recveive a message, we can properly split x and m), and the message itself `m`.
`a` is our tag. We will append `a` to the original message, so that it can be encrypted. This concatenated value will become the initial `t`. 

Now begin the encryption process by generating the key stream. 
Assign the subkey `KEYSENDENC` to variable `K`.
Encrypt a key stream created out of 1) 4-byte counter 2) 4 bytes of `i` and 3) 8 zero-bytes. 
XOR the keystream with the initial `t` up to the length of `t`. Concatenate this with `i`, encoded to 4 bytes, so that the receiver can pull it off. 
Return `t`. 

Function 3: **Receive Message**
![[Pasted image 20251006224520.png]]
Params: secure session state (S), text received from transmitter (t), and additional data to be authenticated (x)
Return: output (m), message that was sent. 

First check that the length of `t` >= 36. Recall that SHA-256 will always give a 32-byte output. This should include that + the 4 byte message number. If the message is not at least this size, we know there must be an error, and we must request the message again. 
First break `t` into `t` and `i`. 
Generate the key stream, just as the sender did. 
The first block of the key stream is a 4 byte counter, 4 bytes of `i`, and 8 zero-bytes at the end. The one difference is that we are using the subkey `KEYRECENC`. 
Now decrypt the message and the MAC field and split them. We can do this split because we know the MAC field is always 32 bytes long. When we do these concatenations, we always need to be sure that we know the length of `x`, the length of `len(x)`, and the length of `i`. We do not need to know the length of `m`. When we decrypt, the result is `m` concatenated with our tag `a`.
Recompute the tag `a'` using the subkey `KEYRECAUTH`.
If `a'` =/= `a`, then we have an authentication failure-- destroy `k` and `m`. 
Else, check if `i` < `MSGCNTREC`, if it is, we have a message out of order-- destroy `k` and `m`. 
If all is wel


> Receiving a message is exactly opposite of sending a message.


