This is a storage and distribution hub for your docker images. its like an online library where all your images live when not active in a container 

you can have: 
- Public registries - open to everyone, community provided
- Private registries - like AWS ECR, secure restricted. 

These are important: 
- streamline deployment - Easily accessed
- Enhanced collab
- Ensure consistency

DockerHub: [https://hub.docker.com/](https://hub.docker.com/ "https://hub.docker.com/")
	Public registry - its like docker github

we can push and pull our docker images from here. 

to do this we would first create the image: 
`docker build -t shahan2/flask-msql:v1 .`

![[Screenshot 2026-05-26 at 23.26.24.png]]
and we push this via: 
`docker push shahan2/flask-mysql:v1`

pull via: 
`docker pull shahan2/flask-mysql:v1`


##### Pushing our images to Amazon ECR 

What is ECR? - Amazon Elastic Container Registry 
this is a fully managed docker registry used to manage private docker images.

Once we make a repo in ECR - AWS gives you commands to authenticate your Docker to registry and push pull etc

- So after creating a registry. We authenticate our Docker using AWS CLI.
- Then we build our image, tag it and push it to the repo we made in ECR. 

All the commands required are provided by ECR Screen.


Error faced when running the last command of `docker run` of our image we pulled from AWS ECR (and creating a container from it) : 
![[Screenshot 2026-05-27 at 11.29.01.png]]

this error is because we dont have our container in our network and the containers cant communicate with each other. - So need to create it/add it to our network. 

```
# Create a custom Docker network
docker network create my-app-network

# Run a MySQL container on the custom network
docker run -d --name mydb --network my-app-network -e MYSQL_ROOT_PASSWORD=my-secret-pw mysql:8

# Run a Flask container on the custom network, mapping port 5002 and using the specified image
docker run -p 5002:5002 --network my-app-network 665727140634.dkr.ecr.eu-west-2.amazonaws.com/flask-mysql:latest
```

also instead of building the image locally, we can pull it from our aws ECR Repo

![[Screenshot 2026-05-27 at 11.45.10.png]]