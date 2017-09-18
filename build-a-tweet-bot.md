# Serverless Event Processing: Building a TweetBot 

<p align = "right"><font size = "2">- Srushith & Ganesh Smarthyam</font></p>

<p align = "center"><font size = "4"><i><b>"By 2022, most platform as a service (PaaS) offerings will evolve to a fundamentally serverless model, rendering the cloud platform architectures dominating in 2017 as legacy architectures” - Gartner</i></b></font></p>

In September OSFY article, we demystified serverless computing. We also discussed pros and cons, technologies, use cases and challenges, etc. How about using serverless computing to simplify or automate your tasks? For example, wouldn’t it be nice to automatically retweet the tweets that has your favourite hashtags (such as #serverless or #opensource). That’s the topic we take up for this month’s article. We are going to implement a bot (let’s call it TweetBot) in which you can specify the hashtags to retweet in specified time intervals.  

In this article, start with writing an auto-retweeting code in Python and get it working in our machine. Later we deploy it in OpenWhisk on IBM Bluemix. For this article, we assume you already know fundamentals of Python programming. You need not know anything about OpenWhisk or Bluemix - we’ll introduce them to you in this article. 

## Developing the TwitterBot 

For writing the Python code for auto-retweeting, the prerequisite is that Python 3 is installed in your machine. 

The Twitter API provides programmatic access to read and write Twitter data, create a new tweet, read user profile and follower data, retweet, and more. For this, first you should must create a Twitter application (see https://apps.twitter.com/) and note down the OAuth credentials for the bot configuration.

The Twitter API in Python can be accessed using TwitterFollowBot Python module. Using this module, you can do much more than just retweeting like auto-following, auto-liking. For developing TwitterBot, you must install the module into a folder rather than the default bin directory. For that, use the following command:

````
pip install --target <target_folder> TwitterFollowBot
````

Let us now create a program that uses TwitterFollowBot Python module to retweet the latest ‘count’ number of  tweets with a specific phrase (‘#Serverless’ in our case). For that, we need to create a TwitterFollowBot instance. The TwitterFollowBot uses the config.txt file in the current directory to configure the bot. So, let us first configure the bot. 

For configuring the bot, you should create a “config.txt” file and fill in the following information so that the bot can connect to the Twitter API. Here are the entries in the ”config.txt” file:

````
OAUTH_TOKEN:			
OAUTH_SECRET:		API keys from 
CONSUMER_KEY:		the twitter app
CONSUMER_SECRET:
TWITTER_HANDLE: <your twitter handle>
ALREADY_FOLLOWED_FILE:already-followed.txt
FOLLOWERS_FILE:followers.txt
FOLLOWS_FILE:following.txt
USERS_KEEP_FOLLOWING:
USERS_KEEP_UNMUTED:
USERS_KEEP_MUTED:
````

The files “already-followed.txt”, ”followers.txt” and ”following.txt” contain the respective twitter ids. You must create these files - you can leave them empty, though. The rest of fields may also be left empty.

````
# Program to retweet five latest tweets based on a hashtag (#Serverless)
from TwitterFollowBot import TwitterBot

def retweet():
	# create an instance of the TwitterFollowBot
	# by default, the bot will look for a configuration file called config.txt 
           # in your current directory
	my_bot = TwitterBot()
	# autoretweets the 5(count) latest tweets that matches the hashtag
	my_bot.auto_rt("#Serverless", count = 5)
	return {'message' : 'retweeted successfully'}

retweet()
````

That’s short and sweet code! Let’s save it as “test.py” file and run it. 

<p align="center">
  <img src="https://user-images.githubusercontent.com/19647546/30533093-313de8e4-9c75-11e7-934e-f1c0afde938d.PNG" />
</p>

When you execute the Python script, it connects to the Twitter API and retweets. The result throws up a warning indicating that the “followers.txt” isn’t updated; you can just ignore that warning or update the files to get rid of the warning. The program displays the tweets that was retweeted, so we know it is working.  

After we got the code working in our machine, it is time to deploy and execute it in the cloud using serverless approach. We are going to use Apache OpenWhisk as the serverless platform. We will be using IBM Bluemix as the cloud platform to deploy the OpenWhisk action(s). 

## Apache OpenWhisk 

Apache OpenWhisk is an open source serverless cloud platform that executes functions in response to events at any scale. 

OpenWhisk was started by IBM and is now incubated by Apache. Adobe is an important contributor to the project and has contributed API Gateway. OpenWhisk executes functions (called actions) in response to events (called triggers). Since it is serverless, you just need to provide your code to execute; in specific, you don’t need to concern how to manage the lifecycle or operations of the underlying containers that execute the code. 

You can run OpenWhisk on your laptop, on-premise, or in the cloud. When running in the cloud, you could use a Platform as as Service (PaaS) version of the OpenWhisk provided by IBM Bluemix or you can provision it yourself into Infrastructure as a Service (IaaS) clouds, such as Bluemix, Amazon EC2, Microsoft Azure and Google Cloud Platform.

### Some key aspects about OpenWhisk:

<p align="center">
  <img src="https://user-images.githubusercontent.com/19647546/30533107-442e44b2-9c75-11e7-8103-ad1288f3544f.PNG" />
</p>

It's open source. If you want, you can explore the code and tinker with it and change it according to your requirements 
Support for a wide range of programming languages including Node.js 6, Python 3, PHP 7.1 and Swift 3.1.1
Actions (serverless functions) can also be custom executable programs packaged in a Docker container, i.e., you can run Docker images in OpenWhisk
Run it locally! None of the major serverless platforms provide this feature. You can build and run actions locally on your own hardware behind your own firewall and then deploy to execute in the cloud 

<p align="center">
  <img src="https://user-images.githubusercontent.com/19647546/30533442-f9eff02e-9c76-11e7-8199-b25d34ba6cac.PNG" />
</p>

## TweetBot using OpenWhisk

For using TweetBot in serverless approach, you need to install OpenWhisk in your machine and have a BlueMix account. For installing OpenWhisk, refer to https://console.bluemix.net/openwhisk/cli for the setup and configuration information. 

The beauty of serverless technology is that you don’t have to rewrite your entire application to go serverless: just tweak the plain code that runs in your machine and you’ll be fine! Surprisingly, our TweetBot requires only one change - it should have a main function with an input parameter (dictionary type) and is to be saved as a __main__.py file. 
 
<p align="center">
  <img src="https://user-images.githubusercontent.com/19647546/30533454-0266ec44-9c77-11e7-8b30-13197ad57c18.PNG" />
</p>

Here is the modified Python code:

````
# Program to retweet five latest tweets based on a hashtag (#Serverless)
from TwitterFollowBot import TwitterBot

def retweet(dict):
	# create an instance of the TwitterFollowBot
	# by default, the bot will look for a configuration file called config.txt 
# in your current directory
	my_bot = TwitterBot()
	# autoretweets the 5(count) latest tweets that matches the hashtag
	my_bot.auto_rt("#Serverless", count = 5)

def main(dict):
	retweet(dict)
	return {'message' : 'retweeted successfully'}
````

Now, save this Python code in a file named “__main__.py”. Create the “config.txt“,“already-followed.txt“, “followers.txt“ and “following.txt“ (as earlier), zip them all with the “__main__.py“ file and the TwitterFollowBot dependency module files.

## Invocation Process

Once the wsk CLI (Command Line Interface) is installed and the zip file is ready, follow these steps:

<p align="center">
  <img src="https://user-images.githubusercontent.com/19647546/30534239-f6d20130-9c7a-11e7-8109-aa43fc3938ff.PNG" />
</p>

### Step 1. Create & update an action:
	Log in to the IBM Bluemix account (https://console.bluemix.net/openwhisk/) and 
	create a new action. You can upload the zip files with dependencies only via the CLI:
	
	Syntax: wsk action create <action-name> --kind <language:version> <file_name>
	Sample Command: wsk action create tweetBot --kind python:3 OpenWhisk.zip

<p align="center">
  <img src="https://user-images.githubusercontent.com/19647546/30533480-25aaf466-9c77-11e7-85d0-6fb132c28878.PNG" />
</p>

### Step 2. Invoke the function (non-blocking mode):
	Syntax: wsk action invoke <action-name>
	Sample Command: wsk action invoke tweetBot 

<p align="center">
  <img src="https://user-images.githubusercontent.com/19647546/30533483-2991b128-9c77-11e7-9317-4b33e55a65e1.PNG" />
</p>

### Step 3. Check for the result:
Since we invoked the function in a non-blocking mode (because we haven’t added the ‘--blocking’ parameter), the command returned immediately, but it is executing in the background. 
	Syntax: wsk activation result <action ID> 
	Sample Command: wsk activation result f4df0d1dcb12488396978d2cda832b09

<p align="center">
  <img src="https://user-images.githubusercontent.com/19647546/30533487-2dfcd13e-9c77-11e7-95ec-4209dc183721.PNG" />
</p>

#### 4.	Check out the logs:
	Syntax: wsk activation logs <action ID>
	Sample Command: wsk activation logs f4df0d1dcb12488396978d2cda832b09

Automate the invocation
	
The moment the action was invoked, your Twitter account would have retweeted the five latest tweets that has the hashtag ‘#Serverless’ in it. However, this is still a manual invocation. For maximum impact, it would be better to automate the invocation process as well so that you can configure the action and forget it once and for all.

<p align="center">
  <img src="https://user-images.githubusercontent.com/19647546/30533747-987bfe8a-9c78-11e7-9b4c-38f5796d2a63.PNG" />
</p>

Periodic trigger would be the best option. It triggers the action based on a specific time and will retweet the latest tweets with ‘#Serverless’ in it. One can either choose a pattern or write a cron expression.

<p align="center">
  <img src="https://user-images.githubusercontent.com/19647546/30535021-40b97488-9c7e-11e7-9322-6ff48098e39d.PNG" />
</p>

<p align="center">
  <img src="https://user-images.githubusercontent.com/19647546/30535065-7bc25338-9c7e-11e7-926d-d5581727bf43.PNG" />
</p>
 
The above pattern will invoke the TweetBot action every weekday (Monday to Friday) every 6 hours keeping your twitter account live without your intervention!  

Before we end this article, here are a few aspects to keep in mind:
OpenWhisk is a open source and free, but to deploy it, we use IBM Bluemix which isn’t free. The TweetBot action will seamlessly run in the free tier, but for any other application, please estimate the monthly costs. The pricing calculator (https://console.bluemix.net/openwhisk/learn/pricing) could be handy.
This action uses the twitter API in the background via the TwitterFollowBot module. Misusing this may lead to banning your Twitter app, so please make sure you clearly read the Twitter automation rules (https://support.twitter.com/articles/76915) 

## Conclusion

In this article, we discussed how we can write a TweetBot to automatically retweet the latest tweets with given hashtags. We wrote the actions (serverless functions) in Python and deployed in OpenWhisk on IBM Bluemix. We also used triggers to automatically invoke the actions in specified time intervals. With this gentle introduction, we invite you to further explore OpenWhisk as well as other exciting serverless technologies. 

## References
- Apache OpenWhisk: https://openwhisk.incubator.apache.org/
- IBM Bluemix Functions: https://console.bluemix.net/openwhisk/
- Twitter API: https://dev.twitter.com/rest/public 




