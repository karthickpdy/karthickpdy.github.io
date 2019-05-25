---
title: Noobs guide to building a chatbot using Lex — Integration with Facebook
layout: post
---

We already have a functioning bot from the last post. If you have not read it please follow the steps in it and build a working bot as this post is a follow up to it. What is the use of bot if it is not linked to any platform, so here we will integrate our bot to Facebook messenger and access it from messenger. Lets get started.

### Step 1 : Create a Facebook app and Facebook Page

1. First we need to create a Facebook app. Go to [Facebook Developer page](https://developers.facebook.com/) and create a new app.

1. Go to “Add a product” and add **Facebook messenger** and you will be taken to the settings page of messenger.

1. You need to generate the **Page Access Token.**  You can either create a **new Facebook page** or select an existing page(Make sure the page is not published if you are just testing).

1. Once you provide a page, page access token is generated.

1. Go to “Dashboard” and get the **App Secret.**

Thats all we need from Facebook for now.

### Step 2 : Creating channel in Lex

1. Go to Amazon Lex console and go to settings tab and **create an alias**.

1. Go to the **Channel tab**and choose **Facebook** channel.

1. Provide the name, description and the Alias you created in the settings.

1. Provide a random text as **Verify Token**. This will be used as authentication for the calls from Facebook. You need to provide the **same Verify Token in Facebook**.

1. Get the Page Access Token and App Secret key from Facebook app as mentioned and fill in them.

1. Click**Activate** and a callback url should be generated for you.

1. Click **Build** and build the bot .

The settings should look something like below:
<p>
<img style="height:500px;width:500px" src="https://cdn-images-1.medium.com/max/3316/1*PmiZmE_v52IBuM0VRua29w.png">
</p>

### Step 3 : Configure callback in Facebook

Now that we got the callback url we need to configure it in Facebook app we created.

1. Go to the Facebook app we created.

1. Copy the **callback url** from Lex and provide it in Webhook settings in messenger.

1. Provide the **same Verify Token**as you gave in Lex channel settings.

1. Provide the events **messages, messaging_postbacks, messaging_optins**and verify and save.

1. Select the page and click on subscribe in the Webhook window to listen to chat from the page.

<p>
<img style="height:500px;width:700px" src="https://cdn-images-1.medium.com/max/3640/1*gbEMK-b6PwqZVCLpgTod_Q.png">
</p>



### Step 4 : Make the page to send events to our bot

1. Go to **Settings** in your Facebook page.

1. Select **Messenger Platform** from the left tab.

1. You will see your Facebook app being listed there.

1. Set the role as **Primary Receiver.**

<p>
<img style="height:400px;width:800px" src="https://cdn-images-1.medium.com/max/2584/1*UynyDqMjcOwHxSM8U2gtNw.png">
</p>




That’s it, now we are all set to chat with our bot. You can go to the Facebook page you created and click on **Send Message** to start chatting.

If all well well, Facebook messenger will be able to communicate with our Lex Bot and you will get response as below.

<p>
<img style="height:600px;width:600px" src="https://cdn-images-1.medium.com/max/2000/1*EXQROrGO7kcSny6ZxJOeTA.png">
</p>


*If you liked this story, feel free to reach out to me at [Kaizen Coder](https://kaizencoder.com/).*