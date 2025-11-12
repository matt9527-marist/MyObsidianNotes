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

**Becoming a CA**
![[Pasted image 20251112161521.png]]

**Asking the CA to sign the Request**
1. Domain verification (DV)  
2. Organization verification (OV)  
3. Extended Verification (EV)

![[Pasted image 20251112162018.png]]

**Creating Intermediate CA Certificate**
![[Pasted image 20251112162805.png]]

**Deploying the Cert in an HTTPS Website**
Edit Apache configuration file. 
- Aliases would be the extension names added to the certificate. 
- Also allows us to edit the index.html file. 
![[Pasted image 20251112162916.png]]
Normally, we would need to store these in the certs folder, which is where the configuration files searches to find these files. 
We also need to edit the etc/hosts file so that it can contain the model website associated with the correct IP address. 
![[Pasted image 20251112162935.png]]

**Adding Root Cert to the Browser Cert in HTTPS Website**
![[Pasted image 20251112163018.png]]
Import our certificate and save it. Add it as a new root certificate to the browser, which will then allow us to visit the Apache website without the error. 

