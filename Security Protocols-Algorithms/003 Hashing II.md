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
1. The hashing function is one-way, which is why it is also called a *trap*
2. The hash is a fixed length
3. The hashing function collision-resistant (> **collision** is when two differnet inputs `m` and `m'` will hash to the same output). SHA256 is the most often used, and it is secure, but we can surmise because of the **birthday paradox**, it is almost guaranteed that there are two different files in the world have the same hash. 
	- But this is only really a problem when we start being able to consistently generate those collisions in the same computing environment. 




