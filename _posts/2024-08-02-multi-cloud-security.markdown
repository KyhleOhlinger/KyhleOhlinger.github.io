---
title: Diving into Multi Cloud Security Frameworks
author: kyhle
date: 2024-08-02 12:00:00 +0200
categories: [Technical, Cloud Security]
description: Hi all, My name is Kyhle Öhlinger and this blog post forms part of my personal blog. If you enjoy any of the posts, feel free to reach out and let me know :) 
image:
  path: /assets/img/multi_cloud.png
  width: 800
  height: 500

---   

As organizations adopt a Multi Cloud strategy, ensuring the security of their cloud environments becomes increasingly complex. With multiple cloud providers, services, and tools in use, organizations must develop a comprehensive security program that addresses the unique challenges of a Multi Cloud environment. In this blog post, I will break down Multi Cloud, discuss some advantages and disadvantages, and talk about Multi Cloud Roadmaps (including my failed attempt at contributing to one).

# What is a Multi Cloud Environment?

Let us take a step back and dive into what a Multi Cloud environment [is](https://www.cloudflare.com/learning/cloud/what-is-multicloud/):

> "Multi-cloud" means multiple public clouds. A company that uses a Multi Cloud deployment incorporates multiple public clouds from more than one cloud provider.

To expand on that broad definition, Multi Cloud typically refers to a cloud strategy where an organization uses multiple cloud services from different cloud service providers (CSPs). This means that an organization can use different cloud providers for different purposes such as using one cloud provider for storage (e.g. AWS), another for data analytics (e.g. GCP), and another for web hosting (e.g. Azure). Using a Multi Cloud strategy can provide several benefits such as reducing the risk of data loss or downtime in case of a failure of one cloud provider and the ability to choose the best cloud provider for a specific use case based on factors such as cost, performance, and security. However, implementing a Multi Cloud strategy can also add complexity to an organization's IT infrastructure as it requires managing and integrating multiple cloud services, and ensuring compatibility between them.

## Adoption of Multi Cloud Environments

During the recent "State of the Cloud" report from [Wiz](https://www.wiz.io/blog/the-top-cloud-security-threats-to-be-aware-of-in-2023), the Wiz team provided a range of statistics and insights based on scanning over 200,000 cloud accounts across several industries. Based on their report, the breakdown of the number of CSPs that organizations use is provided below:
- 22% of companies use three or more platforms
- 35% of companies use two platforms
- 43% of companies use one platform

> "According to our data, the idea of Multi Cloud as a single architecture that spans multiple cloud providers is uncommon. Most companies are only on one cloud and in cases where they are using multiple clouds, the majority of their workloads are on one cloud provider. In fact, about 43% of customers operate entirely on one cloud."

A recent interview by [SentinelOne](https://www.sentinelone.com/blog/staying-secure-in-the-cloud-an-angelneers-interview-with-ely-kahn/) also spoke about Multi Cloud usage and one of the key points is provided below:

> "Rarely is the same application being used across multiple cloud providers. More often, organizations are picking one cloud provider for one type of workload and another cloud provider for another type of workload, because you really like their capabilities in a particular area. Back to the example, perhaps an organization is using Azure for its machine learning, but then using AWS for everything else.

Based on the statistics and quotes provided above, it is unlikely that the companies using multiple cloud service providers (57%) have subject matter experts (SMEs) for all providers. Additionally, with the integration of various Software-as-a-Service (SaaS) providers, the task of effectively securing environments becomes increasingly challenging. Managing Multi Cloud complexity requires new approaches that not only promote automation, but assist in simplification. It requires the implementation of security, operational controls, and reliability into the design, build, deploy (DevOps) processes. Additionally, it requires having the right skills and policies in place, and implementing a cultural shift in how organizations develop and modernize applications for the cloud.

## Advantages and Disadvantages of Multiple Cloud Providers?

One of the most common questions when talking about cloud providers and Multi Cloud environments is "Should I use multiple cloud providers?". In my opinion, the added complexity is not worth the effort of using multiple cloud providers (*for most organizations*). The skills required to secure a single environment is a challenge, and introducing additional providers into your organization's ecosystem will only add additional areas of concern. However, each organization has different requirements. Some of the key difference between single and Multi Cloud environments are provided below:

1. **Vendor Lock-in:** A Multi Cloud environment allows organizations to avoid vendor lock-in by using multiple cloud providers, whereas a single cloud provider ties an organization to that provider's platform.
2. **Diversity:** A Multi Cloud environment provides a diverse range of cloud providers, which allows organizations to choose the best fit for each workload or application. On the other hand, a single cloud provider offers a more standardized solution.
3. **Flexibility:** Multi Cloud environments offer greater flexibility to organizations to scale up or down, optimize costs, and select the best cloud provider for each workload. In contrast, a single cloud provider may limit an organization's flexibility in choosing the best solution for each workload.
4. **Compliance Requirements:** Some organizations may be required to store data in different geographic regions or to use multiple cloud providers to meet regulatory compliance requirements. A Multi Cloud strategy can help meet these requirements.

While a Multi Cloud environment can offer several benefits to organizations, it may not be the best fit for every business. There are situations where a single-cloud environment may be more suitable as described [here](https://hbr.org/sponsored/2022/06/how-to-manage-the-complexity-of-multi-cloud-environments) and  [here](https://www.darkreading.com/zscaler/multicloud-security-challenges-will-persist-in-2023). The main concerns are provided below:
1. **Simplicity:** A Multi Cloud environment can add complexity to an organization's IT infrastructure, which may not be worth the benefits for smaller or less complex systems. Implementing and managing a Multi Cloud environment can be complex, as it involves coordinating between multiple cloud providers, managing data transfer and integration, and ensuring that all systems work together seamlessly. This can lead to increased management and integration costs and require a more skilled workforce to reduce the risk of misconfiguration.
2. **Cost-effectiveness:** While a Multi Cloud strategy can help organizations optimize costs by choosing the most cost-effective cloud provider for each workload, it can also lead to increased costs in terms of management, integration, and data transfer fees. In some cases, a single cloud provider may be more cost-effective. 
3. **Compatibility issues:** Some workloads may not be compatible with all cloud providers, and integrating multiple providers can create compatibility issues. In such cases, a single cloud provider may be the best choice. Different cloud providers may use different APIs and architectures, making it challenging to move data and workloads between different cloud providers. This can lead to interoperability issues and require significant development effort to overcome.
4. **Security concerns:** Security is a top concern for any cloud environment, but it becomes even more complex in a Multi Cloud environment where multiple cloud providers and services are used. Organizations need to ensure that their data is protected across all cloud environments and that the right security controls are in place to mitigate risks. Managing security across multiple cloud providers can be challenging as each provider may have its own security standards and controls which can create security gaps and make it difficult to manage security consistently across all cloud environments. This may increase the risk of data breaches or security incidents.

Overall, the security state of Multi Cloud environments requires careful consideration and management. Organizations should implement a comprehensive security strategy that includes consistent security controls, regular risk assessments, and proactive threat detection and response. By taking a proactive and holistic approach to security, organizations can minimize the risks associated with Multi Cloud environments and ensure their data and applications are secure.

# Let's Talk about Multi Cloud Roadmaps

Last year I had the pleasure of working with several members of the [fwd:CloudSec](https://fwdcloudsec.org/) community on a [Multi Cloud Roadmap based on NIST CSF](https://docs.google.com/spreadsheets/d/14yWqTvsDLdvEfKVrl1YHANqL7nUDuCk4FsQTxCSZIWU/edit#gid=1622352047). While this framework was never completed, the work by Securosis on the [Cloud Security Maturity Model](https://securosis.com/blog/check-out-the-shiny-new-cloud-security-maturity-model-2-0/) highlights a number of the items that the framework was aiming towards. There were a number of fantastic frameworks that it was based on and I wanted to ensure that they were highlighted during this post for anyone that is going down this path.

If your organization is adopting Multi Cloud, or if your organization already utilises multiple cloud providers, the [NIST Cybersecurity Framework (CSF)](https://www.nist.gov/cyberframework/online-learning/five-functions) and the [Amazon Web Services (AWS) Security Model](https://maturitymodel.security.aws.dev/en/model/) frameworks provide a comprehensive approach to security for organizations. Additionally, the Cloud Security Maturity Model linked above is a fantastic resource that I highly recommend reading! In general. organizations that use these frameworks can benefit from enhanced security, reduced risk, and improved compliance with regulatory requirements.

## How would I use a Multi Cloud Roadmap?

One of the key issues with releasing a new framework or roadmap is adoption. If it is not easy to adopt, it is unlikely that anyone will actually use it. Additionally, based on the complexity and variety of organizations that are most likely going to use a framework, there will be several approaches to utilizing something like this. The Multi Cloud roadmap is designed to provide a structured approach to building a comprehensive security program for Multi Cloud environments. A few key steps to using this framework effectively are provided below:
1. **Assess your current security posture:** Before implementing the framework, it is important to assess your current security posture and identify any gaps or weaknesses in your existing security program. This assessment can help you identify areas of focus and prioritize your security efforts.
2. **Understand the framework:** Maturity frameworks consist of several components, including threat management, access control, data protection, and compliance. Each component includes specific security controls and best practices for implementation.
3. **Identify your security objectives:** Once you understand the framework, it is important to identify your organization's security objectives and prioritize the security controls that are most relevant to your needs. This can help you focus your efforts and allocate resources effectively.
4. **Implement the framework:** With your security objectives and priorities in mind, you can begin implementing the security controls outlined in the framework. It is important to take a systematic approach to implementation and ensure that all components of the framework are integrated and working together effectively.
5. **Monitor and update your security program:** A Multi Cloud environment is dynamic, and your security program should be too. It is important to monitor your security program regularly and update it as needed to address new threats or changing business requirements.

# Conclusion

In today's business landscape, Multi Cloud environments have become increasingly common and with them comes the need for a comprehensive security program. Maturity frameworks provide a structured approach to building a robust security program for a Multi Cloud environment, addressing key areas such as threat management, access control, data protection, and compliance. 

As always, if you have any questions or if you would like me to include specific content in my blog, please do reach out!