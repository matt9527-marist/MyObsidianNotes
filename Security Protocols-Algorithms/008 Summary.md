**Secure Channel**
Originally, we used only *symmetric encryption*. 
Recall: we did not describe how the two parties obtained their provided AES keys. We now have discussed various ways of sharing and establishing keys. 
- **Confidentiality**: AES
- **Authentication**: HMAC 
	- Use these in tandem to ensure the integrity of the communications. 

For *asymmetric encryption*, this is what we will be using to establish communications. 
- **Confidentiality**: RSA 
- **Authentication**: PKI 

We establish the communications first with public key encryption. This is because we can openly host the public key on a public website. Once we establish the communications with asymmetric cryptography, we would then swap to using symmetric encryption for better efficiency. 

**How do we swap from asymmetric to symmetric cryptography?**
![[Pasted image 20251029155707.png]]
`X` is the shared symmetric key. 

