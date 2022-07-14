---
title: Blue Team Series Part 4&#58; Note Taking and SOC Projects
author: kyhle
date: 2022-07-14 08:00:00 -0400
categories: [Blue_Team_Series]
description: Hi all, My name is Kyhle Öhlinger and this blog post forms part of my personal blog. If you enjoy any of the posts, feel free to reach out and let me know :) 
image:
  path: /assets/img/soc.jpg
  width: 800
  height: 500
---

In the previous post, we looked at SOC fundamentals and escalations. In this post, I will be wrapping up the series with my thoughts on note taking, potential projects that a SOC can undertake and a review of the series. 

## Note Taking

The purpose of a SOC is to monitor and prevent malicious behavior within an organization's digital estate. Additionally, it provides direct support to the cyber incident response process. In order to provide effective support during incidents, a SOC analyst needs to efficiently preserve case information while working through a ticket. 

To accomplish this, the analyst needs to be able to capture relevant data as they work through the process instead of attempting to reconstruct it after the fact.

### Note Taking Template:
There is a trade off between taking notes effectively and adding time to investigations. The purpose of this template is to assist in organising topics that would be encountered during every investigation into a concise format which could help with future investigations and threat analytics. The fields can be added to a ticket's comment section once the investigation has been completed (or any method that your SOC uses to close tickets).
* **IOCs:** What were the IOCs for this ticket?
* **True / False Positive:** After investigation, was this a true or a false positive?
* **List of Actions Taken:** What process was followed?
* **Observations by the Analyst:** Theories, notes, etc. Any notes that the analyst took during the investigation. This can include screenshots and general comments as the analyst is working through the ticket.

The method that is use to take these notes can be consistent internally, or up to each analyst based on their preferences. If you would like to follow my process, I have a blog post on my notetaking [here](https://ohlinger.co/posts/new-notetaking-tools/) and my Github flow for semi-automated backups can be found [here](https://ohlinger.co/posts/github-flow/).


## SOC Projects
SOC projects should be incorporated in every SOC. Not only will this allow the SOC to focus on additional work, but it will also reduce the likelihood of "alert fatigue" that affects the majority of SOC analysts at one point or another. The aim of SOC projects is to encourage collaboration within the team and allow each analyst to either work together or individually to upskill themselves and improve the SOC, while also providing a creative outlet that they might not get from assessing tickets throughout the day. 

While the types of projects will differ between teams, I have provided a few ideas below that the SOC analysts can take part in, in addition to their role of supporting the business: 
 
* Creating a centralised knowledge repository
* Developing internal training material
* Education around SecOps

### Creating a centralised knowledge repository

This project should be a consistent, ongoing project, and the knowledge base should include; documents, training material, processes, useful information, and anything else that the SOC analysts deem useful. 

### Developing internal training material

There is an abundance of training material available within the field of Information Security however, unless it is condensed to a format that makes sense for an organization, the information can seem overwhelming. The intent of this project would be to create training material for new SOC members to ensure that they understand the internal tooling used by the SOC and are able to be onboarded quicker into the team. An example of the training material that can be created is listed below:
 
1. Note Taking Process
2. Basic Threat Hunting	
3. How to use Internal Tooling	

### Education around SecOps

This project will take the team through the type of information that can be uploaded or pasted onto public infrastructure like CyberChef. Additionally, if there are publicly available tools that do not meet the requirements set out by the internal SOC, then local instances of those tools, such as CyberChef, should be deployed. 

These projects are just examples, and should be expanded upon if your SOC aims to incorporate them into your environment.
 
## Conclusion

This short series was aimed at new analysts looking to join a SOC, as well as any SOCs that are currently facing constant turnover due to a lack in structure and creative outlets. Your job should be fun, it should be a place to learn and improve, and if you do not feel like that is happening, refer to this series and try implement a few of the recommendations in order to improve your day-to-day. 

This series was (for the most part) a high-level overview of several important topics. If you are interested in delving deeper into any of the topics, or if you have any questions, please do reach out!