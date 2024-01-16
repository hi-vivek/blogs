---
title: Creating an AWS WAF IP Set and Associating it with an ALB
date: 2024-01-11
authors: [amanw]
slug: Creating-an-AWS-WAF-IP-Set-and-Associating-it-with-an-ALB
description: >
  Guide to Creating an AWS WAF IP Set and Associating it with an ALB
categories:
  - DevOps
---
# Creating an AWS WAF IP Set and Associating it with an ALB

## Step 1: Create an IP Set

1. Sign in to the AWS Management Console.
2. Open the AWS WAF console.

![Screenshot 2024-01-10 195232](https://github.com/Flairminds/blogs/assets/91743769/52a0d11d-7123-4c30-a3a2-1c122f93c4b5)

## Step 2: Create IP Set with Allowed or Disallowed IPs

1. In the navigation pane, select "IP sets."
2. Choose "Create IP set."
3. Provide a name for the IP set and add the list of IP addresses that you want to allow or disallow.
4. Choose "Create IP set" to save the configuration.

![create-ip-set](https://github.com/Flairminds/blogs/assets/91743769/230face0-43db-4369-9513-6726763df8db)

## Step 3: Associate Web ACL with an AWS Resource (ALB)

1. In the AWS WAF console, navigate to "Web ACLs."
2. Choose the name of the Web ACL you want to associate with a resource.
3. On the "Associated AWS resources" tab, select "Add AWS resources."

![Screenshot 2024-01-10 195426](https://github.com/Flairminds/blogs/assets/91743769/8b1c1507-948c-44dc-8252-7da5d63db37a)


## Step 4: Select ALB as the Resource Type

1. Choose the resource type (ALB) and select the radio button next to the ALB you want to associate.
2. Click "Add" to confirm the association.

![Screenshot 2024-01-10 195836](https://github.com/Flairminds/blogs/assets/91743769/80bcb8c4-13ef-42fe-a1e8-0b4b8b7c9766)


## Step 5: Configure Rules for the Web ACL

1. After associating the ALB, move to the next page to configure rules.
2. You can use AWS managed rules or create your own rules.
3. In this case, select the previously created IP set to allow or disallow specific IPs.
4. Add rules and set their priority based on your requirements.

![Screenshot 2024-01-10 212929](https://github.com/Flairminds/blogs/assets/91743769/4c625a92-f273-4dd2-8c3a-de712e1377d8)
![Screenshot 2024-01-10 212938](https://github.com/Flairminds/blogs/assets/91743769/31db826b-2cf7-4ba0-b5cf-ad8ad3d9d44a)
![Screenshot 2024-01-10 213009](https://github.com/Flairminds/blogs/assets/91743769/e5f00231-739c-4b9c-a59f-e827193c2410)

## Step 6: Review and Create the Web ACL

1. Review the configured settings for the Web ACL.
2. Choose "Create Web ACL" to finalize the process.

![Screenshot 2024-01-10 213058](https://github.com/Flairminds/blogs/assets/91743769/adf86e03-fa06-4c19-adfc-0c608a2b5ca4)

Now, the Web ACL is associated with your ALB, and it includes rules based on the IP set you defined. This setup helps control access to your ALB by allowing or blocking specific IP addresses. Keep in mind that it may take a few moments for changes to take effect.
