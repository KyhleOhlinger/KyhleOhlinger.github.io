---
title: Reducing your Attack Surface by Limiting Cloud Services
author: kyhle
date: 2024-09-11 12:00:00 +0200
categories: [Technical, Cloud Security]
description: Hi all, My name is Kyhle Öhlinger and this blog post forms part of my personal blog. If you enjoy any of the posts, feel free to reach out and let me know :) 
image:
  path: /assets/img/cloud-attack-surface.png
  width: 800
  height: 500

---   

The cloud is confusing. Not only are there numerous services competing for your attention, the number of services per cloud service provider (CSP) are also increasing every year. It is difficult enough for companies to try and secure the services that they make use of, let alone the hundreds of services that they do not use in any way, shape, or form. This begs the question, if the services are not being used, why allow them to increase your attack surface? 

This blog post does not contain any new or novel research, however I hope that it highlights some interesting considerations and serves as a point of reference for organizations that are looking to reduce their attack surface by simply limiting the number of services allowed and enabled within their environments. By reading through this post, you will be equipped with a fundamental understanding of crucial aspects: the concept of an attack surface, excerpts related to concerns within the cloud, and effective strategies for reducing your organization's attack surface by limiting the number of approved services within popular (AWS, Azure, and GCP) CSPs.

# What is an Attack Surface? <a name="attack_surface"></a>

When discussing cloud security, the term "attack surface" refers to the potential points of entry that malicious actors can exploit to gain unauthorized access to a system or the underlying infrastructure. The smaller the attack surface, the easier it is to protect your organization's assets. The attack surface typically includes various components such as networks, virtual machines, databases, APIs, user interfaces, and more. Each component presents an opportunity for attackers to exploit weaknesses and potentially gain access to your organization. By understanding and effectively managing the attack surface, organizations can enhance their cloud security posture and reduce the risk of breaches or unauthorized access.

