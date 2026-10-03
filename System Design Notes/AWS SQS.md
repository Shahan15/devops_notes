
SQS is a Simple Queue Service

what is it used for? its a fully Managed message queuing service that allows software components to communicate asynchronously. 
- Asynchronously means working independently, components are not conflicting with each other
- A message is a small payload of data 

Lets say Service A i.e. Frontend wants to talk to the Backend payment service. But there are loads of requests coming to the backend at the same time, it cant process every single one at the same time. 
- Instead of returning a 504 error to the user. The request is sent to the backend, generates a order_id then writes the processing job to SQS, immediately returns a 202 Accepted to user browser and order_id. Service B will then pick up the processing job from SQS when it can 