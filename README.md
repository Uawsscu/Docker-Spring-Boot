#  How to run a Maven build within a Docker container. ******
   - maven clean
   - maven install  
 #### 1. Dockerfile
 ```` 
    FROM openjdk:8
    EXPOSE 8080
    ADD target/demo-api.jar demo-api.jar 
    ENTRYPOINT ["java","-jar","/demo-api.jar"]
```` 
 #### 2. docker-compose.yml
 ```` 
 version: "3.7"
 services:
    demo-api:
        image: demo-api/image
        build:
          context: .
        ports:
          - 9090:8080
        volumes:
            - ./logs:/logs
 ```` 
 #### 3. logback-spring.xml
 #### 4. pom.xml
   - ###### Create a JAR file & Create image
````  
			<plugin>
				<groupId>com.spotify</groupId>
				<artifactId>dockerfile-maven-plugin</artifactId>
				<version>1.4.13</version>
				<executions>
					<execution>
						<id>default</id>
						<goals>
							<goal>build</goal>
							<goal>push</goal>
						</goals>
					</execution>
				</executions>
				<configuration>
					<repository>${project.build.finalName}/image</repository>
					<buildArgs>
						<JAR_FILE>${project.build.finalName}.jar</JAR_FILE>
					</buildArgs>
				</configuration>
			</plugin>
````  
  - ###### build and run containers by docker-compose
```` 
			<plugin>
				<artifactId>exec-maven-plugin</artifactId>
				<version>3.0.0</version>
				<groupId>org.codehaus.mojo</groupId>
				<executions>
					<execution>
						<id>Run Containers</id>
						<phase>integration-test</phase>
						<configuration>
							<executable>docker-compose</executable>
							<commandlineArgs>up --detach</commandlineArgs>
						</configuration>
						<goals>
							<goal>exec</goal>
						</goals>
					</execution>
				</executions>
			</plugin>
```` 
---------------------------------------------------------------------------------
 
###### DockerCompose
  - $docker-compose up
  
###### Dockerfile (TEST)
  - $docker build . -t spring-boot-docker.jar
  - $docker run -p 9090:8080 spring-boot-docker.jar 
  - check url "http://localhost:9090/hello"
  - $docker image ls (heck image)
  - $docker rmi 22d84a66cda4 (remove image)
  - $docker ps -s (check container)
  - $docker rm -f 65a82c94c7ab (remove container)
 
