# Deployment an app on AKS
This guide will walk you through deploying a Java application on Azure Kubernetes Service (AKS) and after deploying the application, 
you can use Java Diagnostic Tool (diag4j) to do some troubleshooting and monitoring.

## Prerequisites
- Prepare a container registry to store the application image.
- Run Docker in your local environment.

## Steps
- Build the application and generate a Docker image.
```bash
cd samples/sba-test-client

# Here packing OCI image with [Spring Boot Maven Plugin](https://docs.spring.io/spring-boot/maven-plugin/build-image.html)
./mvnw spring-boot:build-image
```

- Push the Docker image to the container registry.
```bash
# Replace the image name with your own container registry.
docker tag sba-test:latest <your-container-image>
docker push <your-container-image>
```

- Deploy the application on AKS.
```bash
# replace the placeholder in sba-test-app.yml with your own container image.
kubectl apply -f sba-test-app.yml
```

