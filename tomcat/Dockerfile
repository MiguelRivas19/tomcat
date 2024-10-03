FROM tomcat
RUN cp -r /usr/local/tomcat/webapps.dist/* /usr/local/tomcat/webapps/

RUN sed -i 's/<\/tomcat-users>//g' /usr/local/tomcat/conf/tomcat-users.xml
RUN echo '<role rolename="admin-gui"/>' | tee -a  /usr/local/tomcat/conf/tomcat-users.xml
RUN echo '<role rolename="manager-gui"/>' | tee -a  /usr/local/tomcat/conf/tomcat-users.xml
RUN echo '<user name="tomcat" password="tomcat" roles="manager-gui,admin-gui" />' | tee -a  /usr/local/tomcat/conf/tomcat-users.xml
RUN echo '</tomcat-users>' | tee -a  /usr/local/tomcat/conf/tomcat-users.xml

# Set the Tomcat Manager apps to allow connections from everywhere
# Note: the -r forces sed to respect full regex
RUN sed -i -r 's/127\\\.\\d\+\\\.\\d\+\\\.\\d\+\|::1\|0:0:0:0:0:0:0:1/\.\*/g' /usr/local/tomcat/webapps/manager/META-INF/context.xml
RUN sed -i -r 's/127\\\.\\d\+\\\.\\d\+\\\.\\d\+\|::1\|0:0:0:0:0:0:0:1/\.\*/g' /usr/local/tomcat/webapps/host-manager/META-INF/context.xml
RUN sed -i -r 's/127\\\.\\d\+\\\.\\d\+\\\.\\d\+\|::1\|0:0:0:0:0:0:0:1/\.\*/g' /usr/local/tomcat/webapps/docs/META-INF/context.xml

# Set debug port for Tomcat
RUN sed -i '299 i JAVA_OPTS="$JAVA_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=*:8787"' /usr/local/tomcat/bin/catalina.sh