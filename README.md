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
yum install -y epel-release; yum install -y htop wget vim mlocate git
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
exit # to exit from root user
```

## Steps for manualy deployment. 
  - git clone https://github.com/gskrscm/devops-handson.git 
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
  - `cd bin; ls`
  - `./app` 
  - `ctrl/cmd + c` 

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
 - Configure jenkins job and select `poll scm` in build triggers. 

## Voice over : Show sample jenkins job with Jenkinfile, nexus and sonar. 
## Broken code demo. 
 - Modify app/app.go eg: remove `f` letter from fmt.println
 
## Next Steps to learn more jenkins and CI and CD. 
- Refer: https://jenkins.io/doc/book/pipeline/
