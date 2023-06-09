# Docker-Bind_mounting
Bind mount can use to mount a file or directory on the host machine is mounted into a container.The file must be specified by its its absolute path on the host machine.

### Reference link
https://hub.docker.com/_/httpd

### Description
Docker is an open platform for developing, shipping, and running applications.
Here we use docker container which can be created to deploy a particular application or environment. The -v flag on docker container Consists of three fields, separated by colon characters (:). 
In the case of bind mounts, the first field is the path to the file or directory on the host machine.
The second field is the path where the file or directory is mounted in the container.
The third field is optional, and is a comma-separated list of options, such as ro, z, and Z.

### Prerequisites
Need to install docker on your machine
Add your username to docker group

### Docker Installation

```
sudo yum install docker -y &> /dev/null
sudo systemctl restart docker.service
sudo systemctl enable docker.service
sudo usermod -a -G docker ec2-user
```
![docker_installation](https://github.com/Nisha-Sugathan/Docker-Bind_mounting/assets/134600837/ba7797c4-9a73-4ce6-b593-2befa5850e0d)


### Navigate to your document root and  create static web files
``` 
 cd /home/ec2-user/project/
 echo "<h1><center>  This is index page </center></h1>" > public_html/index.html
 echo "<h1><center>  This is home page </center></h1>" > public_html/home.html 
```
### Mount the public_html directory to container (Bind mounting)
``` 
docker container run -d -p 8080:80 -v /home/ec2-user/project/public_html/:/usr/local/apache2/htdocs/ --name webserver1  httpd:alpine
``` 
### Container document root file listing
``` 
docker container exec webserver1 ls -l /usr/local/apache2/htdocs/
``` 
Screenshot

![docker_bind](https://github.com/Nisha-Sugathan/Docker-Bind_mounting/assets/134600837/6f38c1e7-f8f0-4173-8ebc-ef0bff80197d)

### Modify the httpd configuration file to serve the web page from home.html
``` 
 vi conf/httpd.conf 
 grep "DirectoryIndex" conf/httpd.conf
 ``` 
 
### Remount the "webservr1" container using the config file on local system
 ``` 
 docker container run -d -p 8080:80 -v /home/ec2-user/project/public_html/:/usr/local/apache2/htdocs/ -v /home/ec2-user/project/httpd.conf/:/usr/local/apache2/conf/httpd.conf --name webserver1  httpd:alpine
 ``` 
### Output URL
```
http://<publicdns_name>:8080
```
### Conclusion
 We can easily modify the httpd configuration files on the local machine and can remount the configuration file to the container using the docker container run commands
