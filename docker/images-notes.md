# docker hub
make an account on http://hub.docker.com (public registry for docker images)
user: anandvimal

http://store.docker.com have certified docker images


# imperative approach

we start with some base image. using that image we create the intermediate container. make build image and commit it. push it to registry.

STEPS
1. pull the image -> FROM
2. run the container.  -> RUN
3. copy source code. -> COPY
4. build/compile
5. commit
6. push


---
1. First approach to make imperative image is to pull a vanilla image and install all dependencies for our app. example for a java based app. we will pull a vanilla image and install :
  - install jdk
  - install mvn
  - mvn compile

2. Second approach we choose an image which has all dependencies already install. Eg: there are images which come with java jdk and maven pre-installed.

---

1. for start lets clone our application code.  
`git clone https://github.com/schoolofdevops/voting-app-worker`  
2.  pull image which has maven.  
`docker container run -idt --name interim schoolofdevops/voteapp-mvn:v0.1.0 sh`
3. cd to /voting-app-worker directory. copy all contents of this dir to container-name/code dir in container. User below command:  
`docker container cp . interim:/code`  
to check if all contents are copied go in container and check  
`docker container exec -it interim sh`  
`pwd; ls`  
we can see with above
4. check if we have all dependencies:  
for linux version:  `cat /etc/issue`  
for maven version:  `mvn --version`  
for java version:  `java -version`  
if all looks good we can call maven to package this stuff:  
for mvn package:  `mvn package`  
5. once `mvn package` command finished you can notice a new `target` directory.  to run the /target/worker-jar-with-dependencies.jar file with java jar commnad.
`java -jar target/worker-jar-with-dependencies.jar`
this will launch the app but will not find redis as we never launched redis docker image. so this wont be a success run. now we need to commit the image as worker image is done. to commit first we need to exit the docker container `exit`.    
 - check all images by command `schoolofdevops/voteapp-mvn`  
 - commit the container with
    - `docker container commit container-CONTAINER_NAME userid/repositoryname:version` generic command
    - `docker container commit interim anandvimal/vote-worker-mvn:v0.1.0`
    - after commiting you will get a sha256 hash as a output that image is commited. to verify do `docker image ls` and you will see your image created with new REPOSTORY with name:   userid/repositoryname (anandvimal/vote-worker-mvn in this case) and TAG : version (v0.1.0 in this case). Also check the CREATED column it should show time from the last commit.  
    - you can verify some info about layers with `docker image history image-id` and `docker image inspect image-id`.
6. Now its time to push the image to docker hub. before that we will try to test the image to make sure we have the right stuff.  
   - first step will be to run the image  
    - `docker container run -idt anandvimal/vote-worker-mvn:v0.1.0 java -jar target/worker-jar-with-dependencies.jar`
    - once container is running check its logs `docker logs container-name` if we can see the logs which says its trying to connect to redis (as we dont have redis yet it will keep trying to connect) we can confirm its working as expected. that means we are ready to push it to docker hub. if we don't see the expected logs we can try debugging the app and
    -
    - `docker image push anandvimal/vote-worker-mvn:v0.1.0`


---

# declarative approach

convert all the instructions on imperative approach in a declarative file called Dockerfile. Feed dockerfile into docker build and get an image.  

## Dockerfiles

automating image builds with a docker file.

````
FROM schoolofdevops/voteapp-mvn:v0.1.0

WORKDIR /code

COPY pom.xml /code/
COPY src/main /code/src/main

RUN mvn package

CMD java -jar target/worker-jar-with-dependencies.jar
````





















-
