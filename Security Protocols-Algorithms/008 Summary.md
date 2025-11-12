**Secure Channel**
Originally, we used only *symmetric encryption*. 
Recall: we did not describe how the two parties obtained their provided AES keys. We now have discussed various ways of sharing and establishing keys. 
- **Confidentiality**: AES
- **Authentication**: HMAC 
	- Use these in tandem to ensure the integrity of the communications. 

For *asymmetric encryption*, this is what we will be using to establish communications. 
- **Confidentiality**: RSA 
- **Authentication**: PKI 

