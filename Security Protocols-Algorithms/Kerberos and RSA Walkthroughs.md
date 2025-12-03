Kerberos
![[Pasted image 20251022155006.png]]
1. Client sends auth request to AS
2. AS sends to client: 1) ticket granting ticket with session info encrypted with the TGS key (yellow) and 2) the session key (red) encrypted with the client key (green)
3. Client decrypts session key (red). Client sends to TGS: 1) session key and ticket granting ticket encr