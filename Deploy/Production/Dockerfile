FROM tomcat:9.0-jre11-slim

# This is to enable tomcat user for manager-gui
COPY Deploy/Production/tomcat-users.xml /usr/local/tomcat/conf/
# This is to enable access to manager
COPY Deploy/Production/context.xml /usr/local/tomcat/webapps/manager/META-INF/
# This is to actually deploy
COPY webapp/target/*.war /usr/local/tomcat/webapps/

EXPOSE 8080

CMD ["catalina.sh", "run"]