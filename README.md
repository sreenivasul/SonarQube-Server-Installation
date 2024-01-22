# Hardware Requirements for SonarQube
----------------------------------------------------
The SonarQube server requires at least 2GB of RAM to run efficiently and 1GB of free RAM for the OS.

# Login as a root user.
sudo su -
 
Install Java ( Java is the Pre Requisite Software)
--------------------------------------------------------------
yum install java-11-openjdk-devel -y

# Download the SonarqQube Server software.
# Goes to opt directory
cd /opt
# Install wget
yum install wget unzip -y
# copy sonarqube url
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.6.1.59531.zip
# Unzip the sonar
unzip sonarqube-9.6.1.59531.zip
# rename it
mv sonarqube-9.6.1.59531 sonarqube


# As a good security practice, SonarQuber Server is not advised to run sonar service as a root user, so create a new user called sonar user  and grant sudo access to manage nexus services as follows.
useradd sonar

# Give the sudo access to sonar user
visudo

sonar   ALL=(ALL)       NOPASSWD: ALL

# Change the owner and group permissions to /opt/sonarqube/ directory.
chown -R sonar:sonar /opt/sonarqube/
chmod -R 755 /opt/sonarqube/
su - sonar
cd /opt/sonarqube/bin/linux-x86-64/
# start the server
./sonar.sh start
# Enable the sonar service
sudo systemctl enable sonar

# Start the sonar service
sudo systemctl start sonar

# Check the status of the  sonar service
sudo systemctl status sonar
