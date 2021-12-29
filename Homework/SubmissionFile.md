## Week 16 Homework Submission File: Penetration Testing 1

#### Step 1: Google Dorking


- Using Google, can you identify who the Chief Executive Officer of Altoro Mutual is:
	Yes you can. With just a few searches you can find him easy. He is Karl Fitzgerald
- How can this information be helpful to an attacker:
	This information is useful to an attacker for the reasons the know who to go after. Their main target and or the best course of action to get to that target. If that information is being shown
	this will allow the attacker to set up an attack flow and who the best targets are going to be. Because not only is the google search showing him, its also showing the title holders.

#### Step 2: DNS and Domain Discovery

Enter the IP address for `demo.testfire.net` into Domain Dossier and answer the following questions based on the results:

  1. Where is the company located:
	Dallas Texas  

  2. What is the NetRange IP address:
	65.61.137.64 - 65.61.137.127

  3. What is the company they use to store their infrastructure:
	Rackspace Backbone Engineering

  4. What is the IP address of the DNS server:
	117.137.61.65

#### Step 3: Shodan

- What open ports and running services did Shodan find:
	the open ports for this are 80.443.8080
#### Step 4: Recon-ng

- Install the Recon module `xssed`.
	marketplace install xssed 
- Set the source to `demo.testfire.net`.
	options set source demo.testfire.net 
- Run the module. 
	run

Is Altoro Mutual vulnerable to XSS: 	
	yes Altoro is vulnerable to cross-site. It is still unfixed since the published mirror on16/12/2011 (xssed.com/mirror/57864/)

### Step 5: Zenmap

Your client has asked that you help identify any vulnerabilities with their file-sharing server. Using the Metasploitable machine to act as your client's server, complete the following:

- Command for Zenmap to run a service scan against the Metasploitable machine: 
	sudo zenmap to open zenmap. then you will select the type of profile(Type of Scan levels)
	and then set the Target parameters to the domain or the ip address, you want to scan. then in the command line use it as a command line for nmap
	nmap -T4 -A -v is running an intense sacn on the target you have selected.
	![image](Images/ZenMapScans.PNG)
 
- Bonus command to output results into a new text file named `zenmapscan.txt`:
	nmap -T4 -A -v -oN zenmapscan.txt 192.168.0.10 
	![image](Images/CommandtoTxt.PNG)

- Zenmap vulnerability script command:
	you would want to run the nmap --script smb-enum-shares 192.168.0.10
	little bonus command I wanted to try. nmap -oN Scriptoutput.txt --script smb-enum-shares 192.168.0.10
	![image](Images/OutputScript.PNG) 

- Once you have identified this vulnerability, answer the following questions for your client:
  1. What is the vulnerability:	
	this vulnerability is targeting the list of shares that belong on the server. This could be anywhere from private files on the webserver, and or just the location of which the company use.

  2. Why is it dangerous:
	This is dangerous because you do not want to allow hackers to infect the share location. People become use to going into the share and seeing it and forwarding it out without even looking.


  3. What mitigation strategies can you recommendations for the client to protect their server:
	Please close these ports. Secondly I would train my team members to look at the email before forwarding it and or opening items.


