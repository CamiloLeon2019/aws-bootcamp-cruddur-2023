# Week 2 — Distributed Tracing

## Contents table

- [Setting up container environment](#setting-up-environment)

## Settign up Honeycomb

I watched Shala's video before this week as part of the prereqs for the ACBP (AWS Cloud Bootcampo Project), so i generated the API Key and enabled it on the gp env variables:

![image](https://user-images.githubusercontent.com/49325152/221980460-95c1d643-81b1-418a-9945-9d9bb48637c3.png)

Once the API key was set, I was able to obtain information from Honeycomb without too much context at the very beginning:

![image](https://user-images.githubusercontent.com/49325152/222326407-d3c84a71-b3a9-4fa0-95af-d388379a6163.png)

![image](https://user-images.githubusercontent.com/49325152/222326430-38f4e70e-e0b4-4baf-ad97-ada3445fc538.png)

It was great to know i was able to obtain data from the app to Honeycomb (at least without a context). Now after providing some context to it with a trace using:

````
from opentelemetry import trace

tracer = trace.get_tracer("home.activities")

````

We are able to get multiple traces, however we need to provide even more context, so we use:

````
with tracer.start_as_current_span("mock-data"):
````

With this we are able to get general data from the home dashboard and we can apply the same to other dashboards as well:

 
