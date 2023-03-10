# Week 2 — Distributed Tracing

## Contents table

- [Setting up tracing](#setting-up-tracing-on-different-platforms)
- [Observability vs Monitoring](#observability-vs-monitoring)
- [My Cloud Journey](#my-cloud-journey)
- [Homework challenges](#homework-challenges)

# Setting up tracing on different platforms

## Honeycomb

I watched Shala's video before this week as part of the prereqs for the ACBP (AWS Cloud Bootcamp Project), so i generated the API Key and enabled it on the gp env variables:

![image](https://user-images.githubusercontent.com/49325152/221980460-95c1d643-81b1-418a-9945-9d9bb48637c3.png)

Once the API key was set, I was able to obtain information from Honeycomb without too much context at the very beginning:

![image](https://user-images.githubusercontent.com/49325152/222326407-d3c84a71-b3a9-4fa0-95af-d388379a6163.png)

![image](https://user-images.githubusercontent.com/49325152/222326430-38f4e70e-e0b4-4baf-ad97-ada3445fc538.png)

It was great to know i was able to obtain data from the app to Honeycomb (at least without a context). Now after providing some context to it with a trace using:

````
from opentelemetry import trace

tracer = trace.get_tracer("home.activities")

````

[Go to top](#contents-table)

## X-Ray

Traces on X-ray being shown 

![image](https://user-images.githubusercontent.com/49325152/222942277-68175e3e-247e-4126-937e-74b6c059b92d.png)

[Go to top](#contents-table)

## Cloudwatch logs

Logs group for backend-flask 

![image](https://user-images.githubusercontent.com/49325152/222942294-8b490ce7-8c43-494a-b424-aad0712abb0f.png)

![image](https://user-images.githubusercontent.com/49325152/222942197-4f2c25d3-6b06-40ca-a659-b0ab9d1d17aa.png)

[Go to top](#contents-table)

## Adding Rollbar

I've been trying to get access to rollbar, however it seems their page is having login issues:

![image](https://user-images.githubusercontent.com/49325152/223019791-ca0171a1-1521-4c7c-8bb3-0f63720205b8.png)

![image](https://user-images.githubusercontent.com/49325152/223019795-7620395a-220a-4878-bdad-1236df9f5e50.png)

I added the rollbar instrumentation and route on the backend app, however it seems i am getting difficulties on the rollbar integration:

![image](https://user-images.githubusercontent.com/49325152/223019938-6b28e73a-c37c-407b-b6aa-6bfc57bfe7a0.png)

I ended up hard coding the rollbar access token to the code and obtaining data and errors:

![image](https://user-images.githubusercontent.com/49325152/223322676-08014fa4-17f0-4990-b8f9-86d5918a0510.png)

![image](https://user-images.githubusercontent.com/49325152/223322748-4fa35b49-1460-419c-bb76-45c54650aa7e.png)

[Go to top](#contents-table)

## Observability vs Monitoring

Having a brief look into Chirag's video about these two topics about logging from our applications, provides me a concept that Monitoring is about what is important to you and Observability is doing a deep look into what is going on. So, the Monitoring part of your application collects as much logs as possible and triggers and alert as soon as something is wrong, while Observability checks on the behavior of the application and provides you with the context to know what specifically is going on.

![image](https://user-images.githubusercontent.com/49325152/222877833-aa20c612-ec4a-49f5-a797-08abb0bf1663.png)

I created a CloudTrail trail and storing the CloudWatch logs on a new S3 bucket:

![image](https://user-images.githubusercontent.com/49325152/222937792-ea1df54f-a603-4bcf-af6e-bcd53317af61.png)

[Go to top](#contents-table)

## My Cloud Journey

I've watched Open Up The Cloud video about the cloud roles available for me and do the homework:

![imagen](https://user-images.githubusercontent.com/49325152/222986620-6f17f106-f2b7-48f6-b401-592d48eb6539.png)

I've reviewed 5 open positions available through Glassdoor and LinkedIn:

![imagen](https://user-images.githubusercontent.com/49325152/222986502-30befb65-87dd-49a4-accf-e16d35857688.png)
![imagen](https://user-images.githubusercontent.com/49325152/222986508-e983d42e-bfec-40ac-baae-8405c8e026c6.png)
![imagen](https://user-images.githubusercontent.com/49325152/222986515-d4af84c4-1729-472d-adfc-004587bd6819.png)
![imagen](https://user-images.githubusercontent.com/49325152/222986525-8369978f-73e7-428e-bdc9-c1e1044d5edd.png)
![imagen](https://user-images.githubusercontent.com/49325152/222986529-15325e6b-752b-4165-842e-2e544d15fbf6.png)

[Go to top](#contents-table)

# Homework challenges 

## Custom spans

We are able to get multiple traces to get general data from the home dashboard (to a obtain information about the current timestamp and the result length (200 HTTP code). We can apply the same to other dashboards as well, so I've added a custom span using the same logic as the one used for the app.now and result.lenght spans. I have done it on the notifications_activities.py to get it on a different dashboard:

````
    with tracer.start_as_current_span("home-notifications-mock-data"):
      span = trace.get_current_span()
    now = datetime.now(timezone.utc).astimezone()
    results = [{
      'uuid': '68f126b0-1ceb-4a33-88be-d90fa7109eee',
      'handle': 'Camilo Leon',
 
 ...
    span.set_attribute("app.user_name", results[0]['handle'])
    return results
````

![image](https://user-images.githubusercontent.com/49325152/222802051-76cf141b-ab24-4615-b340-70d88586fe02.png)

However, i do not get the username string span as i planned:

![image](https://user-images.githubusercontent.com/49325152/222802823-2cba732c-043f-4709-b9a4-5a2d60a71d4f.png)

I realized that the big mistake i made and i should have though before (silly me!) is the indentation of the span and set_attributes:

![image](https://user-images.githubusercontent.com/49325152/223323176-b64ee3ce-5d3f-4fc5-8a27-37e21e36b80d.png)

Now, i see the user name that was hard coded on the notifications app as an attribute of the honeycomb span created:

![image](https://user-images.githubusercontent.com/49325152/223323417-cb555b5a-af2a-4bcd-a25c-0fffe4859db5.png)

[Go to top](#contents-table)

## Custom query 

I've added a new query on Honeycomb where i was able to get the average duration of a request, the maximum and how many of them, grouping them by the user name attribute i created on the notifications section:

![image](https://user-images.githubusercontent.com/49325152/223326014-f4aa4307-b6be-4fc9-ab9d-29852a2e98ee.png)

![image](https://user-images.githubusercontent.com/49325152/223326146-b893cd42-ee1b-4a69-9705-934696dcd08f.png)

I've also added a new board where this query is shown:

![image](https://user-images.githubusercontent.com/49325152/223326346-63f223f8-662d-402d-af0c-8188df1757f5.png)

[Go to top](#contents-table)
