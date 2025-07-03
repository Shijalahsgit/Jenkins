# Jenkins

# Working on Jenkins

## AWS EC2 Instance

- Go to AWS Console
- Instances(running)
- Launch instances (ubuntu / Amazon Linux)

### Run the below commands to install Java and Jenkins

for switching to root user
```
sudo su -
```
Pre-Requisites:
 - Java (JDK)
## Installation of Java
Jenkins requires Java to run and there are multiple Java implementations which we can use. OpenJDK is the most popular one.

```
sudo apt update
sudo apt install fontconfig openjdk-21-jre
java -version
openjdk version "21.0.3" 2024-04-16
OpenJDK Runtime Environment (build 21.0.3+11-Debian-2)
OpenJDK 64-Bit Server VM (build 21.0.3+11-Debian-2, mixed mode, sharing)
```
Verify Java is Installed

```
java -version
```
Now, we can proceed with installing Jenkins

## Installing Jenkins
```
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```
## Start Jenkins
You can enable the Jenkins service to start at boot with the command
```
sudo systemctl enable jenkins
```
```
sudo systemctl start jenkins
```
```
sudo systemctl status jenkins
```
**Note: ** By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules as show below.
to check the port number
```
ps -ef | grep jenkins
```
To change inbound traffic in EC2 instance

- EC2 > Instances > Click on <Instance-ID>
- In the bottom tabs -> Click on Security
- Security groups
- Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed `All traffic`).
![image](https://github.com/user-attachments/assets/33d6f52f-114b-4752-b004-7b40b74ecb18)

### Login to Jenkins using the below URL:
http://ec2-instance-public-ip-address:8080 

![image](https://github.com/user-attachments/assets/ad6cfd82-ebef-4b03-b670-74558edaad8e)

After you login to Jenkins, 
      - Run the command to copy the Jenkins Admin Password - `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`
      - Enter the Administrator password
      
## Click on Install suggested plugins
![image](https://github.com/user-attachments/assets/3f4e6362-84f9-4bb8-a782-dc915d6fdfed)

Wait for the Jenkins to Install suggested plugins
![image](https://github.com/user-attachments/assets/6e29d7d2-195f-4b51-9295-33a0d84125a7)

Create First Admin User or Skip the step [If you want to use this Jenkins instance for future use-cases as well, better to create admin user]

![image](https://github.com/user-attachments/assets/215a5b86-b4b2-4bea-8c18-9b33ecec1617)

Jenkins Installation is Successful. We can now starting using the Jenkins
![image](https://github.com/user-attachments/assets/ff6bcc00-4500-465a-9c33-2609c3a6bdc2)


  

