Preamble: Agent X has to share some documents and images periodically with other agents. Knowing the pitfalls of classical cryptography (remember Mr. Mogambo from earlier exercises!), he decided to go with modern cryptography, specifically symmetric key ciphers. He needs help encrypting and decrypting messages.
We will first specify the activity you need to perform. Guidance on how to perform the activity is given further below.

------------------------------ AES Encryption ------------------------------

Don’t worry, Agent X is not going to ask you to implement a symmetric key cipher 😊 Agent X is using a software that relies on openssl library for providing confidentiality. This is a good “crypto” library that, among many other things, implements symmetric ciphers also. Let su check it out.

Use the "secret.txt" file given in “/home/labDirectory/part1/” folder to encrypt the data in "secret.txt" file as per below.
	- Key = 55110062015112014aaff2d1f
	- IV = 01020304055040302010 (If needed)
	- Encryption Algorithm: AES-128 with ECB and CTR mode
- Encryption Algorithm: AES-256 with CBC, CFB and OFB mode
- Create different output files (i.e. ciphertext as per above), and then create the md5sum of the encrypted files and submit the md5sum (total 5, see submission details below). Note, you can create md5sum of the output file output.bin via: "md5sum output.bin"
- PLEASE DO NOT CHANGE ANY TEXT IN "SECRET.TXT" FILE AS IT WILL AFFECT FINAL MD5SUM TOO

Submission Details:
- In "flags.txt" file, put all the computed md5sum in separate lines (5 in total)

**GUIDANCE**
- openssl enc is the command to encrypt/decrypt a file. This is what is of interest to us now. You can type "man enc" to know more. See this as well https://wiki.openssl.org/index.php/Enc.
- An example usage is openssl enc -aes-128-cbc -e -in plain.txt -out cipher.bin -K 00112233445566778889aabbccddeeff -iv 0102030405060708; where you are asking to encrypt the input plain.txt using AES algorithm with 128 bit key in CBC block mode. The cipher text is to be written in cipher.bin. The key (-K) and IV (-iv) to be used are also specified, expressed in hexadecimal.

--------------------------------------AES Decryption---------------------------------------------
Go to a different folder, “/home/labDirectory/part2/” for this exercise. You are given a ciphertext “/home/labDirectory/part2/secret.bin”. Here, we will see how to decrypt the same. You know the algorithm used is AES. You also found the key and the IV used (given below). But you don’t know which block mode has been used. Using this information, decrypt the ciphertext and submit the plaintext in the form of a flag in the flag.txt file in the appropriate folder.
	- Key: 11152569842abcfdd5116
	- IV: 102030506070ddff
	- Encryption Algorithm: AES
	- Block Modes: It can be any of the CBC, ECB, CFB, OFB, CTR

Submission Details:
- Put the flag you found after decrypting the secret in "flags.txt" file
