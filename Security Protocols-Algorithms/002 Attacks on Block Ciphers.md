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
	- E(m, K<sub>e</sub>) = c where c will always be completely random. This is very difficult because 