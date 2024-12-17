# Deploy an app on AKS
This guide will walk you through how to deploy a Java application on Azure Kubernetes Service (AKS). After deployment, 
you can use Java Diagnostic Tool (diag4j) to do some troubleshooting and monitoring.

## Prerequisites
- Prepare a container registry to store the application image.
- Run Docker in your local environment.

## Steps
1. Build the application and generate a Docker image.
```bash
cd samples/sba-test-client

# Pack OCI image with [Spring Boot Maven Plugin](https://docs.spring.io/spring-boot/maven-plugin/build-image.html)
./mvnw spring-boot:build-image
```

> Optionally, if you want to build your own application, try add this to the pom.xml file:
```
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <configuration>
                <image>
                    <name>sba-test:latest</name>
                </image>
            </configuration>
        </plugin>
    </plugins>
</build>
```

2. Push the Docker image to the container registry.
```bash
# Replace the image name with your own container registry.
docker tag sba-test:latest <your-container-image>
docker push <your-container-image>
```

3. Deploy the application on AKS.
```bash
# replace the placeholders <namespace> & <container-image> in sba-test-app.yml with your own container image just created.
kubectl apply -f sba-test-app.yml
```

