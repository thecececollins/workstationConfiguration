Setting up a Dev Machine

Create remote connectivity from a PC:
Install openSSH Server onto your linux machine
- On the linux machine's terminal type:
	sudo apt-get update
	sudo apt-get install openssh-server
	sudo ufw allow 22



To access your linux terminal remotely:
- Install PuTTY onto the PC: https://the.earth.li/~sgtatham/putty/latest/x86/putty.exe
- Type in your username, @, and then the linux machine's IP address (ex. ccollins@10.15.0.114)
- Make sure the SSH option is selected underneath and the port is 22
- Add a name for the linux computer 
- Hit Save
- Now test it by either double clicking on the new entry in the list or selecting it and pressing Login
- You should see a Terminal window open asking for the password of your linux machine


To access your linux machine's documents
- Install winSCP: https://winscp.net/download/WinSCP-5.9.1-Setup.exe
- Type in your username, @, and then your linux machine's IP address, you'll see it autofill for you into the appropriate fields (ex. ccollins@10.15.0.114)
- Make sure the SFTP option is selected and the port is 22
- Hit Save
- Now test it by either double clicking on the new entry in the list or selecting it and pressing Login
- You should see a window open (very similar to FileZilla) with your PC's docs on the left and linux docs on the right


Add Sudoer (sudo with NOPASSWD):
- In terminal insert: sudo visudo
- Just under the line that looks like the following: root ALL=(ALL) ALL
- Add the following (replacing user with the actual username): user ALL=(ALL) ALL
- Add the following at the very end of the file (replacing user with the actual username): user ALL=(ALL) NOPASSWD: ALL
- Press Ctrl+X and press Y when prompted to save



Set vi as editor:
- set -o vi


$JAVA_HOME & $ADLUCENT_HOME Configuration:
- Goal: have Java 1.7 installed and an environment variable setup like this: echo $JAVA_HOME 
/usr/lib/jvm/java-7-openjdk-amd64

- Uninstall all versions of Java:
	sudo apt-get autoremove openjdk-7-jdk
	sudo apt-get autoremove openjdk-7-jre
- Make sure all java items are removed from /usr/lib/jvm/
- Install Java 7
	sudo add-apt-repository ppa:openjdk-r/ppa
	sudo apt-get update
	sudo apt-get install openjdk-7-jdk
- Find the path, usually: /usr/lib/jvm/.....
- Edit the environment using nano
	- sudo nano /etc/environment
- Add to bottom of file
	- JAVA_HOME="/usr/lib/jvm/java-7-openjdk-amd64"
	- ADLUCENT_HOME="/home/ccollins/adlucn3nt/adlucent_svn/trunk"
- Save /etc/envirenment
- Reload the environment file
	- source /etc/environment
- Verify the change has been made
	- echo $JAVA_HOME
	- echo $ADLUCENT_HOME
- Edit bashrc file
	- sudo nano ~/.bashrc
- Add to bottom or file
	- export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
	- export ADLUCENT_HOME=/home/ccollins/adlucn3nt/adlucent_svn/trunk
- Save ~/.basgrc
- Verify the change has been made
	- cat ~./bashrc | grep -i home

*Where the exact location is dependent on where Java 1.7 lives on your local machine usually you put those environment variable settings in your .bashrc file

***Installation Instructions: https://www.digitalocean.com/community/tutorials/how-to-install-java-on-ubuntu-with-apt-get***



SVN Installation:
- install the svn application
	- sudo apt-get install subversion
- Make a directory where you want the source to live: "adluc3nt"
	- mkdir /home/ccollins/adluc3nt
- Pull down all of the source locally
	- svn co https://wush.net/svn/adluc3nt adluc3nt
- Input computer password
- Input svn username and password

*Anything in SVN ending with just ".properties" is a local copy and may be edited. DO NOT edit anything ending with ".production" or ".simulation" as these are live.



Install mySQL:
- Prepare for mySQl
	- hostname
	- hostname -f
	- sudo apt-get update
	- sudo apt-get upgrade
	- sudo apt-get install mysql-server
- Input root password twice
- Run mySQL as root
	- mysql -u root -p
	- exit
- Allow user to have proper permissions
	- sudo adduser ccollins mysql
	- sudo chmod 770 /var/lib/mysql
- Check group permissions
	- groups



Prepare for integrating clients in mySQL:
- Create a backup directory in the home folder 
	mkdir ~/backup
- Add # to the top 1-3 lines in tomcat.production/bin
	startup.sh & shutdown.sh
- Change the password in tomcat-productions/conf/server.xml to personal password
- Add proper paths to trunk/src/adlucnt.properties
	- bin.dir=/home/ccollins/adluc3nt/adlucent_svn/trunk/bin/
	- logs.dir=/home/ccollins/adluc3nt/adlucent_svn/trunk/logs/
	- reports.dir=/home/ccollins/adluc3nt/adlucent_svn/trunk/reports/
	- webapp.reports.dir=/home/ccollins/adluc3nt/adlucent_svn/trunk/tomcat-production/webapps/reports/
	- webapp.feedreports.dir=/home/ccollins/adluc3nt/adlucent_svn/trunk/tomcat-production/webapps/reports/products/
	- webapp.clientimages.dir=/home/ccollins/adluc3nt/adlucent_svn/trunk/tomcat-production/webapps/adlucent/ClientDashboard/clientdashboard/images/
	- webapp.client.dir=/home/ccollins/adluc3nt/adlucent_svn/trunk/tomcat-production/webapps/adlucent/
	- webapp.client.email.images.dir=/home/ccollins/adluc3nt/adlucent_svn/trunk/tomcat-production/webapps/adlucent/_charts/
- Remove all but root and prefered client from trunk/src/jdbc.properties
- Build the database
	- cd to $ADLUCENT_HOME, then build: 
		- ./thirdparty/apache-ant-1.7.0/bin/ant -f build.xml  (dist -first time only or build -antyime after the first)
		- ex. (ccollins@Groot:~/adluc3nt/adlucent_svn/trunk$ ./thirdparty/apache-ant-1.7.0/bin/ant -f build.xml dist)
	- ./devbin/get_daily-backup.sh system
	- ./devbin/load_daily_backup.sh system
	- ./devbin/create_retailer_db.sh system
	- ./devbin/clean_retailers.sh
	- ./devbin/create_retailer-db.sh [retailer name] root
	- ./devbin/connect_retailer_db.sh system
- Startup tomcat:
	- sudo tomcat-production/bin/startup.sh ; tail -f tomcat-production/logs/catalina.out
- Once clients are added, log into: "localhost" or "ip address"/adlucent/DeepSearch/DeepSearch.html:
	- If remote accessing the localhost machine: ex. 10.15.0.8/adlucent/DeepSearch/DeepSearch.html
	- If currently on the localhost machine: localhost/adlucent/DeepSearch/DeepSearch.html
- Turn off tomcat any time its not being used:
	- sudo tomcat-production/bin/shutdown.sh ; tail -f tomcat-production/logs/catalina.out
