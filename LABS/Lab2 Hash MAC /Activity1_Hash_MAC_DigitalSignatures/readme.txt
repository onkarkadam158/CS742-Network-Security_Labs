Preamble: Agent X has moved to public key systems. He came up with the following procedure to communicate with Agent Z. 
   1. Generate a symmetric key and encrypt it with Agent Z’s public key (C1 is the resulting ciphertext).
   2. Encrypt the message with the symmetric key (C2 is the resulting ciphertext). 
   3. Send C1 and C2 to Agent Z.
  
One fine day Agent Z went to a location and attempted shooting Mr. Gabbar. Much to his horror, Agent Z realized it was a trap and managed to narrowly escape. 
Agent Z is mad and claims he went there based on Agent X’s instructions but Agent X claims he never sent those instructions. What is going on?

Based on the procedure being followed by Agent X in communicating with Agent Z, conjecture as to what could have gone wrong and how the enemy exploited the situation.

It looks like a case of missing integrity/authentication. 
A fix for this is either MACs or digital signatures. 
We will explore hashes (which are also used in keyed hashes and signatures), followed by MACs and digital signatures. Guidance for all is given at the end.


Part 1: Hashes, MACs, and Digital Signatures
-------------------------------------------- Problem Statement ------------------------------------------------------
You are given a secret.txt file in "/home/labDirectory/part1/" folder. You have to do the following for this part of the activity.
 1. Create MD5, and SHA256 hash of the file using openssl
 2. Create SHA256, and SHA512 MACs of this file using openssl. Use "sup3r_s3cret_k3y" as the key.
 3. Create a "private.pem" file in "/home/labDirectory/part1/" directory and sign the secret.txt file with that private.pem key. Once you sign it, create md5sum of the signature.

**NOTE**: The name and location of private.pem must match as suggested in point 3.
------------------------------------------- Submission Details ---------------------------------------------------
Submit the md5 and sha256 hashes, sha256 and sha512 MACs and md5 hash of the document signature in flag.txt file. Make sure to follow the format of flag.txt file.
---------------------------------------------------------------------------------------------------------------------------

Part-2: Verification of the Signatures
---------------------------------------------------- Problem Statement ----------------------------------------------
You are given "secret.txt" and "secret.sign" in "/home/labDirectory/part2" directory and also 3 client private keys in "/home/labDirectory/part2/keys" directory. You need to find out which one of the private keys was used to sign the secret.txt file using openssl.
------------------------------------------------- Submission Details ---------------------------------------------------
Once you identify the key used for signing the secret.txt file, use "rsa-utility.py" given in "/home/labDirectory/part2" to get details about the private key, and submit p (Prime 1), q (Prime 2), and d (Decryption key) in metadata.txt available within "/home/labDirectory/part2" directory in the format suggested in the metadata.txt.

------------------------------------------------- Guidance  ---------------------------------------------------
openssl dgst command can be used to generate the hash value for a file. To see the manuals, you can type man openssl and man dgst. Usage: openssl dgst dgsttype filename 
Replace the dgsttype with a specific one-way hash algorithm, such as -md5,-sha1,-sha256 etc. Try at least 3 different algorithms, the supported one-way hash algorithms can be known by typing man openssl.
    
To generate keyed hashes, you can use -hmac option. The following example generates a keyed hash for a file using the HMAC-MD5 algorithm.
The string following the -hmac option is the key. 
openssl dgst -md5 -hmac "abcdefg" filename. Generate a keyed hash using HMAC-MD5, HMAC-SHA256, and HMAC-SHA1. Vary the key length as well. 

To generate digital signatures, follow these procedures:
To Sign - To sign a file using OpenSSL you need a private key. If you don’t have an RSA key pair, generate one.
You can use the following commands to generate the signature of a file: openssl dgst -sha256 -sign private.pem -out data.sig data

To Verify - Verification requires the public key and knowledge of the hashing algorithm that was used. 
You can use the following command to verify the signature: openssl dgst -sha256 -verify public.pem -signature data.sig data
      