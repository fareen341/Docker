# DOCKER 

<h1>What is Docker</h1>
<p>Docker is a container servicer used to isolate an app/environment so that it run without anoyone's interruption. So the chances of getting the error cuz of other service runnning on our computer get reduced. It takes some portion/resource from our computer.</p>
<p>In short, docker is a container in which you can store all your setup files(related to your product) and can give it to any of your client for  testing/deployment purpose. Also it utilize the container space and avoid the errors.</p>

<h1>How to create Docker image</h1>
<p>First we create docker image then we create container of that image. Image does'nt occupy memory space but container does.</p>
<p>Once we create a docker image we can run it anyware as in AWS, Heroku or any computer etc.</p>

<br>
<p>If someone else is running my created image that means they are using the same environment what we've used so minimal or no chances of getting the error</p>
<p>Image a scnario where you built an application in ubuntu and give it to someone for production the production guy workds on fedora linux system and it has different method of dealing with application so it is showing error to avoid this packaging your application into a container.</p>

<h1>Why Docker</h1>
<p>1)We used virtualization(vmware) technique using hypervisor it was a big success of problem where 10% of the hardware is in use and 80-90% were idle</p>
<p>2)After the virtualization we started using vmwares where we install OS on every virtual machine every OS costs us a lot </p>
<p>3)To save these OS cost we started using containers service which is using the same (OS)kernal we create many containers. One OS many containers. Which is docker.</p>

<p>i)virtualizating hardware(using vmware).</p>
<p>ii)virtualizating OS(using container).</p>
every container have different apps.</p>

<p>Two benefits we are getting by using this technique first virtualization meaning we using virtual machine of cloud platform and on top of that we are running containers.</p>

<p>Docker is created by solomon hykes which invented a company named dotcloud which is again named docker. they are writing all these things in go language</p>

diagram<br>

![Screenshot from 2022-03-04 17-35-20](https://user-images.githubusercontent.com/59610617/156760598-c22d3670-b7f7-43e8-9c5f-181062b0200b.png)


<h1>What is image and container</h1>

![Screenshot from 2021-12-08 11-21-15](https://user-images.githubusercontent.com/59610617/145155628-608e15ce-e5ec-4160-b2e7-eaeb86552340.png)


<h1>How to install Docker?</h1>
<pre>
$ yum install docker -y

//check the service
$ service docker status

//start the service 
$ service docker start

//start the docker service
$ chkconfig docker on

New group is created when installing docker 
$ cat /etc/group/
op: docker

We can add users to Docker group using the RedHat useradd command
</pre>

<h1>Docker commands</h1>
<p>To install and check the status of docker in ubuntu</p>
<pre>When we write docker and hit enter the first command we see we can use it to install the docker or follow other methods given on internet
After download check the version, $ docker --version will show the version meaning docker is installed successfully.

Checking the status of docker:
$ sudo systemctl status docker
If it says active and running that means we dont need to enable it

If it is inactive(dead) we need to enable it:
$ sudo systemctl enable --now docker
</pre>

<p>To pull simple hello-world docker image use command:</p>
  <pre>docker run hello world.</pre>
 
<p>To see all the images curruntly you have in your machine.</p>
<pre>docker images</pre>

<p>To push and pull own images</p>
<pre>
Pushing:

1)Login:
  $ docker login
 
2)Tag the image<br>
<pre>
  $ docker tag image_name:version username/image_name
  $ docker tag python-django:latest fareen341/python-django
  </pre>
  
 
3)After docker images you'll see the image listed
  $ docker images
  op: fareen341/python-django
  
4)Push to docker hub
  $ docker push fareen341/python-django
  
Now after few seconds the image will be listed in the repository section of dockerhub.

Pulling:
To pull the image see public view and grab the command and use to pull the image.
</pre>

<p>To remove an image from your machine</p>
<pre>$ docker rmi image_name</pre>

<p>To run the image</p>
After pull we can run the image using command:<br>
<pre>
$ docker run -p port docker-image-name
Example: $ docker run -p 8000:8000 fareen341/python-django
</pre>

<p>Dockerizing the django application</p>
<pre>
1)Create a django application.
2)Create requirements.txt file using:
  pip freeze > requirements.txt
3)Create a Dockerfile with no extension inside the project file where manage.py is.
4)Edit the Dockerfile:
  <pre>
   # Its a lightweight linux OS with python already installed
   FROM python:3.8-slim-buster

    # The working directory
    WORKDIR /app

    # Copy requirements.txt 
    COPY requirements.txt requirements.txt

    # Running the requirements.txt file
    RUN pip3 install -r requirements.txt

    # Copy all the folders
    COPY . .

    # Run the commands
    CMD ["python3", "manage.py", "runserver", "0.0.0.0:8000"]
