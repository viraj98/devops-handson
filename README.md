# devops-handson

## Creating a new server. 
- Goto - https://portal.azure.com/#home
- Create New VM
  - Give new resoure group name (hint: use  your name as the resource group name)
  - Provide virtual machine name (hint: use  your name as the machine name)
  - Region select West Europe
  - Image select Cento7.5 
  - Size D2s V3
  - Setup username and password
  - Allow public inbound ports http, ssh, 8080,8081


## Setting up Centos 7 Server. 
```
sudo su # switch to root user
yum update -y; yum install -y epel-release; yum install -y htop wget vim mlocate git
yum install -y java-1.8.0-openjdk-devel
wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
yum install -y jenkins
systemctl start jenkins
systemctl enable jenkins
```
- Browsing jenkins url and setting up default plugins is taking 7 to 8 mins. 
```
wget https://storage.googleapis.com/golang/go1.12.5.linux-amd64.tar.gz
tar -zxvf go1.12.5.linux-amd64.tar.gz -C /usr/local
```

## Steps for manualy deployment. 
  - git clone <github repoistory url>
  - cd devops-handson
  - mkdir bin
  - Execute below commands to make go available as command. 
  ``` 
   export GOROOT=/usr/local/go
   export PATH=$PATH:/usr/local/go/bin
   export GOBIN=/home/<user-name>/devops-handson/bin 
  ```
  - ` go version `
  - `go install app/app.go` 
   

## Jenkins job
- Create new jenkins job <Free style>
- Configure git url
- In build step, add bash and add below script 
```
export GOROOT=/usr/local/go
export PATH=$PATH:/usr/local/go/bin
export GOBIN=$WORKSPACE/bin

# Build 
go version
go install $WORKSPACE/app/app.go

# Deployment
if pgrep app; then pkill app; fi
BUILD_ID=dontKillMe nohup $WORKSPACE/bin/app>>app.log & 
echo Deployment successful. 
```

## Enhance jenkins job with build trigger 

## We will explain git pull request builder. (Voice over) - show sample jenkins job. with nexus sonar testing. 
## Broken code demo. 
