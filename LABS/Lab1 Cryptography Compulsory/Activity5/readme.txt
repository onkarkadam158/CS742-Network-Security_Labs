You heard of ECC algorithms which are faster than RSA and using them, there is also a nice way to derive shared keys, 
which make the overall operation very fast. Let us explore this to help Agent X.

---------------------- Problem Statement ---------------------

Agent Z wants to send a message to Agent X.
For this, Agent Z will generate a shared key with her private key and Agent X’s public key (see Guidance for more details).

- Given "public-secp256k1.key" a public key of Agent X, you (on behalf of Agent Z) need to do the following:
  - Create your own public-private key pair and name them exactly "private.key" and "public.key" using openssl.
  - Use openssl to create a shared key with name "sharedKey.pem"
  - Once "sharedKey.pem" is created, wait for 1 minute and a "cipher.txt" file will appear.
  - Use the sharedKey.pem and decrypt the ciphertext using aes-256-ctr with IV as 102030506070ddff. 
  Also here encryption is done using base64 encoded key. See the guidance below for this.

- **NOTE:** Since there might be case where the file is available in the container but VLab editor doesn't show it, If you don't see "cipher.txt" file in VLab editor window after 1-2 minutes have been passed, look at the location "/home/labDirectory/" folder contents from terminal inside the container.
---------------------- Submission Details ---------------------
- Collect the flag available after decrypting the cipher text and submit it in flags.txt file.
 
- NOTE: If you don't see the required files in your labdirectory, then go back try reattempting the labs.


---------------------- Guidance ----------------------
Elliptic-curve Diffie–Hellman (ECDH) is a key agreement framework that allows two parties, each having an elliptic-curve public–private key pair, to establish a shared secret. We will explore this here.

Elliptic Curve Cryptography (ECC) is extensively used within public key encryption, including with TLS, Bitcoin, Ethereum etc. We will first use OpenSSL to create a public-private key pair. For this we will first generate a random private key (priv), and then generate a public key point (i.e. private multiplied by G), using a generator (G) which is a generator point on a given selected elliptic curve. Then we will also see how to derive a shared secret between two parties who have EC key pairs.
We will assume below that Alice wants to communicate with Bob using ECDH, the terminology used is as per this.

1. To first see what are the curves available, use “openssl ecparam -list_curves”

2. Let us first generate a private key for Alice. We need to specify which curve we will use to generate relevant size key. In this example, we have used secp256k1.
“openssl ecparam -name secp256k1 -genkey -out alicepriv.pem”
Use “cat alicepriv.pem” to view your key.

3. If we want to see what are the ECC parameters associated with this key, you can use “openssl ecparam -in alicepriv.pem -text -param_enc explicit -noout”
This specifies the prime defining the finite field, the coefficients a, b of the curve, the generator (both the x- and y-coordinates of the point are packed into a single string), the order or size q of the generated group, and the cofactor also.

4. Let us now generate the public key based on the private key via “openssl ec -in alicepriv.pem -pubout -out alicepub.pem”. You can checkout the key via “cat alicepub.pem”.

5. The “pem” format has a lot of extra stuff (e.g. BEGIN …) and also it is base-64 encoded. It does not really tell what the actual public and private keys are. 
  To find this you can use “openssl ec -in alicepriv.pem -text -noout”. 6. You need to repeat steps 2 and 4 for generating Bob’s private and public key.

7. Now that we have the relevant keys, we can derive a shared key using the below command. 
    This is from the perspective of Alice. “openssl pkeyutl -derive -out abkey1.pem -inkey alicepriv.pem -peerkey bobpub.pem” 
    The abkey1.pem is a shared symmetric key that Alice derived based on its private key and Bob’s public key. 
    This is the key she will use to encrypt messages sent to Bob using any of the symmetric key algorithms like AES etc (e.g. using openssl enc).

8. You can also do the same as above but from Bob’s perspective. Name the key abkey2.pem

9. You can check via “xxd” if the keys abkey1.pem and abkey2.pem are the same. They should be, if you did things correctly!

10. To encrypt with base64 encoded key file use below:
 - `openssl enc -<algo> -base64 -k $(base64 shared.pem) -iv <iv> -e -in <input-file> -out <output-file>`
 - These are important in cases where key files and their bytes are a bit weird and not easily readable.
      