</pre>

To ignore the virtual environment we created use the .dockerignore. file and add venv inside it
*/venv

5)Build the image using the command:
  $ docker build --tag name-of-image .    
  #tag is used to give name to the image
  #dot refers to the current folder
  
  Example:
  $ docker build --tag python-django .
  
6)Publish using the 8000 port
  $ docker run --publish 8000:8000 python-django
  
After this command we can see our application running on port 8000 on browser.
Docker will run each commands given in Dockerfile when we run it.
</pre>

<p>To list all the running containers</p>
This will list all the running docker images.
<pre>$ docker ps
$ docker ps --all      #this will show all the exited container
</pre>

<p>To stop the container</p>
<pre>
1)Do the docker ps, grab the id of the particular container which we want to stop.
2)Run docker stop container_id
  $ docker stop 398298163
</pre>

<p>To kill the running container</p>
<pre>
$ docker kill container_id
</pre>

<p>To list all the files and folders inside the app.</p>
<pre>$ docker run filename ls
EXample:
$ docker run python-django ls
</pre>

<p>To run the commands as in ls, pwd etc</p>
This will run the shell and we can execute the commands
<pre>
$ sudo docker exec -i -t 78cdb05b5163 sh

Run the commands 
ls
pwd
</pre>

<p>To check the logs</p>
We can see the logs of the container which is running.
<pre>$ docker logs container_id</pre>

<p>To completely remove docker from your system along with images and container, follow the below link</p>
<pre>https://askubuntu.com/questions/935569/how-to-completely-uninstall-docker</pre>

<p>To remove/delete the image</p>
<pre>$ docker rmi image-id
if it says error renponse from daemon: conflict: unable to delete df87b56050c2 (must be forced) - image is being used by stopped container then use:
  $ docker rmi -f image_id 

If you use the -f flag and specify the image’s short or long ID, then this command untags and removes all images that match the specified ID.
This command removes images being used by containers.
</pre>

<pre>
This cleans up the dangling images and dead containers.
  $ sudo docker image prune -f && sudo docker container prune -f 
</pre>

<pre>
you can use this command to see if you have hide images.

docker image ls -a

</pre>

<b>Running the docker pull image twice</b><br>
<p>Though we have run ubuntu image twice but still it is showing once on doing docker images meaning it only once download the image if it already exist it won't consume space, it'll run from local. Every images it search first locally and then download from hub. 
If image present locally then it won't be downloaded from docker hub.</p>

<b>Downlaoding particular version</b><br>
<pre>if we do docker run ubuntu: it runs latest ubuntu
to get particular version: docker run ubuntu:version</pre>

<b>Deatched mode</b><br>
<pre>$ docker run -d ubuntu sleep 60
To make it run in the background</pre>

<b>To execute commands inside the container</b><br>
<pre>$ docker exec img_id cat /etc/os-release</pre>

<b>docker run uses</b><br>
<pre>
1)attach/foreground
2)deatach/background(run in background): -d
Cuz if we run $ docker run container it'll run and stop but using -d it runs in the background
3)interactive mode: -it

$ docker run -it ubuntu
o/p: we'll be inside the container
this image is like virtual machine, we can download anything run anything inside this container
this is just like virtual machine
To get out of it: exit
</pre>

<b>Removing image. Reclamaining the space from host(Removing unwanted images from the host):
</b><br>
<pre>
$ docker rmi img_id
if it says image is in use by stopped container, force remove
1)docker rm container_id 		//to remove the container
	 docker rm container_id container_id container_id	//to remove multiple containers
	
2)docker rmi img_id
</pre>

<b>To force remove the image</b><br>
<pre>
$ docker rmi img_id --force
But after docker ps -a our container will still point to tht gone image
</pre>

<b>Interview: docker run VS docker pull</b><br>
<pre>
pull: only download the image
run: download image + run a container
</pre>

<b>docker inspect container_id</b><br>
<pre>
Have information of of env path, graphic drive etc. Detail info of our container
By default every container will have ip addresses.
</pre>

<b>Detailed info of container</b><br>
<pre>
What is activity that is hapenning with our container
$ docker logs container_id
</pre>

<b>Difference betn -a and all, as in docker ps -a</b><br>

<b>To use a image</b><br>
<pre>
$ docker run -p 8080:8080 
The first 8080 is for HOST
2nd one is for CONTAINER

Example:
$ docker run -p 8080:8080 -p 50000:50000 -v /your/home:/var/jenkins_home jenkins

