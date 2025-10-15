Start Secure Channel:
1) Compute using SHA256 the send and receive subkeys for auth and encryption 
2) Swap() the send and receive keys if the party is opposite 
3) Initialize message send and receive counters to 0
4) Package the state as S, and return it
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

Send Message:
1) Check if the message send counter is exhausted with assert()
2) Increment message send counter and set `i` to it
3) Compute auth `a` using HMAC SHA256 and let `t` be the message `m` concatenated with `a`
4) Generate the keystream
5) Form the ciphertext through XOR with keystream and return `t`
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
	a = HMAC_SHA256(KeySendAuth, i || len(x) || x || m)
	t = m || a
	
	# Generate the key stream. Each plaintext block of the block cipher 
	# consists of a 4 byte counter, 4 bytes of i, and 8 zero bytes 
	# Integers are LSB first, E is AES encryption with 256-bit key 
	K = KeySendEnc 
	k = E_K(0 || i || 0) || E_K(1 || i || 0) ... 
	
	# Form the final ciphertext by prepending i 
	# to t concatenated with t XOR'd with the keystream up to len(t)
	t = i || (t XOR bytes(k : len(t)))
	
	return t
```

Receive Message:
1) Check that the length of the ciphertext is at least 36 bytes 
2) Split the ciphertext `t` into `t` and `i`
3) Generate the keystream
4) Decrypt the message and MAC field and split the two 
5) Recompute the authentication 
6) Verify the authentication
```python 
# @params S secure session state, t text received, x protocol data to be auth'd
# Return m the message that was sent 
receiveMessage(S, t, x) --> m 
	# The received message must be at least 36 bytes, consisting of a 4
	# byte message number and a 32 byte MAC field 
	assert(len(t) >= 36)
	
	# Split t into i and the encrypted message + authenticator 
	# Split is well defined because i is 4 bytes long
	i || t = t
	
	# Generate the keystream 
	K = KeyRecEnc
	k = E_K(0 || i || 0) || E_K(1 || i || 0) ... 
	
	# Decrypt the message and MAC field and split the two 
	# We can do the split because we know the MAC field is 32 bytes long 
	m || a = (t XOR bytes(k : len(t))) 
	
	# Recompute the authentication 
	# We know the values len(x) and i are encoded in 4 bytes, LSB first 
	a2 = HMAC_SHA256(KeyRecAuth, i || len(x) || x || m)
	
	# Verify authentication 
	if a2 != a
		destroy k, m
		return AUTHENTICATION_FAILURE
	else if i <= MsgCntRec 
		destroy k, m
		return MESSAGE_ORDER_FAILURE 
	
	MsgCntRec = i 
	return m 
```
















```Python
# params: K session key, R roles for the two parties (Alice and Bob)
# Return S the secure session state 
initSecureSession(K, R):
	# Compute the 4 required subkeys for enc and auth 
	KeySendEnc = SHA256(K, "Encrypt Alice to Bob")
	KeyRecEnc = SHA256(K, "Encrypt Bob to Alice")
	KeySendAuth = SHA256(K, "Auth Alice to Bob")
	Key
```