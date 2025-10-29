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
1. Participants need to have reliable time keeping  
2. The authentication server needs to maintain all of the tickets that are sent to it

Possible Ways to Hack Kerberos
![[Pasted image 20251022160923.png]]
*Pass-the-ticket* – refers to the process of forging a session key and presenting that forgery to the resource as credentials
*Golden Ticket* – A ticket that grants a user domain admin access
*Silver ticket* – A forged ticket that grants access to the service
*Credential stuffing and brute force* – automated continued attempts to guess a password
*Skeleton Key Malware* - take advantage of vulnerabilities with Active Directory, the main auth service for Microsoft (which implements Kerberos). Acts very similar to golden ticket, where this key can gain one access to any service. Specifically through this type of vulnerability. 
*DC Shadow Attack* - Hackers take down the TGS and set up their own with a bed domain controller, embedding themselves into the environment. The system itself requires the TGS to auth legitimate users. 

**What do we Choose?**
If you can, also use Kerberos, or a cloud equivalent. 
If you cannot, significant time and resources wil lgo into developing a secure system like the initial key server. 

**Current State of Key Exchange**
![[Pasted image 20251022162057.png]]
It is profoundly difficult to do key management and key exchange. It is also not scalable because at some point, you just end up with too many keys!
Asymmetric cryptography decreases the need for shared keys between all. 

**Public Key Cryptography**
1. Bob generates a pair of keys (*Sbob, Pbob*) which are his private and  
public key.  
2. He publishes his public key  
3. Alice obtains public key from a website, etc. and uses it to encrypt her  
message and send it to Bob
4. Bob uses his secret key to decrypt the message
![[Pasted image 20251022163312.png]]

## RSA Algorithm 
Takes advantage of the fact that computers are very bad at factoring large prime numbers. 
![[Pasted image 20251029151058.png]]
`p` and `q` are typically very large prime numbers. For simplicity, we will use:
`p = 2` and `q = 7`
We want to generate `e`, `d`, and `N`
`N = p * q` = `N = 14`
Calculate the `Totient(N)` as `T`
`T = (p -1) * (q-1)` = `6`

`e` can be selected, but it has to meet two characteristics:
1) Be within the vector space of 1 ... Totient (1-6 in our example)
2) Must have a GCD between the totient and itself of 1. 
`e = 1, 2, 3, 4, 5, 6?` (really cannot be 6). 
Select `5` as the GCD of both 6 and 5 is 1. 

Next goal is to find `d` such that:
$$e * d \mod{T} = 1$$
$$5 * d \mod{6} = 1$$
For `d` we can try to find all of the multiples for `e`. 
- 1, 2, 3, 4, 5
- 5, 10, 15, 20, 25
	- Then take mod(6) for each of the above numbers and find where this evaluates to 1. 
	- There is more than one answer for `d`. Usually, we want to take the largest `d` we can find. However, this does make math harder. 
- Let's assume we continued up to 45, 50, 55. `55 mod(6) = 1`. We do this because we do not want `d` to be the same as `e`, which is also 5. We can say:
	- `Private Key = (11, 14)`
	- `Public Key = (5, 14)`

`Private Key = (d, N)`
`Public Key = (e, N)`

E = `plaintext^e (mod n)`
D = `ciphertext^d (mod n)`

Define an encoding scheme of "A" = 1, "B" = 2, "C" = 3...
Let's encrypt a given plaintext: `"b" -> 2`
This would be `2^5 mod(14)` = `32 mod(14) = 4`, so therefore `E = 4`, encoding to `"D"`

Let's decrypt a given ciphertext `"D"`
This would be `4^11 mod(14)` = `4,194,304 mod(14) = 2`, so therefore `D = 2`, encoding to `"b"`

We can do all of the above in Excel using MOD() and POWER() functions. 

```python 
RSA(p, q, e):
	# p and q are very big numbers 
	N = p * q; 
	TotientN = (1-p) * (1-q)
	e = {1 ... TotientN} where GCD(e) == 1
	e * d mod(TotientN) = 1
	
	Private_Key = (d, N)
	Public_Key = (e, N)
	
	E = plaintext^e (mod N)
	D = ciphertext^d (mod N)
```

**Overview of Diffie Hellman**
![[Pasted image 20251029155741.png]]
Using the above structure, Alice can keep `a` secret, and Bob can keep `b` secret, but can create a shared key. Bob is able to share some information about `b` using `B`, and Alice is able to share some information about `a` using `B`, by using their secret number `p`.
- How is this powerful with encryption? This allows us to establish a shared *symmetric* key by using the Law of Products of Exponentiation. 
- In this, Alice and Bob are able to calculate a shared secret number, with which they can encrypt and decrypt communications. 

**Modulus Key Size Problem**
![[Pasted image 20251029160308.png]]
The modulus utilized by Diffie Hellman increases very quickly and very drastically with higher key size. If we wanted to use 256-bit AES, the modulus will be very large. 

**MITM Attacks on Diffie Hellman**
![[Pasted image 20251029160415.png]]
Suppose we had a bad actor Eve, who is able to capture data "in the middle" of the communication. Bob wants to send ciphertext to Alice. Eve will collect that ciphertext, and send to Alice a different ciphertext instead. 
Eve can then create her own public and secret keys, discarding the original keys coming in from one of the parties. Eve can then pose as the opposite party when sending her new forged keys back over the channel. 
In this method, Eve then has shared secret keys with both Alice and Bob, but Alice and Bob think that it is only between them. 

**PKI - Asymmetric Cryptographic Solution**
![[Pasted image 20251029155707.png]]
With this scenario, 
