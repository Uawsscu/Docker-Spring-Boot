FROM openjdk:8
EXPOSE 8080
ADD target/demo-api.jar demo-api.jar 


RUN useradd -rUM -s /usr/sbin/nologin heartbeat 
USER heartbeat
VOLUME ./logs


ENTRYPOINT ["java","-jar","/demo-api.jar"]