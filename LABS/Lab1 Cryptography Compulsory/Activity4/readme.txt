RSA Encryption and Decryption

We have explored only the keys earlier, we will explore encryption and decryption here.

Part-1: Encryption
------------------------------ Problem Statement ----------------------------
- Navigate to "/home/labDirectory/part1/" and work in this directory.
- Given the private key, you need to do the following:
   - Create a public key using the private key given to you.
   - Encrypt the secret.txt file using newly created public key and store it in "encrypted.txt"
   - Create md5sum of the output file and submit the md5sum in the flags.txt file
- **NOTE**: The name of the encrypted text file must be "encrypted.txt" and it must be located in "/home/labDirectory/part1/"
- **EXTRA Question**: Try the encryption multiple times and create md5sum of it, you will notice different md5sums every time, meaning the cipher text changes on every encryption. Can you figure out why is this happening?

Part-2: Decryption
------------------------------ Problem Statement ----------------------------
- Navigate to "/home/labDirectory/part2/" and work in this directory.
- Given a cipher text file and its  associated keys (public and private) in “/home/labDirectory/part2/keys/” , decrypt the cipher text.

submit the flag (plaintext) in the flags.txt file

------------------------------------------- Useful Commands --------------------------------------------------
- Create RSA private key:
   - openssl genrsa -out <outfile> <bits>
- Create RSA Public key:
   - openssl rsa -in <private-key> -pubout -out <outfile>
- Encryption using RSA:
   - openssl pkeyutl -encrypt -in <plain-text-file> -out <out-file> -pubin -inkey <public-key>
- Decryption using RSA:
   - openssl pkeyutl -decrypt -in <cipher-text-file> -out <outfile> -inkey <private-key>
- Verify if given public key and private key pair is valid or not:
   - echo "Verified" | openssl pkeyutl -encrypt -pubin -inkey <public-key> | openssl pkeyutl -decrypt -inkey <private-key>
- Extract the details(primes,modulus,public key, private key) from private key file:
   - openssl rsa -in <private-key> -text -noout
      