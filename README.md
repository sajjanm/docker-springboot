# docker-springboot

This is a sample of a Spring Boot dockerized app. In order to run it locally, perform the following commands:

`docker build -t <your-namespace>/booksapp .`
The above command will build a docker image and tag it. 

`docker run -p 8080:8080 --rm <your-namespace>/booksapp`
This command will run the built docker image locally and here a port mapping is also being done with docker's port 8080
local port 8080.


Check if it is working by hitting the following endpoint:

curl http://localhost:8080/books/

# Running this application on AWS ECS Fargate

* Push the image to AWS ECR.
    1. Create a repo on AWS ECR and name it booksapp
    2. Select the just create repository on ECR, it will display the command required to push the image to ECR. 
        NB. If you have different profiles in AWS credentials files, make sure to select the appropriate profile in the very first command.
* Define a task in AWS ECS for defining a container.
    1. Under ECS, go to task definition and select Create new and select Fargate as the type
    2. Define the task memory and CPU size
    3. Add the container image URI and do a port mapping for port 8080.
* Run the task on the default cluster.
    1. Create a new cluster of 'Networking only' as the type.
    2. Let the config create a new VPC in the process.
    3. Enable Container Insights
* Check if the application is working.
    NB. Make sure that you have opened up the port 8080 for that Security Group under Incoming traffic
