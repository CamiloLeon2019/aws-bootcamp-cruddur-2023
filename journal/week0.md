# Week 0 — Billing and Architecture

Hello Andrew (or whoever is reviewing this)

It's my first time using and editing this file text, so i just had to look up on the internet what the heck is a markdown file and i found it very easily on <a href=https://www.ionos.com/digitalguide/websites/web-development/what-is-a-md-file/>IONOS<a>. However i've noticed that this can be used so much better buy checking other's markdown file as a table of contents, so here it is 
  
 ## First steps

- [x] [Pre-requisites](#pre-requisites).
- [x] [Create a billing alarm](#create-sns-topic--alarm).
- [x] [Create a budget](#budget-and-notifications).
- [x] [Create EventBridge rule for a service health issue](#create-eventbridge-rule-for-a-service-health-issue).
- [ ] Open a support ticket and request a service limit at *AWS Console -> Support center -> Create case -> Looking for service limit increases?*.
- [X] Create a Github repository (https://www.github.com).
- [X] Login into Gitpod with github account and create a Gitpod workspace (https://www.gitpod.io).
- [x] Explore github.com/codespaces as an alternative of a CDE.
- [x] Momento: obtain AWS token and configure cli (https://www.gomomento.com).
- [X] Create Lucidchart account (https://www.lucidchart.com).
- [X] Create a free-tier Honeycomb account (https://www.honeycomb.io).
- [X] Create a free-tier Rollbar account (https://www.rollbar.com).
- [x] [Draft & conceptual diagram](#draft--conceptual-diagram).
- [x] [Logical Architectural diagram](#logical-architectural-diagram).
- [ ] [CI/CD Pipeline diagram](#architectural-diagram-of-cicd-logical-pipeline).
- [x] [Review all the questions of each pillars in the Well Architected Tool](#aws-well-architected-tool).

 ## Pre-requisites
  
Now, i understand this would be the journal for every new progress that i have for the project so i'll try to document everything as far as i can. I was part of the live session last Saturday along with Margaret, Shala, Chris and you. I had a great time learning on how the project is going to be and understanding the value of the cloud onto this. I was at my job time back then and the day after, so just now i have the time to review all the documentation available, such as the project outline.
  
I already have some of the pre requisite knowldege and technologies (aws and github account) and i am reading everything to make sure i am up-to-date. 
 
 ![image](https://user-images.githubusercontent.com/49325152/219844208-20e2613b-a3d9-40b7-8551-db8f7b6f2e43.png)

 Link to my journal on github: 
 
 I know that this is part of the homework challenges for this week so here is my IAM portal showing my admin account for my playersslayer96's aws account.
  
 ![image](https://user-images.githubusercontent.com/49325152/218612660-704a450a-b1f0-46e8-8e8c-6a834763363f.png)
   
 To be honest, i feel excited and overwhelmed at the same time with so much stuff to watch and the time available for me, but i see this as a great challenge for me. 
 
 ## <h1> Homework journal 📝 </h1>
  
  The first task has already been done last Saturday along with you and i have some great takeaways from the classs, such as the general scope of the project, stakeholders, goals, methodology as well asimportant knowlegde to acquire throughout the whole bootcamp.
  
  
  
  <h2> Spend considerations 🤑 </h2> 
  
  ![image](https://user-images.githubusercontent.com/49325152/218624288-ae52761b-193e-4cf1-aeef-4eef4fdd563d.png)

  I have reviewed this as part of the AWS-CLF-C01 video of Andrew (big thanks to him for my certification) a couple of months ago, it was great to know how i can be spend and wasting money at some point if i don't use my budget and billing tools available. When entering to my billing dashboard i received a disclaimer that there were some IAM policies being updated, however my IAM user didn't need any update at all. I created my aws account around 6 months ago and haven't used it since the certification. I had EC2 and Cloudwatch services running with no charges (thank god!)
  
![image](https://user-images.githubusercontent.com/49325152/218631336-e8f927af-cc96-44a2-9c67-4ca2f1b4d1c7.png)


While reviewing Chirag's video iwas not able to get billing information for my IAM account correctly so i had to llo up for AWS documentation for help on this and i found this article which was very helpful: (https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_billing.html?icmpid=docs_iam_console#tutorial-billing-step1) 
  
 I configured the Cloudwatch billing alarm and recieve my first notification 😎.
  
  ![image](https://user-images.githubusercontent.com/49325152/218633050-fa1ea6d2-8e40-48d2-b3f0-0b6ab07e07a3.png)

  Watching the video was useful to see the how much money i've spent and i hope that by the end of this project my spent is as unexpensive as possible.
  
<h2> Cloud Security 🔏 </h2>
  
  Watching an hour video seems interesting for me, however some concepts reviewd on the CLF-C01 cert course, such as IAM, but this Cloud security concept is something 'll definetily look into from now on. I think that services, data and app that is cloud-enabled is even more vulnerable to attacks as there are more attack surfaces being publicly available and even private.

I've done already the MFA for my root and IAM admin account, so i just did a refresher there and created my AWS Organizations account:

![image](https://user-images.githubusercontent.com/49325152/218816274-a694a4fc-e041-4074-915d-116dab6476a7.png)
  
Moving forward, I've reviewed the AWS Cloudtrail functionalities and how benefitial it is for logging and visiility of historical data. Following along Ashish cloudtrail logs creation, i created mine and i was relieved to see that creating this trail has <a href=https://aws.amazon.com/cloudtrail/pricing//>no additional charges <a>

IAM users, roles, groups and policies have been checkd for my account as part of the certification course, so i had that already covered, anyways it's a great refresher. 
 
 I've copied the recommended CSPs provided by Ashish:

![image](https://user-images.githubusercontent.com/49325152/218886334-8abe6cab-cb7a-4479-aeff-7b6f3a5af3db.png)

It was difficult for me to understand the difference between regular policies and SCPs, but the general idea of the policies was understood and i really like the concept of configuring and managing them (as well as many other AWS services). 
      
<h2> LucidChart Diagram 👀 </h2>
      
 I have been doing the logical diagram along with Andrew, understanding the best practices that are required when doing a diagram for an application or a service:

![image](https://user-images.githubusercontent.com/49325152/219768111-e5c1e669-f1dc-466f-98c4-f8309bd8ca74.png)

Watching Andrew's video was very useful to know how to get external shapes and i liked how he was able to manage to get the svg for the momento service. Here is the link for my LucidChart diagram: https://lucid.app/lucidchart/d37f4bba-65b7-4bfd-b68d-3b22cb64a4fe/edit?viewport_loc=-444%2C20%2C2994%2C1430%2C0_0&invitationId=inv_9118be86-9d3c-4473-985d-0db5c08eafdc

  I understood that the napkin design and the actual napkin drawing was for this design so here is the one that i did (i hope its undestandable):
  
![1676696931830](https://user-images.githubusercontent.com/49325152/219842868-332b13de-6411-4f42-80e5-f386900377d5.jpg)
  
 The conceptual diagram was much easier to perform and i just copied directly from the original one and using the shapes that came by default on the LucidChart application, so here it's the design ad it's link:
  
  ![image](https://user-images.githubusercontent.com/49325152/219843413-46672066-10f0-48dd-a45d-11c804b67feb.png)
https://lucid.app/lucidchart/596703a1-f23f-4943-a12f-844adec9ef11/edit?viewport_loc=-622%2C-45%2C2994%2C1430%2C0_0&invitationId=inv_531edbcc-542d-4bfd-9298-b3581ddc90a2

      
