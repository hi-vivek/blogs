---
title: Creating an AWS WAF IP Set and Associating it with an ALB
date: 2024-01-11
authors: [amanw]
slug: Creating-an-AWS-WAF-IP-Set-and-Associating-it-with-an-ALB
description: >
  Guide to Creating an AWS WAF IP Set and Associating it with an ALB
categories:
  - DevOps
tags:
  - DevOps
  - WAF
  - Security
  - ALB
---
# Safeguarding Your ALB with AWS WAF: Creating an IP Set and Associating it

## Introduction

In the dynamic landscape of web applications, security is a top priority. AWS provides an effective solution through the Web Application Firewall (WAF), allowing users to control and mitigate potential threats. This blog post guides you through the process of creating an AWS WAF IP set and associating it with an Application Load Balancer (ALB), enhancing the security posture of your applications.

<!-- more -->

## Problem Statement

Web applications are susceptible to various cyber threats, including malicious IP addresses attempting to exploit vulnerabilities. AWS WAF empowers developers and administrators to implement fine-grained access controls, safeguarding web applications from potential attacks. The challenge lies in configuring AWS WAF to effectively filter and manage incoming traffic, specifically targeting an ALB.

## Technical Details

### Step 1: Create an IP Set

1. **Sign in to the AWS Management Console:**
   - Begin by logging in to your AWS account through the AWS Management Console.

2. **Open the AWS WAF console:**
   - Navigate to the AWS WAF console to access the necessary tools.

![Step 1](https://github.com/Flairminds/blogs/assets/91743769/52a0d11d-7123-4c30-a3a2-1c122f93c4b5)

### Step 2: Create IP Set with Allowed or Disallowed IPs

1. **In the navigation pane, select "IP sets":**
   - Identify and choose the "IP sets" option in the navigation pane of the AWS WAF console.

2. **Choose "Create IP set":**
   - Initiate the creation of a new IP set to define the list of IP addresses that are either allowed or disallowed.

3. **Provide a name and configure IP addresses:**
   - Assign a name to the IP set and specify the list of IP addresses based on your security requirements.

4. **Create IP set:**
   - Confirm and save the configuration by choosing the "Create IP set" option.

![Step 2](https://github.com/Flairminds/blogs/assets/91743769/230face0-43db-4369-9513-6726763df8db)

### Step 3: Associate Web ACL with an AWS Resource (ALB)

1. **Navigate to "Web ACLs" in the AWS WAF console:**
   - Access the "Web ACLs" section to manage and configure web access control lists.

2. **Select the desired Web ACL:**
   - Choose the Web ACL that you intend to associate with an AWS resource, in this case, an ALB.

3. **Add AWS resources:**
   - On the "Associated AWS resources" tab, select "Add AWS resources" to link your Web ACL with an ALB.

![Step 3](https://github.com/Flairminds/blogs/assets/91743769/8b1c1507-948c-44dc-8252-7da5d63db37a)

### Step 4: Select ALB as the Resource Type

1. **Choose the resource type (ALB):**
   - Specify ALB as the resource type and select the ALB you want to associate with the Web ACL.

2. **Confirm the association:**
   - Click "Add" to finalize the association between the Web ACL and the chosen ALB.

![Step 4](https://github.com/Flairminds/blogs/assets/91743769/80bcb8c4-13ef-42fe-a1e8-0b4b8b7c9766)

### Step 5: Configure Rules for the Web ACL

1. **Move to rule configuration:**
   - After associating the ALB, proceed to the next page to configure rules for the Web ACL.

2. **Choose rule criteria:**
   - Utilize AWS managed rules or create custom rules based on your security policies.

3. **Select the IP set:**
   - Specifically, select the previously created IP set to allow or disallow traffic from specific IP addresses.

4. **Define rules and priorities:**
   - Add rules and set their priority to align with your security requirements.

![Step 5a](https://github.com/Flairminds/blogs/assets/91743769/4c625a92-f273-4dd2-8c3a-de712e1377d8)
![Step 5b](https://github.com/Flairminds/blogs/assets/91743769/31db826b-2cf7-4ba0-b5cf-ad8ad3d9d44a)
![Step 5c](https://github.com/Flairminds/blogs/assets/91743769/e5f00231-739c-4b9c-a59f-e827193c2410)

### Step 6: Review and Create the Web ACL

1. **Review the configured settings:**
   - Verify the settings for the Web ACL, ensuring that rules and associations are as desired.

2. **Create Web ACL:**
   - Choose "Create Web ACL" to complete the process and apply the specified rules to the associated ALB.

![Step 6](https://github.com/Flairminds/blogs/assets/91743769/adf86e03-fa06-4c19-adfc-0c608a2b5ca4)

Now, your ALB is protected by the configured Web ACL, leveraging the IP set to control access based on specified rules. This comprehensive setup enhances the security of your web applications, allowing you to manage and filter incoming traffic effectively. Keep in mind that there may be a brief delay before changes take effect.

By following these steps, you fortify your AWS infrastructure against potential threats, demonstrating a proactive approach to securing your web applications with AWS WAF.