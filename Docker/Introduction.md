So what are **containers**?
- **Containers** are lightweight portable units for running applications. They bundle the application alongside all of its dependencies ensuring it runs consistently across different environments. - so the application should run smoothly across desktop, laptop, phone, production env etc.

by 'Application' we mean a single component of code like a Flask Script. It does NOT mean the entire multi piece system 

![[Screenshot 2026-05-23 at 20.10.43.png]]

-  **Containers** live above the Docker Engine. Each container containing the app and its required libraries and binaries for it to run

- Below this is the Host OS (Mac OS, Windows etc)

- Below is the actual Infrastructure, this is what the OS is running on. 
  
the docker engine provides the environment to build, run and manage containers 

Benefits of Containers: 
- Isolation of applications - prevents application conflicts. Like App A could run python 3.7 and App B could run 3.8 etc 
- Eliminates the 'Works on my machine' thing - like when the app only works on the dev's computer because his computer has all the dependencies/configs. 
	- How does this actually work? What does this mean? 
	  When we write code, the code doesn't actually talk physical screen or RAM or Hard Drive. 
	  
	  Instead the code relies on basic system files (`.dll` files on windows and `.so` files on Linux) to do everything. So when we want to print something to the console or whatever. these low level libraries handle it. 
	  
	  containers doesn't hold the code only; it holds a copy of all the Linux system files and libraries the app needs to function. 
	  
	  So when we run it for example on a windows or mac laptop. Docker Engine acts as a translator. it grabs the Linux call to the disk or whatever translates it into a raw command to the OS. so no matter which OS it is, it understands. 



Docker - Platform for developing and managing containers. key components: 
- Docker Engine - literal engine powering everything. Core software that runs the containers
- Docker Hub - repo for finding and sharing Docker images. App store for docker images
- Docker Compose - allows management of multi container docker applications. 

Images - These are templates for creating containers. its like a snapshot of an application at a certain point in time. - Immutable. 
	We make these using docker files
	 ![Screenshot 2026-05-24 at 20.08.46.png](app://eb7517261d53ae17b6d8d7f50ec32dee63ef/Users/shahan/Documents/Obsidian%20Vault/Screenshot%202026-05-24%20at%2020.08.46.png?1779649732353)

Containers - these are running instances of the images 


COMMON INTERVIEW QUESTION: 
What is the difference between Containers and Virtual machines? 

When we spin up a VM - like an AWS EC2 instance - a piece of software called a **Hypervisor** simulates a brand new, blank computer. So it loads the guests chosen OS, that can be Linux, Windows, Mac or whatever. But this takes a lot of resources and gigabytes of space. and RAM to run background OS tasks

a Container doesn't need to simulate anything. it just creates an isolated sandbox for the application to run. So Instead of packing an entire OS, the container only holds the application code and binaries. It uses the docker engine to translate the binaries to speak to the OS. This makes Containers highly portable, isolated, resource efficient and takes seconds to start up. 



What is a DockerFile?
- This is a series of instructions to create an image
- Each instruction creates a layer in the image - easy to track changes and optimised builds. 
- They allow for repeatable builds. So you can create exact same environment multiple times. 

5 key commands in docker file: 
- `FROM` - Specifies base image to use for the docker image. e.g. if you have a python image you use python base image etc
- `RUN` - executes commands in container. used to install packages or update dependencies 
- `WORKDIR` - sets the working directory for subsequent instructions. It looks to see if a folder path defined in `WORKDIR` exists inside the container. If it doesn't, **it creates it**. it doesn't put any local files here. it is empty. 
- `COPY` - this copies the files from where we define and dumps it into the folder that `WORKDIR` has created.
- `CMD` - Specifies the command to run when the container starts
 ![Screenshot 2026-05-24 at 20.08.46.png|313](app://eb7517261d53ae17b6d8d7f50ec32dee63ef/Users/shahan/Documents/Obsidian%20Vault/Screenshot%202026-05-24%20at%2020.08.46.png?1779649732353)


Also, In modern software engineering, we use Microservices. This means One container does exactly one job. so e.g.: 
- Flask Container - run python web server and handle requests etc 
- MySQL Container - Run the database engine, manage table files and handle data storage. 


![[Screenshot 2026-05-27 at 12.13.02.png]]

- **`apt-get update`** - This tells the container to download the latest list of available packages and software versions from the official Ubuntu/Debian servers. 
    
- **`&&`** - "if the first command succeeds, immediately run the next command."
    
- **`-y`** - This automatically answers "yes" to the terminal's prompt asking, _"Are you sure you want to install this software and use up disk space?"_ 
    
- **`\` (The Backslash)** - code formatting trick. It tells Docker that the command continues onto the next line. 