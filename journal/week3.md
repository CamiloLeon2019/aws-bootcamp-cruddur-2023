# Week 3 — Decentralized Authentication

## Contents table

- [Cognito configuration](#cognito-configuration)

# Cognito configuration

I've created the user pool according to the configurations determined on the live stream:

![image](https://user-images.githubusercontent.com/49325152/224083459-aa19d7ab-be48-4a53-9100-8e4520a760c9.png)

After creating the environment variables on docker-compose.yml (we are not using Identity Pools), i've modified the App.js file and setting them up on the Amplify.configure function: 

````
Amplify.configure({
  "AWS_PROJECT_REGION": process.env.REACT_APP_AWS_PROJECT_REGION,
  "aws_cognito_region": process.env.REACT_APP_AWS_COGNITO_REGION,
  "aws_user_pools_id": process.env.REACT_APP_AWS_USER_POOLS_ID,
  "aws_user_pools_web_client_id": process.env.REACT_APP_CLIENT_ID,
  "oauth": {},
  Auth: {

    region: process.env.REACT_APP_AWS_PROJECT_REGION,
    userPoolId: process.env.REACT_APP_AWS_USER_POOLS_ID,        
    userPoolWebClientId: process.env.REACT_APP_CLIENT_ID,
  }
});
````

### Sign-in

Obtaining the following error on the sign-in as expected:

![image](https://user-images.githubusercontent.com/49325152/224176594-d00f0a56-7628-4c5c-bc34-6ad3adf90d77.png)

However, after doing the 'user creation' i've received a similar error by console:

![image](https://user-images.githubusercontent.com/49325152/224178566-4a10a7ca-201f-40c4-9a1d-9c606a66d97c.png)

So, we fixed it by using the following command to force the user confirmation

````
aws cognito-idp admin-set-user-password --user-pool-id  us-east-1_59FptcUv8 --username camilol --password Testing1234! --permanent
````

Then we are authenticated, making sure the name and preffered username values are configured for our first user:

![image](https://user-images.githubusercontent.com/49325152/224446393-a99ab909-2e4f-45ff-a287-af2338c4c236.png)

### Sign-up
