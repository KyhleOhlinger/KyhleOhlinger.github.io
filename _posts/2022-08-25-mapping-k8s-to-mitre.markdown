---
title: Mapping K8s to MITRE ATT&CK IDs
author: kyhle
date: 2022-08-25 12:00:00 +0200
categories: [InfoSec, Non-Technical]
description: Hi all, My name is Kyhle Öhlinger and this blog post forms part of my personal blog. If you enjoy any of the posts, feel free to reach out and let me know :) 
image:
  path: /assets/img/conferences.png
  width: 800
  height: 500
---

Last year, Microsoft released the second version of the [threat matrix](
https://www.microsoft.com/security/blog/2021/07/21/the-evolution-of-a-matrix-how-attck-for-containers-was-built/) for Kubernetes. Version 2 added new techniques that were found by Microsoft researchers and techniques that were suggested by the community, while also removing several techniques which were no longer relevant. While looking into Kubernetes detections, I needed to map them back to MITRE IDs. I started looking into the current Container framework by [MITRE](https://attack.mitre.org/matrices/enterprise/containers/) and realised that the framework did not include a number of the tactics presented by the Microsoft Kubernetes threat matrix. The reason is detailed within Microsoft's blog post, but I have included an excerpt below:

> ATT&CK focuses on real-world techniques that are seen in the wild. In contrast, many of the techniques in the threat matrix were observed during research work and not necessarily as part of an active attack.

While this made sense, it did not help my situation and I needed to find a way to map the events back to valid MITRE IDs. This post describes the mappings, and I have created a [GitHub page](https://github.com/KyhleOhlinger/K8-Mitre-Mapping) which includes the mappings in a tabular format as well as a description for each TTP for quick reference. 

## Threat Matrix Mappings 
> The MITRE mappings were created by Microsoft and are not officially supported by the MITRE ATT&CK framework. Where possible, mappings from the Microsoft Kubernetes threat matrix to the existing MITRE ATT&CK techniques have been made.
{: .prompt-warning }

| Microsoft Threat Matrix Name | Technique(s) | MITRE ATT&CK Mapping|
|:--|:--|--:|
| Using Cloud Credentials | Initial Access| [T1078.004](https://attack.mitre.org/techniques/T1078/004/) |
| Compromised Images in Registry | Initial Access | [T1525](https://attack.mitre.org/techniques/T1525/) |
| Kubeconfig File | Initial Access | [T1552.001](https://attack.mitre.org/techniques/T1552/001/) |
| Application Vulnerability | Initial Access | [T1190](https://attack.mitre.org/techniques/T1190/) |
| Exposed Sensitive Interfaces | Initial Access | [T1133](https://attack.mitre.org/techniques/T1133/) |
| Exec Into Container | Execution | [T1609](https://attack.mitre.org/techniques/T1609/) | 
| bash/cmd Inside Container | Execution | [T1609](https://attack.mitre.org/techniques/T1609/) |
| New Container | Execution | [T1610](https://attack.mitre.org/techniques/T1610/) |
| Application Exploit (RCE) | Execution | [T1203](https://attack.mitre.org/techniques/T1203/) |
| SSH Server Running Inside Container | Execution | [T1021.004](https://attack.mitre.org/techniques/T1021/004/) |
| Sidecar Injection | Execution | [T1055](https://attack.mitre.org/techniques/T1055/) |
| Backdoor Container | Persistence | [T1053.007](https://attack.mitre.org/techniques/T1053/007/) |
| Writeable hostPath Mount | Persistence | [T1611](https://attack.mitre.org/techniques/T1611/) |
| Kubernetes CronJob | Persistence | [T1053.007](https://attack.mitre.org/techniques/T1053/007/) |
| Malicious Admission Controller | Persistence | [T1056](https://attack.mitre.org/techniques/T1056/) | 
| Privileged Container | Privilege Escalation | [T1611](https://attack.mitre.org/techniques/T1611/) |
| Cluster-Admin Binding | Privilege Escalation | [T1098](https://attack.mitre.org/techniques/T1098/) |
| hostPath Mount | Privilege Escalation | [T1611](https://attack.mitre.org/techniques/T1611/) |
| Access Cloud Resources | Privilege Escalation | [T1550](https://attack.mitre.org/techniques/T1550/) |
| Clear Container Logs | Defense Evasion | [T1070](https://attack.mitre.org/techniques/T1070/) | 
| Delete K8s Events | Defense Evasion | [T1562](https://attack.mitre.org/techniques/T1562/) |
| Pod / Container Name Similarity | Defense Evasion | [T1036.005](https://attack.mitre.org/techniques/T1036/005/) |
| Connect From Proxy Server | Defense Evasion | [T1090](https://attack.mitre.org/techniques/T1090/) | 
| List K8S Secrets | Credential Access | [T1552.007](https://attack.mitre.org/techniques/T1552/007/) |
| Mount Service Principal | Credential Access |  [T1528](https://attack.mitre.org/techniques/T1528/), [T1078.003](https://attack.mitre.org/techniques/T1078/003/) |
| Access Container Service Account | Credential Access |  [T1528](https://attack.mitre.org/techniques/T1528/), [T1078.003](https://attack.mitre.org/techniques/T1078/003/) |
| Application Credentials in Configuration Files | Credential Access | [T1552.001](https://attack.mitre.org/techniques/T1552/001/) |
| Access Managed Identity Credential | Credential Access | [T1552.005](https://attack.mitre.org/techniques/T1552/005/) |
| Malicious Admission Controller | Credential Access | [T1056](https://attack.mitre.org/techniques/T1056/) | 
| Access the K8S API Server | Discovery | [T1613](https://attack.mitre.org/techniques/T1613/) |
| Access Kubelet API | Discovery | [T1046](https://attack.mitre.org/techniques/T1046/) |
| Network Mapping | Discovery | [T1046](https://attack.mitre.org/techniques/T1046/) |
| Access Kubernetes Dashboard | Discovery | [T1538](https://attack.mitre.org/techniques/T1538/) |
| Instance Metadata API | Discovery | [T1552.005](https://attack.mitre.org/techniques/T1552/005/) |
| Access Cloud Resources | Lateral Movement | [T1550](https://attack.mitre.org/techniques/T1550/) |
| Container Service Account | Lateral Movement | [T1078.003](https://attack.mitre.org/techniques/T1078/003/) | 
| Cluster Internal Networking | Lateral Movement | [T1599](https://attack.mitre.org/techniques/T1599/) |
| Application Credentials in Configuration Files | Lateral Movement | [T1552.001](https://attack.mitre.org/techniques/T1552/001/) |
| Writeable Volume Mounts on the Host | Lateral Movement | [T1611](https://attack.mitre.org/techniques/T1611/) |
| CoreDNS Poisoning | Lateral Movement | [T1071.004](https://attack.mitre.org/techniques/T1071/004/) |
| ARP Poisoning and IP Spoofing | Lateral Movement | [T1557.002](https://attack.mitre.org/techniques/T1557/002/) |
| Images from a Private Registry | Collection | [T1213](https://attack.mitre.org/techniques/T1213/) |
| Data Destruction | Impact | [T1485](https://attack.mitre.org/techniques/T1485/) |
| Resource Hijacking | Impact | [T1496](https://attack.mitre.org/techniques/T1496/) |
| Denial of Service | Impact | [T1499](https://attack.mitre.org/techniques/T1499/), [T1498](https://attack.mitre.org/techniques/T1498/) |

## Stratus Red Team Mappings
In addition to the Microsoft threat matrix mappings, I included mappings for the techniques outlined within the Stratus Red Team [toolkit](https://stratus-red-team.cloud/attack-techniques/list/). However, *Create Client Certificate Credential* was not mapped as the technique does not work on AWS EKS. 

| Stratus Red Team Name | Microsoft Threat Matrix Name | Technique(s) | MITRE ATT&CK Mapping|
|:-----------------------------|:-----------------|:-----------------|--------:|
| Dump All Secrets	| List K8s Secrets | Credential Access |  [T1557.002](https://attack.mitre.org/techniques/T1557/002/)   | 
| Steal Pod Service Account Token |  Access Container Service Account | Credential Access | [T1550](https://attack.mitre.org/techniques/T1550/) |
| Create Admin ClusterRole	| Cluster-Admin Binding | Persistence, Privilege Escalation | [T1098](https://attack.mitre.org/techniques/T1098/) |
| Create Long-Lived Token | N/A | Persistence |  [T1098.001](https://attack.mitre.org/techniques/T1098/001/) |
| Container breakout via hostPath volume mount	| Writeable hostPath Mount | Privilege Escalation | [T1611](https://attack.mitre.org/techniques/T1611/) |
| Privilege escalation through node/proxy permissions | N/A | Privilege Escalation | [T1548](https://attack.mitre.org/techniques/T1548/) | 
| Run a Privileged Pod	| Privileged Container | Privilege Escalation | [T1611](https://attack.mitre.org/techniques/T1611/) |



## MITRE Containers 

The MITRE ATT&CK IDs provided above were created for a specific purpose and I hope that it can be improved by the community to assist with Kubernetes MITRE mappings. However, the current MITRE Containers matrix should be the defacto for your organisation and is something that all organisations (who use MITRE) should reference. I also believe that everyone should read the Microsoft blog post referenced above, as it is a lot more comprehensive but does not include mappings to MITRE IDs. 


If you enjoyed this and would like to add to it, or if you would like to collaborate to improve the mappings, pleased do reach out!