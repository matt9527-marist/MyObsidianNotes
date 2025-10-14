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
	
	# Compute authentication
	a = HMAC_SHA256(KeySendAuth, i || len(x) || m)
	t = m || a
	
	# Generate the key stream. Each plaintext block of the block cipher 
	# consists of a 4 byte counter, 4 bytes of i, and 8 zero bytes 
	# Integers are LSB first, E is AES encryption with 256-bit key 
	K = KeySendEnc 
	k = E_K(0 || i || 0) || E_K(1 || i || 0) ... 
	
	# Form the final ciphertext by prepending i 
	# to t concatenated with t XOR'd with the keystream up to len(t)
	t = i || (t XOR bytes(k : len(t))
	
	return t
```

Receive Message 
```python 
# @params S secure session state, t text received, x protocol data to be auth'd
# Return m the message that was sent 
receiveMessage(S, t, x) --> m 
	# The received message must be at least 36 bytes, consisting of a 4
	# byte message number and a 32 byte MAC field 
	assert(len(t) >= 36)
	
	# Split t into i and the encrypted message + authenticator 
	# Split is well defined because i is 4 bytes long
	t = i || t
	
```

