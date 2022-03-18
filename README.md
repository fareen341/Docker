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
 
2)Tag the image
  $ docker tag <image_name>:version username/image_name
  $ docker tag python-django:latest fareen341/python-django
 
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

