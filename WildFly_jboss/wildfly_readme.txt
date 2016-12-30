=======
WildFly
=======


# Docker
# https://github.com/JBoss-Dockerfiles/wildfly
#
# Deploy

Dockerfile
	FROM jboss/wildfly
	ADD sample.war /opt/jboss/wildfly/standalone/deployments/

docker build --tag=wildfly-app .

docker run -it -d --name wildfly-app -P wildfly-app

# http://localhost:<PORT>/<sample>




# ADMIN console

Dockerfile
	FROM jboss/wildfly
	RUN /opt/jboss/wildfly/bin/add-user.sh <admin_user_name> <password> --silent
	CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]


docker build -t wildfly-admin .

docker run -ti --name wildfly-admin -d -p 9990:9990 -p 8080:8080 wildfly-admin

docker exec -ti wildfly-admin /opt/jboss/wildfly/bin/add-user.sh

# http://localhost:<PORT>



# CLI

./bin/jboss-cli.sh --connect

help --commands
ls deployment



	

