## Challenge Name: Agent Sudo
Category: Enumerate, Exploit, Brute-Force, Hash Cracking

Difficulty: Easy

Challenge Description: You found a secret server located under the deep sea. Your task is to hack inside the server and reveal the truth.

### Approach

**1. <How many open ports?> / Answer: 3**
  
  By running a simple nmap scan, I can see the ports 21, 22 and 80 are running ftp, ssh and http respectively.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Agent%20Sudo/Screenshots/nmap_scan.png>)


**2. <How you redirect yourself to a secret page?> / Answer: user-agent**
  
  Checking the http server, we are prompted with a text saying we need to use our user-agent.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Agent%20Sudo/Screenshots/redirect_secret_page.png>)


**3. <What is the agent name?> / Answer: chris**
  
  I can try intercepting the request through Burp.
  
  Given from the previous text, we had someone named Agent R.
  
  I'll try doing different Agents to see if one works.
  
  Agent C works and we have the page!

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Agent%20Sudo/Screenshots/user_agent_chris.png>)

**4. <FTP password?> / Answer: crystal**
  
  Seems like chris' password is weak, I'll try to force my way in using hydra.
  
  Got it!
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Agent%20Sudo/Screenshots/chris_hydra_cracked.png>)


**5. <Zip file password?> / Answer: alien**
  
  Logging in to the ftp server using the credentials from before, I downloaded 3 files to my own computer.  
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Agent%20Sudo/Screenshots/ftp_files.png>)

  One of the text files tells us information about Agent J's password stored in one of the photos.
  
  I'll check for steganography with binwalk, which searches for embedded files.
  
  cutie.png has a zip file and a txt file that I extracted. Seems to be password protected. I'll use John.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Agent%20Sudo/Screenshots/binwalk_picture.png>)
  
  And cracked!

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Agent%20Sudo/Screenshots/zip_file_password.png>)
  
  We get a new message now with a code.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Agent%20Sudo/Screenshots/to_agent_R_text_file.png>)

    LINKS:
      https://medium.com/@ujjawal.soni2002/cracking-a-password-protected-zip-file-using-john-the-ripper-f39e657cbfa8

**6. <steg password?> / Answer: Area51**
  
  The code seems to be in Base64.
  
  Running it on a decoder, we get the password.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Agent%20Sudo/Screenshots/base64_decode.png>)

    LINKS: 
      https://hashes.com/en/tools/hash_identifier
      https://www.base64decode.org
      

**7. <Who is the other agent (in full name)?> / Answer: james**
  
  When testing steghide on the photos, it seems like cute-alien.jpg has something hidden on it.
  
  Test the new password we got.
  
  Got a file!

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Agent%20Sudo/Screenshots/steghide_extract.png>)
  
**8. <SSH password?> / Answer: hackerrules!**
  
  The password was on the file from before.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Agent%20Sudo/Screenshots/message_text.png>)
  
**9. <What is the user flag?> / Answer: b03d975e8c92a7c04146cfa7a5a313c7**
  
  Logging in with the previous username and password, the first flag is there.
  
**10. <What is the incident of the photo called?> / Answer: Roswell alien autopsy**
  
  A quick google search of the image tells me about the picture.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Agent%20Sudo/Screenshots/alien_autopsy.png>)
  
**11. <CVE number for the escalation?> / Answer: CVE-2019-14287**
  
  Seeing the commands, I can run bash but it is different than before. Instead of NOPASSWD, it has !root.
  
  Looking up, there is an exploit in Exploit-DB.

    LINKS:
      https://www.exploit-db.com/exploits/47502
  
**12. <What is the root flag?> / Answer: b53a02f55b57d4439e3341834d70c062**
  
  I downloaded the exploit to my computer and then setup an http server to transfer it to the attacking computer.
  
  Once downloaded, I ran the script and I am root!

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Agent%20Sudo/Screenshots/sudo_access.png>)
  
### Reflections

Lengthy one, helped me improve my steganography skills as well as improve my cracking skills.
  

---
[Back to home](<https://github.com/saucea/CTFs/blob/main/README.md>)
