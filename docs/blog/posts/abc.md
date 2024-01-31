# How to setup Jenkins master agent and slave agent on AWS ec2 Instance

## <p align="center">Jenkins Master-Agent Creation

### Create a security group that allows inbound traffic like below and in outbound traffic allow all traffic.</h4>

![image](https://github.com/Flairminds/blogs/assets/135031436/23d46609-a89c-4cba-ac57-bcda5cc0c702)

![image](https://github.com/Flairminds/blogs/assets/135031436/4eec679c-d5b3-42b7-8abf-5203d7c6cef3)


**Launch ec2 instance of Jenkins master agent by selecting the same security group and connect it to putty or git bash.**

![image](https://github.com/Flairminds/blogs/assets/135031436/81a06926-4728-484b-b931-07a554908305)

**Do all this steps on ec2 instance in order to install Jenkins**

1. Ensure that your software packages are up to date on your instance by using the following command to perform a quick software update:

   [ec2-user ~]$ sudo yum update –y

2. Add the Jenkins repo using the following command:
   [ec2-user ~]$ sudo wget -O /etc/yum.repos.d/jenkins.repo \ https://pkg.jenkins.io/redhat-stable/jenkins.repo

3. Import a key file from Jenkins-CI to enable installation from the package:

   [ec2-user ~]$ sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

   [ec2-user ~]$ sudo yum upgrade

4. Install Java (Amazon Linux 2023):

   [ec2-user ~]$ sudo dnf install java-17-amazon-corretto -y

5. Install Jenkins:

   [ec2-user ~]$ sudo yum install jenkins -y

6. Enable the Jenkins service to start at boot:

   [ec2-user ~]$ sudo systemctl enable jenkins

7. Start Jenkins as a service:

   [ec2-user ~]$ sudo systemctl start jenkins

8. You can check the status of the Jenkins service using the command:

   [ec2-user ~]$ sudo systemctl status Jenkins

![image](https://github.com/Flairminds/blogs/assets/135031436/1e08716a-f9c8-43cd-99c6-82c4af8ab58a)

**Configuring Jenkins to create a master agent on ec2**

1. Connect to http://<your\_server\_public\_DNS>:8080 from your browser. You will be able to access Jenkins through its management interface:

![image](https://github.com/Flairminds/blogs/assets/135031436/ff7fb5ba-8b1f-4bf6-95ef-b3e0f128ce8d)

2. As prompted, enter the password found in **/var/lib/jenkins/secrets/initialAdminPassword**.

  ![image](https://github.com/Flairminds/blogs/assets/135031436/23c49024-d1bc-44e1-9eb0-c6e063f38a73)

3. Once the installation is complete, the **Create First Admin User** will open. Enter your information, and then select **Save and Continue**.

![image](https://github.com/Flairminds/blogs/assets/135031436/c818468b-77f8-4092-b4ac-f4cbd0dca727)


4. On the left-hand side, select **Manage Jenkins**, and then select **Manage Plugins**.
5. Select the **Available** tab, and then enter **Amazon EC2 plugin** at the top right.
6. Select the checkbox next to **Amazon EC2 plugin**, and then select **Install without restart**.

![image](https://github.com/Flairminds/blogs/assets/135031436/e45b8388-4e62-46d4-aefe-7a19bba2fe1c)

**Verify your master agent as build-in-node and it is in synched**

![image](https://github.com/Flairminds/blogs/assets/135031436/3dd5bf03-7732-4e11-9cbe-b06b2fc5937c)


<h2><p align="center">Jenkins Slave-Agent Creation</p></h2>

**Launch ec2 instance of Jenkins master agent by selecting the same security group and connect it to putty or git bash.**

![image](https://github.com/Flairminds/blogs/assets/135031436/a92eddf3-7dae-437a-a0ad-181ac00de336)

**Do all this steps on ec2 instance in order to install Jenkins**

1. Ensure that your software packages are up to date on your instance by using the following command to perform a quick software update:

   [ec2-user ~]$ sudo yum update –y

2. Add the Jenkins repo using the following command:
   
   [ec2-user ~]$ sudo wget -O /etc/yum.repos.d/jenkins.repo \ https://pkg.jenkins.io/redhat-stable/jenkins.repo

3. Import a key file from Jenkins-CI to enable installation from the package:

   [ec2-user ~]$ sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

   [ec2-user ~]$ sudo yum upgrade

4. Install Java (Amazon Linux 2023):

   [ec2-user ~]$ sudo dnf install java-17-amazon-corretto -y

5. Install Jenkins:

   [ec2-user ~]$ sudo yum install jenkins -y

6. Enable the Jenkins service to start at boot:

   [ec2-user ~]$ sudo systemctl enable jenkins

7. Start Jenkins as a service:

   [ec2-user ~]$ sudo systemctl start jenkins

8. You can check the status of the Jenkins service using the command:

   [ec2-user ~]$ sudo systemctl status Jenkins

**Under manage Jenkins -> Nodes -> New node**

![image](https://github.com/Flairminds/blogs/assets/135031436/07d36060-82d1-427b-8361-e9bb13734282)


![image](https://github.com/Flairminds/blogs/assets/135031436/f35aeabc-b134-43d3-8c4e-445f3069ecf6)


**Give host as Public ip of your slave ec2 instance and in credentials click on Add.**

![image](https://github.com/Flairminds/blogs/assets/135031436/bda2ab94-8e6f-447d-b881-f4ef0ede1f93)

![image](https://github.com/Flairminds/blogs/assets/135031436/2dbe8c58-20fd-4656-bbc9-0424b14b9db4)


**Enter private key of slave-agent ec2**

![image](https://github.com/Flairminds/blogs/assets/135031436/0f14c5fd-1a72-4689-a384-03779dad9cdb)


**In host key verification strategy select non verifying.**

**Save.**

**You will see that your agent will be in sync .**

![image](https://github.com/Flairminds/blogs/assets/135031436/697df35a-c599-4651-915b-b4af07e209bd)


