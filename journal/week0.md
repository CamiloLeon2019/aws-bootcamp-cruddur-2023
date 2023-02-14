# Week 0 — Billing and Architecture

Hello Andrew (or whoever is reviewing this)

It's my first time using and editing this file text, so i just had to look up on the internet what the heck is a markdown file and i found it very easily on <a href=https://www.ionos.com/digitalguide/websites/web-development/what-is-a-md-file/>IONOS<a>. 

Now, i understand this would be the journal for every new progress that i have for the project so i'll try to document everything as far as i can. I was part of the live session last Saturday along with Margaret, Shala, Chris and you. I had a great time learning on how the project is going to be and understanding the value of the cloud onto this. I was at my job time back then and the day after, so just now i have the time to review all the documentation available, such as the project outline.
  
I already ahve some of the pre requisite knowldege and technologies (aws and github account) and i am reading everything to make sure i am up-to-date. I know that this is part of the homework challenges for this week so here is my IAM portal showing my admin account for my playersslayer96's aws account.
  
 ![image](https://user-images.githubusercontent.com/49325152/218612660-704a450a-b1f0-46e8-8e8c-6a834763363f.png)
  
 I am also part of a study group (not a team) which it is very useful to catch up besides the official discord group.
 
  ![image](https://user-images.githubusercontent.com/49325152/218608954-0ffd44d6-92d0-493c-8e4f-d46ea6a63c0e.png)
  
 To be honest, i feel excited and overwhelmed at the same time with so much stuff to watch and the time available for me, but i see this as a great challenge for me. 
 
  <h1> Homework journal 📝 </h1>
  
  The first task has already been done last Saturday along with you and i have some great takeaways from the classs, such as the general scope of the project, stakeholders, goals, methodology as well asimportant knowlegde to acquire throughout the whole bootcamp.
  
  <h2> Spend considerations 🤑 </h2> 
  
  ![image](https://user-images.githubusercontent.com/49325152/218624288-ae52761b-193e-4cf1-aeef-4eef4fdd563d.png)

  I have reviewed this as part of the AWS-CLF-C01 video of Andrew (big thanks to him for my certification) a couple of months ago, it was great to know how i can be spend and wasting money at some point if i don't use my budget and billing tools available. When entering to my billing dashboard i received a disclaimer that there were some IAM policies being updated, however my IAM user didn't need any update at all. I created my aws account around 6 months ago and haven't used it since the certification. I had EC2 and Cloudwatch services running with no charges (thank god!)
  
![image](https://user-images.githubusercontent.com/49325152/218631336-e8f927af-cc96-44a2-9c67-4ca2f1b4d1c7.png)


While reviewing Chirag's video iwas not able to get billing information for my IAM account correctly so i had to llo up for AWS documentation for help on this and i found this article which was very helpful: (https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_billing.html?icmpid=docs_iam_console#tutorial-billing-step1) 
  
 I configured the Cloudwatch billing alarm and recieve my first notification 😎.
  
  ![image](https://user-images.githubusercontent.com/49325152/218633050-fa1ea6d2-8e40-48d2-b3f0-0b6ab07e07a3.png)

  Watching the video was useful to see the how much money i've spent and i hope that by the end of this project my spent is as unexpensive as possible.
  
    <h2> Cloud Security 🔏 <h2>
  
  Watching an hour video seems interesting for me, however some concepts reviewd on the CLF-C01 cert course, such as IAM, but this Cloud security concept is something 'll definetily look into from now on. I think that services, data and app that is cloud-enabled is even more vulnerable to attacks as there are more attack surfaces being publicly available and even private.

I've done already the MFA for my root and IAM admin account, so i just did a refresher there and created my AWS Organizations account:

![image](https://user-images.githubusercontent.com/49325152/218816274-a694a4fc-e041-4074-915d-116dab6476a7.png)
  
Moving forward, I've reviewed the AWS Cloudtrail functionalities and how benefitial it is for logging and visiility of historical data. Following along Ashish cloudtrail logs creation, i created mine and i was relieved to see that creating this trail has <a href=https://aws.amazon.com/cloudtrail/pricing//>no additional charges <a>

  
