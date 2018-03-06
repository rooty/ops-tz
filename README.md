# ops-tz
Task definition:

Create test Nginx server with GitHub webhook deployment triggering, using Jenkinsfile.

Stages:

Build. Compile the latest version of Nginx server with a lua-nginx-module.
Dockerize. Create a docker image with adding custom nginx.conf and index.html from the repository files. Push docker image to the public Docker registry.
Deploy. Deploy Nginx container on EC2 instance using docker-machine.

Deploy should start by push event to the master branch.

Output:

Push the final code revision to a public GitHub repository and share URL link to it.



http://34.224.68.57/
http://34.224.68.57/hellolua

не решено как в Jenkinsfile деплоить если уже запущена виртуалка и задеплоин контейнер
Мало знаю про Jenkinsfile и то как это сделать проверки и ветвление по условию

