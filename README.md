# Extra-Knowledge

We can use Netlify to get free instance.<br>
We can use FreeNom to get free domain: The limitation is you can only get domains ending in .tk, .ml, .ga, .cf, or .gq<br>

<h1>What is Docker</h1>
<p>Docker is a container servicer used to isolate an app/environment so that it run without anoyone's interruption. So the chances of getting the error cuz of other service runnning on our computer get reduced. It takes some portion/resource from our computer.</p>
<p>In short, docker is a container in which you can store all your setup files(related to your product) and can give it to any of your client for  testing/deployment purpose. Also it utilize the container space and avoid the errors.</p>

<h1>How to create Docker image</h1>
<p>First we create docker image then we create container of that image. Image does'nt occupy memory space but container does.</p>
<p>Once we create a docker image we can run it anyware as in AWS, Heroku or any computer etc.</p>

<br>
<p>If someone else is running my created image that means they are using the same environment what we've used so minimal or no chances of getting the error</p>

<h1>Interview Question</h1>
<b>What is docker</b>
<p>Image a scnario where you built an application in ubuntu and give it to someone for production the production guy workds on fedora linux system and it has different method of dealing with application so it is showing error to avoid this packaging your application into a container.</p>

<h1>What is image and container</h1>

![Screenshot from 2021-12-08 11-21-15](https://user-images.githubusercontent.com/59610617/145155628-608e15ce-e5ec-4160-b2e7-eaeb86552340.png)


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
  $ dockerrun --publish 8000:8000 python-django
  
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
# ls
# pwd
</pre>

<p>To check the logs</p>
We can see the logs of the container which is running.
<pre>$ docker logs container_id</pre>
