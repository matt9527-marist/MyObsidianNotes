**How do we attack monoalphabetic ciphers?**
![[Pasted image 20250910142216.png]]
We can compare the **frequency** of singular letters and see how much they show up in the ciphertext vs. standard English text. "e" is one of the most common letters in the English text. 

![[Pasted image 20250910142340.png]]
We may also look at the frequencies of bigrams and trigrams, which is checking the frequency of the combination of two letters. 
We can see very often occurrences of "th" or "in" or "se" in the English language. 
Starting with singular character frequency clues, we can build up to bigrams and trigrams for bigger clues. This can slowly uncover the plaintext message. 

What is the solution to this? **The Enigma Machine**
- This machine produced a mapping for letters through a set of gears that represented a set of ciphers. With this in use, the same high frequency bigram and trigram will not be applicable to the next cipher in the next gear. 

## Attacks on Block ciphers
Most common is chosen-plaintext attack
Specific Block Cipher Attacks:
- Related-Key Attack 
	- Noticing that there may be similarities between two keys. Keys are created on something such as sequencing. Suppose we begin a communication session, if an attacker sees the key and realizes the key has the session number, this is a similarity that can be used to break the communications' encryption by being able to guess the key.
- Chosen-Key Attack
	- Usually one part of the key remains the same, and we only change future parts of the key. This allows us to break the key down in the future and decrypt the message. 

**The Ideal Block Cipher**
Ideal = Perfectly Secure (this does not exist, nor will it ever exist)
1. Ciphertext is a completely random permutation based on the key. 
	- E(m, K<sub>e</sub>) = c where c will always be completely random. This is very difficult because randomness in computing is often just pseudorandomness. 
2. These random permutations are independent 
3. The ideal block cipher as a uniform probability distribution over the set of all possible block ciphers.
	- The outcome of any given block is completely random. For example, in the English language, this would mean that all combinations of letters (bigrams, trigrams+) would have constant frequency with no noticeable variation. 

**Realistic Block Ciphers**
![[Pasted image 20250910154826.png]]
The above is an example of a realistic block cipher. Suppose we have a very large text file. The cipher will break this file into chunks of 128 bits. We will have a *Key Expansion* function that generates *round keys* that will perform a series of encryption rounds on the chunk. The provisional text and end ciphertext will be of the same size. 

*Never* use a block cipher that has not been published and peer-reviewed. *Rounds* - most block ciphers iterate through a weak cipher. 
How do we break this?
- We might try to break round 1, and then we would move on to the next round, and then the subsequent round... etc. for as many rounds as it takes to break the ciphertext. 

## Encryption Algorithms
**Data Encryption Standard (DES)**
NOT SECURE -> any modern device can crack DES in relatively short periods of time. 
- Legacy encryption due to a block size of 64 bits and a key size of 56 bits. 
- Survives as 3DES, which encrypts, decrypts, and encrypts with DES. 
- DES and 3DES are not recommended. 

![[Pasted image 20250910155359.png]]
Split the original 64 bit block into two 32 bit segments. 
*K<sub>i</sub>* is our round key. Therefore, the image is representing one round of DES.
1) *R* is fed into the overall function *f*, first going through the *Expand* function. This expands that initial 32 bit segment to 48 bits. 
2) XOR the expanded 48 bit result with *K<sub>i</sub>*
3) Feed the result into an *S* box, which is a direct one-to-one mapping of different bits within the resulting XOR between the expansion and the round key. The *S* box will map the 48 bit expansion back to 32 bits. (8 groups of 6 bits down to 8 groups of 4 bits)
4) Feed the result into a bit shuffle function.
5) Take the result and XOR it with the original *L* segment bits. 
Across 16 rounds, the result of this process will become the new *R* in the next round. There will be 16 runs of function *f*.

The block and key sizes are much smaller than what we use today.

**Advanced Encryption Standard (AES)**
- Block size of 128 bits instead of DES's 64
- Key length and Rounds: (Variable as options for companies)
	- 128 bit key at 10 rounds
	- 192 bit key at 12 rounds
	- 256 bit key at 14 rounds 
	(Cannot swap these)
	Why have multiple options when 256 is the most secure? Why do overkill? Some may opt for lower levels of security in order to increase performance. 
![[Pasted image 20250917143411.png]]
1. Break 128 bits into 16 bit inputs. 
2. XOR the inputs with a 16 bit round key 
3. Input the 16 bit output into an *S* box which gives an output of 8 bits.
4. Output moves into predefined *Mix* function.
5. Results of the *Mix* function are output back as 16 bits and are fed into the next round.
**Advantages**: This is all operating in **parallel**. This is what allowed us to double the bit size by increasing speed significantly. AES is able to have triple peed as DES, but with significantly higher security.
**Disadvantages**: Will be naturally broken someday. 

**Serpent** is the 1/3 speed version of AES, so just as fast as DES, but is highly secure. Current attacks can only crack up to 12 rounds.
What does this mean?

Suppose we are working with AES, and we have 10 rounds of encryption:
1. Round 1: P --> C1. If we know how to get back to P1, the round is said to have been cracked. 
2. Round 2: C2. We won't have C1 at this point. We have to work from C2 back to the plaintext. We cannot iterate through rounds back to the plaintext. We have to go from C2 right to the plaintext, not knowing what C1 actually is. 
3. Round 3: C3, even harder. This continues further:
4. ...
5. ...
	...
6) 

