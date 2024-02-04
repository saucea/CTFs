## Challenge Name: OhSINT
Category: OSINT, Internet, Dorks

Difficulty: Easy

Challenge Description: Are you able to use open source intelligence to solve this challenge?

### Approach

**1. <What is this user's avatar of?> / Answer: cat**
  
  Using a tool like ‘exiftool’, I looked at the information of the picture. I found a copyright by “OWoodflint”.
  
  Seaching this name on Google, I found a twitter user.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Ports.PNG>)

**2. <What city is this person in?> / Answer: London**
  
  I also found a github with the same username and a repository for a social network project.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Apache_Version.PNG>)

**3. <What is the SSID of the WAP he connected to? > / Answer: UnileverWiFi**
  
  Taking a look at the twitter account, there was a post with a Bssid.
  
  Using this info on a bssid lookup, I found the SSID of the WAP.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Service.PNG>)
  
    LINKS:
      https://github.com/Mahamedm/CVE-2019-9053-Exploit-Python-3

**4. <What is his personal email address?> / Answer: OWoodflint@gmail.com**
  
  From the same Github that I found before, his email was also included.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Directories.PNG>)

**5. <What site did you find his email address on?> / Answer: Github**
  
    LINKS:
      https://github.com/Mahamedm/CVE-2019-9053-Exploit-Python-3
     
**6. <Where was he gone on holiday?> / Answer: New York**
  
  A link to a wordpress site was included. However, the site was removed.
  
  I searched on the Wayback Machine to see the history of the site.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Python.PNG>)

    LINKS:
		  https://web.archive.org/web/20210525030508/https://oliverwoodflint.wordpress.com/

**7. <What is the person's password?> / Answer: pennYDr0pper.!**
	
  Searching through the source code, there was hidden text.
	
  It can also be seen by highlighting the text.
	
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Python.PNG>)
	
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/RootMe/Screenshots/Python.PNG>)
  
---
[Back to home](<https://github.com/saucea/CTFs/blob/main/README.md>)
