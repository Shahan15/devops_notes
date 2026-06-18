
#### Cache Mounts

By default, a docker container is isolated. it doesn't have access to your hard drive. Also docker containers are ephemeral (temporary). So when a specific step in the `Dockerfile` is run, the temporary container instance is deleted and any temporary files are thrown away. 

a **Mount** is a bridge between these isolated instances and your hard drive. When we attach a mount we are telling docker write the files to this location in the hard-drive. This allows the files to exist even after the container is off. 

##### So how is this related?

When we run Go application. the code is compiled. it translates every line and saves these files (called `.a` files) into a local folder called `Compiler Cache` 

So when we run it a second time, with a mount attached - like for example if we change a print statement or something. Docker checks the local hard-drive sees the compiled code and packages and sees these haven't changed. so it uses that. 


