## Hash Functions and Message Authentication Codes

So far, everything we've discussed is about confidentiality and keeping communication private. Now, we are discussing authentication and verifying the integrity of received messages. 
*How do we verify that a file is the same file we expect and has not been tampered with since being created or last updated?*
(Related to our lab: We will create two applications, programming one to say that the app (1) location is good, and the app (2) location is bad. We will then generate an MD5 collision with the same hash for both apps.)

**Properties of Hash Functions**
`M -> h(M)`
1. The hashing function is one-way
2. The hash is a fixed length
3. The hashing function collision-resistant