-v: for volume
/your/home: this is for for host(should be available on host)
/var/jenkins_home: this is for container(should be available on container)

$ docker run -p 8080:8080 -p 50000:50000 -v /tmp:/var/jenkins_home jenkins
if for some reason if container goes down it'll store data on /tmp . so we can run the container again using the same command so it'll recover from that /tmp folder
</pre>

<b>Error</b><br>
<pre>
1)manifest: its not found
if we encounter this error then use the colon & version
</pre>

<b>Sample image(for sleep)</b><br>
<pre>
Dockerfile
FROM ubuntu:20.04        	//or :latest
ENTRYPOINT ["sleep"]		//the very first command(it can be yum to install some package)
CMD ['50']

//build an image
$ docker build -t sleepercell .

//running the image
$ docker run -d sleepercell

If we modify the Dockerfile and add few more command:
it'll never download the ubuntu again and other commands again which were already present, it'll start from the command which is not present.
So that is why it is called layer architecture(it can be reutilized the instruction which is written inside dockerfile/imagefile). 

Whenever we built image, its build using Dockerfile

Redis: in memory database(data will be stored in memory). V fast processing of data, real time processing of data

microservice: diving one application to multiple services(as in application, cache, db etc) & each application we'll run inside one image.

Example: votingapp application use microservices(python(for voting), redis, .net, db, nodejs). So we need 5 different container to run this image. So we nned:
i)5 containers
2)5 images
 first of all we need radis image, then votingapp(using python), then database, then .net, then node js

We can create an image for Nagios download cuz it takes long steps 
</pre>

<h3>Voting App</h3>
<pre>
METHOD 1: manuall process

To run sample voting application given by docker ppl:
1)clone there repo
2)get the necessary images so look the version of all these images in DockerCompose.yml and get those images
i)first we need redis image
	$ sudo docker run -d --name=redis redis:5.0-alpine3.10
ii)now we need vote application ->get inside vote
build the image using the current folder 
vote $ sudo docker build -t votingapp .
$ sudo docker images
	
//run the image(check the port on DockerCompose.yml file):
$ docker run -p 5000:80 --link redis:redis votingapp
always left is image i.e port 5000 and right is the container i.e port 80
Check on browser aws_dns:5000
	
iii)now we need db:
We need to run the environment varible for postgres
You can see on DockerCompose.yml they use 2 env variable postgres_user & postgres_pswd

$ sudo docker run -d --name=db -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres postgres:9.4
//-e: for env variable	

$ docker ps
//postgres container running

iv)now we need worker appln
Go to worker folder
worker $ sudo docker build -t workerapp .

//run image 
$ sudo docker run -d --link redis:redis --link db:db workerapp

v)now we need result
result $ docker build resultapp .

//run image it is web appln so look for port
$ sudo docker run -d -p 5001:80 --link db:db resultapp


CONCLUSION:
We need 5 virtual machines atleast using older technology. But here we using 1GB ram we're running complete application with two databases & 5 containers


METHOD 2: automate process using docker compose.
In the above method we run 3 different dockerfile.
We decide which container or image should run now.
We did all these things manually/individually.

To automate the above steps:
How to create multiple container in the single point of time?
-> Docker Compose(used to create multiple container in whatever order we want) it is basically yaml file. 
1)We need to downlowd docker compose(it has docker engine prerequisite).
2)Go to docker compose official page and copy paste the cmd to install it

Step 1: remove all the container and images we've created from above steps

