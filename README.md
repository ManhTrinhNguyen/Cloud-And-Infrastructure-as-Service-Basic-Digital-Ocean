# Cloud-And-Infrastructure-as-Service-Basic-Digital-Ocean

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

Step 3 : Connect to Server : `ssh root@<IP-address>`

!!! Note : Best Practice is to use SSH key to authenticate with a remote Server
