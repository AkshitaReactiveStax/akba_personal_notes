```
docker --version
```

docker engine and cli version is different from docker desktop version . they are managed independently . 


```
docker ps       # Shows running containers  
docker ps -a    # Shows all containers (including stopped ones)
```
gives a list of containers running or non-running on your machine . 


```
docker stop <container_id>     # Stop a running container 

docker rm <container_id>       # Remove a container

docker rmi <image_id>          # Remove an image  
```


```
docker pull ubuntu
```

```
docker run -it ubuntu bash
```
-it flag is to interact with the ubuntu container and run bash . 



```
docker build -t my-java-app .
```

This command is used to **build a Docker image** from a Dockerfile.

• **docker build** → This command creates a Docker image based on the instructions in a Dockerfile.

• **-t my-java-app** → The -t (or --tag) flag is used to assign a **name** (tag) to the image. Here, the image is named my-java-app.

• **.** → The dot (.) specifies the **build context**, meaning it looks for the Dockerfile in the current directory.



```
docker run my-java-app
```
This command is used to **run a container** based on the my-java-app image.

• **docker run** → Starts a new container from the specified image.

• **my-java-app** → The name of the image that the container will be created from.



**What happens when you run these commands?**

1. docker build -t my-java-app .

• Reads the Dockerfile in the current directory.

• Copies necessary files and installs dependencies.

• Creates an image named my-java-app.

1. docker run my-java-app

• Creates a container from the my-java-app image.

• Runs the application inside the container.

• If the app is a web server, it runs inside the container but won’t be accessible unless ports are exposed.



for creating a functional docker image through a dockerfile :

```
# Use a base image with OpenJDK
FROM eclipse-temurin:17-jdk-alpine 
# Alpine-based JDK (lightweight)

# Set the working directory inside the container
WORKDIR /app

# Copy the JAR file into the container
COPY target/my-spring-boot-app.jar app.jar

# Expose the port (should match the application.properties server port)
EXPOSE 8080

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
```

**Pros:**
✅ **Lightweight** – Uses an **Alpine-based** JDK, reducing the final image size (~100MB).

✅ **Fast build** – Minimal layers, making it easy to build and deploy.

✅ **Simple and effective** – Good for local development and quick deployments.  

**Cons:**
❌ **Runs as root** – This can be a security risk in production.

❌ **No user permissions set** – If the container is compromised, an attacker has root access.



```
# Use a base image with OpenJDK
FROM eclipse-temurin:17-jdk  # Full JDK (not Alpine)

# Create a non-root user
RUN groupadd --system spring && useradd --system --create-home --gid spring spring

# (Optional) Install additional tools (commented out)
RUN #apt-get update && apt-get install -y netcat && rm -rf /var/lib/apt/lists/*

# Switch to the non-root user
USER spring:spring

# Use a build argument to specify the JAR file location
ARG JAR_FILE=target/*.jar

# Copy the JAR into the container
COPY ${JAR_FILE} app.jar

# Run the application
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

**Key Features:**

• **Uses eclipse-temurin:17-jdk (not Alpine)** → A standard JDK, but larger than Alpine.

• **Creates a non-root user (spring)** → Improves security by running the app as a non-privileged user.

• **Uses ARG JAR_FILE=target/*.jar** → Allows flexibility in specifying the JAR file dynamically during build time.

• **(Optional) Installs additional tools (netcat)** → This part is commented out, but it shows how to install utilities if needed.

• **Switches to USER spring:spring** → Ensures the application doesn’t run as root.

  

**Pros:**
✅ **More secure** – Runs as a non-root user, reducing security risks.

✅ **Flexible build** – Uses ARG JAR_FILE for dynamic JAR selection.

✅ **Can install dependencies if needed** – Useful for debugging or additional tools.


**Cons:**
❌ **Larger image size** – Since it’s not using Alpine, the image is bigger (~200MB+).

❌ **More complex build** – Requires extra setup to create a user and manage permissions.

  

**When to Use?**

• Best for **production environments** where **security** is a priority.

• When you need **user permissions and flexibility** in specifying the JAR file dynamically.

• If you might need **extra system tools** (e.g., netcat, curl), which is easier on a full JDK image.


---------------------------------------
**How to See Directories Inside a Running Container?**


You can **explore the container’s filesystem** using these commands:

**🔹 Option 1: Run an Interactive Shell in the Container**

If the container is **already running**, use:
```
docker exec -it <container_id> sh
```

or, if the container has bash installed:
```
docker exec -it <container_id> bash
```

• This opens a **terminal inside the container**.

• You can now use normal Linux commands like:
```

ls -l   # List files in the current directory

cd /app # Move into the /app directory

