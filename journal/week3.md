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

I received the confirmation code on my inbox and put it on the confirmation page:

![image](https://user-images.githubusercontent.com/49325152/224862663-92444f1a-28fd-4565-afff-a5c8dca98c34.png)

### Recover password 

After confirming i was able to signing up with the OTP, i also was bale to get the recovery code:

![image](https://user-images.githubusercontent.com/49325152/224864694-6d59f76e-cad9-4821-be25-3bf00af8fc6d.png)

![image](https://user-images.githubusercontent.com/49325152/224864766-41de1018-5127-44dc-81a7-50f288bf462f.png)

![image](https://user-images.githubusercontent.com/49325152/224864799-b9569fce-6b74-49e5-9437-a5d5926f6043.png)

Honestly, i am falling behind right now and i'll love to do the review of the code and make the confirmation page look prettier:

### JWT on the back-end

I validated the JWT was generated correctly:

![image](https://user-images.githubusercontent.com/49325152/224869570-7f9a13f4-ba4e-4e50-a109-8b1258b29198.png)

