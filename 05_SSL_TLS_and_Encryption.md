# For encryption there are two keys are used

1. Symmentric key
2. Asymmetric key

---

### 1. Symmentric key

Only one key is used for both encryption and dedryption at both client and server's end.
Problem is of sending the key between them

### 2. Asymmetric key

Client has both public and private key (its own)

when client sends something , it sends through the public key to server, there , the server can access the information through its private key and vice versa

Security is compromised here because the hacker can sit between the path b/w client and server and it can modify the public key being sent by anyone and then decrypt it using its own privaate key

SSL certificate verifies it (Certificate authority)

---

# Process

1. CA took the public key and the domain from the server
2. converted it to SHA
3. It encrypts this SHA with its own private key
4. It names that thing signature

## What was sent :

1. the Signature
2. Public key of the server

## At client end

1. Checked the public key of the server
2. Decrypts the Signature using the public key of CA
3. It got the HASH value that was sent by the server
4. It deos the same thing as on the server side (the conversion to SHA using domain and public key of server)
5. If both of SHA values are equal , things get authenticated
