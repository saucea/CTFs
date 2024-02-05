## Challenge Name: OhSINT
Category: OSINT, Internet, Dorks

Difficulty: Easy

Challenge Description: Are you able to use open source intelligence to solve this challenge?

### Approach

**1. <What is this user's avatar of?> / Answer: cat**
  
  Using a tool like ‘exiftool’, I looked at the information of the picture. I found a copyright by “OWoodflint”.
  
  Seaching this name on Google, I found a twitter user.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/OhSINT/Screenshots/copyright_name.png>)

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/OhSINT/Screenshots/twitter_cat_profile.png>)

**2. <What city is this person in?> / Answer: London**
  
  I also found a github with the same username and a repository for a social network project.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/OhSINT/Screenshots/github_location.png>)

**3. <What is the SSID of the WAP he connected to? > / Answer: UnileverWiFi**
  
  Taking a look at the twitter account, there was a post with an Bssid.
  
  Using this info on a bssid lookup, I found the SSID of the WAP.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/OhSINT/Screenshots/bssid_twitter.png>)
  
    LINKS:
      https://www.wigle.net/

**4. <What is his personal email address?> / Answer: OWoodflint@gmail.com**
  
  From the same Github that I found before, his email was also included.

  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/OhSINT/Screenshots/github_email.png>)

**5. <What site did you find his email address on?> / Answer: Github**
  
    LINKS:
      https://github.com/OWoodfl1nt/people_finder
     
**6. <Where was he gone on holiday?> / Answer: New York**
  
  A link to a wordpress site was included. However, the site was removed.
  
  I searched on the Wayback Machine to see the history of the site.
  
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/OhSINT/Screenshots/wordpress_site_holiday.png>)
	
    LINKS:
      https://web.archive.org/web/20210525030508/https://oliverwoodflint.wordpress.com/

**7. <What is the person's password?> / Answer: pennYDr0pper.!**
	
  Searching through the source code, there was hidden text.
	
  It can also be seen by highlighting the text.
	
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/OhSINT/Screenshots/site_password.png>)
	
  ![img](<https://github.com/saucea/CTFs/blob/main/TryHackMe/OhSINT/Screenshots/site_password_highlight.png>)
  
---
[Back to home](<https://github.com/saucea/CTFs/blob/main/README.md>)
