# Week 1 — App Containerization

## Contents table

- [Setting up container environment](#setting-up-environment)
- [Issues committing](#docker-commit)
- [Notifications endpoint](#notifications-endpoint)
- [Postgres and DynamoDB installation](#db-install)
- [Docker on Windows](#docker-on-windows)

## Setting up environment

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

[Go back to top](#contents-table)

#### Building and running container

```
docker run --rm -p 4567:4567 -it -e FRONTEND_URL='*' -e BACKEND_URL='*' backend-flask
```
Curiousily this time it shows the json file formatted

![image](https://user-images.githubusercontent.com/49325152/220776910-906b9593-8c4b-4e79-a671-5462ce4f53e4.png)

Docker process being shown:

![image](https://user-images.githubusercontent.com/49325152/220776930-23a36cab-111a-4ba4-adca-75dde12a1bb4.png)

[Go back to top](#contents-table)

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

[Go back to top](#contents-table)

## Docker commit 

I encounter this error when trying to committ from gitpod:

![image](https://user-images.githubusercontent.com/49325152/220798269-3676369b-86f2-48d1-bde3-4c0693f710e7.png)

![image](https://user-images.githubusercontent.com/49325152/220798671-d7d2d5c6-8aad-4fd1-a227-1895a7bd8f2e.png)

I had to understand the output a little better in order to committ correctly:

    git config pull.rebase false: this will merge the changes from the remote branch into your local branch.
    git config pull.rebase true: this will reapply your local changes on top of the changes from the remote branch.
    git config pull.ff only: this will only allow fast-forward merges, which means that your local branch will be updated only if the changes from the remote branch can be applied cleanly on top of your local changes.

![image](https://user-images.githubusercontent.com/49325152/220798206-2f58f745-c99c-46a9-ae39-31472b91e03d.png)

[Go back to top](#contents-table)

## Notifications endpoint

### Backend
We create a new notification endpoint on openapi yml file (its preview feature for checking on api object is great) by adding a new path, we add /api/activities/notifications there and copy he content from another endpoint to use as a guide, we did it this time from home:

```
  /api/activities/notifications:
    get:
      description: 'Return a feed on activity for all of the followers and people i follow'
      tags:
        - activities
      parameters: []
      responses:
        '200':
          description: Returns an array of activities
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Activity'

```
Also, to have this information on the backend we need to modify the app.py file adding a new route there, the same name as we put on the yml file, we also need to create a new service on our services folder which will be the one where notifications_activities.py will be stored to have the objects retrieved:

![image](https://user-images.githubusercontent.com/49325152/220805859-49f5e077-5d86-4aae-83d5-175a6f1b1249.png)

### Frontend

We need to create new files for the js and css, basically by copying the same format from the Home page and sycnronizing the backend with the frontend by using:

```
 const backend_url = `${process.env.REACT_APP_BACKEND_URL}/api/activities/notifications`
```

![image](https://user-images.githubusercontent.com/49325152/220806610-cd6213d1-30d3-4274-b975-1b68e5317498.png)

Once that is syncronized we can do Composer up, npm install for the frontend and run the server:

![image](https://user-images.githubusercontent.com/49325152/221374352-ae26322a-a88a-4686-b135-74b1f4691d39.png)

## DB install

### Postgres

On docker-compose.yml:

````
  db:
    image: postgres:13-alpine
    restart: always
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=password
    ports:
      - '5432:5432'
    volumes: 
      - db:/var/lib/postgresql/data
````

Gitpod does not come with a PostgreSQL client pre-installed, so we need to install it manually with:

````
  - name: postgres
    init: |
      curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc|sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg
      echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" |sudo tee  /etc/apt/sources.list.d/pgdg.list
      sudo apt update
      sudo apt install -y postgresql-client-13 libpq-dev
````

After applying such commmands there i got the same error as Andrew:

![image](https://user-images.githubusercontent.com/49325152/221387313-16a65990-a754-48bc-a5db-572c446d1eb8.png)

So, it requires the host argument to look for the localhost, so we use:
````
psql -Upostgres --host localhost
````

![image](https://user-images.githubusercontent.com/49325152/221387748-65052dee-14c4-4c0e-9425-c861bccd366c.png)

![image](https://user-images.githubusercontent.com/49325152/221387881-d764da86-25c3-4dee-a603-71e7b87082f2.png)


### DynamoDB

````
  dynamodb-local:
    # https://stackoverflow.com/questions/67533058/persist-local-dynamodb-data-in-volumes-lack-permission-unable-to-open-databa
    # We needed to add user:root to get this working.
    user: root
    command: "-jar DynamoDBLocal.jar -sharedDb -dbPath ./data"
    image: "amazon/dynamodb-local:latest"
    container_name: dynamodb-local
    ports:
      - "8000:8000"
    volumes:
      - "./docker/dynamodb:/home/dynamodblocal/data"
    working_dir: /home/dynamodblocal
````

[Go back to top](#contents-table)

## Docker on Windows

After installing Docker on my laptop, i needed to upload the WSL kernel for my machine:

![image](https://user-images.githubusercontent.com/49325152/221442423-2dc0afbd-3116-4b77-a780-04e41f7f7e48.png)

I had to follow this guide to enable the Windows Subsystem for Linux: https://learn.microsoft.com/en-us/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package

After performing the steps described there, Docker has been installed on my computer:

![image](https://user-images.githubusercontent.com/49325152/221444083-1e27bf67-50cd-40be-b099-437449566ee2.png)

