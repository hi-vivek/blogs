# **How to setup Jenkins master agent and slave agent on AWS ec2 Instance**

## <p align="center">**Jenkins Master-Agent Creation**

### Create a security group that allows inbound traffic like below and in outbound traffic allow all traffic.

![image](https://github.com/Flairminds/blogs/assets/135031436/0f77141e-095f-49b8-a471-1f0497e087c0)

![image](https://github.com/Flairminds/blogs/assets/135031436/56230aa6-3d8f-45f4-9b70-8d10bcd1859c)

### Launch ec2 instance of Jenkins master agent by selecting the same security group and connect it to putty or git bash.

![image](https://github.com/Flairminds/blogs/assets/135031436/81a06926-4728-484b-b931-07a554908305)

### Steps for installing jenkins

1. Ensure that your software packages are up to date on your instance by using the following command to perform a quick software update:
   ```bash
   sudo yum update –y
   ```
2. Add the Jenkins repo using the following command:
   ```bash
   sudo wget -O /etc/yum.repos.d/jenkins.repo \ https://pkg.jenkins.io/redhat-stable/jenkins.repo
   ```
3. Import a key file from Jenkins-CI to enable installation from the package:
   ```bash
   sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
   sudo yum upgrade
   ```
4. Install Java (Amazon Linux 2023):
   ```bash
   sudo dnf install java-17-amazon-corretto -y
   ```
5. Install Jenkins:
   ```bash
   sudo yum install jenkins -y
   ```
6. Enable the Jenkins service to start at boot:
   ```bash
   sudo systemctl enable jenkins
   ```
7. Start Jenkins as a service:
   ```bash
   sudo systemctl start jenkins
   ```
8. You can check the status of the Jenkins service using the command:
   ```bash
   sudo systemctl status Jenkins
   ```
![image](https://github.com/Flairminds/blogs/assets/135031436/f56a8209-c87e-4db4-bfb6-d5fd10ce628e)


### Configuring Jenkins to create a master agent on ec2

1. Connect to http://<your\_server\_public\_DNS>:8080 from your browser. You will be able to access Jenkins through its management interface:

![image](https://github.com/Flairminds/blogs/assets/135031436/4101ebd6-eefa-4c7c-824b-a487cefab52f)

2. As prompted, enter the password found in **/var/lib/jenkins/secrets/initialAdminPassword**.

  ![image](https://github.com/Flairminds/blogs/assets/135031436/3635e206-f86a-4adf-aae0-84f8e4bd1732)

3. Once the installation is complete, the **Create First Admin User** will open. Enter your information, and then select **Save and Continue**.

![image](https://github.com/Flairminds/blogs/assets/135031436/62ff5a7c-e391-4ab1-8b95-5eae03a6d611)

4. On the left-hand side, select **Manage Jenkins**, and then select **Manage Plugins**.
5. Select the **Available** tab, and then enter **Amazon EC2 plugin** at the top right.
6. Select the checkbox next to **Amazon EC2 plugin**, and then select **Install without restart**.

![image](https://github.com/Flairminds/blogs/assets/135031436/06be932e-b0e9-475d-be76-9701c25f5fdd)

### Verify your master agent as build-in-node and it is in synched

![image](https://github.com/Flairminds/blogs/assets/135031436/2810a64b-5e39-4cd3-99a4-743ae01afcb5)

## <p align="center">**Jenkins Slave-Agent Creation**</p>

### Launch ec2 instance of Jenkins master agent by selecting the same security group and connect it to putty or git bash.

![image](https://github.com/Flairminds/blogs/assets/135031436/9dcb3973-8102-49f1-a33d-d89bc8ed933d)

[Refer this step in order to install jenkins](#Steps-for-installing-jenkins)

### Under manage Jenkins -> Nodes -> New node

![image](https://github.com/Flairminds/blogs/assets/135031436/5bbd6f78-13cd-41c0-99f0-928a259e092b)

![image](https://github.com/Flairminds/blogs/assets/135031436/9db58f00-62ac-4bc7-ab23-3b2d902ac8cc)

### Give host as Public ip of your slave ec2 instance and in credentials click on Add.

![image](https://github.com/Flairminds/blogs/assets/135031436/0f620c53-f091-4c9f-9d8e-be546229d444)

![image](https://github.com/Flairminds/blogs/assets/135031436/584b9e18-5bd4-4a07-a193-1df0f68429eb)

### Enter private key of slave-agent ec2

![image](https://github.com/Flairminds/blogs/assets/135031436/5e00d5d0-a390-4fac-afa7-59477ecd5d12)

### In host key verification strategy select non verifying.

### Save.

### You will see that your agent will be in sync .

![image](https://github.com/Flairminds/blogs/assets/135031436/1890227e-bbc7-4c97-b45b-b63ea865aea4)


