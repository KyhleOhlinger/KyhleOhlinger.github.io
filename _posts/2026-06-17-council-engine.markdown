---
title: Council Engine&#58;  A Standalone Multi-Agent Debate Framework
author: kyhle
date: 2026-06-17 12:00:00 +0200
categories: [Technical, AI & LLMs]
description: Hi all, My name is Kyhle Öhlinger and this blog post forms part of my personal blog. If you enjoy any of the posts, feel free to reach out and let me know :) 
image:
  path: /assets/img/council-engine.png
  width: 800
  height: 500

--- 

Recently, I’ve been diving deep into [Daniel Miessler’s Personal AI Infrastructure (PAI)](https://github.com/danielmiessler/Personal_AI_Infrastructure/) ecosystem. One of the concepts that stood out to me the most was the ["Council"](https://github.com/danielmiessler/Personal_AI_Infrastructure/tree/main/Packs/Council) - a collaborative-adversarial multi-agent debate framework. To paraphrase his work; standard LLMs are inherently trained to be helpful, agreeable, and balanced. But when you are making complex architectural or security decisions, you don't want agreeable, you want "intellectual friction".

I wanted to experiment with this Council workflow, but I didn't necessarily want to deploy the entire, overarching PAI ecosystem to do it. So, over the past few days, I’ve been working on a standalone Python implementation that captures the core philosophy of the framework without the heavy dependencies. The result is the [Council Engine](https://github.com/KyhleOhlinger/council-engine).

**I'm not going to write this and pretend that Council was my idea, because it wasn't**. However, I am going to describe what I believe the overarching ideology was for this specific PAI module and why I wanted to create a standalone version for myself. 

## The Core Concept: Intellectual Friction
The premise of the Council is simple: the best decisions emerge when specialized experts with opposing biases are forced to debate a topic. Instead of asking a single AI model a question and getting a middle-of-the-road (or, more likely, an overly positive) answer, the Council Engine spins up distinct personas. For a software architecture problem, you might spin up a paranoid Security Engineer, a pragmatic Infrastructure Architect, and a velocity-focused Product Lead.

The engine runs these agents through a multi-round loop:
- **Parallel Generation:** The agents analyze the problem and state their initial case.
- **Sequential Debate:** The agents read each other's responses and actively attack flaws, expose hidden assumptions, or concede to better logic.
- **Executive Synthesis:** A final "judge" reads the resulting transcript and synthesizes a definitive recommendation based on the points of convergence and friction.

If you know PAI Council already, the prompts, round labels, and transcript structure should feel familiar. If you do not, you still get the core experience: a readable debate transcript plus an orchestrated final verdict. As with PAI, the Council Engine relies entirely on the filesystem for its context. You feed it Markdown files for the problem state, JSON files for the expert personas, and it spits out a final Markdown file containing the full transcript and result. If you are interested in multi-agent workflows or just want a better way to stress-test your ideas, feel free to check out the repository, spin up some custom experts, and let them fight it out.

## Why I built a standalone version
PAI Council is powerful, but it is also embedded in a specific environment: Claude Code skills, agent composition tooling, voice notifications, execution logging, and the broader PAI directory layout. That is the right shape for a personal AI operating system. It is not necessarily the right shape if you want to run the same debate pattern from a terminal, wire it into CI, review a draft blog post before publishing, or swap between OpenAI-compatible APIs and Cursor’s agent runtime.

That separation is the main design bet. PAI Council is a skill. Council Engine is a small runtime for that skill’s behavior. The goal here isn't to replace the full PAI infrastructure, but rather to isolate the Council pattern, strip away the ecosystem-specific dependencies, and make it highly operational.
- **Pack-Based Modularity:** Instead of spreading Council behaviors across system skill files and user overrides, a "Council" is just a self-contained folder. If you want to deploy a new domain (like real estate or security), you copy a pack of Markdown and JSON files. You never touch the Python code.
- **Strict Artifact Review:** While standard PAI debates handle freeform context, this engine explicitly structures inputs into a current_state (the artifact) and an ideal_state (the acceptance criteria). 
- **Decoupled Backends:** PAI assumes you are operating inside the Claude Code agent runtime. This implementation abstracts the LLM layer, letting you swap between standard APIs via LiteLLM or agent-style execution via the cursor-sdk.
- **A Pure CLI Toolchain:** Instead of interacting with the Council through conversational prompting inside a chat session, you get explicit terminal commands. This makes the entire framework scriptable, repeatable, and easy to integrate into larger automation pipelines.


### Dual-Engine Backend: LiteLLM & Cursor SDK
Because I tend to bounce between different LLMs depending on the task, I built the engine to be highly flexible. I implemented a router that allows you to choose your backend on the fly using an `--engine` flag:
- **LiteLLM Engine:** This allows you to plug in standard API keys and use OpenAI, Anthropic, or Gemini models.
- **Cursor SDK Engine:** Since I spend a lot of my time in Cursor, I integrated the newly released cursor-sdk. This allows you to run the entire multi-agent debate natively using Cursor's agents, leveraging your existing IDE login without needing to pass separate API keys.

The benefit of this backend approach is that if you're using a different implementation / LLM, you should be able to add in a new "module" with relative ease. 


## Conclusion
This standalone engine is fundamentally an homage to the structural thinking philosophy from PAI. By stripping away the larger environmental requirements of PAI, I wanted to see if its core value could be captured in a portable CLI that fits into my daily workflows, and I believe that this project has done just that.

If you find yourself constantly bouncing between models for a second opinion, or if you just want an adversarial way to stress-test your code, writing, or architectures, I highly encourage you to clone the repository and play with it. Spin up your own expert packs, tweak the formats, and see what kind of friction you can generate. You can find the full source code and setup instructions over on my [GitHub](https://github.com/KyhleOhlinger/council-engine).

As always, if you have any questions or comments, please reach out!