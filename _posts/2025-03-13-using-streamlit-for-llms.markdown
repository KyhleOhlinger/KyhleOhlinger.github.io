---
title: Creating a Basic Streamlit Application for Fabric Formatted Prompts
author: kyhle
date: 2025-03-13 12:00:00 +0200
categories: [Technical, AI & LLMs]
description: Hi all, My name is Kyhle Öhlinger and this blog post forms part of my personal blog. If you enjoy any of the posts, feel free to reach out and let me know :) 
image:
  path: /assets/img/AI/streamlit.png
  width: 800
  height: 500
--- 

During my previous [blog post](https://ohlinger.co/posts/testing-ai-setups/), I presented a mockup for my current AI toolset. This included how I generally make use of different products / tools and try to combine them into different solutions on a daily basis. 

![img-description](/assets/img/AI/20250213103649.png)
_Overview of my Current AI Usage_

The idea behind this post was finding a way to combine prompt-engineering with a simple frontend to assist in learning more about GCP. Using the methodology I described within the "How to Build Your Own Chatbots with AI" [blog post](https://ohlinger.co/posts/creating-chatbots/), I created 4 prompts (bots?) for my usecase:
- GCP Security Architecture Bot
- GCP Red Team Bot
- GCP Blue Team Bot
- Security Content Summarizer Bot

This blog post will dive into the different prompts that I created for this use case as well as a working version of "GCP Tutor", which you can grab from [GitHub](https://github.com/KyhleOhlinger/gcp-scripts/tree/main/gcp_tutor).

# Fabric Patterns

Before we dive into the prompts, I would be remiss if I didn't mention one of the tools that I set out to investigate in my previous blog post - [Fabric]( https://github.com/danielmiessler/fabric/tree/main). Fabric was created by Daniel Miessler and, as per the Fabric documentation, the goal of Fabric was to "apply AI to everyday challenges":
> Since the start of 2023 and GenAI we've seen a massive number of AI applications for accomplishing tasks. It's powerful, but _it's not easy to integrate this functionality into our lives._
> 
> **In other words, AI doesn't have a capabilities problem—it has an _integration_ problem.**
> 
> Fabric was created to address this by enabling everyone to granularly apply AI to everyday challenges.


The basic structure of Fabric Patterns is provided below:

```
# IDENTITY and PURPOSE
This section is used for the basic identity and definition of the bot

# STEPS
A list of steps that the bot should follow

# OUTPUT INSTRUCTIONS
The output requirements for the bot

# INPUT
INPUT: User input which will be fed into the prompt
```

While I am not using Fabric for this specific application, I honestly really enjoy this structure for prompt-engineering and it's the structure that I used to create the different bots for this project.

# "Prompt-Engineering" a GCP Tutor
I could simply provide the Python code for the GCP tutor but I thought it would be more useful to share the initial requirements / prompts that I fed into my [bot creator prompt](https://github.com/KyhleOhlinger/prompt-engineering/blob/main/Prompt%20Files/system_bot.md) for each agent, in addition to the prompts contained within the codebase, so that you can follow along or craft your own versions!

### GCP Security Architecture Bot
I am a cloud security engineer in a modern Cloud first organization. I want to improve our GCP security architecture, posture, and understanding of the cloud services provider. I need a bot that prioritizes cloud for application security and security engineering as opposed to corporate security where we have a much smaller footprint. Additionally, the bot should be able to provide information to help teach the user about the topics instead of simply providing answers. Where possible, the output should include Terraform code for GCP.

### GCP Red Team Bot
You are a GCP Red teamer (penetration tester) bot. Your task is to take in user input and determine if there are methods of exploitation available to you. This has to include a description of the attack space, a red team overview of the topic, and potential attack paths. During your research, you need to use the following websites as reference and, where an attack is possible, you have to provide reference to where you identified this issue.
- https://hackingthe.cloud/gcp/general-knowledge/default-account-names/
- https://rhinosecuritylabs.com/blog/?category=gcp
- https://cloud.hacktricks.wiki/en/pentesting-cloud/gcp-security/index.html
- https://cloud.hacktricks.wiki/en/pentesting-cloud/workspace-security/index.html
- https://cloudsecdocs.com/gcp/services/iam/projects/
- https://cloud.google.com/docs

Where possible, provide POCs on how to perform the attack, but do not make up attacks where they do not exist. 

### GCP Blue Team Bot
You are a GCP Blue teamer (security analyst) bot. Your task is to take in user input and determine if there are areas of exploitation / weakness which you need to defend against. This has to include a description of the attack space, a blue team overview of the topic, potential areas for monitoring, logging, extra defense, etc. During your research, you need to use the following websites as reference and provide references to Mitre techniques. 
- https://attack.mitre.org/matrices/enterprise/cloud/ 
- https://github.com/center-for-threat-informed-defense/security-stack-mappings/tree/main/mappings/GCP 
- https://center-for-threat-informed-defense.github.io/mappings-explorer/external/gcp/

You need to provide a summary table for the attack type, gcp log sources required to identify the activity, and Mitre techniques associated with the attack. When referencing log sources, you need to start your research using the following resources:
- https://cloud.google.com/logging/docs 

Finally, you need to create a detection for the use case. The detection should be written in Sigma and YARA-L. As reference, the following repositories contain a code base full of examples which you need to use when creating detections:
- Sigma Rule Repository: https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/gcp
- YARA-L Rule Repository: https://github.com/chronicle/detection-rules/tree/main/rules/community/gcp

### Security Content Summarizer Bot
You are a summarizer bot, you specialize in taking in information from different sources and creating a 1-page cheatsheet / summarization of the topic. This sheet generally takes in 3 different viewpoints of a topic (architecture, red team overview, blue team overview) to create the summary. 

# Streamlit Application

As part of this journey, I came across a [video](https://www.youtube.com/watch?v=OXRroHmYr6M) by Dave Gilmore who touches on using [Streamlit](https://streamlit.io/) with [CrewAI](https://www.crewai.com/). Unfortunately, there is no easy way to use Fabric patterns in CrewAI, but we can still use Streamlit to host a web application for our prompts. 

The simple codebase that I created for the application is provided on [GitHub](https://github.com/KyhleOhlinger/gcp-scripts/tree/main/gcp_tutor). I am using Vertex AI with [Application Default Credentials (ADC)](https://cloud.google.com/docs/authentication/provide-credentials-adc) for authentication - if you're looking to use a different LLM, I have some standalone [runner scripts](https://github.com/KyhleOhlinger/prompt-engineering/tree/main/Python%20Scripts) which may be useful in modifying the code for different authentication methods. 

## GCP Security Tutor
> The term "Tutor" is used lightly here, it is more akin to a convenient method of one-shot prompting several prompts at once. Future iterations will function more as actual agents, but this is just the first iteration which can be used to provide different perspectives to the same user input. 
{: .prompt-info }

If you run the code `streamlit run gcp_tutor.py`, it will launch a simple frontend for the python codebase as shown in the screenshot below:

![img-description](/assets/img/AI/20250213094932.png)
_Security Tutor Input_

After you have provided user input, the application will reach out to the LLM that you have configured and provide output in a tab formatted page:

![img-description](/assets/img/AI/20250213095207.png)
_Content Generation_

As a bonus, if all 3 prompts are selected, I added in functionality to create a 1-page cheatsheet based on the content created by the various AI Agents:

![img-description](/assets/img/AI/20250213095515.png)
_Cheatsheet Generation_

# What's Next?
This was the first dive into chaining some prompts together with a simple Python script for my specific use case. I'm going to continue learning more about Agents and managing fleets with Atomic Agents and N8N! As always, if you have any questions or comments, please reach out! Also, if you have any tidbits on using CrewAI with Fabric Patterns, please do let me know!