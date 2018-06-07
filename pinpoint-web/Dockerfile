FROM tomcat:8-jre8

LABEL maintainer="Roy Kim <roy.kim@navercorp.com>"

ARG PINPOINT_VERSION=${PINPOINT_VERSION:-1.7.3}
ARG INSTALL_URL=https://github.com/naver/pinpoint/releases/download/${PINPOINT_VERSION}/pinpoint-web-${PINPOINT_VERSION}.war

COPY /build/scripts/start-web.sh /usr/local/bin/

RUN chmod a+x /usr/local/bin/start-web.sh \
    && curl -SL ${INSTALL_URL} -o pinpoint-web.war \
    && rm -rf /usr/local/tomcat/webapps \
    && mkdir -p /usr/local/tomcat/webapps \
    && unzip pinpoint-web.war -d /usr/local/tomcat/webapps/ROOT \
    && rm -rf pinpoint-web.war
    
    
    
RUN chgrp -R 0 /usr/local/tomcat && \
    chmod -R g=u /usr/local/tomcat && \
    chgrp -R 0 /usr/local/bin && \
    chmod -R g=u /usr/local/bin && \
    chgrp -R 0 /tmp/ && \
    chmod -R g=u /tmp/ && \
    chmod g=u /etc/passwd && \
    chmod 755 /usr/local/tomcat/bin/catalina.sh

ENTRYPOINT ["/usr/local/bin/start-web.sh"]
