Kerberos
![[Pasted image 20251022155006.png]]
1. Client sends auth request to AS
2. AS sends to client: 1) ticket granting ticket with session info encrypted with the TGS key (yellow) and 2) the session key (red) encrypted with the client key (green)
3. Client decrypts session key (red). Client sends to TGS: 1) session key and encrypted ticket granting ticket and 2) requested service ID and timestamp encrypted with session key 
4. TGS decrypts session key with TGS key (yellow) and decrypts requested service ID with session key. TGS sends to client 1) service ticket and service exchange key (blue) with session info encrypted using the service key (black) and 2) service exchange key (blue) encrypted with session key
5. Client decrypts service exchange key (blue). Client sends to Service Server SS: 1) encrypted service ticket and 2) requested service ID and timestamp encrypted with the service exchange key
6. SS decrypts service ticket and service exchange key using service key (black). SS sends to client: access to service with timestamp encrypted with the service exchange key.

RSA: Given p and q prime numbers
Let p = 2 and q = 7
Find e, d, and N:

N (modulus) = p * q = 14 
