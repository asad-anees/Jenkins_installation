# Jenkins_installation
Installation of Jenkins on Ubuntu:
Jenkins is a CI/CD software platform that supports continuous integration (CI) and continuous delivery (CD). It’s used to automate software testing, building, delivery, and deployment. Using Jenkins on Ubuntu creates a powerful management tool that takes a development workflow to the next level.

Prerequisites

A system running Ubuntu 22.04 Jammy Jellyfish.
A user account with administrator privileges.
Access to a terminal window / command line (CTRL+ALT+T).

Java 8 or 11 installed on Ubuntu.

Step 1: Install Java:
Jenkins requires the Java Runtime Environment (JRE). This guide uses OpenJDK for the Java environment. OpenJDK is a Development Kit, and includes the Java Runtime Environment.

At the time of writing this article, Jenkins only supports Java 8 and Java 11 on Ubuntu. You can have multiple versions of Java installed on Ubuntu. If you do, make sure Java 8 or Java 11 is set as the default version.

Follow the steps below to install Java on Ubuntu:

1. Check if you already have Java installed on your Ubuntu system:
java -version

2. First, open a terminal window and update the system package repository by running:
sudo apt update

Enter your administrator password and wait for the update to complete.

3. Depending on which Java version you want to install, Java 8 or 11, run one of the following commands:

To install OpenJDK 8, run:
sudo apt install openjdk-8-jdk -y

To install OpenJDK 11, run:
sudo apt install openjdk-11-jdk -y

We install OpenJDK version 11 on our system:

Step 2: Add Jenkins Repository
It is recommended to install Jenkins using the project-maintained repository, rather than from the default Ubuntu repository. The reason for that is because the Jenkins version in the default Ubuntu repository might not be the latest available version, which means it could lack the latest features and bug fixes.

Follow the steps below to add the Jenkins repository to your Ubuntu system.

1. Start by importing the GPG key. The GPG key verifies package integrity but there is no output. Run:

curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null

2. Add the Jenkins software repository to the source list and provide the authentication key:

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

The command adds the Long Term Support (LTS) stable release to the sources list, but there is no output.

Step 3: Install Jenkins
After setting up the prerequisites, follow the steps below to install Jenkins on Ubuntu:

1. Update the system repository one more time. Updating refreshes the cache and makes the system aware of the new Jenkins repository.

sudo apt update

2. Install Jenkins by running:

sudo apt install jenkins -y

Wait for the download and installation to complete.


3. To check if Jenkins is installed and running, run the following command:

sudo systemctl status jenkins

A bright green entry labelled active (running) should appear in the output, indicating that the service is running.

4. Exit the status screen by pressing Ctrl+Z.

Note: If the Jenkins service is not running or active, run the following command to start it:

sudo systemctl enable --now jenkins


Step 4: Modify Firewall to Allow Jenkins
Allow Jenkins to communicate by setting up the default UFW firewall.

1. Open port 8080 by running the following commands:

sudo ufw allow 8080

sudo ufw status

If you're using a different firewall application, follow its specific instructions to allow traffic on port 8080.

2. If you haven't configured the UFW firewall yet, it displays as inactive. Enable UFW by running:

sudo ufw enable

Note: If you need to change the port, check out our article How to Change Port for Jenkins

Step 5: Set up Jenkins
Follow the steps below to set up Jenkins and start using it:

1. Open a web browser, and navigate to your server' IP address. Use the following syntax:

http://ip_address_or_domain:8080

Use the actual IP address or domain name for the server you're using Jenkins on. For example, if you're running Jenkins locally, use localhost (127.0.0.1):

http://localhost:8080

A page opens prompting you to Unlock Jenkins. Obtain the required administrator password in the next step.

2. Obtain the default Jenkins unlock password by opening the terminal and running the following command:

sudo cat /var/lib/jenkins/secrets/initialAdminPassword

3. The system returns an alphanumeric code. Enter that code in the Administrator password field and click Continue.

4. The setup prompts to either Install suggested plugins or Select plugins to install. It’s fine to simply install the suggested plugins.

You can always install more plugins later. The system continues the initial Jenkins setup.

5. The next step is the Create First Admin User. Enter the credentials you want to use for your Jenkins administrator, then click Save and Continue.

6. After this, you should set up the Instance Configuration. This is the preferred network address for this Jenkins installation. Confirm the address you want to use for your server. This is most likely the same address you used to get to this configuration page.

7. Once you specify the Jenkins URL, click Save and Finish.

8. You should see a page that says Jenkins is ready! Click Start using Jenkins to open the Jenkins dashboard.

9. Note: Check out our guide on how to restart Jenkins manually - a useful practice while troubleshooting issues.

Conclusion

You should now have a working installation of Jenkins on your Ubuntu 22.04 system. Next, discover how to setup Jenkins on a Kubernetes cluster. If you are using a different distribution of Linux, we also have a guide on how to install Jenkins od Debian 10, and how to install Jenkins on CentOS.
