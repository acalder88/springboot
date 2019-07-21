FROM openjdk:8-jdk-alpine

EXPOSE 8080

ENV JAVA_VER=1.8.0

#RUN addgroup -S -g 1000 test
#RUN adduser -D -S -G test -u 1000 -s /bin/ash test

#WORKDIR /home/test

COPY clarifi-loan-handler-service.jar .
COPY start.sh .

RUN chown test:test start.sh
RUN chmod ug+x start.sh

USER test

ENTRYPOINT ["sh", "start.sh"]
