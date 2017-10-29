# kubernetes-node-microservices
A kubernetes example running node.js microservices with application gateway

To run kubernetes in aws
1 - install vm to separate your test to final server configurations
cd ~/work-link/dockers/devops-box/
git clone https://github.com/wardviaene/devops-box.git
vagrant up
vagrant ssh

export KOPS_STATE_STORE=s3://k8s-microservices
// or in all commands
// --state=s3://k8s-microservices

kops create cluster --name=k8smicroservice.tk --zones=us-east-1a --master-zones=us-east-1a --node-count=2 --node-size=t2.micro --master-size=t2.micro --dns-zone=k8smicroservice.tk


 * edit your node instance group: kops edit ig --name=k8smicroservice.tk nodes
additionalPolicies:
    node: |
      [
        {
          "Effect": "Allow",
          "Action": ["ec2:*"],
          "Resource": ["*"]
        },
        {
          "Effect": "Allow",
          "Action": ["elasticloadbalancing:*"],
          "Resource": ["*"]
        },
        {
          "Effect": "Allow",
          "Action": ["route53:*"],
          "Resource": ["*"]
        },
        {
          "Effect": "Allow",
          "Action": ["kms:*"],
          "Resource": ["*"]
        }
      ]

 * edit your master instance group: kops edit ig --name=k8smicroservice.tk master-us-east-1a
additionalPolicies:
    node: |
      [
        {
          "Effect": "Allow",
          "Action": ["ec2:*"],
          "Resource": ["*"]
        },
        {
          "Effect": "Allow",
          "Action": ["elasticloadbalancing:*"],
          "Resource": ["*"]
        },
        {
          "Effect": "Allow",
          "Action": ["route53:*"],
          "Resource": ["*"]
        },
        {
          "Effect": "Allow",
          "Action": ["kms:*"],
          "Resource": ["*"]
        }
      ]


kops update cluster k8smicroservice.tk --yes

kops delete cluster --name=k8smicroservice.tk

