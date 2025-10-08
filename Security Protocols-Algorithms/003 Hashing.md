## Hash Functions and Message Authentication Codes

So far, everything we've discussed is about confidentiality and keeping communication private. Now, we are discussing authentication and verifying the integrity of received messages. 
*How do we verify that a file is the same file we expect and has not been tampered with since being created or last updated?*
(Related to our lab: We will create two applications, programming one to say that the app (1) location is good, and the app (2) location is bad. We will then generate an MD5 collision with the same hash for both apps.)

**What are hash functions?**
- A function that takes as input an arbitrarily long string of bits and produces a fixed size result.
	- Alice sends a message `m` with a message authentication tag `a`. 
	- `m` is public, but Alice is able to ensure that `m` is actually from her using hashing. 
	- Interceptor Eve does not have tag `a`, so she cannot create a message that can be verified in the same way. 
	- Do not use the same key for hashing as with encryption. 
![[Pasted image 20251001142941.png]]

**Properties of Hash Functions**
`M -> h(M)`
1. The hashing function is one-way, which is why it is also called a *trapdoor function*. You cannot decrypt a hash. 
2. The hash is a fixed length
3. The hashing function collision-resistant (> **collision** is when two differnet inputs `m` and `m'` will hash to the same output). SHA256 is the most often used, and it is secure, but we can surmise because of the **birthday paradox**, it is almost guaranteed that there are two different files in the world have the same hash. 
	- But this is only really a problem when we start being able to consistently generate those collisions in the same computing environment. 

Antiviruses like to use hashes (signature-based AV) to identify malware. Malware writers know that this is used, so they may use padding in their code or malware to force AVs to reidenfity malware patterns. There are other ways AVs do it though. 
Other forms of AV:
- Heuristic-based AV
- Behavioral-based AV
	Both look at the actual processes spawned by malware and noticing the patterns. 

**Real Hash Functions**
• Very few existing functions  
• Iterative through block sequencing, with padding at the  
end  
• A compression is used at the end  
• Advantages of this model:  
• Streams of data are processed more efficiently  
• Easier to implement than handling variable length strings  
directly

**MD5**- 128-bit function, splits it into 32 bit "words"
- Uses 4 rounds of addition, XOR, AND, OR, and rotation operations 
- Very efficient for 32-bit CPUs. 
	- Not collision resistant (as we will see in lab)
**SHA1** - Insecure Hash Algorithm, 160-bit hash function based on MD4, the predecessor to MD5. 
- Offers more security than MD5, albeit slower than MD5. 
- 160-bit result size leads to collisions. 
- Similar to triple DES from DES.
**SHA2** - SHA2 is a family including SHA224, 256, 384, and 512. 
Designed to be used with 128, 192, and 256-bit key sizes from AES.
- Slow, takes long to compute as AES or Twofish 
- SHA3
	- Built of Sponge Construction (absord data like a sponge and output the fixed hash data), uses random permutations to "absorb" large amounts of data. 

![[Pasted image 20251001145303.png]]
1. The MD (Message Digest) Series  
• Developed by Ron Rivest  
• Includes MD2, MD4, MD5, & *MD6*  
2. The SHA Series  
• Standardized by NIST  
• Includes SHA-0, SHA-1, *SHA-2* (might need to be replaced), and *SHA-3*

Running hash functions 
![[Pasted image 20251001145553.png]]
Performane measuring![[Pasted image 20251001150149.png]]
We can compare it to AES.

**Which Hash functions do we use?**
- Recommended SHA-2 family, or SHA-3. If SHA-2, use at least SHA256. 