Understanding DockerCompose:
1)build: is basicalliy build we used above i.e docker build ./vote  (. :from current dir, /vote: create vote folder)
2)They did not use build for redis cuz its image is available already.
3)They are Linking using depends on in docker compose file. So worker is linked with redis and db too.
Visit to download docker-compose(https://phoenixnap.com/kb/install-docker-compose-on-ubuntu-20-04)

Running docker compose:
$ docker-compose up
This single comand will run all 5 containers.

Check both the port aws_dns:5000 & aws_dns:5001 both app is running.

<b>Error:</b>
$ sudo docker rmi 4f73503d10e5
Error response from daemon: conflict: unable to delete 4f73503d10e5 (must be forced) - image is being used by stopped container
Soln: $ docker ps -a
remove all the stopped containers using $ docker rm exited_container_name
</pre>

<h1>Running the docker provided sample application voting app</h1>
<pre>
Step 1: Clone it
Step 2: We need redis container to run in background
$ docker run -d --name=redis redis:5.0-alpine3.10
--name: naming the container

Step 3: build the image go inside vote folder
$ ll		//will display vote folder
vote $ docker build -t votingapp .

Step 4: running the build image
$ docker run -d -p 5000:80 --link redis:redis img_name
why 5000: cuz dockerfile has 5000 port, 5000:80
so enable 5000 in ec2 security group
80: our application using it
--link: to link our application with redis db
redis:redis , for image: for container
if --link not working use -link

Next flow
Step 5: Install postgres sql
We need to use environment variable, if we dont give env variable it'll give error expected that 
example: 
docker run -d --name=db -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres postgres:9.4
o/p: postgres container will be up & running

Step 6: build worker application
go inside worker
worker $ docker built -t workerapp .

Step 6: running worker app
$ docker run -d -link redis:redis db:db workerapp

Step 7: cd result/
result $ docker built -t resultapp .

Step 8: running the image
$ docker run -d -p 5001:80 -link db:db resultapp


<b>Result: if we run the entire code in vmware we need 5 virtual machine atleast
And we're running all these in 1gb cpu machine, so container service is powerfull
</b>

Note: we need 5000 port no. in AWS
if customer hitting 5000 port he'll se vote app and if he'll hit 5001 then he'll see result app.


We have used 5 images and in that we use 2 images(redis, postgres) from dockerhub and wrote dockerfile for other 3

All these we are doing manually: creating image manually, creating container manually

Docker run in ad-hoc command(single command)
</pre>

<h1>Running all the 5 containers using docker compose</h1>
<pre>
What is docker compose?
To create multiple images, it is basically yaml file

Running all the 5 containers using docker compose:
In github read docker-compose.yml

inside this image they build vote app first & they have created 5 services
They have build all 3 images first and for other 2 they have used image
depends_on: for linking containers together  


Step 1: install docker compose from docker compose install page for linux run all the steps given to install docker-compose
$ docker-compose --version 
 
Step 2: go inside the example-vote app
example-vote $ docker-compose up
</pre>

<h1>Creating image for django(backend) react(frontend) using docker compose</h1>
<pre>
<pre>    
services:
  web:
    build: ./OnlineShop
    command: python manage.py runserver 0.0.0.0:8000
    ports:
      - "8000:8000"

  frontend:
    build: ./online-shop
    command: npm run start
    depends_on:
      - web			//meaning web container will run first
    ports:
      - "3000:3000"
</pre>

For docker compose to run there should be dockerfile in both frontend and backend
and the run
$ docker-compose up 

EXAMPLE:
https://github.com/fareen341/watch-app-docker-compose

<h1>Docker Components and Its related questions</h1>
<h3>Volumes</h3>
1. First of all data in container referes to data as in: Application logs, User upload files, Cache data etc.
2. In production env more than one container will be running for HA, so they should share the data using shared remote storage.

<h3>Port</h3>
$ -p <host_port>:<container_port>
-p: port

Everytime we see 2 ports and names given, which is speerated by colon then it'd follow the above like only host:container.

Example:
docker run -p 8080:80 my_web_app

explain: You are exposing port 80 of the container (<container_port>) to port 8080 on the host (<host_port>). It means that the application running inside the container, which listens on port 80, will be accessible from the host system at http://localhost:8080.

<h3>Network</h3>
1. In docker compose network is used for communication between different containers.
2. Example: in voting-app they have defined one custom named back-tier netweok and use that netweok in docker file.

<h3>Link and Depends on</h3>
1. We use --link option allows you to link the container to another container by its name or alias. 
2. In docker compose we run depends_on
3. We have:
	i. Default network
 	ii. User defined network
4. When you define services in a Docker Compose file without specifying any network, Docker Compose automatically creates a default bridge network for the services.
5. Each service is connected to this default network, and Docker Compose assigns a unique DNS name to each service based on its service name.
6. This default bridge network allows the services to communicate with each other using their service names as hostnames.

<h3>Services</h3>
Each service corresponds to a container in your multi-container application. Within the services section, you define the various attributes and settings for each service.
<pre>
version: '3'  # Specify the Compose file version (e.g., '3' is commonly used)

services:
  service1:   # Service name (can be any meaningful name)
    image: <image_name>:<tag>  # Specify the Docker image and its tag to be used for the service
    # Add other configurations for the service

  service2:
    image: <image_name>:<tag>
    # Add other configurations for the service
#You can define more services below if needed
</pre>

<h3>Scaling in docker compose</h3>
1. Scaling is like replicas, like we've deployment in k8s. So it create that number of containers
2. Example: For example, to scale the webapp service to have three replicas:
$ docker-compose up --scale webapp=3

<h3>Environment variable</h3>
1. Inline definition: giving in the same compose file:
<pre>
version: '3'

services:
  webapp:
    image: my_webapp_image:latest
    environment:
      - ENV_VARIABLE1=value1
      - ENV_VARIABLE2=value2

</pre>

2. External File:
<pre>
.env:
ENV_VARIABLE1=value1
ENV_VARIABLE2=value2



docker-compose:
version: '3'

services:
  webapp:
    image: my_webapp_image:latest
    env_file:
      - .env
</pre>


<h2>Override default configurations defined in a Docker Compose file</h3>
1. Docker Compose allows you to use additional Compose files to override or extend the configurations in the base docker-compose.yml file.
2. By default, Docker Compose looks for an optional file named docker-compose.override.yml and automatically reads it if present.
3. The settings in the docker-compose.override.yml file take precedence over the base file.
You can define additional services, networks, volumes, and other configurations in the override file.
For example, let's assume the docker-compose.yml file has the following configuration:
<pre>
version: '3'

services:
  webapp:
    image: nginx:latest
    ports:
      - "80:80"
    environment:
      ENV_VARIABLE: default_value
</pre>
You can create a docker-compose.override.yml file with the following content to override the environment variable:
<pre>
version: '3'

services:
  webapp:
    environment:
      ENV_VARIABLE: my_custom_value
</pre>
When you run docker-compose up, Docker Compose will read both files, and the ENV_VARIABLE will be overridden with the value from the docker-compose.override.yml file.

4. Using override file is helpfull when yoy've different environments for eg: Dev, Stage, Production.

<h3>Difference between the build and image attributes in a Docker Compose file</h3>
1. `build` used for building custom image. 
2. `image` used when we have existing image. Example: we've redis image for voting app and workerapp as a custom image.

<h3>Q: How can you monitor and troubleshoot Docker containers and their performance?</h3>
1. We can use k8s for automatically monitoring and handling. 
2. If we dont want to use k8s we can use prometheus tool or serive avaialble in AWS or cloudwatch container insights i guess.

<h3>Q: How do you handle secret management in Docker and containers?</h3>
So for conatiner db credential would be secret.
1. If we're using k8s then we can use secret feature of k8s.
2. We can use Docker secret for storing secret.
3. We can use AWS secret maanger for storing docker secret. See more: https://stackoverflow.com/questions/71704931/set-aws-secret-manager-value-in-docker-environment
</pre>
 

<h1>Extra</h1>
<pre>
To copy file from local to docker container:
docker cp foo.txt container_id:/foo.txt
Example:
$ docker cp test fd1a92d80971:/app/teste

Link followed: https://stackoverflow.com/questions/22907231/how-to-copy-files-from-host-to-docker-container
</pre>

<h1>Interview Questions</h1>
<pre>
Sure! Here are some common Docker and Docker Compose interview questions that you might come across:

Docker:

What is Docker? How does it differ from traditional virtualization?
Explain the basic architecture of Docker.
How do you create a Docker image? What is a Dockerfile, and what does it contain?
What is a Docker container? How is it different from an image?
How do you manage data persistence in Docker containers?
What is the purpose of Docker volumes and when would you use them?
What is the difference between Docker image and Docker registry?
How do you share Docker images with others?
Explain the concept of Docker layers and why they are important.
How can you secure Docker containers? What are some best practices?
Docker Compose:

What is Docker Compose, and why is it used?
How do you define services and their configurations in a Docker Compose file?
What are the benefits of using Docker Compose over individual docker run commands?
How do you scale services defined in a Docker Compose file?
What is the purpose of the depends_on attribute in Docker Compose?
How do you manage environment variables in Docker Compose?
Can you explain the networking in Docker Compose? How can services communicate with each other?
How do you override default configurations defined in a Docker Compose file?
What is the difference between the build and image attributes in a Docker Compose file?
How do you integrate Docker Compose with other orchestration tools like Kubernetes?
General Docker and Containerization:

What are the main benefits of using Docker in a development workflow?
How do containers contribute to continuous integration and continuous deployment (CI/CD)?
Can you explain the concept of container orchestration and why it is essential for production deployments?
What are the major differences between Docker and other containerization technologies, such as Kubernetes and Podman?
How does Docker support microservices architecture?
What is Docker Swarm, and how does it differ from Docker Compose?
Explain the concept of Docker networking and the available network drivers.
How can you monitor and troubleshoot Docker containers and their performance?
How do you handle secret management in Docker and containers?
What are some common challenges you might face when using Docker in production environments?
</pre>

 # Install package inside docker
<pre>
  $ apt update
  $ apt install nano
  # apt install -y git	
</pre>
