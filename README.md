# 1. Build docker image with react app

### 1. Make a `Dockerfile` file with the following content and add it to the project root.
```
FROM node:9.6.1

# set working directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# install and cache app dependencies
COPY . .
RUN npm install
EXPOSE 3000

# start app
CMD ["npm", "start"]
```

### 2. Make a `.dockerignore` file with the following content and add it to the project root.

```
node_modules
```
### 3. Built the docker image by running the following:

```
docker build -t app_name
```

### 4. Now, the app shold be able to run locally by running: 
```
docker run -p 5000:5000 app_name
```

# 2. Push the app to DockerHub

### 1. Creat a repository in DockerHub to put the app and run ``docker login`` to follow instruction to login.

### 2. Tag the image by running: 
```
docker tag image_id repo_name/app_name:tag
```
### 3. Push to DockerHub
```
docker push repo_name/app_name
```

# 3. Deploy on AWS
### 1. Login to AWS console and choose `Elastic Container Service` from `All Services`.

### 2. Go to `Task Definitions` and click `Create New Task Definition`, it will ask for some information to create the task.

### 3. After finish creating task definition, select the Task Definition you just create and click `Action` and choose `Run Task`.

### 4. You can view the Task in `Clusters > the clusters you choose in step 3 > task you created in step 2`, once the `Last status` change from `PENDING` to `RUNNING`, you can copy the public ip address to view your app.