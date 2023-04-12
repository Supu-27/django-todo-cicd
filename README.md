# django-todo
A simple todo app built with django

Resources &Technology Used :

1.AWS Free Tier Account

2.EC2 Instance : t2 micro

3.Django Todo App

4.Docker Image

5.Jenkins

6.Git and GitHub






Step 1: Set up of AWS EC2 instance

1.Create the ec2 instance with following details

2.Name : Jenkins cicd

3.AMI : Ubuntu 20.04 LTS

4.Key Pair : todo-app

5.SG : Allowing SSH at Port 22


Make connection with EC2 Instance using Terminal with the help of key pair

Now we are on EC2 instance. So create a new directory named Projects

mkdir projects

Now change directory to the newly created directory using cd command

cd projects

clone the django todo app repo in the project directory

git clone https://github.com/shreys7/django-todo.git

Change directory and move to the django-todo directory

cd django-todo/

Add your instance's public IP to allowed host in setting.py file

vi todoApp/settings.py

find allowed host and enter your public IP or just enter '*' so that all Ip are allowed then press esc and use :wq to go back to the terminal and Install docker on the EC2 instance



Step 2 : Create dockerfile and run it using vim create a Dockerfile

vi Dockerfile enter insert mode by pressing "i" and write the file as per the following


FROM python:

RUN pip install django==3.2


COPY . .


RUN python manage.py migrate


CMD ["python","manage.py","runserver","0.0.0.0:8001"]

press esc and use :wq and enter to save the file and exit vim.

Now build the docker file we created

sudo docker build . -t todo-app

Now you will get a container ID. Copy that container ID and run the container with the following command.

sudo docker run -p 8001:8001 62761281ad8f

Now go to your browser and copy your public IP and use it to check if the app is running or not.

example : 3.89.220.210:8001



Step 3 : Install and setup jenkins on your EC2 instance


Update your system in EC2 Terminal

sudo apt update -y 

Install java :

sudo apt install openjdk-11-jre


Install jenkins : Just copy these commands, paste them and run them one by one onto your terminal

curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
  
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
  
sudo apt-get update

sudo apt-get install jenkins


Start Jenkins with these commands :

You can enable the Jenkins service to start at boot with the command:

sudo systemctl enable jenkins

You can start the Jenkins service with the command:

sudo systemctl start jenkins

You can check the status of the Jenkins service using the command:

sudo systemctl status jenkins


Then Add port 8001 to your inbound rules in security groups to allow traffic on it like we did for port 8001.

Now open Jenkins in browser by using public IP and port number


Get the password from given location and paste it here

sudo cat /var/lib/jenkins/secrets/initialAdminPassword

Click install suggested plugin and go ahead ith the installation


create and setup your admin user and your are done. You must be on the Jenkins homepage now



Open your terminal and add jenkins to sudoers s shon in the screen shot so that when we build our job in jenkins it can have sudo access sudo visudo use above command to open the file and then add jenkins like this

Get the password from given location and paste it here
  
  
