---
title: How I "Skill Up" in New Topics
author: kyhle
date: 2024-08-09 12:00:00 +0200
categories: [Career]
description: Hi all, My name is Kyhle Öhlinger and this blog post forms part of my personal blog. If you enjoy any of the posts, feel free to reach out and let me know :) 
image:
  path: /assets/img/studying.png
  width: 800
  height: 500

--- 

# Introduction

I was recently asked about methods that I use to learn new topics (tools / platforms / technologies, etc.). The question itself seemed simple to answer, "I just read about the topic and look for blogs explaining the issues with it", but that answer did not actually convey anything that someone else could use in their day-to-day to skill up in different topics. It was also not an accurate depiction of the methods that I use when I try to skill up in a new topic. 

I (fortunately?) have a consulting background, during which time I was required to: context switch constantly, pick up new topics, including; tools, techniques, processes, technology, etc. on a whim, and provide subject matter expertise (SME) to clients based on my learnings. Based on my consulting background, I had not given much thought to methods I use learn about new topics, effectively, within a short timespan. I asked the person to sit down next to me while I guided them through my process and that led me to this post. This blog post details my process when it comes to learning about new topics, my recent undertaking of learning more about GCP, and advice on getting started. 

# My General Process

> This is not the way that I think anyone recommends skilling up on new topics, but this is the way that I have found to work for me. 
{: .prompt-info }


When it comes to learning, note taking is an imperative part of the process for me - it's the way I learn, and it is the main tool that I use when I approach learning about new topics. If you would like to know about my note taking tools - I wrote a [post](/posts/new-notetaking-tools/) about it a while ago.

When it comes down to how I learn about a new topic, I use the following approach:
- Identify the topic
- Set a time limit on learning / skilling up
	- This is probably the most important part of initially leaning about a new topic. You can always spend more time researching about something, but 
	- If I give myself a hard deadline, I am more likely to actually spend the time learning about it. (I use this method when booking exams as well).
- Group main categories of what I want to learn together
- Find useful talks/blogs on the topic and identify research which discusses breaking / hacking the topic
- **Most importantly for me**, get hands-on with the topic
- When in doubt, read the topic's documentation (RTFM)

"But Kyhle, there's so much to read!". Correct, but this approach also helps me narrow down what I need to read by identifying key concepts that I want to learn about from the start.  Is this the most effective use of my time? I don't know... But it has enabled me to become semi-proficient in a variety of topics within a very short amount of time. This approach has also generally allowed me to backfill the rest of my knowledge gaps overtime without anyone realizing (I hope). 

# My Recent Undertaking

To answer this question a bit more thoroughly, I will describe the methods I recently used to become more familiar with key concepts in Google Cloud Platform (GCP). The goal of this undertaking was to provide me with a solid foundation before starting any GCP certifications (backfill additional areas), and since I had a bit of a time crunch, I set myself a time limit of 3 days.

## Group Categories Together

Before I started looking into resources, I wrote down categories of concepts that I wanted to learn about within GCP. I come from an AWS background and I believed that learning these concepts would be the best use of my time to become semi-proficient with GCP in the short term. 

Initial research:
- Find useful blog posts / conference talks about GCP and attacking GCP.

Look into GCP documentation:
- Start with the basics, learn about:
	- How it works (What is GCP)
	- Types of authentication, types of accounts, etc.
	- How services work in GCP
	- How does workspace work / integrate with Google Cloud
- Digging deeper:
	- Structure of API calls & how to interact with GCP
	- Types of logs and what is important for security
	- Breakdown on areas / services that most detection libraries focus
	- Breakdown of different GCP attacks and attack paths
	- How to perform incident response (IR) in GCP environments


## Note Taking and Getting Hands-On

Based on the main categories, I then created sections within my note taking tool and started diving into what I wanted to learn by: 
- Dividing categories into sub categories and actionable hands-on items
- Finding relevant documentation
- Taking notes and clicking around the platform

At the end of the process, my note structure looked like this:

![img-description](/assets/img/Notetaking/20240806114547.png)
_Note Taking Structure_


Each section contained; references, screenshots, code snippets, information from documentation, etc. on the various items that I was interested in learning about, as well as any potential gotcha's when interacting with the platform. I also created a tracker on different blogs, Github pages, etc. which I could use in the future to learn about both attacking & defending GCP:

![img-description](/assets/img/Notetaking/20240806114810.png)
_Collecting Resources_

The links above would not all be relevant to my initial goal of getting up to speed with GCP, but they would come in handy if I decided to target a specific area within GCP or if I wanted to look into methods to detect abuse against GCP services, etc. at a later stage.

# Putting it all Together

At this point I have a decent base from which I can either learn more about the specific topic or move on to the next! At the very least, I have:
- Notes on the main concepts of the topic
- Interacted with the topic (hands-on)
- Identified methods that other's have used to attack & defend the topic
- Built a list of additional resources which I can use to  improve my knowledge in the future

If this blog post did not convey it, my method to learning is not an exact science. There are most likely better ways to learn but this is what works for me (YMMV). If you read this post, I hope you have a better idea of what may (or may not) work for you during your adventures into new topics! As always, if you have any questions or if you would like me to include specific content in my blog, please do reach out!


