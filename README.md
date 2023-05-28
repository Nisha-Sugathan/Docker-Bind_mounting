# Docker-Bind_mounting
Bind mount can use to mount a file or directory on the host machine is mounted into a container.The file must be specified by its its absolute path on the host machine.

# Reference link
https://hub.docker.com/_/httpd

# Description
Docker is an open platform for developing, shipping, and running applications.
Here we use docker container which can be created to deploy a particular application or environment.

# Prerequisites
Need to install docker on your machine
Add your username to docker group

# Navigate to your document root and  create static web files
``` cd /home/ec2-user/project/public_html/
 echo "<h1><center>  This is index page </center></h1>" > public_html/index.html
 echo "<h1><center>  This is home page </center></h1>" > public_html/home.html ```

