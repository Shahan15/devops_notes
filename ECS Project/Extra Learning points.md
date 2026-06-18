
#### Cache Mounts

By default, a docker container is isolated. it doesn't have access to your hard drive. Also docker containers are ephemeral (temporary). So when a specific step in the `Dockerfile` is run, the temporary container instance is deleted and any temporary files are thrown away. 

a **Mount** is a bridge between these isolated instances and your hard drive. When we attach a mount we are telling docker write the files to this location in the hard-drive. This allows the files to exist even after the container is off. 

##### So how is this related?

When we run Go application. the code is compiled. it translates every line and saves these files (called `.a` files) into a local folder called `Compiler Cache` 

So when we run it a second time, with a mount attached - like for example if we change a print statement or something. Docker checks the local hard-drive sees the compiled code and packages and sees these haven't changed. so it uses that. 


#### AWS networking/Infrastructure how it all ties together

We have our image in ECR - Elastic Container Registry. This is just a repo to store your image

Then we have ECS Cluster - Elastic Container Service. Cluster just means 'grouping' for your container deployments. like you might have a cluster for production or staging etc. 
	 ECS makes you handle the infrastructure required to run the containers. 

For Serverless ECS we can use Fargate 

However to Run the ECS - We need a Task Definition - This is a JSON blueprint that tells Amazon HOW to run your Docker Containers - its like a docker-compose. 


##### ALB 

Next we have an Application Load Balancer - This Sits INFRONT of our ECS and it distributes traffic and allows different microservices to use the same URL and also balances traffic i.e. if you have multiple EC2 instances, makes sure one isnt getting all the traffic. 

###### So how is this relevant to our project?

Although we don't have different microservices such as frontend, backend since Go consumes the frontend assets into the backend and serves the frontend files directly. So Everything is in one container.

Here ALB functions as a way to ensure High Availability. We would run multiple copies of that One container. So if there is loads of traffic the ALB will distribute the traffic to the identical containers. 
It also handles SSL/TSL termination - https


