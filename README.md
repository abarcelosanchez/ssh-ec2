# ssh-ec2

This is a script for connecting to AWS ec2 instances via ssh. It automatically open port 22 for you IP in AWS security group and when you exit from instance, delete this port.

## Prerequisites

Software required:
* Install **awscli** and configure your AWS profiles (https://docs.aws.amazon.com/es_es/cli/latest/userguide/cli-install-macos.html).
* Install **jq** (https://stedolan.github.io/jq/download/)

Conditions:
* Save in your `$HOME/.ssh` all ec2 instances keys (**.pem** files). Also you can save it in other path, but is important keep all files in the same location. When you configure this script, you have to set this path.
* Knowing the **username** of your ec2 instances to connect with it. Usually in AWS it is `ubuntu` (if you are using Ubuntu SO) or if your are using Elastic Beanstalk instance it would be `ec2-user`.
* Save this script in `/usr/local/bin` to use it globally.
* AWS instances have to have **'Name'** tag configured.

## Steps
### 1. Configuration
Run
```
$ ssh-ec2 -c 
```
or
```
$ ssh-ec2 --configure
```
Then you have to set:
```
########################################

             CONFIGURING

########################################

1. Where are key or pem file path located? (defaul path ~/.ssh)

2. Write one AWS instance tag name different to 'Name' to identify your instance (Leave empty if you do not need more)
```

### 2. Running
Then you only have to run:
```sh
$ ssh-ec2 <ec2_username>
```

## Help
Run
```
$ ssh-ec2 -h
```
or
```
$ ssh-ec2 --help
```

This script will ask you several questions that you have to answer:

* Which AWS profile. It will show you all AWS profiles configured in your local machine
* Which AWS ec2 (instance). It will show you all instances in your AWS account, their status and their keys (.pem files).
* Which ec2 pem. It will show you all keys in your `$HOME/.ssh` location and which key (.pem) has the ec2 selected

Answer these questions and you will connect via ssh with the instance. The script open the ssh port for your public IP in ec2 Sequrity Group, and when you exit from instance, the script remove your public ip from ec2 Sequrity Group. 

## **Important recommendation**
**When you are choosing the AWS profile, instance name or instance pem, it is recomended to tap double click in the name that you want to select and then paste (CRT/CMD+v). Doing this you won't never write a wrong name and you connection will be work fine**