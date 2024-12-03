# Ubuntu-Github-Jenkins-for-CI-CD-
E-commerce website used on jenkins for CI/Cd with help of git hub &amp; ubuntu terminal on localhost 8080

--------------------------------------------------------------

# How to install jenkins on ubuntu terminal step by step process :

# Step1-Debian/Ubuntu

Long Term Support release
A LTS (Long-Term Support) release is chosen every 12 weeks from the stream of regular releases as the stable release for that time period. It can be installed from the debian-stable apt repository

### copy link:

     - sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
       https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
       echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
        https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
       /etc/apt/sources.list.d/jenkins.list > /dev/null
     - sudo apt-get update
     - sudo apt-get install jenkins

. The package installation will:
. Setup Jenkins as a daemon launched on start. Run systemctl cat jenkins for more details.
. Create a ‘jenkins’ user to run this service.
. Direct console log output to systemd-journald. Run journalctl -u jenkins.service if you are troubleshooting Jenkins.
. Populate /lib/systemd/system/jenkins.service with configuration parameters for the launch, e.g JENKINS_HOME
### Set Jenkins to listen on port 8080. Access this port with your browser to start configuration.

# Step2-Installation of Java

Jenkins requires Java to run, yet not all Linux distributions include Java by default. Additionally, not all Java versions are compatible with Jenkins.
There are multiple Java implementations which you can use. OpenJDK is the most popular one at the moment, we will use it in this guide.
Update the Debian apt repositories, install OpenJDK 17, and check the installation with the commands:

### installjava :

   - sudo apt update
   - sudo apt install fontconfig openjdk-17-jre

    - java -version
    - openjdk version "17.0.8" 2023-07-18
   OpenJDK Runtime Environment (build 17.0.8+7-Debian-1deb12u1)
   OpenJDK 64-Bit Server VM (build 17.0.8+7-Debian-1deb12u1, mixed mode, sharing)

# Step4-Start Jenkins

You can enable the Jenkins service to start at boot with the command:
###
    - sudo systemctl enable jenkins
  
You can start the Jenkins service with the command:
###
    - sudo systemctl start jenkins

You can check the status of the Jenkins service using the command:
###
    - sudo systemctl status jenkins

If everything has been set up correctly, you should see an output like this:

Loaded: loaded (/lib/systemd/system/jenkins.service; enabled; vendor preset: enabled)
Active: active (running) since Tue 2018-11-13 16:19:01 +03; 4min 57s ago
- If you have a firewall installed, you must add Jenkins as an exception. You must change YOURPORT in the script below to the port you want to use. Port 8080 is the most 
  common.

YOURPORT=8080

PERM="--permanent"

SERV="$PERM --service=jenkins"

firewall-cmd $PERM --new-service=jenkins

firewall-cmd $SERV --set-short="Jenkins ports"

firewall-cmd $SERV --set-description="Jenkins port exceptions"

firewall-cmd $SERV --add-port=$YOURPORT/tcp

firewall-cmd $PERM --add-service=jenkins

firewall-cmd --zone=public --add-service=http --permanent

firewall-cmd --reload

### also used :
    - sudo ufw allow 8080
    - sudo ufw status 

# step4- Post-installation setup wizard
After downloading, installing and running Jenkins using one of the procedures above (except for installation with Jenkins Operator), the post-installation setup wizard begins.
This setup wizard takes you through a few quick "one-off" steps to unlock Jenkins, customize it with plugins and create the first administrator user through which you can continue accessing Jenkins.

# step5-Unlocking Jenkins
  https://www.jenkins.io/doc/book/installing/linux/#unlocking-jenkins

- When you first access a new Jenkins controller, you are asked to unlock it using an automatically-generated password.
1. Browse to http://localhost:8080 (or whichever port you configured for Jenkins when installing it) and wait until the Unlock Jenkins page appears.

  ![image](https://github.com/user-attachments/assets/582178bc-b0b0-458c-a9b9-ea3294c742b7)

2.  From the Jenkins console log output, copy the automatically-generated alphanumeric password (between the 2 sets of asterisks).

  ![image](https://github.com/user-attachments/assets/f3abf5fb-e5da-41d0-9396-da84bd0dd720)

  # Note:

- The command: sudo cat /var/lib/jenkins/secrets/initialAdminPassword will print the password at console.
  If you are running Jenkins in Docker using the official jenkins/jenkins image you can use sudo docker exec ${CONTAINER_ID or CONTAINER_NAME} cat 
  /var/jenkins_home/secrets/initialAdminPassword to print the password in the console without having to exec into the container.

3. On the Unlock Jenkins page, paste this password into the Administrator password field and click Continue.
   Note:
 . The Jenkins console log indicates the location (in the Jenkins home directory) where this password can also be obtained. This password must be entered in the setup wizard 
   on new Jenkins installations before you can access Jenkins’s main UI. This password also serves as the default administrator account’s password (with username "admin") if 
   you happen to skip the subsequent user-creation step in the setup wizard.

# Customizing Jenkins with plugins
. After unlocking Jenkins, the Customize Jenkins page appears. Here you can install any number of useful plugins as part of your initial setup.
  Click one of the two options shown:
. Install suggested plugins - to install the recommended set of plugins, which are based on most common use cases.
. Select plugins to install - to choose which set of plugins to initially install. When you first access the plugin selection page, the suggested plugins are selected by 
  default.
. If you are not sure what plugins you need, choose Install suggested plugins. You can install (or remove) additional Jenkins plugins at a later point in time via the Manage 
   Jenkins > Plugins page in Jenkins.
. The setup wizard shows the progression of Jenkins being configured and your chosen set of Jenkins plugins being installed. This process may take a few minutes.

# Creating the first administrator user
Finally, after customizing Jenkins with plugins, Jenkins asks you to create your first administrator user.

1. When the Create First Admin User page appears, specify the details for your administrator user in the respective fields and click Save and Finish.
2. When the Jenkins is ready page appears, click Start using Jenkins.
   Notes:
.  This page may indicate Jenkins is almost ready! instead and if so, click Restart.
.  If the page does not automatically refresh after a minute, use your web browser to refresh the page manually.
3. If required, log in to Jenkins with the credentials of the user you just created and you are ready to start using Jenkins!

...................................................................................................................


# After installing step now you know use your github for CI/CD pipeline process

1. login to github account.
2. Go to particular repository you want build on Jenkins like :https://github.com/Sureshbeniwa06/E-commerce-.git
3. Now go to jenkins and build new poject. 

# Process to build project on jenkins

1. Go to dashboard.
2. Select new item.
3. Enter a new item name.
4. Select an item type like :Freestyle,maven,pipeline etc.
5. Click on ohk
6. Go to particular project you want to make then go to description(fill any text like:description of project).
7. Go to scm(source code management)
   -Git 
    Repositories
   -Repository URL
                https://github.com/Sureshbeniwa06/E-commerce-.git
   -Credentials:
    Sureshbeniwa06 /******
8. Save & apply.

##### That is only basic project for ci/cd pipeline on jenkins use of github,ubuntu,jenkins #### 



  

