
`docker images` - lists all docker images locally

`docker inspect image_id` - gives more details/comprehensive 

`docker rmi image_id` - Removes image. Wont remove image that is being used by a container. 

`docker system prune` - Removes all unused networks, unused images

`docker ps` - Current running containers

`docker stop` - stops the current running of a container

`docker rm` - Permanently deletes running container 

##### Making our Image Lighter
Our image is like 300mb which is slow and slows deployments and development and storage

To optimise this - we can use multi stage builds. This allows us to use multiple 'FROM' statements in our docker files 

Simple docker file
![[Screenshot 2026-05-27 at 12.28.12.png|434]]


Multi stage:

![[Screenshot 2026-05-27 at 12.28.28.png|449]]

this made our image almost 4-5x smaller. 

so how does this work?
To understand this we have to go into how docker functions under behind the scenes.
- When we write `RUN` or `COPY`, Docker bakes those files into a permanent layer on your hard drive. In a single stage build, Everything you pull into the container stays there forever.
  
  Multi Stage builds let you use temporary  construction scaffolding that gets deleted after the final image is constructed. 
  
  Step 1: The Heavy Lifting (build)
  We start with `FROM python:3.8` and then we run a heavy `RUN` command of 
  `RUN apt-get update && apt-get install -y gcc python3-dev libmariadb-dev pkg-config`. This makes the image jump from 100MB to 400 500MB
  For this the OS downloads lots of stuff, from compiler engines to packages configs etc. But these are never used. We download them in the first place because mysqlclient is written in C which requires a compiler.
  
   Step 2: Production Stage
   We start this stage with: `FROM python3.8-slim`. A clean slate. No Compilers or anything. 
   
   Step 3: selective Cherry-Picking
   `COPY --from=build /app /app` now from the first stage we grab only the /app folder. This now contains the pre-compiled Python packages. 


  
  









