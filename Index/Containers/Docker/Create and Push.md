# Create and Push

---

[http://blog.shippable.com/build-a-docker-image-and-push-it-to-docker-hub](http://blog.shippable.com/build-a-docker-image-and-push-it-to-docker-hub)

# **Step-by-step instructions**

Follow the steps below in order to build and push your Docker image.

# **Step 1: Prep your machine**

- Create a GitHub repository that will hold the code to build the image. If you do not have your own Dockerfile or application, please feel free to clone our sample here: [https://github.com/devops-recipes/node_app](https://github.com/devops-recipes/node_app)
- Create an account on [Docker Hub](https://hub.docker.com/).
- Install Docker on your local machine. [Refer to the Docker [Getting Started Guide](https://docs.docker.com/get-started/)]
- Login to Docker Hub: `docker login` with your credentials. [Refer to the [docker login docs](https://docs.docker.com/engine/reference/commandline/login/) for a complete reference]

    docker login --username=yourhubusername --password=yourpassword

# **Step 2: Build and Push image**

- Your Dockerfile will look something like this:

**Dockerfile**

    FROM readytalk/nodejs
    
    # Add our configuration files and scripts
    WORKDIR /app
    ADD . /app
    RUN npm install
    EXPOSE 80
    
    ENTRYPOINT ["/nodejs/bin/npm", "start"]

- Build your image by executing the `docker build` command. `DOCKER_ACC` is the name of your account `$DOCKER_REPO` is your image name and `$IMG_TAG` is your tag

    docker build -t $DOCKER_ACC/$DOCKER_REPO:$IMG_TAG .

- Now, you can push this image to your hub by executing the `docker push` command.

    sudo docker push $DOCKER_ACC/$DOCKER_REPO:$IMG_TAG