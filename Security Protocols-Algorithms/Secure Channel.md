Start Secure Channel:
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
		Swap(KeySendEnc, KeyRecEnc)
		Swap(KeySendAuth, KeyRecAuth)
		
	# Init send/receive counters at 0
	MsgCntSend, MsgCntRec = 0 
	# Package the state 
	S = (KeySendEnc, KeyRecEnc, KeySendAuth, KeyRecAuth, MsgCntSend, MsgCntRec)
	return S
```

Send Message
```python 
# params S secure session state, m message, x protocol data to be auth'd 
# Return t data to be transmitted to receiver 
sendMessage(S, m, x) --> t
	# Ensure message count has not been maxed out
	# Recreate session if message count is maxed out
	assert(MsgCntSend < 2^32 - 1)
	MsgCntSend++ 
	i = MsgCntSend 
	
	# Compute authenticati
```


