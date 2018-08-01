---
title: Java
---

## Spring Boot + Maven + Docker

Add to your `pom.xml`

```xml
            <plugin>
                <groupId>com.spotify</groupId>
                <artifactId>dockerfile-maven-plugin</artifactId>
                <version>1.4.0</version>
                <configuration>
                    <repository>IMAGENAME</repository>
                    <forceCreation>true</forceCreation>
                    <buildArgs>
                        <JAR_FILE>target/${project.build.finalName}.jar</JAR_FILE>
                    </buildArgs>
                </configuration>
</plugin>
```

Dockerfile

```yml
FROM openjdk:8

ARG JAR_FILE
ADD ${JAR_FILE} /app.jar

EXPOSE 8080

ENTRYPOINT ["java","-jar","/app.jar"]
```

Build with `mvn dockerfile:build`