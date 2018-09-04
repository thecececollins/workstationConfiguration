## Setting up a Dev Machine

**Create remote connectivity from a PC:**
Install openSSH Server onto your linux machine
- On the linux machine's terminal type:
	sudo apt-get update
	sudo apt-get install openssh-server
	sudo ufw allow 22



**To access your linux terminal remotely:**
- Install PuTTY onto the PC: https://the.earth.li/~sgtatham/putty/latest/x86/putty.exe
- Type in your username, @, and then the linux machine's IP address (ex. username@10.15.0.xxx)
- Make sure the SSH option is selected underneath and the port is 22
- Add a name for the linux computer 
- Hit Save
- Now test it by either double clicking on the new entry in the list or selecting it and pressing Login
- You should see a Terminal window open asking for the password of your linux machine


**To access your linux machine's documents:**
- Install winSCP: https://winscp.net/download/WinSCP-5.9.1-Setup.exe
- Type in your username, @, and then your linux machine's IP address, you'll see it autofill for you into the appropriate fields (ex. username@10.15.0.xxx)
- Make sure the SFTP option is selected and the port is 22
- Hit Save
- Now test it by either double clicking on the new entry in the list or selecting it and pressing Login
- You should see a window open (very similar to FileZilla) with your PC's docs on the left and linux docs on the right


**Add Sudoer (sudo with NOPASSWD):**
- In terminal insert: `sudo visudo`
- Just under the line that looks like the following: `root ALL = (ALL) ALL`
- Add the following (replacing user with the actual username): `user ALL = (ALL) ALL`
- Add the following at the very end of the file (replacing user with the actual username): `user ALL = (ALL) NOPASSWD: ALL`
- Press Ctrl+X and press Y when prompted to save



**Set vi as editor in Terminal:**
- `set -o vi`


**$JAVA_HOME Configuration:**
_Goal: have Java 1.7 installed and an environment variable setup like this: echo $JAVA_HOME 
/usr/lib/jvm/java-7-openjdk-amd64_

- Uninstall all versions of Java:
	`sudo apt-get autoremove openjdk-7-jdk`
	`sudo apt-get autoremove openjdk-7-jre`
- Make sure all java items are removed from /usr/lib/jvm/
- Install Java 7
	`sudo add-apt-repository ppa:openjdk-r/ppa`
	`sudo apt-get update`
	`sudo apt-get install openjdk-7-jdk`
- Find the path, usually: /usr/lib/jvm/.....
- Edit the environment using vi
	- sudo vi /etc/environment
- Add to bottom of file
	- `JAVA_HOME="/usr/lib/jvm/java-7-openjdk-amd64"`
- Save /etc/envirenment
- Reload the environment file
	- `source /etc/environment`
- Verify the change has been made
	- `echo $JAVA_HOME`
- Edit bashrc file
	- `sudo nano ~/.bashrc`
- Add to bottom or file
	- `export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64`
- Save ~/.basgrc
- Verify the change has been made
	- `cat ~./bashrc | grep -i home`

_Where the exact location is dependent on where Java 1.7 lives on your local machine usually you put those environment variable settings in your .bashrc file._

***Installation Instructions: https://www.digitalocean.com/community/tutorials/how-to-install-java-on-ubuntu-with-apt-get***



**Install mySQL:**
- Prepare for mySQl
	- `hostname`
	- `hostname -f`
	- `sudo apt-get update`
	- `sudo apt-get upgrade`
	- `sudo apt-get install mysql-server`
- Input root password twice
- Run mySQL as root
	- `mysql -u root -p`
	- `exit`
- Allow user to have proper permissions
	- `sudo adduser _username_ mysql`
	- `sudo chmod 770 /var/lib/mysql`
- Check group permissions
	- groups
