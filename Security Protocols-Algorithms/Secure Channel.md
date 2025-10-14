```python
# @params K key of the channel, 256 bits, R role specifying party
# Return S the state of the secure channel
initializeSecureChannel(K, R) --> S
	# Compute 4 required subkeys 
	KeySendEnc = SHA256(K, "Enc Alice to Bob")
	KeyRecEnc = SHA256(K, "Enc Bob to Alice")
	KeySendAuth = SHA256(K, "Auth Alice to Bob")
	KeyRecAuth = SHA256(K, "Auth Bob to Alice")
	# Swap keys if the party is Bob
	if R == "Bob":
		Swap(KeySendA)
```
