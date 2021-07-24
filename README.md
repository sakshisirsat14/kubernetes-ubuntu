# Install Kubernetes on AWS Ubuntu
Deploy a Kubernetes Cluster under 5 mins!

## Architecture
![architecture diagram](docs/kubernetes_aws.png)

## Resources Created by this Template
- Worker Node EC2 [WrokerNode]
- Master Node EC2 [MasterNode]
- Master Security Group [KuberentesSGMasterNode]
- Worker Secuirty Group [KuberentesSGWorkerNode]

## Flow
1. EventBridge Rule is triggered daily at 2AM EST, invoking the <NAME_OF_LAMBDA>_tableUpdater functions
2. The Lambda functions retrieve credentials from Secrets Manager

## File Tree Structure
```bash
.
├── README.md
├── docs
│   ├── Kubernetes - AWS.pdf
│   └── Kubernetes_aws.png
├── install_components.sh
├── kube_init.sh
├── kubernetes_dashboard.sh
├── parameters.txt
└── template.yaml

1 directory, 8 files
```

## Management
All resources are built and tested using [AWS CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html) and stored in [Github](https://github.com/Naz513/kubernetes-ubuntu).

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