## Attacks on Hash Functions 
![[Pasted image 20251001152927.png]]
**Collisions**
- Taking a prefiex file (added as a prefix onto a generated P and Q from the MD5 collision generation)
- Echo a string into "prefix"
- Use `md5collgen` on the file to create to binary files, msg1, and msg2. 
- Use `md5sum` on the two messages to see the same outputs. 
![[Pasted image 20251001153120.png]]
![[Pasted image 20251001153320.png]]
May notice there is little initial difference, but this is a collision. `md5collgen` generates P and Q using edits in small, strategic spots. 
This is due to a vulnerability in the Merkle-Damgard construction. 
![[Pasted image 20251001153439.png]]
P and Q are generated from the program, but the prefix and suffix are what is meaningful to us. 

**Applications of Hash Functions**
![[Pasted image 20251001154335.png]]
Linux storage of passwords. Not just for the passwords, but also for the *salt* of the password. 
*Salt* - used to generate different hashes for the same password according to the user by using randomness. 

We do not just hash once on passwords. Usually, we would hash thousands of times over. When we scale dictionary attacks (how you attack a password vault, potentially using hashes), this makes brute force attacks much more difficult. 

## Message Authentication Codes 
**MAC** - A construction that detects tampering with messages.
![[Pasted image 20251001155408.png]]
Integrity vs. Confidentiality 
MAC code (tag) and message are sent to Bob. 
- Speaking specifically about the tag, `a`, Alice sends her message with this tag as the identifier confirming that the message comes from her. If Eve sends a message `m'` that Bob checks with the hashing function using the shared key between him and Alice, it will output `a'`, not `a`.

**CBC-MAC**
• Uses a CBC-mode block cipher to encrypt message m.  
• The last block (or half the last block) (usually 128 bits) of the ciphertext becomes the  
MAC.  
• *Never use the same key for encryption & authentication.* Why? 
	Consider, we have key`K`, tag`a`, message `m`, and ciphertext `c`
	To encrypt, we could use `AES-CBC(K, m)` --> `c`
	To decrypt, we use `AES-CBC(K, c)` --> `a`
	If we use the same function to generate the tag, `AES-CBC(K, m)` --> `a`.
	Notice this creates similarities between the tag and our ciphertext. We would be communicating `c` and the last block of `c`, which is the tag and not secure. 
• Susceptible to collision attacks  
• Steps to properly implement CBC-MAC:  
We have `m`, `K`, and we want to create `a`.
1. Construct a string `s` from l and m, where l is the length of m in a  
fixed-length format.  `s = m || l ...000`
2. Pad `s` until it is a multiple of the block size, usually 128 bits long.  
3. Apply CBC-MAC to `s` : `AES-CBC(S, K_a)` --> `A`, which is really the entire encrypted `s`.
4. Only output the last ciphertext block, and no other parts or  
intermediate stages. `a` is this last block.
**CMAC: A more secure version of CBC-MAC**
• NIST has standardized CMAC as a streamlined  
implementation of CBC-MAC.  
• Same as CBC-MAC but:  
	• CMAC xors 1 of 2 special values into the last block prior to the  
	last iteration of cipher encryption  
	• Special values are derived from the CMAC key.  
	• The special value is chosen based on whether the length of  
	the message is a multiple of the block cipher’s block length.
**HMAC**
• Why would a hash be a good solution for a MAC?  
• HMAC hashes the message and then the output is  
hashed with the key. 
$$SHA_{256}(K \oplus b || h(K \oplus  q))$$
where `b` and `q` are special values and `h` is just SHA256 hashing. 
• Resistant to attacks such as key recovery attacks and  
collision attacks  
• It is recommended that SHA-256 be used as the hash  
function.
**GMAC**
 GMAC is also standardized by NIST  
5Attributes:  
	• Designed for 128-block ciphers.  
	• Very efficient  
	• Inputs – message, nonce, and the key  
Steps:  
	• Computes a simple mathematical function on m  
	• Encrypts the output of this message with a block cipher in CTR  
	mode.  
	• Nonce is used as the IV for CTR.

*Which one to choose?*
• HMAC with SHA-256 is recommended  
• GMAC is fast, but it only provides 64 bits of security

