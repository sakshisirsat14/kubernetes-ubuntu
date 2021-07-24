# Install Kubernetes on AWS Ubuntu
Deploy a Kubernetes Cluster under 5 mins!

## Architecture
![architecture diagram](docs/architecture.png)

## Functions & S3 Created by this Template
- Lambda Function: [v_concurrent_user_tableUpdater](lambdas/v_concurrent_user_tableUpdater)

## Flow
1. EventBridge Rule is triggered daily at 2AM EST, invoking the <NAME_OF_LAMBDA>_tableUpdater functions
2. The Lambda functions retrieve credentials from Secrets Manager

## File Tree Structure
```bash

```

## Management
All resources are built and tested using [AWS Serverless Application Framework (SAM)](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/what-is-sam.html), deployed using [AWS CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html) and monitored with [Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html).

## How to use?
### Pre-requisites
- AWS CLI installed and configured
- AWS SAM installed

### Commands
Build a serverless application and prepare if for cloudformation
```bash
sam build
```

cd kubernetes-ubuntu/

ls -ltr

./install_components.sh

./kube_init.sh

kubeadm join 172.31.0.157:6443 --token adeboj.npvnuqd7jitrzt4w \
        --discovery-token-ca-cert-hash sha256:bef75b43c6a50b53e621ea3ba55a19a189392117935743db6d2f4f0b35adb427

cd kubernetes-ubuntu/

ls -ltr

./install_components.sh

sudo kubeadm join 172.31.0.157:6443 --token adeboj.npvnuqd7jitrzt4w \
        --discovery-token-ca-cert-hash sha256:bef75b43c6a50b53e621ea3ba55a19a189392117935743db6d2f4f0b35adb427

watch kubectl get nodes

./kubernetes_dashboard.sh

kubectl get pods -n kubernetes-dashboard

copy the token from 4/5 Get the Token step

kubectl get svc -n kubernetes-dashboard

Copy the Port for kube-dash before /TCP

Enter the Node Ip along with the kube-dash port

Once you see a screen, enter the Toke that we just took from previous step
