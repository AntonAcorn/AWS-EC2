# AWS-EC2
Deploying to Amazon cloud AWS EC2

Connecting to AWS server

ssh -i <Name.pem> ec2-user@<ec2-3-84-6-212.compute-1.amazonaws.com> (after@ dns или ip from AWS.Amazon.com)
Name.pem - ssh key, you can get it on website: aws.amazon.com
Command is running from ssh key directory

sudo yum update

yum list java* (searching for which Java to install)

sudo yum install java-1.8.0

sudo /usr/sbin/alternatives --config java (check what kind of Java version we have and should use)
sudo /usr/sbin/alternatives --config javac (check what kind of Java version we have and should use)

sudo wget <http> - download Tomcat from tomcat.apache.org/ (tar.gz)

Ls

Find this file and unzip: 
sudo tar xvf <NAME> -C /usr/share (after -C in which folder(-C, --directory DIR))

ls -lrt /usr/share


(The sudo ln -s is used to create a symbolic link. The -R is used to recursively operate on all files and directories under the given directory.)
sudo ln -s /usr/share/apache-tomcat-9.0.70 /usr/share/tomcat9 (create link to folder)

Creating User and Group:
sudo groupadd --system tomcat
sudo useradd -d /usr/share/tomcat9 -r -s /bin/false -g tomcat tomcat

Add permission:
sudo chown -R tomcat:tomcat /usr/share/apache-tomcat-9.0.70

Create file with Tomcat settings 
(vi - run text editor, press i to edit)

sudo vi /etc/systemd/system/<tomcat9.service>

Esc :wq (write and quit) 

sudo systemctl daemon-reload
sudo systemctl enable <tomcat9> (<tomcat9.service> - tomcat9 without.service)

sudo systemctl start <tomcat9>

http://ec2-3-84-6-212.compute-1.amazonaws.com:8080 (public DNS dns from amazonAWS, 8080 standart tomcat port, I made special security settings for this port). 
Press  manager app, but it does not work, because we use different comuters. We address from localhost to ec2 server, 
we should change
Manager's context.xml

fix gile:
sudo vi /usr/share/tomcat9/webapps/manager/META-INF/context.xml (comment value)

sudo systemctl restart <tomcat>

Create User
sudo vi /usr/share/tomcat9/conf/tomcat-users.xml

Add to file tomcat-users.xml
<role rolename="manager-gui"/>
<user username="tomcat" password="12345" roles="manager-gui"/>
