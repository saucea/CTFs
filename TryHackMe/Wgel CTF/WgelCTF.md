## Challenge Name: Wgel CTF
Category: Security

Difficulty: Easy

Challenge Description: Can you exfiltrate the root flag?

### Approach

**1. <User flag?> / Answer: 057c67131c3d5e42dd5cd3075b198ff6**
  
  Running an nmap scan: ssh on port 22 and http on port 80.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Wgel%20CTF/Screenshots/nmap_scan.png>)
  
  Checking the default page, there is a comment including the name “Jessie”.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Wgel%20CTF/Screenshots/jessie_comment.png>)
  
  Doing a scan of hidden directories, I was able to find what seems like the main page on /sitemap. Seems normal but doing another scan I found an ssh private key on /.ssh.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Wgel%20CTF/Screenshots/gobuster_first_scan.png>)
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Wgel%20CTF/Screenshots/ssh_private_key.png>)
  
  Copying the private key to my system and changing to its appropiate permissions (chmod 600), I can try logging in as jessie from the previous comment I found.
  
  I'm in!
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Wgel%20CTF/Screenshots/ssh_login_priv_key.png>)
  
  Flag is inside the /Documents directory and I just cat to read it.
  

**2. <Root flag?> / Answer: b1b968b37519ad1daa6408188649263d**
  
  I checked the commands permissions and I can run wget as root with no password.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Wgel%20CTF/Screenshots/commands_permissions.png>)
  
  I can create a new sudoers file in my system to then download and replace the sudoers file on this system to gain root permissions.
  
  The sudoers file tells you which commands a user can run, so now I can run any command without a password.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Wgel%20CTF/Screenshots/sudoers_file.png>)
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Wgel%20CTF/Screenshots/sudo_new_permissions.png>)
  
  I am now root and can read the flag inside the root directory!
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Wgel%20CTF/Screenshots/root_access.png>)

    LINKS:
      https://gtfobins.github.io/gtfobins/wget/

### Reflections

I learned a new privilege escalation technique that I did not know about. Other than that, it was a straightforward CTF.
  
---
[Back to home](<https://github.com/saucea/CTFs/blob/main/README.md>)
