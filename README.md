# aws-jenkins

## Create EC2 Instance (Ubuntu 18.04 Image)
- Custom Ports 22 and 8080 to accept "MyIP"
- Change key pem file with `chmod 400 <pem>`
- Launch instance and SSH to host `ssh -i <pem> ubuntu@<ec2-instance>`

## Install Jenkins 

```
# Step 1 - Update existing packages
sudo apt-get update

# Step 2 - Install Java
sudo apt install -y default-jdk

# Step 3 - Download Jenkins package. 
# You can go to http://pkg.jenkins.io/debian/ to see the available commands
# First, add a key to your system
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -

# # Step 4 - Add the following entry in your /etc/apt/sources.list:
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'

# # Step 5 -Update your local package index
sudo apt-get update

# Step 6 - Install Jenkins
sudo apt-get install -y jenkins

# Step 7 - Start the Jenkins server
sudo systemctl start jenkins

# Step 8 - Enable the service to load during boot
sudo systemctl enable jenkins
sudo systemctl status jenkins
```

Should see Jenkins started successfully

```
● jenkins.service - LSB: Start Jenkins at boot time
   Loaded: loaded (/etc/init.d/jenkins; generated)
   Active: active (exited) since Sun 2020-08-30 19:53:03 UTC; 1min 7s ago
     Docs: man:systemd-sysv-generator(8)
    Tasks: 0 (limit: 1140)
   CGroup: /system.slice/jenkins.service

Aug 30 19:53:01 ip-172-31-7-163 systemd[1]: Starting LSB: Start Jenkins at boot time...
Aug 30 19:53:02 ip-172-31-7-163 jenkins[7324]: Correct java version found
Aug 30 19:53:02 ip-172-31-7-163 jenkins[7324]:  * Starting Jenkins Automation Server jenkins
Aug 30 19:53:02 ip-172-31-7-163 su[7372]: Successful su for jenkins by root
Aug 30 19:53:02 ip-172-31-7-163 su[7372]: + ??? root:jenkins
Aug 30 19:53:02 ip-172-31-7-163 su[7372]: pam_unix(su:session): session opened for user jenkins by (uid=0)
Aug 30 19:53:02 ip-172-31-7-163 su[7372]: pam_unix(su:session): session closed for user jenkins
Aug 30 19:53:03 ip-172-31-7-163 jenkins[7324]:    ...done.
Aug 30 19:53:03 ip-172-31-7-163 systemd[1]: Started LSB: Start Jenkins at boot time.
```

### Configure Jenkins
- Visit Jenkins Web UI `<ec2 public ip>:8080`
- SSH ec2 instance
```
 sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
- Click "Manage Jenkins" --> "Manage Plugins" --> "Available" 
- Search "Blue Ocean" and select related plugins
- Search "AWS" and select "Pipeline AWS Steps"
- Install & Restart Jenkins
