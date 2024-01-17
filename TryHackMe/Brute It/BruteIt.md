## Challenge Name: Brute It
Category: Security, Brute Force, Hash Cracking, Privilege Escalation

Difficulty: Easy

Challenge Description: Learn how to brute, hash cracking and escalate privileges in this box!

### Approach

**1. <How many ports are open?> / Answer: 2**
  
  Running a simple nmap scan, I can see the ports 22 and 80 are running ssh and http respectively.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Brute%20It/Screenshots/nmap_scan_ports.png>)


**2. <What version of SSH is running?> / Answer: OpenSSH 7.6p1**
  
  With the scan from before, I added the -sV flag to show the versions of the service.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Brute%20It/Screenshots/nmap_scan_ssh_version.png>)


**3. <What version of Apache is running?> / Answer: 2.4.29**
  
  Same as before, the -sV flag showed me the version of Apache running.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Brute%20It/Screenshots/nmap_scan_apache_version.png>)

**4. <Which Linux distribution is running?> / Answer: Ubuntu**
  
  I can see this in the nmap scan.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Brute%20It/Screenshots/nmap_scan_distribution.png>)

**5. <Search for hidden directories on web server. What is the hidden directory?> / Answer: /admin**
  
  I can run gobuster with a wordlist, where I found an interesting directory (/admin).
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Brute%20It/Screenshots/gobuster_scan.png>)

**6. <What is the user:password of the admin panel?> / Answer: admin:xavier**

  The username was written on a comment when I was inspecting the website's code.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Brute%20It/Screenshots/http_comment_admin.png>)
  
  I need to force my way using hydra for an http-post.
  
  Checking with the previous username and a random password, I inspected the website and checked the Network tab. There, I headed to the POST method and looked at the request payload which contained the Raw format I can use for hydra.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Brute%20It/Screenshots/http_post_form.png>)
  
  And Cracked!
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Brute%20It/Screenshots/hydra_http_post_cracked.png>)
  
    LINKS:
  	  https://infinitelogins.com/2020/02/22/how-to-brute-force-websites-using-hydra/

**7. <Crack the RSA key you found. What is John's RSA private Key passphrase?> / Answer: rockinroll**
  
  The RSA key was on the website after putting the correct username and password. I copied it to my device.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Brute%20It/Screenshots/rsa_key_website.png>)
  
  Using ssh2john, I can quickly get the passphrase.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Brute%20It/Screenshots/ssh2john_cracked.png>)
  
    LINKS:
  		https://null-byte.wonderhowto.com/how-to/crack-ssh-private-key-passwords-with-john-ripper-0302810/
    
**8. <user.txt?> / Answer: THM{a_password_is_not_a_barrier}**
  
  I can now login to ssh as john with the previous private key using the passphrase cracked with john.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Brute%20It/Screenshots/ssh_login.png>)
  
**9. <Web flag?> / Answer: THM{brut3_f0rce_is_e4sy}**
  
  Found on the website after logging in with previous credentials.
  
**10. <What is the root's password?> / Answer: football**
  
  Checking permissions I can run, cat can be used as root with no password. This means I can read the /etc/passwd and /etc/shadow files.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Brute%20It/Screenshots/sudo_permissions.png>)
  
  First I need to unshadow them and use john to crack the password.
  
  Cracked and I am now root!
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Brute%20It/Screenshots/unshadowed_text.png>)
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Brute%20It/Screenshots/root_access.png>)
  
    LINKS:
  		https://erev0s.com/blog/cracking-etcshadow-john/
  
**11. <root.txt?> / Answer: THM{pr1v1l3g3_3sc4l4t10n}**
  
### Reflections

Good CTF to practice cracking with John and other tools. 
  

---
[Back to home](<https://github.com/saucea/CTFs/blob/main/README.md>)
