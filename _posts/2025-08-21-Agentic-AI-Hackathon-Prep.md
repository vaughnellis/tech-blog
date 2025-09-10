---
layout: post
permalink: "/post/software-engineering/agentic-ai-hackathon-prep"
title:  "Agentic AI Hackathon Prep Plan"
categories: [AI & ML, Software Engineering]
tags: [AI Agents, Azure, Semantic Kernel, AutoGen, Microsoft, Hackathon]
---

Hey there!

Come join me as I start my prep for the Agentic AI Hackathon hosted on the 25th of August (just a few more days!!)

I hear the term Agents from colleagues but it hasn't peaked my interest just yet because of the huge pile of list on my bucket.
I didn't want to add more to the list! 😅

Let's now build a prep plan together with Copilot!

The recommended learning & hands-on Plan:

### Phase 1: Foundations

* Goal: Familiarise with agentic AI basics, Azure setup, Semantic Kernel, and AutoGen.
* Actions:
    - Complete the <a href="https://learn.microsoft.com/en-us/training/paths/develop-ai-agents-on-azure/">Develop AI Agents on Azure </a> learning path.
    - Dive into the <a href="https://learn.microsoft.com/en-us/training/modules/develop-ai-agent-with-semantic-kernel/"> Develop an AI agent with Semantic Kernel</a> module.
    - Explore <a href="https://learn.microsoft.com/en-us/training/modules/orchestrate-semantic-kernel-multi-agent-solution/"> Multi-Agent orchestration with Semantic Kernel</a> module.
    - Read through Microsoft's <a href="https://microsoft.github.io/PartnerResources/skilling/ai-ml-academy/agenticAI"> Agentic AI</a> resources.
    - Look for blogs around <a href="https://techcommunity.microsoft.com/blog/educatordeveloperblog/using-azure-ai-agent-service-with-autogen--semantic-kernel-to-build-a-multi-agen/4363121/">Using Azure AI Agent Service with AutoGen / Semantic Kernel to build a multi-agent's solution</a> for architectural insight.
    - <a href="https://microsoft.github.io/AI_Agents_Hackathon/#stream-schedule">Watch expert livestreams </a> occurred from April 8 -30 which covers a wide-range of topics such as SK, AutoGen, Azure Agent SDK, and Microsoft 365 Agents SDK. 

### Phase 2: Hands-On Build & Explore
* Goal: Build simple agents and gradually layer complexity
* Actions:
    - Simple Agent Build
        - Use the exercise <a href="https://github.com/MicrosoftLearning/mslearn-ai-agents/blob/main/Instructions/04-semantic-kernel.md/">Develop an Azure AI agent with the Semantic Kernel SDK</a> to create a {build-your-own-use-case} agent
    - Tool Integration
        - Add further functionality!
    - Multi-Agent Orchestration
        - Implement <a href="https://learn.microsoft.com/en-us/training/modules/orchestrate-semantic-kernel-multi-agent-solution"> orchestration patterns such as concurrent, sequential, group chat, handoff, and magentic using Semantic Kernel SDK </a>.
    - AutoGen Integration
        - <a href="https://devblogs.microsoft.com/semantic-kernel/semantic-kernel-and-autogen-part-2/">Learn how AutoGen can orchestrate multiple agents, and optionally integrate Semantic Kernel and AutoGen </a>.


### Phase 3: Deep Dive
* Goal: Build prototypes to gain more experience
* Actions:
    - Azure AI Agents: 
        - Build and deploy a single agent with real actions.
    - End-to-End Multi-Agent: 
        - Build an agent chain that uses orchestration patterns.
    - Enable Multi-Agent Frameworks: 
        - Focus on framework-level integration (SK + AutoGen).
    - Presentation Builder: 
        - Pair agent orchestration with document generation.
* Prep:
    - Sketch architecture: determine agents, tools, interactions.
    - Build minimal viable prototype with Semantic Kernel and/or AutoGen.
    - Use Azure Foundry SDK (C# or Python).
    - Add output layer such as web interface / presentation export.
    - Incorporate security and governance basics (human-in-loop, input sanitisation)


Let me know your thoughts and here's to a fun and exciting hacking!