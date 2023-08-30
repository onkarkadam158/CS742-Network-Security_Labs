RSA Key Verification

Preamble: Life has been going well for Agent X, thanks to your help. But when is life ever a bed of roses? Agent X gets information from many field agents. He meets them once (after tremendous effort to keep the meeting secret) and shares a secret key with them (he maintains a separate key for each agent). But managing so many keys is getting overwhelming. Further, some of these agents are careless and tend to lose keys. Meeting them again, passing on new keys etc, i.e the overall key management is turning out to be a major pain in the a$$ in execution. He needs help again!

You know asymmetric key algorithms can help in above key management. All agents just need Agent X's public key, which is not even a secret, even enemies can know it. Let us explore this new cipher in some detail.

------------------------------------------- Problem Statement -------------------------------------------------
- Given a public key and multiple private keys, your task is to identify the correct private key that pairs with the given public key. The goal here is to understand the key structure.

------------------------------------------- Submission Details -------------------------------------------------
- Once correct key is identified, use the "rsa-utility.py" available in your labdirectory to get primes(p,q), modulus(n), totient value(phi) and encryption-decryption keys(d,e). But submit only the p, q, and d as obtained from the stdout (after running the python script) in the metadata.txt file.

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