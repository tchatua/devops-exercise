# DevOps Exercise

## Process

- Fork this repository to your personal GitHub account. If you prefer, you may create your own private repository instead.
- Complete your project and push your code to your repository.
- Send a link to your public repo or invite [@joeles](https://github.com/joeles) and [@ShawnConn](https://github.com/ShawnConn) as collaborators if it is private.

## Project Requirements

### Overview

Write **Terraform** that can be used to deploy the three-tiered "click counter" application contained in this repository. Use the `front`, `back`, and `redis` images detailed below.

- Use Dockerfile in the `front` directory of this repo to build `front` image
- Use Dockerfile in the `back` directory of this repo to build `back` image
- Push built images to free container registry like Dockerhub, Github Packages, or AWS ECR
- Use any version of `redis` from Dockerhub
- Use Terraform and any additional scripting to deploy containers to a free-tier option in AWS like **EC2** and/or **Lambda + API Gateway**

If you have questions or something seems "not right", please reach out via email.

### Application details

- `back` app
    - Requires these ENV vars:
        - `REDIS_SERVER` - Address of Redis container in the form of `<host>:<port>`
    - Binds to port
        - `4000`
    - Provides these endpoints:
        - `/api/clicks` - Returns current click count
        - `/api/clicks/incr` - Increments click count by 1 and returns new click count
        - `/api/ping` - Returns static "pong" response
- `front` app
    - Requires these ENV vars:
        - `BACKEND_API_URL` - Address of the Back container reachable from the server-side in the form of `http://<host>`
        - `CLIENT_API_URL` -  Address of the Back container reachable from the client-side in the form of `http://<host>`
        - Note: depending on how you've networked the containers, these to vars could be the same
    - Binds to port
        -  `3000`
    - Provides:
        - `/`  - Click counter display/UI

- `redis` image
    - Requires these ENV vars:
        - None
    - Binds to port 
        - `6379`

### Extra credit

- Hide the `3000`/`4000` ports and make the service available over port `80` using the method of your choice
- Implement basic security measures
- Add DNS or other customizations

## Interview

During your online interview, we will:

- Walk through your solution and use it to deploy the application
- Discuss any challenges and successes of your implementation
- Cover additional questions, both technical and otherwise
- Answer any questions you may have

