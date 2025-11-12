**Elements of a Certificate**
When we download a certificate from a website, what are the key elements to look for?
1. The Public Key 
	- Querying a specific website or service. Through TLS, they provide their public key that verifies their X.509 certificate. 
2. The Owner of the Public Key 
3. The Certificate Authority's Signature

**PayPal's Certificate**
![[Pasted image 20251112155352.png]]
TLS port 443
![[Pasted image 20251112155419.png]]

**The Certificate Authority's Certificate**
![[Pasted image 20251112160232.png]]
This certificate as a CA (Digicert) is valid for a much longer time, at least much longer than Paypal's certificate. We can still do encryption and decryption with this, and we still have all the information needed to verify the certificate. 
This is indicated by the term: CA:TRUE. 
Pathlen tells us how long the chain of certification can be. If it was 1, this means that this CA can then validate another CA. 