pwd     # Show the current directory
```


```
docker images 
```
to check all the images in your docker 


```
docker run -d -p 8080:8080 --name my-container my-java-app
```

**Explanation:**

• -d → Runs the container in **detached mode** (in the background).

• -p 8080:8080 → Maps port **8080 on your machine** to port **8080 inside the container** (should match the EXPOSE 8080 in your Dockerfile).

• --name my-container → Gives the container a name (my-container).

• my-java-app → The name of the **Docker image** you created earlier.



---------------------------------------

#### search docker images in docker registry

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#search-docker-images-in-docker-registry)

docker search ubuntu docker search --limit 10 ubuntu

### to delete everything (images ) in the local docker system, please stop all the containers

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#to-delete-everything-images--in-the-local-docker-system-please-stop-all-the-containers)

docker system prune -a

### to prune docker volumes

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#to-prune-docker-volumes)

docker volume prune

### to list docker volumnes

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#to-list-docker-volumnes)

docker volume ls

### List all Docker Images

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#list-all-docker-images)

docker images -a

### list all docker images’ hashcodes only

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#list-all-docker-images-hashcodes-only)

docker images -q --no-trunc

### list all docker images’ full hashcodes only

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#list-all-docker-images-full-hashcodes-only)

docker images -q --no-trunc

### List All Running Docker Containers

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#list-all-running-docker-containers)

docker ps

### List All Docker Containers

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#list-all-docker-containers)

docker ps -a

#### how to check the ip address of a running container *( you need to provide the container id in the end)

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#how-to-check-the-ip-address-of-a-running-container---you-need-to-provide-the-container-id-in-the-end)

docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}'

### Start a Docker Container

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#start-a-docker-container)

docker start

### Stop a Docker Container

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#stop-a-docker-container)

docker stop

### Kill All Running Containers

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#kill-all-running-containers)

docker kill $(docker ps -q)

### View the logs of a Running Docker Container

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#view-the-logs-of-a-running-docker-container)

docker logs

### View the logs (with follow mode) of a Running Docker Container

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#view-the-logs-with-follow-mode-of-a-running-docker-container)

docker logs -f

### Delete All Stopped Docker Containers

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#delete-all-stopped-docker-containers)

### Use -f option to nuke the running containers too.

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#use--f-option-to-nuke-the-running-containers-too)

docker rm (dockerps−a−q)dockerrm−f(docker ps -a -q)

### Remove a Docker Image

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#remove-a-docker-image)

docker rmi [](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md)

### Delete All Docker Images

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#delete-all-docker-images)

docker rmi $(docker images -q)

### Delete All Untagged (dangling) Docker Images

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#delete-all-untagged-dangling-docker-images)

docker rmi $(docker images -q -f dangling=true)

### Delete All Images

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#delete-all-images)

docker rmi $(docker images -q)

### Remove Dangling Volumes

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#remove-dangling-volumes)

docker volume rm -f $(docker volume ls -f dangling=true -q)

### Open a Shell into a running container

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#open-a-shell-into-a-running-container)

sudo docker exec -it bash

### To inspect the internals of a built image

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#to-inspect-the-internals-of-a-built-image)

docker image inspect mongo or rmohr/activemq

### to pull docker images from docker hub (or any other registry)

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#to-pull-docker-images-from-docker-hub-or-any-other-registry)

```
docker pull mysql or docker pull rmohr/activemq
```

### to build a docker image based on a Dockerfile [with the tag mentioned with -t flag]

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#to-build-a-docker-image-based-on-a-dockerfile-with-the-tag-mentioned-with--t-flag)

```
docker-build -t /my-springboot-image -f Dockerfile-name .
```

### creates a tag first argument is source tag and 2nd argument is tag under which we are saving it

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#creates-a-tag--first-argument-is-source-tag-and-2nd-argument-is-tag-under-which-we-are-saving-it)

```
docker tag
```

### check the docker images (it should show your image build with proper tag name)

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#check-the-docker-images-it-should-show-your-image-build-with-proper-tag-name)

```
docker images
```

### push the newly built docker image to docker hub (or any other registry to which you logged in earlier)

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#push-the-newly-built-docker-image-to-docker-hub-or-any-other-registry-to-which-you-logged-in-earlier)

```
docker push /my-springboot-image
```

### ### Docker run an image

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#-docker-run-an-image)

### To Run a mongo image

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#to-run-a-mongo-image)

```
docker run --rm -p 27017:27017 --name some-mongo -d -v /Users//mydataDir:/data/db mongo
```

### To run a mySql image

[](https://github.com/FullStackLabsCa/boca-spring-boot-app/blob/main/boca-spring-boot-app-instance/Docker-Commands.md#to-run-a-mysql-image)

```
docker run --rm --name=test-mysql2 -v /my/own/datadir=/var/lib/mysql --env=“MYSQL_ROOT_PASSWORD=mypassword” --env=“MYSQL_USER=myuser” --env=“MYSQL_PASSWORD=mypassword” mysql
```


---------------------------------------

