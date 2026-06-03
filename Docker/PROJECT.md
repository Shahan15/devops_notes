
### APP.PY

![[Screenshot 2026-05-28 at 22.35.30.png]]

### DOCKER FILE

![[Screenshot 2026-05-28 at 22.35.40.png]]

### DOCKER COMPOSE FILE

![[Screenshot 2026-05-28 at 22.35.55.png]]



#### Explanation

So here we are building a simple flask/redis web app. the `(/)` root returns a welcome message and the `(/count)` returns the visitor count to the website. 

Key notes: 
- Redis is a fast lightweight database. it does not require a password or anything. the computer spins it up locally.
  
- When we download packages and libraries and such we in python we usually do it in a virtual environment (venv). This is also usually used to stop conflicts between different versions you may have installed in other projects or something. it also stops packages and libraries being installed globally on your machine. Anyone else using your app would need the EXACT SAME version of python and libraries installed globally or have to install the exact same version 
	- Since we are using docker we dont need to do this. Flask and Redis are containerised. All its dependencies, specific versions we used in development is packaged into one container. Anyone can pick up the app, run the container and it would work.  

- sometimes we can have old cached versions of our app (lets say we fixed a bug) so we need to run `docker-compose up --build`
  

#### Problems faced

##### ISSUE 1

<table>
  <tr>
    <td><img src="Screenshot 2026-05-28 at 22.50.26.png" width="350"></td>
    <td><img src="Screenshot 2026-05-28 at 22.50.58.png" width="350"></td>
  </tr>
</table>

- ISSUE: 
  One problem i faced was that docker couldnt find a 'myredis' and i would get the following error message: 
  `redis.exceptions.ConnectionError: Error -2 connecting to redis:6379. Name or service not known.`
  
  This error means that flask is looking for a host named 'redis' but cant find it. 
  
  SOLUTION:
   Here notice in image 2 (right one) we have 
```python
redis=Redis(host="myredis")
```

before i had `host='redis'` (the standard syntax) this parameter tells python the network address of where this Redis DB is? usually we would do host='localhost' if we were running redis directly on our computer. 

But we are actually running Redis in our Docker Container so it had to match our docker-compose file. 

##### ISSUE 2

<table>
  <tr>
    <td><img src="Screenshot 2026-05-28 at 23.03.23.png" width="350"></td>
    <td><img src="Screenshot 2026-05-28 at 23.03.43.png" width="350"></td>
  </tr>
</table>

ISSUE: When i first ran docker-compose up with my the docker file being image 1(on the left) i got the following error:
`ImportError: No module named 'flask'`

This is because pip install, by default installs Python packages deep into global system folder `(user/local/lib)`. So when we Run `COPY --from=build /app /app` we grab the /app directory but this doesnt actually contain Flask or Redis. 


SOLUTION: 
So here we have to tell python to download these packages into /app directly. we did this by 
`RUN pip install --target=/app flask redis` and `ENV PYTHONPATH=/app` to tell python where to look for modules. 
