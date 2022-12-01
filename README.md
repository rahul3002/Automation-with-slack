# Automation with the Slack API in Python
 

## What is Slack?
Slack is a communication application. It can help us connect with employees, customers, and partners. It allows teams to collaborate with images, videos and voice messages. It also allows huddles across teams, time zones, and physical spaces. The Slack API has allowed it to become a highly integrated tool that fits well with other commonly used software like Jira and Google Calendar. By following this course, you can make your application more integrated by incorporating Slack’s API. If you want to integrate your application with the Slack API, this is for you.

## Slack API
The Slack API helps automate repetitive tasks by providing programmatic access to Slack’s functionality. Slack also has excellent documentation with a built-in tool to test the individual endpoints.

![SlackAPI](https://github.com/rahul3002/Automation-with-slack/blob/main/slack_api_logo_vogue.png)

## Set Up the API keys

- Set up a Slack account
- Create a workspace
- Create a Slack application
- Add scopes and install the application
- Add the Slack application to a channel
- Add your user ID
- Verification
- Add the API keys below

- **Bot User OAuth Token:** We use this to authenticate and specify the different scopes of the caller.
-  **Channel ID:** We use this code to identify the channel (group) in Slack.
-  **Member ID:** We use this code to identify a user or member.

## Set up a Slack account

### We’ll use the steps below to set up an account in Slack:

- Go to Slack’s website to set up an account.

![1](https://github.com/rahul3002/Automation-with-slack/blob/main/1.png)
- Click “SIGN UP WITH EMAIL.”

![2](https://github.com/rahul3002/Automation-with-slack/blob/main/2.png)
- Enter your email and click “Continue.”
![3](https://github.com/rahul3002/Automation-with-slack/blob/main/3.png)
- Copy and paste the 6-character code sent to your email.

## Create a workspace
![workspace](https://github.com/rahul3002/Automation-with-slack/blob/main/4.png)

The user needs to sign up to Slack to use the API. It is advisable to make a new workspace 

- Once we’ve signed up, click the “Create a Workspace” button.
- Enter the name of the company.
![A](https://github.com/rahul3002/Automation-with-slack/blob/main/A.png)
- Enter the channel’s name you want to start with.
![B](https://github.com/rahul3002/Automation-with-slack/blob/main/B.png)
- Skip the options of adding other people.
![C](https://github.com/rahul3002/Automation-with-slack/blob/main/B.png)
- Launch your newly created workspace.

## Add the Slack application to a channel

We’ll use the channel ID to interact with the API. For example, we’ll use it to send messages to the channel and more.

- Go to your Slack application on your desktop or browser.
- Open the channel settings by clicking its name.
- Add the Slack application you made in the “Integrations” tab from the channel’s settings.
- Go back to the “About” tab and copy the ID beside the Channel ID.
- Paste the ID in the code widget next to CHANNEL_ID at the end of this lesson.

## Add your user ID

In certain API calls, we need to specify a user using their user ID.  

- Go to the Slack application on your desktop or browser.
- Click on your profile image in the top-right corner.
- Click the “Profile” button in the pop-up menu. You’ll see an expanded profile.
- Click the three dots labeled “More.”
- Click “Copy Member ID” in the pop-up menu to copy the ID.
- Paste the ID in the code widget next to USER_ID at the end of this lesson.

## Verification

Next, we need to verify the IDs and the API token that were added. Run the executable widget below to verify if all the keys entered are correct and work as they should.

- Add the API keys below

```
#Using some hidden code to send a request to the 

#Slack API to verify that the setup is correct and complete!

 print(validation)

```

## Send Messages

- Overview


### We can use the Slack application to automate a daily message to a channel or send a joke to a colleague. We use Slack’s Chat API for this.

Let’s look at the following endpoints:

- chat.meMessage: This endpoint sends an italicized action text message to a channel.
- chat.postMessage: This endpoint sends a message to a channel.
- chat.scheduleMessage: This endpoint schedules a message to be sent to a channel in the future.


## Send a “me” message

We’ll start with the most straightforward endpoint first—the https://slack.com/api/chat.meMessage endpoint. This endpoint allows us to send an italicized “me” message to a specific channel. This endpoint is relatively straightforward and has no optional arguments.

Some important query parameters for the chat.meMessage endpoint are the following:

Let’s call the chat.meMessage endpoint. Click the “Run” button to post a “Hello World!” message using this endpoint.

```
import requests
import json

url = "https://slack.com/api/chat.meMessage"
data = {
    'channel':'{{CHANNEL_ID}}', 
    'text':'Hello World!'
}
headers = {
    'Authorization': 'Bearer {{TOKEN}}',
    'Content-Type': 'application/x-www-form-urlencoded'
}

response = requests.post(url, headers=headers, params=data)
print(json.dumps(response.json(), indent=4))

```

- Lines 1–2: We import the requests and JSON Python modules.
- Line 4: We specify the URL for the desired endpoint.
- Lines 5–8: We specify the channel and text parameters that will be passed to the post function as an argument. We use the channel to specify the channel ID.
- Lines 9–12: We specify the POST request headers.
- Line 14: We package all the parameters we have specified till now and send a POST request.
- Line 15: We use the print command to print the stored response variable. Since the response is in the JSON format, we use the .json() and json.dumps to view it.

## Post a message#

To post a message, we access the https://slack.com/api/chat.postMessage endpoint. Unlike chat.meMessage, it can send attachments, blocks, and text. We can use this endpoint to post messages to a public, private, or IM channel.

- We can use the endpoint to send the following types of messages on Slack:

   - **Attachments (legacy):** This is a JSON-based array of structured attachments: like "[{"pretext": "pre-hello", "text": "text-world"}]".
   - **Blocks:** This is a JSON-based array of structured blocks, like "[{"type": "section", "text": {"type": "plain_text", "text": "Hello world"}}]".
   - **Text:** This is a simple text like "Hey, I'm Rahul Bagal!".

Let’s call the chat.postMessage endpoint. Click the “Run” button to post a message containing a block to the channel.

```
import requests
import json

url = "https://slack.com/api/chat.postMessage"
data = {
	'channel':'{{CHANNEL_ID}}',
	"blocks": '''[
		{
			"type": "section",
			"text": {
				"type": "mrkdwn",
				"text": "You have a new request:\n*<exampleEmployeeLink.com | Andy Brown - New device request>*"
			}
		},
		{
			"type": "section",
			"fields": [
				{
					"type": "mrkdwn",
					"text": "*Type:*\n ..."
				},
				{
					"type": "mrkdwn",
					"text": "*When:*\n ..."
				},
				{
					"type": "mrkdwn",
					"text": "*Last Update:*\n ..."
				},
				{
					"type": "mrkdwn",
					"text": "*Reason:*\n ... "
				},
				{
					"type": "mrkdwn",
					"text": "*Specification:*\n ..."
				}
			]
		}
	]'''
}
headers = {
    'Authorization': 'Bearer {{TOKEN}}',
    'Content-Type': 'application/x-www-form-urlencoded',
}

response = requests.get(url, headers=headers,params=data)
print(json.dumps(response.json(), indent=4))

```










```
import requests
import json

url = "https://slack.com/api/chat.postMessage"
data = {
    'thread_ts':'{{ts}}',
    'reply_broadcast':'true',
    'channel':'{{CHANNEL_ID}}',
    'text':'Replying to the previous message!!'
}
headers = {
    'Authorization': 'Bearer {{TOKEN}}',
    'Content-Type': 'application/x-www-form-urlencoded',
}

response = requests.get(url, headers=headers, params=data)
print(json.dumps(response.json(), indent=4))

```

The chat.postMessage endpoint works similarly to chat.meMessage in the first code widget, but it can have varying responses. These responses depend on the optional parameters sent with the request. In the second code widget, we use the extracted timestamp, ts, and then use the optional arguments to reply to a message using the chat.postMessage endpoint.

## Schedule a message

To schedule a message, we access the https://slack.com/api/chat.scheduleMessage endpoint. This method schedules a message for sending to public, private, and IM channels at the specified time in the future.

Some important query parameters for the chat.scheduleMessage endpoint are the following:

```
import requests
import json
import time

epoch_time = int(time.time()) 

url = "https://slack.com/api/chat.scheduleMessage"
headers = {
    'Authorization': 'Bearer {{TOKEN}}',
    'Content-Type': 'application/x-www-form-urlencoded',
}
data = {
    'channel':'{{CHANNEL_ID}}',
    'text':'Hello World! - sent to the channel after 1 minute',
    'post_at':str(epoch_time+(60*1))
}

response = requests.get(url, headers=headers,params=data)
print("Response: ",json.dumps(response.json(), indent=4))

```

This endpoint call is similar to the calls we’ve made before, but in this case, we are also specifying the Unix EPOCH timestamp using the time module.

- Line 5: We use the time module’s time() function to get the current Unix EPOCH time as an integer.
- Line 15: We add one minute (60 seconds) to the current Unix EPOCH timestamp and convert it into a string.


