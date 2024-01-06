## Challenge Name: Simple CTF
Category: Security, Enumeration, Privesc

Difficulty: Easy

Challenge Description: Beginner level ctf

### Approach

**1. <How many services are running under port 1000?> / Answer: 2**
  
  I ran an nmap scan with the -p flag to specify only the ports from 1-1000
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Ports.PNG>)


**2. <What is running on the higher port?> / Answer: ssh**
  
  Run same scan but adding the -sV flag for version detection.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Apache_Version.PNG>)


**3. <What's the CVE you're using against the application? > / Answer: CVE-2019-9053**
  
  I will take a look at the http server first.
  
  Seems like it just takes me to the default page. We can use gobuster and take a look at hidden directories.
  
  /simple seems interesting. Took me to a CMS Made Simple Website.
  
  Taking a look at the version on Exploit Database, I can try using SQL Injection.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Service.PNG>)

**4. <To what kind of vulnerability is the application vulnerable?> / Answer: sqli**
  
  Based on the information from before, I found that the version of the website is vulnerable to the SQL injection CVE.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Directories.PNG>)



**4. <What's the password?> / Answer: secret**
  
  The CVE from exploit database did not work.
  
  Found one from github that worked.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Reverse_Shell_Upload.PNG>)

 

    LINKS:
     https://github.com/Mahamedm/CVE-2019-9053-Exploit-Python-3
     

**4. <Where can you login with the details obtained?> / Answer: ssh**
  
  I'll try FTP first with username mitch and password secret.
  
  Doesn't seem to work.
  
  SSH? Works.


  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Python.PNG>)


    LINKS:


**5. <What's the user flag?> / Answer: G00d j0b, keep up!**
	
	No problem reading the file


**6. <Is there any other user in the home directory? What's its name?> / Answer: sunbath**
    
    If I go back a directory I can see the users.
    
    Seems like another user named sunbath
    
    
**7. <What can you leverage to spawn a privileged shell?> / Answer: vim**
   
   No interest SUID files appear.
   
   Can I see the sudo permissions? Yes.
   
   vim can run as root, I can use gtfobins.
   
   Following gtfobins, I am now root!

	
    ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Python.PNG>)

**5. <What's the root flag?> / Answer: W3ll d0n3. You made it!**
  
### Reflections

Overall, it was good practice. The instructions helped a lot as they served as clues on what to do next.
  

---
[Back to home](<https://github.com/saucea/CTFs/blob/main/README.md>)
