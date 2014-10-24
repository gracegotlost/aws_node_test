aws_node_test
=============
– set up your remote computer with EC2 (Elastic Cloud)

1. Go to http://aws.amazon.com
2. Sign up, if you haven't already
	– you will need credit/debit card + phone verification
	– You get 1-year free under micro t2 tier if you're new member.
3. Sign in to the Console
4. You arrive at AWS console that presents bunch of services and tools
5. Select EC2 under Compute & Networking
6. On top-right corner, change the server location to N.Virginia since it is closer to us
7. We are ready to create an INSTANCE, typically means the SERVER
	– Go to Instances
	– Select Ubuntu Server 14.04 LTS (HVM), SSD Volume Type
	– Select t2.micro (Free tier eligible)
	– Edit security groups
		– Add port 445, 80, 8080, and range of 3000-4000
		– In doing this, we allow connections on these port numbers
	– Launch Instance
	– Create a new key pair, name it 'myKey01', Hit Download Key Pair
	– Launch Instance

8. You will wait until Status Checks change from "Initializing" to "2/2 checks passed"
9. In your instance Description,
	– Copy Public IP, also remember it for further use
10. In Terminal,
	– Change permission of myKey01.pem we just donwload
	– sudo chmod 0600 ~/Download/myKey01.pem
	– ssh ubuntu@your_public_ip -i ~/Download/myKey01.pem
11. You are INSIDE YOUR REMOTE COMPUTER!
12. Let's add a user and configure some ssh
	– sudo adduser “yourname”
	- Enter password
13. Add user to ADMIN group
	- sudo visudo
	– follow ROOT configuration
	– edit sshd config
	– sudo nano /etc/ssh/sshd_config
	– See my guiding
14. Update and Install apps
	- sudo add-apt-repository ppa:chris-lea/node.js
	- sudo apt-get update
	- sudo apt-get install nodejs samba
	- alias node=nodejs
	- sudo npm install -g forever nodemon
15. Configure samba and mount it
https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20(Command-line%20interface/Linux%20Terminal)%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!

	- sudo nano /etc/samba/smb.conf
	In your “share” folder
	- sudo chmod -R 0777 .

edit

	- sudo restart smbd

16. In your mac, from Finder, Go > Connect to server.
	– smb://your-ip-of-the-server
