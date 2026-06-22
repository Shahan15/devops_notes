 Docker provides default networking options used to manage how containers communicate: 
 - Bridge Network - Network option for containers on the same machine. Containers can communicate with each other using their own IP addresses. Isolated from the Host machine network
 - Host - A container uses the Host machine directly. No distinction between Host and Container
 - None - No network interface at all. Its like a room with no doors or windows. No network access at all

Note: Each container has its *own* IP address

Flask and MySQL live in their own containers. Here we are linking these and making it so they are able to communicate. To do this, we have to make a virtual network inside the host computer. 


To link containers together we use MySQLdb and create a custom network:  

![[Screenshot 2026-05-26 at 17.15.06.png]]

and we run: 
`docker network create my-custom-network` 

This will allow us to connect our flask and mysql together

then we run: 
`docker run -d --name mydb --network my-custom-network -e MYSQL_ROOT_PASSWORD=my-secret-pw mysql:8`

This command spins up your database. Here is what each piece of the syntax does:

- `-d`: Run in **detached mode**. This keeps the container running silently in the background so it doesn’t hijack your terminal screen.
    
- `--name mydb`: This is crucial! You are naming this container sandbox `mydb`.
    
- `--network my-custom-network`: You are dropping this database container right into the private neighborhood you created in Phase 1.
    
- `-e MYSQL_ROOT_PASSWORD=my-secret-pw`: The `-e` flag sets an **Environment Variable** inside the container. The official MySQL image looks for this specific variable to automatically set the database master password.
    
- `mysql:5.7`: The frozen image Docker downloads from the cloud to build this sandbox.

When you run your Flask container, it sits in the background listening.

When you type `http://127.0.0.1:5002/` into your browser:

1. Your browser hits your **Host machine (your laptop)** on port `5002`.
    
2. Docker forwards that request directly inside the isolated Flask container workspace.
    
3. Inside the workspace, the Flask app triggers the `hello_world()` function.
    
4. The Flask app reaches out across the private `my-custom-network` to the container named `mydb`.
    
5. `mydb` answers back with its version number.
    
6. Flask renders the text onto your screen.


Next we build the image: 
`docker build -t hello-flask-mysql .` --> this creates the image of our app. its like a .exe file for an app

`-t` this allows us to tag the image 

next we actually build the container: 
`docker run -d --name myapp --network my-custom-network -p 5002:5002 hello-flask-mysql`


|**Component**|**What it Means**|**Technical Purpose**|
|---|---|---|
|**`docker run`**|**The Core Action**|Tells Docker to create a brand new container from an image and start it up.|
|**`-d`**|**Detached Mode**|Runs the container silently in the background. It frees up your terminal immediately so you can keep typing other commands while the app runs.|
|**`--name myapp`**|**Container Naming**|Assigns the friendly name `myapp` to this running instance. If you don't provide this, Docker will randomly assign a funny name (like `determined_bohr`). Naming it makes it easy to run commands like `docker logs myapp` or `docker stop myapp`.|
|**`--network my-custom-network`**|**Network Isolation**|Plugs this container directly into an existing virtual network called `my-custom-network`. This allows this container to easily talk to other containers (like a MySQL database) on that same network using just their container names as hostnames.|
|**`-p 5002:5002`**|**Port Mapping**|Bridges the gap between your host machine (Mac/PC) and the isolated container. It follows the pattern `HostPort:ContainerPort`. It opens up port `5002` on your actual computer and routes all traffic directly into port `5002` inside the container where the Flask app is listening.|
|**`hello-flask-mysql`**|**The Blueprint (Image)**|This is the final argument and tells Docker _which_ image blueprint to use to spawn this container. It will look for `hello-flask-mysql` locally on your machine, and if it can't find it, it will try to pull it from Docker Hub.|

 _Analogy:_ It's what happens when you double-click the installer and the actual application opens up on your screen.

