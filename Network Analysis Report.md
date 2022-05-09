## Network Analysis

### Time Thieves

At least two users on the network have been wasting time on YouTube. Usually, IT wouldn't pay much mind to this behavior, but it seems these people have created their own web server on the corporate network. So far, Security knows the following about these time thieves:

  ●	They have set up an Active Directory network.

●	They are constantly watching videos on YouTube.

●	Their IP addresses are somewhere in the range 10.6.12.0/24.

You must inspect your traffic capture to answer the following questions:
1.	What is the domain name of the users' custom site? Frank-n-Ted-DC.Frank-n-Ted.com

![11](https://user-images.githubusercontent.com/92223941/167333195-9ebedd09-b922-4d6c-98bf-79eab2a99372.PNG)


 
2.	What is the IP address of the Domain Controller (DC) of the AD network? 10.6.12.12

![12](https://user-images.githubusercontent.com/92223941/167333273-daabede7-d7fb-4791-86ba-1c8e9c9e6290.PNG)

 
3.	What is the name of the malware downloaded to the 10.6.12.203 machine? Once you have found the file, export it to your Kali machine's desktop. June11.dll

![31](https://user-images.githubusercontent.com/92223941/167333501-329220bd-e3d0-428f-a402-ee30b951f112.PNG)
![312](https://user-images.githubusercontent.com/92223941/167333541-1dd1fc6d-d743-471c-a139-15742d68474c.PNG)



 
 

4.	Upload the file to VirusTotal.com. What kind of malware is this classified as? Trojan

![4](https://user-images.githubusercontent.com/92223941/167333616-c988aa4e-b5f3-4032-a5de-54bddddad9e2.PNG)


 

### Vulnerable Windows Machines

The Security team received reports of an infected Windows host on the network. They know the following:

●	Machines in the network live in the range 172.16.4.0/24.

●	The domain mind-hammer.net is associated with the infected computer.

●	The DC for this network lives at 172.16.4.4 and is named Mind-Hammer-DC.

●	The network has standard gateway and broadcast addresses.

Inspect your traffic to answer the following questions:
1.	Find the following information about the infected Windows machine:

    ○	**Host name:** Rotterdam-PC
   
    ○	**IP address:** 172.16.4.205
  
    ○	**MAC address:** 00:59:07:b0:63:a4
    
    ![1b](https://user-images.githubusercontent.com/92223941/167333687-e44cfc1d-9136-43a5-aa9e-5f2b1f1df8bb.PNG)

 
2.	What is the username of the Windows user whose computer is infected? Matthijs.devries

![2b](https://user-images.githubusercontent.com/92223941/167333758-0a3b6781-9a49-4b8a-9360-ada462cbcf00.PNG)

 
3.	What are the IP addresses used in the actual infection traffic? 172.16.4.205, 185.243.115.84, 166.62.11.64

![3b](https://user-images.githubusercontent.com/92223941/167333790-f177d057-023d-44f0-b3bf-c9b7a7c3747a.PNG)

 
4.	As a bonus, retrieve the desktop background of the Windows host.

### Illegal Downloads

IT was informed that some users are torrenting on the network. The Security team does not forbid the use of torrents for legitimate purposes, such as downloading operating systems. However, they have a strict policy against copyright infringement.

IT shared the following about the torrent activity:

●	The machines using torrents live in the range 10.0.0.0/24 and are clients of an AD domain.

●	The DC of this domain lives at 10.0.0.2 and is named DogOfTheYear-DC.

●	The DC is associated with the domain dogoftheyear.net.

Your task is to isolate torrent traffic and answer the following questions:
1.	Find the following information about the machine with IP address 10.0.0.201:

    ○	**MAC address:** 00:16:17:18:66:c8
  
    ○	**Windows username:** elmer.blanco
  
    ○	**OS version:** Windows NT 10.0
    
    ![1c1](https://user-images.githubusercontent.com/92223941/167333855-261387b4-1c3a-4184-9480-49c644cdc6ce.PNG)
    ![1c2](https://user-images.githubusercontent.com/92223941/167333874-20f18be9-7195-465c-9f27-cbb96e6012ec.PNG)


 
 
2.	Which torrent file did the user download? Betty_Boop_Rythm_on_the_Reservation.avi.torrent

![2c](https://user-images.githubusercontent.com/92223941/167333914-2b06bad0-f94a-4b4c-b6a3-58979b355059.PNG)


