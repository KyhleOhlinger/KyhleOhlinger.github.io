---
title: High-Level Overview of my Current AI Toolset
author: kyhle
date: 2025-02-14 12:00:00 +0200
categories: [Technical, AI & LLMs]
description: Hi all, My name is Kyhle Öhlinger and this blog post forms part of my personal blog. If you enjoy any of the posts, feel free to reach out and let me know :) 
image:
  path: /assets/img/AI/ai_agents.jpeg
  width: 800
  height: 500
--- 

I have been playing with artificial intelligence (AI) Chatbots on-and-off for the past 2 years which resulted in a few [blog posts](https://ohlinger.co/categories/ai-llms/) regarding my thoughts, usage, and completed CTFs. At the start of February, I set myself a goal to learn more about the hype around AI, Chatbots, Agents, etc. The first thing I learned about was [how I can start creating chatbots effectively](https://ohlinger.co/posts/creating-chatbots/) and from there I dove into chaining bots / prompts together to perform simple tasks. 

This blog post includes high-level breakdown of the different concepts and key terminology surrounding AI Chatbots and provides a AI toolset that I am aiming to make use of in my day-to-day life. 

# Prompts vs Bots vs Agents
If you've seen anything related to AI, you will have been bombarded with information about prompts which later lead to bots and currently AI Agents are all the hype. Before we dive into the setup that I am testing out, I have provided a breakdown of my understanding of these concepts:
- **Prompts**: User input to the AI models (ChatGPT, Claude, etc.)
	- E.g. Summarize this blog post for me. 
- **Bots**: Instructions for the models themselves which users then interact with via prompts. They generally help provided tailored output for users by including background information and specific tasks that the chatbot needs to perform.
	- E.g. You are a GCP Research bot, you need to use website A for all of your research and only provide output in list format. 
- **Agents**: A user can create a series of bots (agents) which can run on user input or other user requirements (triggers). This sound super fancy but it's effectively a modularized script with triggers. 
	- E.g. Python script that triggers on a new blog post and then calls other functions (agents) to summarize the output, pull out IOCs, send slack messages, etc. 

If you want a more in-depth breakdown of Key Terminology within the field of Chatbots / AI, I've included a [Key Terminology](#key-terminology) section at the end of this blogpost. 

# My Current AI Toolset
During my research, I tested out a number of new tools and my current setup includes:
- **ChatGPTs:** I mostly use Gemini models through Vertex AI
- **AI-Assisted Code Editors:** I recently switched from VS Code to Cursor and I've enjoyed the change thusfar
- **AI Agent Frameworks:** Most of my prompts are in the style of [Fabric patterns](https://github.com/danielmiessler/fabric/tree/main/patterns) and I haven't found a framework that reliably uses the patterns at this point (I am excited to test out Atomic Agents which will hopefully handle this use case).
- While working with different frameworks, I have also looked into methods of hosting simple Python based web applications. One of my favourite applications is [Streamlit](https://streamlit.io/) - An open-source Python library for building interactive web applications and dashboards.

The mockup below shows my current setup for AI Usage and how I generally interact with the different tools: 

![img-description](/assets/img/AI/20250213103649.png)
_Overview of my Current AI Usage_

The sections below provide a breakdown of the different tools that I have tested out, that I am currently working with, or plan to work with in the near future.

### Chatbots
Chatbots leverage AI to engage in human-like conversations and I generally use Chatbots for quick once off questions or when I am working through a specific problem. The table below highlights some notable chatbots:

| **Tool**                                                | **Category**        | **Description**                                                                                                                                                               |
| ------------------------------------------------------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [ChatGPT](https://chat.openai.com/)                     | GPTs                | OpenAI’s conversational AI model designed for natural language tasks—from casual conversation to creative writing and problem solving.                                        |
| **[Gemini](https://gemini.google.com)**                    | GPTs                | Google’s next-generation generative AI model built for advanced applications and deeper integration across its products.                                                      |
| [Claude](https://www.anthropic.com/claude)              | GPTs                | Anthropic’s AI assistant known for its safety-oriented design and robust natural language understanding in conversation.                                                      |

### AI-Assisted Code Editors
AI-assisted code editors enhance the development experience by offering intelligent code completion, bug detection, and automated refactoring. The table below highlights some notable code editors:

| **Tool**                                                | **Category**        | **Description**                                                                                                                                                               |
| ------------------------------------------------------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VSC with Copilot](https://github.com/features/copilot) | AI Editor           | Visual Studio Code integrated with GitHub Copilot, an AI-powered code assistant that provides context-aware code suggestions to boost developer productivity.                 |
| **[Cursor AI](https://www.cursor.com/)**                   | AI Editor           | An AI-driven code editor offering intelligent code completions, documentation lookup, and interactive assistance to streamline coding.                                        |


### AI Agent Frameworks
AI agent frameworks provide the infrastructure for building autonomous systems that can reason, plan, and execute tasks with minimal human intervention. I personally think that the current AI frameworks aren't ready to be used in production environments (yet), but they are fun to play with. The table below highlights some notable frameworks:

| **Tool**                                                | **Category**        | **Description**                                                                                                                                                               |
| ------------------------------------------------------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [CrewAI](https://www.crewai.com/open-source)            | Multi-agent Systems | An open-source framework for multi-agent systems that allows multiple AI agents to collaborate on complex tasks.              |
| [Langchain](https://www.langchain.com/)                 | Multi-agent Systems | A framework that simplifies building applications with large language models by managing tool integrations and orchestrating agent interactions.                             

### Additional Tooling
Finally, the table below include tools that I plan on testing (and hopefully using) in the future:

| **Tool**                                                     | **Category**                       | **Description**                                                                                                                                      |
| ------------------------------------------------------------ | ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Fabric](https://github.com/danielmiessler/fabric/tree/main) | Deployment Tool / Fleet Management | A Python-based framework designed to enable everyone to granularly apply AI to everyday challenges.            |
| [Atomic Agents](https://github.com/BrainBlend-AI/atomic-agents)                  | Multi-agent Systems           | Lightweight and modular framework for building Agentic AI pipelines and application.                                     |
| [n8n](https://n8n.io/)                                       | Automation Tool                    | An open-source automation platform that enables users to build custom workflows connecting various apps and services without heavy coding.           |


# Conclusion

Based on my own research and suggestions from others, I have tested out a number of different AI tools from Chatbots to Automation platforms. This process has changed how I interact with AI on a day-to-day basis and I encourage all of you to take the time and find what works for your use cases! If you found it useful or have additional tools that I should test out, please do let me know! And, as always, feel free to reach out for any questions or suggestions you may have.

# Key Terminology
## Prompts
A **prompt** is the natural language input or instruction you give to a model (such as a large language model) to elicit a desired response. Prompts can be simple queries, detailed instructions, or even multi-part contexts that steer the model’s output. The practice of crafting effective prompts (often called _prompt engineering_) is critical for obtaining useful, accurate, or creative outputs from generative models.  
### Bots
A **bot** is a software application designed to perform automated tasks over the Internet or within specific systems. In the context of chatbots, a bot is often a conversational program that responds to user inputs using predefined rules or machine learning algorithms. Bots can range from simple rule-based systems (which might, for example, respond to keywords) to sophisticated applications that incorporate natural language processing and even generative AI to simulate human-like conversation. Bots may work in messaging platforms, on websites, or as background scripts that perform tasks such as web crawling or moderation.  
### Agents
An **agent** in AI is a broader concept referring to any autonomous system that perceives its environment, makes decisions, and takes actions to achieve specific goals. Unlike many simple bots, agents typically have the following characteristics:
- **Autonomy:** They operate without continuous human intervention.
- **Reactivity:** They perceive changes in their environment and respond accordingly.
- **Proactivity:** They can take initiative, plan, and even learn from experience.
- **Goal-Directed Behavior:** They work to achieve defined objectives, sometimes using learning algorithms or planning strategies.

In many contexts, a chatbot may be considered a type of agent if it acts autonomously in managing conversations or executing tasks, but “agent” usually implies a higher level of decision-making and adaptation.  

## Additional Useful Chatbot Terminology
When exploring chatbot and conversational AI systems, here are some key terms and concepts that frequently arise:
- **Conversational AI / Virtual Assistant:**  
    Systems that use natural language processing (NLP) to understand and generate human-like responses. Examples include Siri, Alexa, and ChatGPT.
- **Natural Language Processing (NLP):**  
    The field of AI concerned with the interaction between computers and human language. It includes tasks like language understanding, translation, and sentiment analysis.
- **Natural Language Understanding (NLU) & Natural Language Generation (NLG):**  
    NLU focuses on understanding the intent behind user input, while NLG is about generating coherent and contextually appropriate text responses.
- **Prompt Engineering:**  
    The art and science of crafting effective prompts to optimize the output of AI models. Techniques include providing context, examples (few-shot learning), and even chain-of-thought instructions.  
- **Chain-of-Thought (CoT) Prompting:**  
    A technique where the model is encouraged to reason through problems step by step (often by appending phrases like “let’s think step by step”) to arrive at a final answer.
- **In-Context Learning:**  
    The model’s ability to adapt its responses based on the examples provided directly in the prompt without further training. This is often seen in few-shot learning setups.
- **Dialogue Management:**  
    The framework that controls how a chatbot tracks conversation context, manages turn-taking, and decides on appropriate responses.
- **Intent, Entities, and Slots:**
    - **Intent:** The purpose behind a user’s input (e.g., booking a flight, asking for weather).
    - **Entities:** Specific pieces of information extracted from the conversation (e.g., dates, locations).
    - **Slots:** Variables that hold values (filled by entities) required to fulfill an intent.
- **Fallback / Human Handover:**  
    When a chatbot cannot handle a query, it either falls back to a default response or transfers the conversation to a human operator.
- **Autoresponder:**  
    A simple type of chatbot programmed to provide automatic responses to common queries.
- **API Integration:**  
    Many chatbots connect to other systems via APIs (Application Programming Interfaces) to fetch data or execute transactions.
- **Multimodal:**  
    The capability to process and integrate multiple types of data (such as text, images, and speech) for richer interactions.
