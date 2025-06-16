
- [Setup a Server](#Setup-a-Server)

- [Deploy and run Application](#Deploy-and-run-Application)

- [Create And Congiure Linux User on Cloud Server](#Create-And-Congiure-Linux-User-on-Cloud-Server)
  
## Cloud-And-Infrastructure-as-Service-Basic-Digital-Ocean

#### Demo Project:

Create server and deploy application on DigitalOcean

#### Technologies used:

DigitalOcean, Linux, Java, Gradle

#### Project Description:

Setup and configure a server on DigitalOcean Create and configure a new Linux user on the Droplet (Security best practice)
Deploy and run a Java Gradle application on Droplet

#### Setup a Server 

Go to Digital Ocean and Create an account 

Step 1 : Go to Digital ocean -> Create Droplet -> Choose Region and Capacity -> Create SSH key

Step 2 : To create SSH key :

  - In terminal : `ssh-keygen` . There will be `.ssh/id_rsa and`, `.ssh/id_rsa.pub` . Then `cat .ssh/id_rsa.pub` take this content and put it into Digital ocean
   
<img width="600" alt="Screenshot 2025-03-18 at 14 37 03" src="https://github.com/user-attachments/assets/49d7f9df-e2c3-4162-9a5e-7495435fd593" />

Step 3 : Create Firewall to protect the Server 

- Using Firewall we will explicitly allow public access on specific port and ip address

- We need to open port 22 so we can ssh into it 

<img width="600" alt="Screenshot 2025-06-16 at 10 53 51" src="https://github.com/user-attachments/assets/04e513dd-8d3d-4c66-935c-f96bf5517c52" />

Step 4 : Connect to Server : `ssh root@<IP-address>`

!!! Note : Best Practice is to use SSH key to authenticate with a remote Server

Step 5: Install Java on the server 

- First I need to update a server `apt update` (I use apt bcs I use Ubuntu Image)

- To install Java : `apt install opdenjdk-17-jre-headless`

- To check if we have java or not . Put `java` in the terminal

#### Deploy and run Application

I will clone this Java React Project into my Repository `git clone https://gitlab.com/twn-devops-bootcamp/latest/05-cloud/java-react-example.git`

Go to to root project `cd java-react`

Then I will build the Java project into a artifacrt : `gradle build` 

Now I have a Jar file

<img width="400" alt="Screenshot 2025-06-16 at 11 01 15" src="https://github.com/user-attachments/assets/918094a2-a87a-4c82-acc1-2475eb38a118" />

Now I want that Jar file to run on the Ubuntu Server `scp <file locally> <destination on the server>` For example : `scp build/libs/java-react-example.jar root@<server-ipaddress>:/root`

Now I should see a Jart file on Digital ocean 

<img width="397" alt="Screenshot 2025-06-16 at 11 04 21" src="https://github.com/user-attachments/assets/6a7da783-7ea1-4386-99d9-cce49b81e8fa" />

Since I have install Java Now I can run Java : `java -jar java-react-example.jar`

<img width="400" alt="Screenshot 2025-06-16 at 11 05 20" src="https://github.com/user-attachments/assets/db7cd96c-1091-411a-b73a-930a39a2beb0" />

The Application is listening on Port `7071` so I need to configure Firewall to open the port `7071` so I can connect to the application from the Browser 

To check that the Processes running `ps aux | grep java`

<img width="400" alt="Screenshot 2025-06-16 at 11 08 46" src="https://github.com/user-attachments/assets/f344f954-6653-4995-bc14-61c737a2a7e0" />

Now I can see it running with a Process id `5199`

I can use `netstat -ltpn` to check on which port the application is running . 

I need to install net-tools in order to use `netstat` `apt install net-tools`

This will actually the servers only that have the Active Internet Connection

 <img width="400" alt="Screenshot 2025-06-16 at 11 11 19" src="https://github.com/user-attachments/assets/7e118ce1-d9ff-466d-a3f0-e34bc06969f2" />

#### Create And Congiure Linux User on Cloud Server

As a Security Best Practice you should Actually not execute services as a Root user 

Create a separate user for every Application I deploy and Run 

Give it only the Permission it needs to run the App 

Never work with Root User . If I am a Admin I should create a Admin user with Admin Privileges and I can work on that Admin User

To create a new user `adduser tim`

- I will need to set my password

I want to allow `tim user` can execute command that root user can execute . So I will add `tim user` to `sudo group` : `usrmod -aG sudo tim`

I can switch to `tim user`: `su - tim` . Now I can execute command that need privileges with `sudo`

`$` for Standard Linux User 

`#` for Root user

Now I try to access to a server from my local machine as a `tim user` : `ssh tim@<ipaddress>` It will not working bcs I need to provide my ssh key that I have configure for root user also for this user . It doesn't recognize me 

I will ssh again as a root `ssh root@<ip-address>` . Then I will swtich to `tim user` 

Now I need to take my Public ssh key and copy that . Then I will go back to a Server and create a `.ssh` folder `mkdir .ssh`

In `.ssh` folder I will create a file `sudo vim .ssh/authorized_keys` This command will create a new file and give me a Vim editor . 

Now I will copy the public ssh key from my local and paste in the `authorized_keys` file  . 

So Now I can ssh to a Server using `tim user` : `ssh tim@ipaddress`

















