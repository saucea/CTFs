## Challenge Name: Lazy Admin
Category: Security, Linux

Difficulty: Easy

Challenge Description: Easy linux machine to practice your skills

### Approach

**1. <What is the user flag?> / Answer: THM{63e5bce9271952aad1113b6f1ac28a07}**
  
  I ran a simple nmap scan first to see which services are available.
  
  SSH on port 22 and http on port 80. I'll look at the http server first to find if there is anything on there.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Lazy%20Admin/Screenshots/Nmap_Scan.png>)
  
  It first takes me to the default page. Nothing seems to be out of the ordinary. I'll do a scan to see if there are any hidden directories.
  
  Seems like the main website is on a directory called /content. While checking on it, there is nothing interesting. Running another scan though takes me to 2 interesting directories, /as and /inc. /as is a login page, I could try to force my way in but while looking at /inc, a mysql backup was in there containing the username and password.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Lazy%20Admin/Screenshots/gobuster_scan.png>)

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Lazy%20Admin/Screenshots/gobuster_scan_2.png>)

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Lazy%20Admin/Screenshots/login_page.png>)
  
  The username is stored in plaintext as “manager”, while the password seems to be stored as a hash. Running an identifier, it was stored as MD5. Now using a decrypt tool, I got the password “Password123”.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Lazy%20Admin/Screenshots/mysql_backup.png>)

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Lazy%20Admin/Screenshots/hash_identifier.png>)

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Lazy%20Admin/Screenshots/hash_decrypt.png>)
  
  I'm in!
  
  Searching through the content, it seems we can upload a reverse shell on the "Ads" column. I'll use the code from a reverse shell I found online.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Lazy%20Admin/Screenshots/Ads_code.png>)

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Lazy%20Admin/Screenshots/reverse_shell_file.png>)
  
  And I got access!

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Lazy%20Admin/Screenshots/reverse_shell_access.png>)
  
  There is a user named itguy that contains a file named user.txt, the first flag!

    LINKS:
      https://github.com/pentestmonkey/php-reverse-shell

**2. <What is the root flag?> / Answer: THM{6637f41d0177b6f37cb20d775124699f}**
  
  Now checking permissions, I can run backup.pl file as root. It seems to use a file named /etc/copy.sh containing a reverse shell. I have necessary permissions to edit this file, so all I have to do is change the ip to mine.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Lazy%20Admin/Screenshots/sudo_permissions.png>)

  Running the backup.pl file, I am now root!

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/Lazy%20Admin/Screenshots/root_access.png>)

  
### Reflections

Good practice for getting a grasp on reverse shells and how they work. Also helped with permissions on linux.
  

---
[Back to home](<https://github.com/saucea/CTFs/blob/main/README.md>)
