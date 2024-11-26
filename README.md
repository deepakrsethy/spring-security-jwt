# spring-security-jwt

## JWT
JSON Web Token
Commonly used for manging authorization.
The idea behind JWT is to create a standard way between two parties to communicate securely.
Uses RFC 7519 common standards
Widely used for authorizartion.

## Need for JWT

# HTTP : Stateless protocol
No state or session is maintained in HTTP interactions. So each request/interaction between the client and the server has to be self sufficient.
Which means it should contain everything that is required by the server to serve the request.

Problem:
When the response is dynamic and we want to implement some type of Authorization for the resources. it becomes a overhead to share the user information in each request.
Then how the WebApplications work. It does not ask us to provide Authentication upon visiting each url/page. So how is this done?
It could be done using below technologies
- Session Token
- JSON Web Token (JWT)

### Session Token:

#### Case study:
A customer calls customer care to complain about the new Television he bought. 
Before the customer care can help the customer , the customer has to authenticate him self by providing his credentials ( customerId, name, registred email id, phone number etc.)
Once the customer is authenticated, the customer care hears the customer out. List out everything in this system and share the complaint number. 

Now for subesquent interaction by the customer with the customer care, the customer does not need to authenticate himself again. The customer can share the complaint number shared the by the customer care.
From this complaint number all the details of the customer can be pulled off. The customer care will keep on maintaing this complaint number, till it is resolved or deleted.

<img width="509" alt="image" src="https://github.com/user-attachments/assets/b1047d87-af10-44b6-a9b5-bfeb12180867">


This complaint number is an example of Session Token, how the system uses it to server client requests.

When the client/user authenticates itself with server then the server creates a session with a session id and share the same with the client response. 
The client then saves this sessonid information in the cookies and share the same with the server in the subsequent requests in the header of the request. 
This is most popular mechanism for authorization. 

#### Problems with session
It is assumed that there is only one monolithic application which behaves the server.

But in case of microservices where there are multiple instances of same server, then it may be the first request will go instance-1 of the server, then the second request may go to instance-2 of the server.
So maintaining session id will be difficult.

To fix this,we may use a shared radis cache, where the session information can be stored. All the services will refer to this share radis cache for the session information. But now we have created a single point of failure.

Or to fix this issue we may maintain the session information in the load balancer itself and always forwards the request for particular session to a particular server always. This will decrease the efficiency of the microservice architecture.
This is called sticky session pattern. 

When there are multiple services are involved to serve a client request the session Id need to be shared among them making it difficult to maintain.

### JWT Token:

#### Case study: (Continued ...)
In case sessionId, the complaint no was shared with customer 
In case of JWT, the server sends a JWT token. The client may save the token 
<img width="908" alt="image" src="https://github.com/user-attachments/assets/c0cdd412-2427-4b80-963e-8d70611a7b70">
