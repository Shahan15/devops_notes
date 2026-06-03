
So we made a simple web app in VS code![[Screenshot 2026-05-26 at 10.14.50.png]]

it just prints Hello World. Then we made the Docker File to make the image: 
![[Screenshot 2026-05-26 at 10.15.22.png]]


Then we ran the command: 

`docker build -t hello-flask .`

`-t` lets you name the image, in this case it is hello-flask


Then to actually run the container we just created we ran: 

`docker run -d -p 5002:5002 hello-flask`

`-d` --> runs the container in 'detached' mode meaning running it in the background 

`-p 5002:5002`  --> this maps port 5002 on our machine to port 5002 in the container 

and then the name of the image 'hello-flask'


Before we were doing `python3 app.py` to run the application. but now when we go to: 
http://127.0.0.1:5002/ --> you can see this is running fine. The container is running 

`docker stop d0ffb5f82022` --> stops container

d0ffb5f82022 is the container id
