Kerberos
![[Pasted image 20251022155006.png]]
1. Authentication process begins with client and authentication server AS sharing the same client key (green). The client requests to authenticate to AS. AS sends back a session key (red) that is encrypted with the client key. 
2. Client can decrypt the session key, which will sign exchanges between the client and the ticket granting server TGS. Client sends