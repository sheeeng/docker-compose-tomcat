FROM library/tomcat:9.0.30-jdk11-openjdk

EXPOSE 8080

ARG USER_NAME=tomcat
ARG USER_PASSWORD=changeit

RUN cp \
    --archive \
    --recursive \
    --verbose \
    ${CATALINA_HOME}/webapps.dist/* \
    ${CATALINA_HOME}/webapps/

RUN sed --in-place "\$i \  <role rolename=\"manager-gui\"/>" conf/tomcat-users.xml
RUN sed --in-place "\$i \  <user username="\"${USER_NAME}-manager"\" password="\"${USER_PASSWORD}"\" roles=\"manager-gui\"/>" conf/tomcat-users.xml

RUN sed --in-place "\$i \  <role rolename=\"manager-script\"/>" conf/tomcat-users.xml
RUN sed --in-place "\$i \  <role rolename=\"manager-jmx\"/>" conf/tomcat-users.xml
RUN sed --in-place "\$i \  <role rolename=\"manager-status\"/>" conf/tomcat-users.xml

RUN sed --in-place "\$i \  <role rolename=\"admin-gui\"/>" conf/tomcat-users.xml
RUN sed --in-place "\$i \  <user username="\"${USER_NAME}"-admin\" password="\"${USER_PASSWORD}"\" roles=\"admin-gui\"/>" conf/tomcat-users.xml

RUN cat conf/tomcat-users.xml

# COPY tomcat-users.xml /usr/local/tomcat/conf/
COPY context.xml /usr/local/tomcat/webapps/manager/META-INF/
COPY context.xml /usr/local/tomcat/webapps/host-manager/META-INF/context.xml

CMD ["catalina.sh", "run"]
