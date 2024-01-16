---
title: Creating Index Snapshots in Amazon OpenSearch Service
date: 2024-01-11
authors: [amanw]
slug: Creating-Index-Snapshots-in-Amazon-OpenSearch-Service
description: >
  Guide to Creating Index Snapshots in Amazon OpenSearch Service
categories:
  - DevOps
---
# Document: Creating Index Snapshots in Amazon OpenSearch Service

## Overview

Snapshots in Amazon OpenSearch Service are essential backups of a cluster's indexes and state. This includes cluster settings, node information, index settings, and shard allocation. Snapshots come in two forms: Automated and Manual.

### Automated Snapshots

Automated snapshots are solely for cluster recovery and are stored in a preconfigured Amazon S3 bucket at no extra cost. They are crucial for restoring a domain in cases of red cluster status or data loss. The frequency of automated snapshots varies based on the OpenSearch or Elasticsearch version running on the domain.

- **For OpenSearch or Elasticsearch 5.3 and later:**
  - Automated snapshots are taken hourly and retained for up to 336 snapshots for 14 days.
  
- **For Elasticsearch 5.1 and earlier:**
  - Daily automated snapshots are taken during a specified hour, with retention of up to 14 snapshots, and no snapshot data retained for more than 30 days.

### Manual Snapshots

Manual snapshots serve for both cluster recovery and data migration between clusters. Users initiate manual snapshots, and these are stored in their own Amazon S3 bucket, subject to standard S3 charges. They can also be used to migrate from a self-managed OpenSearch cluster to an OpenSearch Service domain.

## Snapshot Management

### Prerequisites

Before creating manual snapshots, ensure the following prerequisites are met:

- **S3 Bucket:**
  - Create an S3 bucket to store manual snapshots for your OpenSearch Service domain.

- **IAM Role:**
  - Create an IAM role (referred to as TheSnapshotRole) with necessary policies for OpenSearch Service access.

- **Permissions:**
  - Attach specific policies to TheSnapshotRole allowing access to the S3 bucket and IAM permissions.

### IAM Role
Create an IAM role to delegate permissions to OpenSearch Service. Follow the instructions in the IAM User Guide. This document refers to this role as TheSnapshotRole.

Attach IAM Policy to TheSnapshotRole
Attach the following policy to **TheSnapshotRole** to grant access to the S3 bucket:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": [
        "s3:ListBucket"
      ],
      "Effect": "Allow",
      "Resource": [
        "arn:aws:s3:::s3-bucket-name"
      ]
    },
    {
      "Action": [
        "s3:GetObject",
        "s3:PutObject",
        "s3:DeleteObject"
      ],
      "Effect": "Allow",
      "Resource": [
        "arn:aws:s3:::s3-bucket-name/*"
      ]
    }
  ]
}
```
#### Edit Trust Relationship
Edit the trust relationship of **TheSnapshotRole** to specify OpenSearch Service in the Principal statement. 

Here's an example:

```json 
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "",
      "Effect": "Allow",
      "Principal": {
        "Service": "es.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```
### Permissions
To register the snapshot repository, you need the ability to pass **TheSnapshotRole** to OpenSearch Service and access to the **es:ESHttpPut** action. Attach the following policy to the IAM role whose credentials are used to sign the request:
 ```json
 {
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "iam:PassRole",
      "Resource": "arn:aws:iam::123456789012:role/TheSnapshotRole"
    },
    {
      "Effect": "Allow",
      "Action": "es:ESHttpPut",
      "Resource": "arn:aws:es:region:123456789012:domain/domain-name/*"
    }
  ]
}
```


### Registering a Manual Snapshot Repository

**Map the snapshot role in OpenSearch Dashboards (if using fine-grained access control):**
   - Navigate to OpenSearch Dashboards plugin for your domain, choose Security, Roles, and select the manage_snapshots role. Map the role ARN that has permissions to pass TheSnapshotRole.

#### 1. Access the OpenSearch domain.
![Screenshot 2024-01-15 122411](https://github.com/Flairminds/blogs/assets/91743769/3c15450e-4765-4ec0-add7-f518d7c70964)

#### 2. Navigate to the Security tab to manage access controls.
![Screenshot 2024-01-15 122430](https://github.com/Flairminds/blogs/assets/91743769/c96bab91-ad63-490e-8ebb-b4bf215fafff)


#### 3. Go to the Roles section, focusing on the "snapshot_management" role.
![Screenshot 2024-01-15 122504](https://github.com/Flairminds/blogs/assets/91743769/04ad1916-a30a-4a84-8fee-ced89ad043ec)


#### 4. Map a user to this role to grant necessary permissions.
![Screenshot 2024-01-15 122519](https://github.com/Flairminds/blogs/assets/91743769/ebbc507c-0df5-47d0-b350-c0e10fb2844e)


#### 5. Add the Amazon Resource Name (ARN) of the user responsible for registering the snapshot repository.
![Screenshot 2024-01-15 122709](https://github.com/Flairminds/blogs/assets/91743769/d5bb52f8-9b70-4fb2-9bc6-46de82325084)

### Using the Sample Python Client

- A Python client is provided for easier automation. Update variables in the sample code and use it to register a snapshot repository.

```python
import boto3
import requests
from requests_aws4auth import AWS4Auth

host = '' # domain endpoint
region = '' # e.g. us-west-1
service = 'es'
credentials = boto3.Session().get_credentials()
awsauth = AWS4Auth(credentials.access_key, credentials.secret_key, region, service, session_token=credentials.token)

# Register repository

path = '/_snapshot/my-snapshot-repo-name' # the OpenSearch API endpoint
url = host + path

payload = {
  "type": "s3",
  "settings": {
    "bucket": "s3-bucket-name",
    "region": "us-west-1",
    "role_arn": "arn:aws:iam::123456789012:role/snapshot-role"
  }
}

headers = {"Content-Type": "application/json"}

r = requests.put(url, auth=awsauth, json=payload, headers=headers)

print(r.status_code)
print(r.text)
