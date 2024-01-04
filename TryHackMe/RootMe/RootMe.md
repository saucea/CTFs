## Challenge Name: RootMe
Category: Security, Web, Linux, Privilege-Escalation

Difficulty: Easy

Challenge Description: A ctf for beginners, can you root me?

### Approach

**1. <Scan the machine, how many ports are open?> / Answer: 2**
  
  By running a simple nmap scan, I can see the ports 22 and 80 are running ssh and http respectively.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Ports.PNG>)


**2. <What version of Apache is running?> / Answer: 2.4.29**
  
  I ran a similar scan but adding the -sV flag for version detection.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Apache_Version.PNG>)


**3. <What service is running on port 22?> / Answer: ssh**
  
  From my previous scan, ssh is detected on port 22.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Service.PNG>)

**4. <What is the hidden directory?> / Answer: /panel/**
  
  I ran gobuster with a wordlist of common directories names. Two interesting directories seem of use (/panel and /uploads). Seems like a reverse shell can be uploaded to /panel.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Directories.PNG>)

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Panel_Directory.PNG>)


**4. <Find a form to upload and get a reverse shell, and find the flag.> / Answer: THM{y0u_g0t_a_sh3ll}**
  
  I tried uploading a pre-made PHP Reverse Shell from a github repository but an error appeared that didn't allowed PHP files.

  Can I try bypassing it by changing the file's extension?

  After trying a few alternate extensions for a php file, .php3 worked.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Reverse_Shell_Upload.PNG>)

  I could now switch to the /uploads directory that we found using gobuster before. I first setup a netcat server and ran the reverse shell.

  I'm in!

  It seems that we need to find a file named **user.txt**. Let's use the find command.

  Success!

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/First_Flag.PNG>)

  LINKS:
  
    https://github.com/pentestmonkey/php-reverse-shell
    https://vulp3cula.gitbook.io/hackers-grimoire/exploitation/web-application/file-upload-bypass

**4. <Search for files with SUID permission, which file is weird?> / Answer: /usr/bin/python**
  
  I searched through the files with SUID permission using the find command.

  Python? Can I use it to escalate to root?

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Python.PNG>)

  Looks like we can follow gtfobins for this.

  Success! I am now Root!

  Flag: THM{pr1v1l3g3_3sc4l4t10n}

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Root.PNG>)

  LINKS: 
    
    https://gtfobins.github.io/gtfobins/python/
    https://docs.oracle.com/cd/E19683-01/816-4883/6mb2joatb/index.html

  
### Reflections

Overall, it was good practice. The instructions helped a lot as they served as clues on what to do next.
  

---
[Back to home](<https://github.com/saucea/CTFs/blob/main/README.md>)
