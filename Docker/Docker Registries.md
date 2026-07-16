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



to tag image example:

docker tag memos-ecs:latest 446276073026.dkr.ecr.eu-west-1.amazonaws.com/memos-ecs:latest

##### The Breakdown

#### 1. `docker tag`

This tells the Docker CLI that you want to create an alias for an image that already exists locally on your MacBook Air. It does not create a copy or duplicate the image files; it just adds a new name tag to the exact same image ID.

#### 2. `memos-ecs:latest` (The Source)

This is the name and version tag of the image currently sitting on your local machine that you just finished building.

#### 3. `446276073026.dkr.ecr.eu-west-1.amazonaws.com/memos-ecs:latest` (The Target)

This long string is the explicit address blueprint required by AWS. Docker needs this entire format to know where to upload the image on the internet. It breaks down into three core components:

| **Component**           | **Example from your command**                  | **What it means**                                                                                                                    |
| ----------------------- | ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| **AWS Registry Domain** | `446276073026.dkr.ecr.eu-west-1.amazonaws.com` | Your specific AWS Account ID (`446276073026`) and the specific region (`eu-west-1`, which is Ireland) where your ECR registry lives. |
| **Repository Name**     | `/memos-ecs`                                   | The specific bucket/repository inside your ECR console created to hold this project's images.                                        |
| **Image Tag**           | `:latest`                                      | The version label for this build.                                                                                                    |


docker push 446276073026.dkr.ecr.eu-west-1.amazonaws.com/url-shortner:latest