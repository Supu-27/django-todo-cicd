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

