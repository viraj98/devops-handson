# devops-handson

## Creating a new server. 
- Goto - https://portal.azure.com/#home
- Create New VM
  - Give new resoure group name
  - Provide virtual machine name
  - Region select West Europe
  - Image select Cento7.5 D2s V3
  - Setup username and password
  - Allow public inbound ports http, ssh


## Setting up Centos 7 Server. 

- yum update -y
- yum install -y epel-release; yum install -y htop wget nload vim mlocate
- yum install -y docker
- yum install -y git

systemctl status docker
systemctl start docker
systemctl enable docker

yum install python-pip
pip install docker-compose

