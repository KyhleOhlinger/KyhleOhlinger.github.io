---
title: Looking into OpenAI's ChatGPT
author: kyhle
date: 2022-12-08 12:00:00 +0200
categories: [InfoSec, Technical]
description: Hi all, My name is Kyhle Öhlinger and this blog post forms part of my personal blog. If you enjoy any of the posts, feel free to reach out and let me know :) 
image:
  path: /assets/img/ai.jpeg
  width: 800
  height: 150
---

The past few months have been quite busy for me, which can be seen in the lack of content that I have been putting out on this blog. I would love to say that I've been doing some new, novel research, but the truth is that I've been spending time exploring Toronto and enjoying a new city. However, I haven't been all play and no work - I have just completed an external blogpost which will be linked here as soon as it is released by the company!

As the final technical post for the year, I wanted to dive into the hype of OpenAI's ChatGPT and the integration with DALL-E. While this blogpost is not going to be anything new, it is something that I've been looking into, and I hope that it can help someone who is looking to explore the new technology. Before we get into the technical portion, what is ChatGPT and DALL-E?

### OpenAI's ChatGPT

OpenAI recently released a new Artificial Intelligence (AI) trained model called [ChatGPT](https://beta.openai.com/). The chatbot is free for public testing and if you are unaware of the technology, it was designed to mimic human-like conversations based on user input (prompts).

> We’ve trained a model called ChatGPT which interacts in a conversational way. The dialogue format makes it possible for ChatGPT to answer followup questions, admit its mistakes, challenge incorrect premises, and reject inappropriate requests. ChatGPT is a sibling model to InstructGPT, which is trained to follow an instruction in a prompt and provide a detailed response.

A full post detailing ChatGPT, its uses and its limitations can be found on OpenAI's blog: <https://openai.com/blog/chatgpt/>.

### OpenAI's DALL-E Integration

In addition to ChatGPT, OpenAI have also integrated [Dall-E](https://labs.openai.com/) into their API suite. While DALL-E has been around for a while, the integration is incredible in terms of fully automated workflow using AI.

> DALL·E’s flexibility allows users to create and edit original images ranging from the artistic to the photorealistic. DALL·E excels at following natural language descriptions so users can plainly describe what they want to see. As our research evolves, we will continue to bring the state of the art into the API, including advances in image quality, latency, scalability, and usability.

A full post detailing the DALL-E integration, its uses and its limitations can be found on OpenAI's blog: <https://openai.com/blog/dall-e-api-now-available-in-public-beta/>.

## My Experience with OpenAI's ChatGPT and DALL-E

The technology itself is pretty spectacular. As a resource which can be used to obtain facts in a relatively short amount of time, it seems to succeed. However, when attempting to automate non-factual information which requires additional insight into a topic, it does fall short. For instance, if you were to ask the chatbot to list the symptoms of COVID, it would be able to provide them to you based on scientific papers, but if you ask it to create a new cocktail recipe, it does not have the built in capabilities to determine what makes a good cocktail.

The biggest concern that I have with any AI is that they are often "confidently wrong" in the output that is provided, and it is no different in terms of ChatGPT. I don't believe that it is in a place (yet) where it can be integrated into production pipelines and I doubt that it will be able to replace people's jobs. I do think that it is an amazing piece of technology and OpenAI's implementation and open beta has highlighted just how far the world has come in terms of publicly accessible artificial intelligence. 

With all that being said, I did use the ChatGPT functionality to create some scripts to integrate with both ChatGPT and DALL-E which are provided below and, at the end of the post, I have included some fun output from my time interacting with the platform.

### OpenAI's API

> If you need your organization information (Org Name or ID) you can retrieve them from the Settings tab.
{: .prompt-tip }

OpenAI have provided a ton of [documentation](https://beta.openai.com/docs/introduction) that can be used for integrating the ChatGPT and DALL-E components into your own workflow or scripts. I personally believe that the technology is too new to have trusted versions of ChatGPT integration on GitHub (regardless of the number of projects that are already available), and so I wanted to try creating some basic python scripts to do just that. To get started with the API, you will need to generate an API key which can be done from within the "View API Keys" tab:


![img-description](/assets/img/OpenAi/img1.png)
_OpenAI's API Settings_


Once you have opened the web page, you will be able to generate the API key that can be used to integrate with the OpenAI API:


![img-description](/assets/img/OpenAi/img2.png)
_Generating an API key_


### Initial Python Script Generation

To create an initial python script, I wanted to see how good the ChatGPT was at producing information so I started with asking ChatGPT to create a python script to interact with itself: 

![img-description](/assets/img/OpenAi/img3.png)
_OpenAI's ChatGPT creating a Python script'_

Much to my surprise it did pretty well as it would not take a ton of work to get it into a functional state. I have provided the script below:

```python
import requests

# Get an API key from https://beta.openai.com/
openai_key = "<enter your API key here>"

# Create a session to use for making requests
openai_session = requests.Session()

# Set the API key for the session
openai_session.headers.update({'Authorization': 'Bearer ' + openai_key})
 
# Create the request body
request_body = {
    "prompt": "What is the capital of France?",
    "max_tokens": 100
}
 
# Make the request
response = openai_session.post('https://api.openai.com/v1/engines/davinci/completions', json=request_body)
 
# Extract the response
data = response.json()
 
# Print the response
print(data['choices'][0]['text']) # prints "Paris"
```

### DALL-E python integration

As above, to create an initial python script I used ChatGPT with the `create a python script to interact with https://beta.openai.com/ and send output to dall-e` prompt, and I have provided the script below:

```python
import requests
 
#Enter the API key for openai
api_key = '<enter your API key here>'
 
# Set the endpoint for the OpenAI API
endpoint = 'https://api.openai.com/v1/engines/dall-e/completions'
 
# Set the headers for the request
headers = {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer ' + api_key
}
 
# Define the request body
data = {
    'prompt': 'A picture of a cat',
    'temperature': 0.5,
    'top_p': 1.0
}
 
# Send the request
response = requests.post(endpoint, json=data, headers=headers)
 
# Print the response
print(response.json())
```
 
Unfortunately, I got the following error when trying to run the code, but it was still worth a shot:
> {'error': {'message': 'That model does not exist', 'type': 'invalid_request_error', 'param': None, 'code': None}}
 
## Closing Thoughts
 
The potential for something like OpenAI’s ChatGPT to eventually supplant a search engine like Google isn't a new idea, but this delivery of OpenAI's underlying technology is the closest approximation yet to how that would work in a fully fleshed out system. I don't think that us humans have anything to be concerned about at this point in time, but who knows what the future holds.

As always, feel free to reach out with any questions you may have. I leave you with a poem about a snow alpaca in Toronto and some of my favourite DALL-E generated images:

```text
The snowflakes start to fall,
All across the city of Toronto.
A special kind of magic,
The lights of Christmas glow.
 
The snow starts to drift,
In the crisp winter air.
The city transformed,
A blanket of snow so fair.
 
The streets filled with people,
All out in the snow.
The holiday spirit,
A joyful spirit aglow.
 
The Christmas trees sparkle,
The streets filled with cheer.
The snowflakes like starlight,
A beautiful winter so near.
 
The city of Toronto,
So alive and bright.
The snowflakes come down,
On this Christmas night.
```
 
![img-description](/assets/img/OpenAi/img4.png)
_DALL-E Generated Images_
