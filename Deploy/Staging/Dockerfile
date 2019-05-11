FROM tomcat:9.0-jre11-slim

COPY server.xml tomcat-users.xml /usr/local/tomcat/conf/
COPY context.xml /usr/local/tomcat/webapps/manager/META-INF/
COPY ../../webapp/target/*.war /usr/local/tomcat/webapps/

EXPOSE 8090

CMD ["catalina.sh", "run"]