#### AWS SQS

SQS is a Simple Queue Service

what is it used for? its a fully Managed message queuing service that allows software components to communicate asynchronously. 
- Asynchronously means working independently, components are not conflicting with each other
- A message is a small payload of data 

Lets say Service A i.e. Frontend wants to talk to the Backend payment service. But there are loads of requests coming to the backend at the same time, it cant process every single one at the same time. 
- Instead of returning a 504 error to the user. The request is sent to the backend, generates a order_id then writes the processing job to SQS, immediately returns a 202 Accepted to user browser and order_id. Service B will then pick up the processing job from SQS when it can 

#### Cognito 

This is a fully managed customer identity and access management service. It lets you add user sign up's, sign in's, access control and user management for web and mobile apps.


#### API Gateway

This is a reverse proxy, it sits between external clients i.e. web apps, mobile apps and your backend services or microservices. So instead of a client directly connecting to dozens of backend services. it hits a API gateway. This then maps incoming URL Paths (`/users, /payments, /orders`) to the correct service to handle the request. E.g. ECS Container, EC2 instance or AWS lambda. 

It also performs validations of JWT Tokens or OAuth tokens. 

