---
title: From Curiosity to Creativity&#58; My Thoughts on Prompt Engineering
author: kyhle
date: 2024-12-02 12:00:00 +0200
categories: [Technical, AI & LLMs]
description: Hi all, My name is Kyhle Öhlinger and this blog post forms part of my personal blog. If you enjoy any of the posts, feel free to reach out and let me know :) 
image:
  path: /assets/img/prompt_engineering.jpg
  width: 800
  height: 500

--- 

Over the last few months, I have been attempting to learn more about Large Language Models (LLMs) and, as a result, I stumbled across prompt engineering and prompt engineering attacks. To improve my own knowledge of different LLM models and their susceptibility to attack, I have completed a few CTFs including ones from Wiz and WithSecure. If you haven't seen them already, I have writeups for both CTFs on my blog: [1](https://ohlinger.co/posts/wiz-llm-challenge/),[2](https://ohlinger.co/posts/withsecure-myllmbank-challenge/). This blog post is going to be a small braindump of my thoughts on prompt engineering and the methods that I found to work when creating prompts and asking ChatGPT style LLMs questions.

# High-Level Difference Between Prompt Engineering and Prompt Engineering Attacks
 Before we dive into prompt engineering, here's a quick breakdown of the differences between prompt engineering and prompt engineering attacks.

**Prompt engineering** is the process of designing and refining the prompts given to AI language models (e.g. ChatGPT, Llama, Gemini, etc.), to produce desired outputs. The goal of prompt engineering is to frame the questions (prompts) in such a way that the LLMs generate accurate, relevant, and useful responses. Depending on how deep you want to go, this could involve understanding the model's behaviour in an effort to craft prompts that lead to the most effective results.

**Prompt engineering attacks** involve deliberately crafting questions (prompts) to manipulate or exploit a LLM model's output in unintended ways. These attacks can take various forms, such as: Prompt Injection Attacks, Adversarial Prompts, Data Poisoning, and more. 

The key difference between prompt engineering and prompt engineering attacks lies in the intent and outcome:
- **Prompt Engineering** is a constructive practice aimed at improving the quality and relevance of AI-generated content. It’s used to refine how models respond to legitimate requests.
- **Prompt Engineering Attacks** are destructive practices aimed at exploiting or manipulating AI models to produce harmful, biased, or misleading content. The intent here is to subvert the model’s intended functionality.


Prompt engineering attacks are possible because LLMs cannot easily discern the difference between legitimate and malicious user input. LLMs are based on natural language and since they have no parsing or syntax trees and no separation between instructions and data, they are inherently susceptible to injection-based attacks. Alright, with that out of the way lets talk about prompt engineering. 

# My Experience with Prompt Engineering

> I have spent most of my time with prompt engineering working with ChatGPT and Gemini, but the ideas should be transferable to other LLMs. 
{: .prompt-info }

> Prompting is an art. You will likely need to try a few different approaches for your prompt if you don’t get your desired outcome the first time.

There are tons of blog posts and marketing material which you can research for the main use cases of LLMs, my personal use cases thus far have been:
- **Writing assistance:** when writing emails, blog posts, etc. I've used LLMs to either help reword a few sentences or even help me list some useful ideas which I could then expand upon. 
- **Creative thinking:** This may sound strange, but working with an "interactive soundboard" has helped me be more creative and it has also helped me dive into new areas of thinking that I previously blocked myself off from. 
- **Create original images:** To be fair I haven't used DALL-E a lot, but I have used some ChatGPT prompts along with DALL-E to create some wallpapers for my HomeAssistant Dashboards and bring character designs to life for a DND campaign. 
- **Creating consistent summaries for work:** I have used LLMs to create summaries for different aspects of my work day including documentation for detections to ensure that all of the documentation that the security team make use of have a similar look and feel. 
- **Summarizing and understanding financial information:** I have also used LLMs to summarize tax information and different account types as an initial frame of reference after moving to Canada. 

While that is not an exhaustive list, those are the most common items that I have used it for. As you can see, my use cases have mostly been a combination of summarization and creativity. When using LLMs for creative input or quick writing assistance I generally start with some **context** and provide the **audience** type (the target audience for the output). For the most part, this has been sufficient. You are able to work with the LLM, refine output, build on the creative responses in an interactive manner, and iterate until you have your desired output. 

