Allows Management of multi container docker applications 
	Allows you to define all your services in a single file and manage them collectively

Docker-compose.yml file --> this lists all the services your application needs. its a blueprint that describes each container. which image to use, which port to expose. 
	This allows you to spin up your entire application with one command. And allows you to manage all of them very easily. Also you don't need to create a custom network. 

Why is this important: 
- Makes development and testing easier 
- Ensures consistency - works in all environments 
- Enhances teamwork - every team member is using the same environment, can share code easily 

Example: 
![[Screenshot 2026-05-26 at 22.58.55.png]]

`version` - Which version of the file format to use
 
`services` - we list all the different parts of our app i.e. Web service, Flask and database service 

`build` - This tells docker compose to build the web service from the docker file in the current directory 

`ports` - port to expose 

`depends on` - docker-compose will start this first before starting the web service  i.e. will start the database server


to start the docker compose we use `docker-compose up`

and `docker-compose down` to terminate it. 
we can also use `docker-compose logs` to see the logs 