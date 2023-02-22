# Week 1 — App Containerization

## Contents table

[Setting up container environmnent}(#Setting-up-environment)
[Setting up container environmnent}(#Setting-up-environment)

### Setting up environment

#### Installing backend

I've followed the instructions and get flask installed on the container and obtaining the json file

```
#changes directory to /backend-flask
cd backend-flask

#sets  the environment variables to be run
export FRONTEND_URL="*"
export BACKEND_URL="*"

#gets the python/flask server runnning on port 4567
python3 -m flask run --host=0.0.0.0 --port=4567

```
![image](https://user-images.githubusercontent.com/49325152/220764000-9e92a6cf-b84b-4f13-b309-54dadfa04607.png)
![image](https://user-images.githubusercontent.com/49325152/220764152-45cb0f1f-7c10-4f28-9ec0-4700b533419d.png)
![image](https://user-images.githubusercontent.com/49325152/220764754-66187c42-ac6c-4d3c-9868-798116232b06.png)

#### Building and running container

```
docker run --rm -p 4567:4567 -it -e FRONTEND_URL='*' -e BACKEND_URL='*' backend-flask
```
Curiousily this time it shows the json file formatted

![image](https://user-images.githubusercontent.com/49325152/220776910-906b9593-8c4b-4e79-a671-5462ce4f53e4.png)

Docker process being shown:

![image](https://user-images.githubusercontent.com/49325152/220776930-23a36cab-111a-4ba4-adca-75dde12a1bb4.png)

### Installing frontend

```
FROM node:16.18

ENV PORT=3000

COPY . /frontend-react-js
WORKDIR /frontend-react-js
RUN npm install
EXPOSE ${PORT}
CMD ["npm", "start"]
```

I have no idea why the port 8000, 5432 and 46093 were opened:

![image](https://user-images.githubusercontent.com/49325152/220785781-292f5fa4-5381-45bf-ab6c-074854a27ca8.png)

![image](https://user-images.githubusercontent.com/49325152/220786496-189c2f7d-e127-48e8-8314-7a1317450353.png)