However, for specific work tasks, summarizations, etc. LLMs do have a tendency to talk in circles or hallucinate. There are a large number of methods that can be used for effective prompt engineering. My favourite at this point is the [COSTAR method](https://freedium.cfd/https://towardsdatascience.com/how-i-won-singapores-gpt-4-prompt-engineering-competition-34c195a93d41?gi=15e8906b8668).

# Introduction to the COSTAR Framework

> Effective prompt structuring is crucial for eliciting optimal responses from an LLM. The CO-STAR framework, a brainchild of GovTech Singapore's Data Science & AI team, is a handy template for structuring prompts. It considers all the key aspects that influence the effectiveness and relevance of an LLM's response, leading to more optimal responses.

The abstract above was taken from the [Toward Science Article](https://freedium.cfd/https://towardsdatascience.com/how-i-won-singapores-gpt-4-prompt-engineering-competition-34c195a93d41?gi=15e8906b8668), also linked in the [Useful Resources](#useful-resources) section. The breakdown below was copied directly from the article:
- **(C) Context: Provide background information on the task:** This helps the LLM understand the specific scenario being discussed, ensuring its response is relevant.
- **(O) Objective: Define what the task is that you want the LLM to perform:** Being clear about your objective helps the LLM to focus its response on meeting that specific goal.
- **(S) Style: Specify the writing style you want the LLM to use:** This could be a particular famous person's style of writing, or a particular expert in a profession, like a business analyst expert or CEO. This guides the LLM to respond with the manner and choice of words aligned with your needs.
- **(T) Tone: Set the attitude of the response:** This ensures the LLM's response resonates with the intended sentiment or emotional context required. Examples are formal, humorous, empathetic, among others.
- **(A) Audience: Identify who the response is intended for:** Tailoring the LLM's response to an audience, such as experts in a field, beginners, children, and so on, ensures that it is appropriate and understandable in your required context.
- **(R) Response: Provide the response format:** This ensures that the LLM outputs in the exact format that you require for downstream tasks. Examples include a list, a JSON, a professional report, and so on. For most LLM applications which work on the LLM responses programmatically for downstream manipulations, a JSON output format would be ideal.

I have found the COSTAR method to be far superior to other methods for more complex prompting. Using the principals described above, you are able to format your prompts into a more precise manner for the LLM to interact with. As an example, the screenshot below shows the COSTAR format in action for a ChatGPT prompt:


![img-description](/assets/img/WithSecureChallenge/20240820105640.png)
_COSTAR Format within ChatGPT_

This is a very simplistic idea, but by ensuring that you set some relevant fields in even your basic prompts, you will be able to extract more useful, insightful, and relevant information from the LLM. 

# Common Pitfalls and Tips for Prompt Engineering

In prompt engineering, even small missteps can lead to unexpected results or reduce the effectiveness of a model's response. These are some areas that I've encountered while learning about prompt engineering:

1. **Overloading the Prompt**: Adding excessive detail or unnecessary information, hoping for a perfect response. However, this can confuse the model and dilute its focus. **Tip:** Refine and streamline prompts, focusing only on essential context and key details.
2. **Lack of Specificity:** Vague prompts often lead to generic responses. For example, asking, "Explain this topic" without specifics can result in a response that lacks depth or relevance. **Tip:** Clearly define goals and constraints so that the model knows exactly what is expected.
3. **Misjudging Complexity:** Complex questions with multiple parts can lead to incomplete or scattered answers. **Tip:** Break down complex prompts into simpler parts and organize them logically, helping the model respond effectively.
4. **Forgetting Follow-Up Adjustments:** A prompt may need tweaking based on initial responses but I found myself stopping after the first attempt. **Tip:** Use prompts iteratively and adjust parameters as needed to achieve optimal results.
    
By keeping these pitfalls in mind, I have been able to generate clearer and more targeted prompts, ultimately enhancing the model's output quality. I have also been using markdown-style organization and referencing what I consider to be "known good" or "truths" in a "knowledge base" for the most complex tasks. This is a bit more involved but it has helped reduce false positives in the instances that I have needed to use LLMs to assist with work related tasks. If you are interested in how I have been using this method, please do reach out!

# Closing Thoughts

After using LLMs for a few months, I particularly enjoy the creative assistant aspect of LLMs outside of work. I personally don't think that LLMs are at the point where they can do my job for me, but I do think that I can use them to do a lot of the "dirty work". As time progresses, I think that using LLMs will become a requirement instead of a convenience and users that are able to create more effective prompts and adapt prompt designs for newer applications will be able to extract more refined data than those who do not embrace LLMs. 

If you're looking for some resources to learn more about LLMs, COSTAR, or Prompt Engineering in general, I have included a [Useful Resources](#useful-resources) section below.  I'm not sure if this blog post is useful or more of a random assortment of thoughts but if you enjoyed it, please do reach out!

# Useful Resources

## Guides and Cheatsheets
- <https://github.com/danielmiessler/fabric/tree/main>
- COSTAR: <https://freedium.cfd/https://towardsdatascience.com/how-i-won-singapores-gpt-4-prompt-engineering-competition-34c195a93d41?gi=15e8906b8668>
- Anthropic's Guide to Prompt Engineering: <https://docs.anthropic.com/en/docs/prompt-engineering>
- AI & Machine Learning in CyberSecurity: <https://tldrsec.com/p/ai-machine-learning-cybersecurity>
- Prompt Engineering Guide: <https://www.promptingguide.ai/>
- Demystifying LLMs: <https://calebsima.com/2023/08/16/demystifing-llms-and-threats/>
- Cheatsheet: <https://start.me/p/9oJvxx/applying-llms-genai-to-cyber-security>
- <https://archive.org/details/securing-llm-backed-systems-essential-authorization-practices-20240806/mode/2up>
- Prompt Generation by OpenAI: <https://platform.openai.com/docs/guides/prompt-generation>

## AI Courses
- Microsoft: <https://learn.microsoft.com/en-us/training/paths/ai-security-fundamentals/>
- Anthropic: <https://github.com/anthropics/courses/blob/master/anthropic_api_fundamentals/01_getting_started.ipynb>

## AI Talks
- <https://tldrsec.com/p/tldr-every-ai-talk-bsideslv-blackhat-defcon-2024>
- <https://tldrsec.com/p/2024-bsideslv-blackhat-ai-talks>
- <https://www.youtube.com/playlist?list=PLbZzXF2qC3RtlV2pwcvdbsCBc1Vb8kwVw>