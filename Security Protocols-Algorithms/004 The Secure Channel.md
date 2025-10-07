Putting everything together. 
**Secure Channel** - Secure session created for a user or client in order to communicate with your app. 

**Properties of the Secure Channel**
1. Roles to be set:
2. The Key needs to be set - currently exists, and only Alice and Bob know it. 
   Known as the session key
   256-bit value to achieve a proper security level
3. Messages or information stream?
   Think UDP vs. TCP- TCP using discrete messages vs. UDP's info stream. At the cryptographic layer, we want to keep things in terms of discrete messages
4. Security Properties
   Eve only knows the timing and the size
   Bob can tell when Eve manipulates message sequencing

