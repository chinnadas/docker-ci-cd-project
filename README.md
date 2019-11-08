# docker-ci-cd-project

Docker ci/cd project:
=================

maven project warfile Deploying in to Docker tomcat-container
------------------------------------------------------------------------------------
sudo usermod -aG docker ubuntu
sudo usermod -aG docker jenkins


1.freestyle project

2.git clone https://github.com/chinnadas/gameoflife-java-project.git

3. build using maven.

4.Docker file. (/root)

                   FROM tomcat:8-jre8
	MAINTAINER chinnadas
	COPY /gameoflife.war /usr/local/tomcat/webapps/gameoflife.war
	EXPOSE 8081
	CMD ["catalina.sh", "run"]


5.shell script.(jenkins server under build)

	#!/bin/bash
	sudo -i
	sudo cp -r /var/lib/jenkins/workspace/my-project/gameoflife-web/target/gameoflife.war /root
	sudo rm -rf gameoflife.war
	sudo chmod -R 777 /root/gameoflife.war
	sudo docker build -t mytomcat /root/
	sudo docker rm -f container2
	sudo docker run -d --name container2 -p 8081:8080 mytomcat.

6. build now project.

