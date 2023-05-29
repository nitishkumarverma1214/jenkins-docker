# This repo will help you step the jenkins using docker

## Step to perform

1. pull the repo
2. create a docker network

```
docker network create jenkins
```

3. build the dockerfile

```
docker build -t myjenkins-blueocean:2.387.3-1 .
```

4. Run the jenkins image

```
docker run \
  --name jenkins-blueocean \
  --restart=on-failure \
  --detach \
  --network jenkins \
  --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client \
  --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 \
  --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.387.3-1
```

5. To setup jenkins password

```
docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword
```

6. Select the recommended plugins

7. setup the username and password
   ` username : jenkins-user password: Jenkins@123`

8. In the dashboard select the new item

9. Enter the project name and select the freestyle project
