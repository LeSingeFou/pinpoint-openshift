FROM tomcat:8-jre8

LABEL maintainer="Roy Kim <roy.kim@navercorp.com>"

ARG PINPOINT_VERSION=${PINPOINT_VERSION:-1.7.3}

COPY /build/pinpoint-quickstart-testapp.war quickstart.war

ADD pinpoint-agent-1.7.3.tar.gz /pinpoint-agent

COPY /build/configure-agent.sh /pinpoint-agent/

RUN apt-get update && apt-get install net-tools -y && apt-get install lsof -y  && apt-get install procps -y

RUN rm -rf /usr/local/tomcat/webapps \
    && mkdir -p /usr/local/tomcat/webapps \
    && unzip quickstart.war -d /usr/local/tomcat/webapps/ROOT \
    && rm -rf quickstart.war \
    && chmod a+x /pinpoint-agent/configure-agent.sh
    

RUN chgrp -R 0 /usr/local/tomcat && \
    chmod -R g=u /usr/local/tomcat && \
    chgrp -R 0 /tmp && \
    chmod -R g=u /tmp && \
    chgrp -R 0 /pinpoint-agent && \
    chmod -R g=u /pinpoint-agent && \
    chmod 755 /usr/local/tomcat/bin/catalina.sh && \
    chmod 777 /pinpoint-agent/configure-agent.sh && \
    chmod 755 /pinpoint-agent/script/networktest.sh



CMD [ "/pinpoint-agent/configure-agent.sh"]
