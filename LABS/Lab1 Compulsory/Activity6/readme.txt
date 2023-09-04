Abusing Modular Arithmetic to exfiltrate secrets.

-----------------------------------------------------------------------------------------------------
Problem Statement:
- There is an application running on port 9001, which provides a feature wherein the application provides you with rsa public key pair (e,n), 
	and asks for cipher text to be decrypted by the private key of the application.
- The flow of application is:
 - You are given (e,n) by the application when you connect to it.
 - The application then asks for cipher text in long integer format. Here as a user you can encrypt some text , let's say "Hello World!" using (e,n) pair and submit it on application to get it decrypted by the application.
- The application however also has a secret cipher-text that is shown to you. You can't decrypt it since you don't have the private key of the application.
	 You can bruteforce it though, but it will take forever.
- You could pass the same cipher text to the application, but the application itself is self aware and won't decrypt it's own secret text.
- Your task is to trick the application into decrypting its own cipher text.
- **EXTRA**: Use “netcat” as tool to communicate to port 9001.
	- “nc -nv 127.0.0.1 9001”
- **HINT:** Modular Arithmetic used in RSA can be helpful. Look at how to forge a new ciphertext which includes already available ciphertext.
- **NOTE:** We have provided utility scripts in "/home/labDirectory/utils", which you can use as follows:
 - "encryptor.py": To create encrypted long number from plain text. Here you will need to change hard-coded n, and e inside the script itself. Usage: python3 encryptor.py "Example Text"
 - ascii-to-long-converter.py: To convert any plain text into long number. Usage: python3 ascii-to-long-converter.py "Example Text"
 - long-to-ascii-converter.py: To convert any long number to equivalent ascii plain text. Usage: python3 long-to-ascii-converter.py 21499996864371468652163463284

-----------------------------------------------------------------------------------------------------
Submission Details:
- Once you trick the application to reveal its secret, you will get a flag, submit it in "flags.txt" file in your labdirectory.
      