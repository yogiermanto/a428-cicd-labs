# a428-cicd-labs

Repository untuk Kelas Belajar Implementasi CI/CD

# Running jenkins

docker network create jenkins

docker run \
 --name jenkins-docker \
 --detach \
 --privileged \
 --network jenkins \
 --network-alias docker \
 --env DOCKER_TLS_CERTDIR=/certs \
 --volume jenkins-docker-certs:/certs/client \
 --volume jenkins-data:/var/jenkins_home \
 --publish 2376:2376 \
 --publish 3000:3000 --publish 5000:5000 \
 --restart always \
 docker:dind \
 --storage-driver overlay2

docker run \
 --name jenkins-blueocean \
 --detach \
 --network jenkins \
 --env DOCKER_HOST=tcp://docker:2376 \
 --env DOCKER_CERT_PATH=/certs/client \
 --env DOCKER_TLS_VERIFY=1 \
 --publish 8080:8080 \
 --publish 50000:50000 \
 --volume jenkins-data:/var/jenkins_home \
 --volume jenkins-docker-certs:/certs/client:ro \
 --volume "$HOME":/home \
 --restart=on-failure \
 --env JAVA_OPTS="-Dhudson.plugins.git.GitSCM.ALLOW_LOCAL_CHECKOUT=true" \
 myjenkins-blueocean:2.426.2-1
