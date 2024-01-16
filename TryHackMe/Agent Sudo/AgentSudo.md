## Challenge Name: Agent Sudo
Category: Enumerate, Exploit, Brute-Force, Hash Cracking

Difficulty: Easy

Challenge Description: You found a secret server located under the deep sea. Your task is to hack inside the server and reveal the truth.

### Approach

**1. <How many open ports?> / Answer: 3**
  
  By running a simple nmap scan, I can see the ports 21, 22 and 80 are running ftp, ssh and http respectively.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Ports.PNG>)


**2. <How you redirect yourself to a secret page?> / Answer: user-agent**
  
  Checking the http server, we are prompted with a text saying we need to use our user-agent.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Apache_Version.PNG>)


**3. <What is the agent name?> / Answer: chris**
  
  I can try intercepting the request through Burp.
  
  Given from the previous text, we had someone named Agent R.
  
  I'll try doing different Agents to see if one works.
  
  Agent C works and we have the page!

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Service.PNG>)

**4. <FTP password?> / Answer: crystal**
  
  Seems like chris' password is weak, I'll try to force my way in using hydra.
  
  Got it!
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Directories.PNG>)


**5. <Zip file password> / Answer: alien**
  
  Logging in to the ftp server using the credentials from before, I downloaded 3 files to my own computer  
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Reverse_Shell_Upload.PNG>)

  One of the text files tells us information about Agent J's password stored in one of the photos.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/First_Flag.PNG>)
  
  I'll check for steganography with binwalk, which searches for embedded files.
  
  cutie.png has a zip file and a txt file that I extracted. Seems to be password protected. I'll use John.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/First_Flag.PNG>)
  
  And cracked!
  
  We get a new message now with a code.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/First_Flag.PNG>)

    LINKS:
      https://github.com/pentestmonkey/php-reverse-shell
      https://vulp3cula.gitbook.io/hackers-grimoire/exploitation/web-application/file-upload-bypass

**6. <steg password?> / Answer: Area51**
  
  The code seems to be in Base64.
  
  Running it on a decoder, we get the password.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Root.PNG>)

    LINKS: 
      https://gtfobins.github.io/gtfobins/python/
      https://docs.oracle.com/cd/E19683-01/816-4883/6mb2joatb/index.html

**7. <Who is the other agent (in full name)?> / Answer: jamessteg**
  
  When testing steghide on the photos, it seems like cute-alien.jpg has something hidden on it.
  
  Test the new password we got.
  
  Got a file!

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Root.PNG>)
  
**8. <SSH password?> / Answer: hackerrules!**
  
  The password was on the file from before.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Root.PNG>)
  
**9. <SSH password?> / Answer: hackerrules!**
  
  The password was on the file from before.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Root.PNG>)
  
**10. <What is the user flag?> / Answer: b03d975e8c92a7c04146cfa7a5a313c7**
  
  Logging in with the previous username and password, the first flag is there.
  
**11. <What is the incident of the photo called?> / Answer: Roswell alien autopsy**
  
  A quick google search of the image tells me about the picture.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Root.PNG>)
  
**12. <CVE number for the escalation?> / Answer: CVE-2019-14287**
  
  Seeing the commands, I can run bash but it is different than before. Instead of NOPASSWD, it has !root.
  
  Looking up, there is an exploit in Exploit-DB.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Root.PNG>)
  
**13. <What is the root flag?> / Answer: b53a02f55b57d4439e3341834d70c062**
  
  I downloaded the exploit to my computer and then setup an http server to transfer it to the attacking computer.
  
  Once downloaded, I ran the script and I am root!

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Root.PNG>)
  
### Reflections

Overall, it was good practice. The instructions helped a lot as they served as clues on what to do next.
  

---
[Back to home](<https://github.com/saucea/CTFs/blob/main/README.md>)
