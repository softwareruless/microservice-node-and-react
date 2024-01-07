# microservice-node-and-react
 I am sharing with you the project I did to improve myself.


# microservice-node-and-react App

While doing this project, I learned how to develop microservices with node.js. I run my project using 
Docker and Kubernetes and I can easily get output while developing. 
When you examine the file structure, you will see more than one folder.

**client**: There are components within a simple React application with which we can interact with endpoints.

**posts**: There are endpoints to create and list our 'Posts'.

```
URL: '/posts/create'
body : { title : "string" }
type : POST

URL : '/posts'
type : GET
```

**comments**: We create special comments for that post with the given 'postID' and list these comments again.
```
URL : '/posts/:id/comments'
body : { content : "string" }
type : POST

URL : '/posts/:id/comments'
type : GET
```

**moderation**: the created 'comments' are filtered at this stage. If there is a banned word in it, 'status' is updated as 'rejected', otherwise it is updated as 'approved'.

Endpoints in this service are not operated directly by a user. It is triggered thanks to the 'event-bus' service.


**event-bus**: event requests coming here are directed back to the services for processing by the necessary services.

For example, after a 'comment' is created, this event must be directed to the 'posts' service so that the comments of the same post can be updated in the 'post' service.

**query**: If a problem occurs in any of the microservices during operation, 'events' are stored here and processed again after the 'service' comes back to life.

**infra/k8s**: This directory contains deployment files for each service.

Additionally, services are accessed with the help of ingress-nginx.

The skaffold.yaml file was created to avoid running the code more than once during the deployment phase.

## Installation

Node, docker, kubernetes and skaffold must be installed on your computer.

```
skaffold dev
```
