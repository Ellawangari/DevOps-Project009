# DevOps-Project009

****Project Implementation****

The project tasks were for a Jenkins server, to configure a job to automatically deploy source codes changes from Git to NFS server
  
****Key Takeaways****
-  Automation of tasks using Jenkins server.

****STEPS****

**Step 1: Installing and configuring Jenkins**

- Launced an EC2 Ubuntu Server and named it Jenkins.
 ![alt text](https://github.com/Ellawangari/DevOps-Project009/blob/main/Images/1.PNG)
 
- Installed JDK( since Jenkins is Java Based)
 ``` 
 sudo apt update
sudo apt install default-jdk-headless

```
 - Installed Jenkins 
  ```
 wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
    /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt-get install jenkins

```
 ![alt text](https://github.com/Ellawangari/DevOps-Project009/blob/main/Images/2.PNG)
 
- Ensured Jenkins is up and running ` sudo systemctl status jenkins`
 ![alt text](https://github.com/Ellawangari/DevOps-Project009/blob/main/Images/4.PNG)

- Created a new ibound rule to open port 8080 since Jenkin uses this as the default port.
 ![alt text](https://github.com/Ellawangari/DevOps-Project009/blob/main/Images/3.PNG)
 
- Accessed Jenkins using the public ip address on port 8080 on the browser.
 ![alt text](https://github.com/Ellawangari/DevOps-Project009/blob/main/Images/5.PNG)
 
- Performed initial Jenkins setup . Accessed the Administator password from the following file `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`
 ![alt text](https://github.com/Ellawangari/DevOps-Project009/blob/main/Images/6.PNG)
  ![alt text](https://github.com/Ellawangari/DevOps-Project009/blob/main/Images/7.PNG)
   ![alt text](https://github.com/Ellawangari/DevOps-Project009/blob/main/Images/8.PNG)
   
   
**Step 2:  Configured Jenkins to retrieve source codes from GitHub using Webhooks**
   
 - Forked tooling project from darey-io repository and enabled and created a webhoook from github settings page.
  ![alt text](https://github.com/Ellawangari/DevOps-Project009/blob/main/Images/9.PNG)

- Created a freestyle project called tooling_github from jenkins web console.
   ![alt text](https://github.com/Ellawangari/DevOps-Project009/blob/main/Images/10.PNG)
 
- Connected the tooling project on jenkins web console to my github project and added neccesary credentials.
- Click on the build icon to run the job.This was a manual trigger.
 ![alt text](https://github.com/Ellawangari/DevOps-Project009/blob/main/Images/11.PNG)
 
- Configured the jenkins build job  to be triggered by the github webhook
  ![alt text](https://github.com/Ellawangari/DevOps-Project009/blob/main/Images/12.PNG)
 
- Configured post build actions to archive the files called artifacts.
- Made changes to the read me file and a buld job was triggered by the github webhook.
  ![alt text](https://github.com/Ellawangari/DevOps-Project009/blob/main/Images/13.PNG)
  
- Jenkins artifacts are stored on the server locally on `ls /var/lib/jenkins/jobs/tooling_github/builds/<build_number>/archive/`
  
  
  **Step 3:  Configured Jenkins to copy files to NFS server via SSH**
  
  - On Manage Plugins I installed publish over ssh plugin 
  ![alt text](https://github.com/Ellawangari/DevOps-Project009/blob/main/Images/14.PNG)
  
  - On the Publish over SSH pluging configuration added the private key and other details to be able to connect to my NFS server.
   ![alt text](https://github.com/Ellawangari/DevOps-Project009/blob/main/Images/15.PNG)
   - Also tested the configuration returned success before saving the details and also ensuring TCP port 22 was open.
   - Changed the read me file again and the files we succefully transferred to my nfs /mnt/apps directory.
      ![alt text](https://github.com/Ellawangari/DevOps-Project009/blob/main/Images/16.PNG)
       ![alt text](https://github.com/Ellawangari/DevOps-Project009/blob/main/Images/17.PNG)
       
