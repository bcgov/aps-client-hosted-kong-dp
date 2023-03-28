# Client Hosted Kong Data Plane

## AWS

Reference: https://github.com/terraform-aws-modules/terraform-aws-eks

Identity:

- create a new user and add an Access key under "Security credentials"

Authorization:

- user must have "AmazonEKSClusterPolicy" and "AmazonEC2FullAccess", "IAMFullAccess", "CloudWatchLogsFullAccess", "AWSKeyManagementServicePowerUser".. plus eks:TagResource but couldn't find a Policy so found a custom policy to use.
- https://aws-ia.github.io/terraform-aws-eks-blueprints/main/iam/minimum-iam-policy/
- Policy: "EKS-custom"

```
aws sts get-caller-identity
aws configure

cd terraform/workspaces/aws
rm -rf .terraform .terraform.lock.hcl
terraform init
terraform apply

aws eks update-kubeconfig --region us-west-1 --name ex-aws

kubectl get services

```

To analyze the resources, you can use `Rover`:

Installation: https://github.com/im2nguyen/rover#installation

```
./rover_0.3.2_darwin_arm64/rover_v0.3.2
```

### AWS Billing

| Resource                                 | Cost                            | Cost 24/30  | Actual |
| ---------------------------------------- | ------------------------------- | ----------- | ------ |
| Elastic Load Balancing                   | USD $0.0252 / hour + Gb         | 22.42 / mth | $2.83  |
| Elastic Compute Cloud                    | USD $0.107 / hour + Nat Hr + Gb | 70.08 / mth | $2.22  |
| Elastic Container Service for Kubernetes |                                 | 73.00 / mth | $0.17  |
| CloudWatch                               | $0                              |             | $0     |
| Data Transfer                            | $0                              |             | $0     |
| Key Management Service                   | $0                              |             | $0     |
| Lambda                                   | $0                              |             | $0     |

- - 24 hours \* 30 days

### AWS Troubleshooting

```
2023/02/28 22:20:12 [crit] 1110#0: *288 [lua] targets.lua:248: could not
 reschedule DNS resolver timer: process exiting, context: ngx.timer
```

## Azure

Try using: https://github.com/Azure/terraform-azurerm-aks

### Azure Billing

| Resource      | Cost | Cost 24/30 | Actual |
| ------------- | ---- | ---------- | ------ |
| Data Transfer | $0   |            | $0     |

## GCP

```
gcloud config list
```

| Resource          | Cost  | Cost 24/30 | Actual |
| ----------------- | ----- | ---------- | ------ |
| Compute Engine    | $2.48 |            | $0     |
| Kubernetes Engine | $2.63 |            | $0     |
| Cloud Storage     | $0.01 |            | $0     |
| Networking        | $0.40 |            | $0     |
| Cloud Logging     | $0    |            | $0     |
| Cloud Functions   | $0    |            | $0     |