[Okta](https://www.okta.com/) and [Informer](https://informer.io/) both have great posts ([1](https://www.okta.com/identity-101/what-is-an-attack-surface/) and [2](https://informer.io/resources/5-ways-to-reduce-cloud-attack-surface)) on attack surfaces, attack vectors, and attack surface reduction steps which I would recommend reading if you are looking to learn more about this topic and methods to identify areas of weakness within your organization. 

# State of the Industry Excerpts <a name="statistics"></a>

I was going to do a dive deep into this part, but it ended up being a bit redundant and drew attention away from the main point of the post. Fortunately for me, a number of organizations publish reports and have already done the heavy lifting when it comes to statistics based on cloud services and challenges within Cloud Security. If you have read this far and you are still wondering why this post is even relevant, I have included a few extracts from various resources below.

### Incidents in Cloud <a name="incidents"></a>

[Mandiant](https://www.mandiant.com) with their [M-Trends Report](https://www.mandiant.com/m-trends) and [Palo Alto](https://www.paloaltonetworks.com/) with their [Unit 42 Cloud Threat Report](https://start.paloaltonetworks.com/unit-42-cloud-threat-report-volume-7-success.html?) have some fantastic breakdowns of security incidents, exploitation vectors, and statistics. With the increase in cloud usage across providers, the following was taken from the Palo Alto report:

> "The more organizations that adopt cloud-native technologies, the higher the number of cloud-native applications becomes. The popularity and complexity of the technology then expands the attack surface with vulnerabilities and  misconfigurations for cybercriminals to exploit."

Cloud security requires a unique set of skills that combine traditional security practices with an understanding of cloud architecture, virtualization, and various cloud service providers. Professionals need to be well-versed in areas such as identity and access management, network security, data encryption, threat intelligence, incident response, and compliance frameworks specific to cloud environments. The skillset shortage mainly stems from the rapid growth and evolution of cloud technologies which have outpaced the availability of specialized training and education programs. 

### New Services are Constantly Added <a name="new_services"></a>

[Wiz](https://www.wiz.io/) have provided number of statistics in their [The State of the Cloud](https://www.wiz.io/blog/the-top-cloud-security-threats-to-be-aware-of-in-2023) report, including the following about cloud based services:

> Cloud providers keep increasing their offerings and their complexity. In addition to growing in size, cloud providers are also becoming more complex. AWS has added APIs at a steady pace, with about 40 new services and 1600 new actions per year for the past 6 years. The yearly spikes are due to the annual AWS re:Invent conference where they release large numbers of new features.

> Additionally, the privileges available to control API access have increased in the past year across the top three cloud providers by 15% for AWS, 20% for Azure, and 45% for GCP.

### Skillset Shortage in Cloud Security<a name="skill_shortage"></a>

A word from [Snyk](https://snyk.io) on [Skillset Challenges](https://snyk.io/series/cloud-security/challenges/):
> This is perhaps the largest, non-malicious insider threat facing organizations today, and this concept is the culmination of many of the topics we've already discussed in this article.
> Remember, misconfiguration of your cloud platform and APIs opens the door to a host of data vulnerabilities. Failure to understand and comply with data regulations can subject your organization to the wrath of government authorities while sullying your reputation as well. A failure to adopt adequate and documented access control and change management practices will likely leave your organization vulnerable to insider and outsider threats, and may bring unwanted public attention and lawsuits as well.

As well as a post from [DarkReading](https://darkreading.com) on [Addressing Cybersecurity's Talent Shortage & Its Impact on CISOs](https://www.darkreading.com/endpoint/addressing-cybersecurity-talent-shortage-its-impact-on-cisos):

> What's behind this growing shortage? We're seeing organizations shift their approach to cloud-first strategies to achieve greater scale and flexibility. At the same time, they're using more than one cloud technology provider and multiple database providers, resulting in more work, more alerts, and more data. This creates a need for new tools, changes in practice and skill, and overall involvement due to complexity.


# How can we Protect our Organizations at a High-Level? <a name="high_level_overview"></a>

With that information in mind, how can you go about logically identifying active services within your environment and effectively limit the number of services? Additionally, with these services enabled, how do you monitor for potential abuse in the future?

1. **Provider hierarchies:** Understanding the [hierarchies within cloud service providers](https://blog.matrixpost.net/google-cloud-organization-vs-aws-organizations-vs-microsoft-azure-management-groups/) can help you effectively identify active services in your environment. Providers often offer organizational or account structures that allow you to group resources and services. By organizing your environment into logical groups, such as by department or project, you can assess which services are being actively used within each group.

2. **Logging basics:** Understanding logging basics and what is possible across various services is a crucial aspect of monitoring and securing your cloud environment. Different cloud services provide various logging capabilities. By understanding the logging features specific to each service, you can effectively monitor and analyze the logs to identify any suspicious or abusive activities. Familiarize yourself with the available logs, including audit logs, access logs, and activity logs, and configure them to capture relevant information for analysis.

3. **Identify services:** Conducting a comprehensive assessment of your environment is essential to identify the services that are actively being used. This involves understanding the dependencies between services, reviewing service usage metrics, billing, logs, and engaging with stakeholders to determine which services are critical to ongoing operations.

4. **Create a list of "Active/Allowed" services**: After identifying the services in use, develop a list of "Active/Allowed" services. This list should include the services required for your organization's operations and any approved exceptions. By creating and maintaining a centralized inventory, you can ensure that only authorized services are enabled, reducing the attack surface and potential vulnerabilities. One method to accomplish this is through the use of Service Control Policies - [SummitRoute](https://summitroute.com/blog/2020/03/25/aws_scp_best_practices/#allow-only-approved-services) has a fantastic breakdown of SCP best practices for AWS and a similar approach can be applied across cloud providers. 

5. **Monitor spikes in calls to "Denied" services**: Implement monitoring mechanisms to track any changes to the list of active services or unexpected usage patterns. Set up alerts or triggers to notify your team when new services are provisioned or when there is a spike in requests for denied services. This proactive approach enables you to quickly identify and address any unauthorized or potentially abusive activities, preventing them from escalating into security incidents.

6. **Create a process for including and excluding services:** When considering the inclusion or retirement of services in your cloud environment, it's crucial to have a well-defined and standardized process in place. This process should involve clear guidelines, governance, and security reviews to ensure that services are maintained and introduced seamlessly and securely. It is imperative that this process is not a blocker within your organization and that the stakeholders see the value of this undertaking. 

By following these steps, you can logically identify the active services within your environment, effectively limit the number of enabled services, and establish a process for ongoing monitoring and abuse detection. This helps ensure that your cloud environment remains secure and aligned with your organization's operational needs.  Now that we have covered the process from a high-level, I will dive a bit deeper into how to do the allow list creation across the cloud service providers mentioned at the start.


# Safeguards to Ensure that Business is not Disrupted <a name="safeguards"></a>

If you are implementing an allowed list of services within your organization, there are a few safeguards that you should implement to ensure that your business is not negatively impacted by these changes. Rami had a great [post](https://ramimac.me/aws-allowlisting) on how [Figma](https://www.figma.com/) went through the process for their AWS environment and some caveats that they stumbled upon during the implementation.

When creating policies within cloud providers, it is important to consider safeguards to prevent business disruptions. While I am not going to go into depth with each component, I have provided high-level safeguards and best practices to ensure a smooth transition when creating and enforcing policies:

1. **Thoroughly Plan and Test:** Before implementing any new policies, thoroughly plan and assess potential impact. Consider conducting thorough testing in a non-production environment to determine any potential disruptions or unintended consequences.

2. **Start with Non-Disruptive Policies:** Begin by implementing policies that have minimal impact on existing resources and business operations. This approach minimizes the chances of unintended disruptions and allows for gradual policy enforcement.

3. **Use Staging Environments:** Implement policies in a staging or non-production environment first to assess their impact and verify their effectiveness. This ensures that your business-critical resources and workflows are not affected during the initial policy implementation.

4. **Monitor and Audit Policy Enforcement:** Continuously monitor and audit the impact of policy enforcement on your environment. This helps identify any disruptions or issues early on and allows for timely adjustments or corrections.

5. **Implement Rollback Plans:** Have a rollback plan in place to revert back to the original state if policy enforcement results in significant disruptions or unexpected issues. This plan should detail the steps to reverse or modify policies to restore normal operation.

6. **Communicate Changes and Educate Users:** Inform and educate affected users, teams, or stakeholders about the new policies and their potential impact. Provide clear communication and training to ensure everyone understands the changes and the reasons behind them.

7. **Use Policy Compliance Reports:** Regularly review policy compliance reports provided by the cloud provider to ensure policies are effectively enforced without inadvertently blocking critical business activities. Adjust policies as needed based on compliance findings.
   
8. **Have a Process for Allowing Services:** While limiting your attack surface is important, you need to have methods to support the business. If the organization intends on utilizing new services or would like to remove a service from the block list, ensure that there is an easy, automated way to onboard these services and not become a blocker.

9.  **Continuous Improvement:** Continuously evaluate the effectiveness of the policies and procedures and refine them over time. Adapt these features based on evolving requirements and feedback from teams, ensuring they strike the right balance between security/control and business continuity.

By following these safeguards and best practices, you can mitigate disruptions and minimize the impact on business operations when creating and enforcing policies within cloud providers. Remember that these types of features should be implemented gradually and with careful consideration for your specific business requirements and environment.


# Conclusion <a name="conclusion"></a>

The dynamic nature of cloud security with the rising adoption of cloud-native technologies and the increasing number of cloud-native applications means that threats to cloud based resources are ever evolving. The rate of new services being introduced also makes it challenging for professionals to keep up with the latest techniques and practices. It can seem impossible to secure each and every part of the business and a number of organizations struggle with retaining the right talent. To combat this, organizations either need to hire a large number of professionals who are up-to-date with every aspect of the ever evolving cloud or, more realistically, they need to find ways to prioritize strong security measures and reduce their attack surface. 

By limiting the number of services enabled within the cloud service provider, organizations can effectively reduce their attack surface. Taking a proactive approach to evaluate the necessity of each service and disabling unnecessary ones can significantly minimize the areas vulnerable to exploitation. Moreover, this approach allows for more efficient monitoring and allocation of resources, ensuring that security measures are concentrated on the essential components. 

I hope that you have learned something from this post and, as always, feel free to reach out to me with any comments!