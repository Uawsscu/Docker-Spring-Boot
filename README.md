# Create a JAR file from a Maven project
   - maven clean
   - maven install

# DockerCompose ******
  - $docker-compose up
  
# Dockerfile (TEST)
  - $docker build . -t spring-boot-docker.jar
  - $docker run -p 9090:8080 spring-boot-docker.jar 
  - check url "http://localhost:9090/hello"
  - $docker image ls (heck image)
  - $docker rmi 22d84a66cda4 (remove image)
  - $docker ps -s (check container)
  - $docker rm -f 65a82c94c7ab (remove container)
