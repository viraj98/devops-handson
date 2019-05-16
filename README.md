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

- yum update -y; yum install -y epel-release; yum install -y htop wget nload vim mlocate git python-pip
- yum install java-1.8.0-openjdk-devel
- wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
- rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
- yum install -y jenkins
- systemctl start jenkins
- systemctl enable jenkins
- Browsing jenkins url and setting up default plugin is taking 7 to 8 mins. 
