Preamble: Agent X has installed a spy Agent Z in the enemy organization. This spy works as a secretary under Mr. Gabbar. 
Mr. Gabbar currently trusts Agent Z as a secretary (and not for anything that involves high security) and Agent X wants to exploit this trust to get a signed document from Gabbar that gives permission 
to Agent Z to enter a high-security area (and once there steal some documents).
Agent Z cannot just sneak in such a document (like shown in bollywood movies) and get Gabbar’s signature. 
Gabbar reads everything carefully before signing. And note we are dealing with digital signatures, not some pen based signature. 
And Gabbar signs a hash of messages and not the message directly (he is smarter than Mogambo).

------------------------------------------ Problem Statement -------------------------------------
Exercise 1: Weak collision property

You decided to go with the following strategy. 
You have a routine “office order” (permissions.txt in "/home/labDirectory/part1" folder) that Agent Z can make Gabbar sign. 
You are also given an "evil-permission.txt" (in "/home/labDirectory/part1" folder) which has an extra permission in it to give high-security entry to Agent Z. 
Your task is to now manipulate "evil-permissions.txt" in such a way that it's MD5 hash'es first 16 bits (4 characters) match to "permissions.txt" file's MD5 hash's first 16 bits (4 characters)

This essentially boils down to breaking the weak collision property of a hash.

**NOTE**: There will be a special line in permissions file which has statement relating to "Unique Bytes Dump". Do not change this line as it is important for uniqueness of your lab work.

Guidance:
- We will use the brute-force method to see how long it takes to break this property.
- Most of the hash functions are quite strong against the brute-force attack and it will take us years to break them. To make the task feasible, we will reduce the length of the hash value to 16 bits. Use the first 16 bits of MD5 hash function for this lab.
- Keep on modifying spaces in evil-permissions.txt and recalculating its hash till it matches (first 16 bits) with that of permissions.txt. (Write a program/script to do this automatically in loop)
- If you want to reset the files given to you, you can use "reset.sh" the bash script available in "/home/labDirectory/part1" directory. 
	
Exercise 2: Strong Collision Property

Darn! Above is taking too long to break. You want your approach to be more efficient. You heard about the birthday problem and decided to adopt that strategy in your solution. 
So, you decided to create versions of permissions1.txt as well and find any version of permissions1.txt whose hash matches any version of permissions2.txt. This essentially boils down to breaking the strong collision property of a hash.

Guidance:
You have been given permissions1.txt and permissions2.txt in "/home/labDirectory/part2/" which contains some content which was originally meant to be sent. You task is to make changes to both permissions1.txt and permissions2.txt in such a way that they differing only in spaces and when MD5 hash is calculated from them, they have same first 16 bits in their MD5 hash. (Write a program/script to do this automatically in loop)
- If you want to reset the files given to you, you can use "reset.sh" the bash script available in "/home/labDirectory/part2" directory.

**NOTE**: There will be a special line in permissions file which has statement relating to "Unique Bytes Dump". Do not change this line as it is important for uniqueness of your lab work.

Reference: https://www.researchgate.net/profile/Ganesh_Gupta4/publication/271704029_What_is_Birthday_attack/links/54cfbdcc0cf24601c0958a1e/What-is-Birthday-attack.pdf

----------------------------------------- Submission Details -------------------------------------------
- Weak Collision: evil-permissions.txt(different from permissions.txt) such that its hash matches in first 16 bit to that of permissions.txt given.
- Strong Collision: permissions1.txt and permissions2.txt  (permissions1.txt is the modified one, should differ in spaces from that provided), such that they are different in content but have same first 16 bit of hash.
      