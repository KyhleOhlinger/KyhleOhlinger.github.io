---
title: Modular Tracking for Maturity in Detection Engineering
author: kyhle
date: 2023-09-01 12:00:00 +0200
categories: [InfoSec, Non-Technical]
description: Hi all, My name is Kyhle Öhlinger and this blog post forms part of my personal blog. If you enjoy any of the posts, feel free to reach out and let me know :) 
image:
  path: /assets/img/detection-eng.jpg
  width: 800
  height: 500

---   


### Introduction

In the fast-paced world of cloud security, detection engineering is an imperative part of keeping your organization safe. Within detection engineering, new projects emerge frequently and priorities shift rapidly, having a structured approach to not only track progress but to integrate new Cloud Service Providers (CSPs) is crucial. In this blog post, we will explore a Proof of Concept (PoC) for a modular approach that enables the creation of projects while providing a means to track team maturity across CSPs. With this approach, your detection engineering team can effectively prioritize efforts and seamlessly integrate new objectives and CSPs into their yearly strategy.

### The Idea

The driving force behind this PoC was the need to revamp our current cloud security roadmap for the cloud detection engineering team. The roadmap strategy needed to be able to justify the team's work, measure progress, and make informed decisions regarding the team's focus areas, while still allowing for flexibility for ad-hoc projects and shifting business requirements. With other standards such as MITRE and NIST in place for audits, we sought a solution that would align with the unique nature of our work, which often involved ad-hoc projects and a variety of CSPs.

1. **Modular Approach:**
To address the dynamic nature of our work, the PoC proposes a modular approach. Rather than relying on a static roadmap, projects are broken down into smaller, self-contained modules that can be flexibly adapted to meet evolving business requirements. This ensures that the team can respond effectively to new challenges and seamlessly integrate new CSPs or objectives.

2. **Project Spanning Multiple CSPs:**
In our connected world, it is increasingly common for organizations to rely on multiple CSPs for different aspects of their operations. Recognizing this, the PoC emphasizes the importance of projects that can be adapted to include additional CSPs, in the likely event that a new provider is required to be supported. This approach enables the team to address security challenges holistically and ensure that a consistent and comprehensive roadmap exists which can be expanded to include new providers.

1. **Maturity Levels for Objectives:**
To help filter and prioritize efforts, the PoC suggests assigning maturity levels to each objective. These levels are determined internally and reflect the team's assessment of the completeness and effectiveness of their work on specific objectives. By systematically tracking and measuring maturity levels, the team can identify areas for improvement and channel resources accordingly.

### What This Is Not

It is important to note that the proposed solution is not a framework for audits, nor is it intended to be a one-size-fits-all solution. It is a PoC that addressed our specific needs and operational challenges. Additionally, as with any early-stage concept, this approach may evolve or even prove to be ineffective. Therefore, it is essential to remain open to adaptation and refinement based on real-world feedback and results. If you or your team intend on using this, it will almost certainly require refinement and adaptation to suit your environment. 

### Conclusion

The excel template is [here](/assets/excel/detection-tracker.xlsx). The quick preview doesn't seem to work at all on my blog, but it does open correctly once you download it. Feel free to use it as a base and change it as you need to. I hope this helps someone, even if it just helps you come to terms with organisation tactics that do or don't work in your own situation.

In the ever-evolving landscape of cloud security, having a modular approach to project creation while tracking team maturity across CSPs is vital. This PoC offers a promising solution to address these challenges for detection engineering teams by allowing the team to justify their work, measure progress, and make informed decisions. By embracing the flexibility of a modular approach and taking into account the maturity levels of objectives, we can prioritize efforts effectively and seamlessly integrate new CSPs and objectives with ease. While not a comprehensive coverage map across CSPs in terms of the Kill-chain/MITRE, this PoC provides a practical foundation to thrive and adapt in an increasingly complex security landscape.