Example CloudFormation Nested Stack Architecture for Elastic Kubernetes Service

Requirements:

S3 Bucket for Storage of Nested Stacks
- place the following template files into an S3 Bucket you have access to:

1. vpc.yaml
2. ekscluster.yaml			
3. workernodeinstanceprofile.yaml
4. workernodesecuritygroup.yaml
5. nodegroup.yaml

- create a new CloudFormation Stack using parent.yaml
- you *must* create the parent stack using the IAM Credentials you want to access the APIServer Endpoint with!
- set parameters as desired

$ aws cloudformation create-stack --stack-name ExampleEKS --parameters file://./parentparameters.json --template-body file://./parent.yaml --capabilities CAPABILITY_IAM


Example Parent Stack Parameters

```json

[
  {
    "ParameterValue": "192.168.32.0/19",
    "ParameterKey": "Subnet01Block"
  },
  {
    "ParameterValue": "1.10",
    "ParameterKey": "ClusterVersion"
  },
  {
    "ParameterValue": "MyNodeGroup",
    "ParameterKey": "NodeGroupName"
  },
  {
    "ParameterValue": "192.168.128.0/19",
    "ParameterKey": "Subnet04Block"
  },
  {
    "ParameterValue": "192.168.0.0/16",
    "ParameterKey": "VpcBlock"
  },
  {
    "ParameterValue": "1",
    "ParameterKey": "NodeAutoScalingGroupMinSize"
  },
  {
    "ParameterValue": "t2.medium",
    "ParameterKey": "NodeInstanceType"
  },
  {
    "ParameterValue": "192.168.64.0/19",
    "ParameterKey": "Subnet02Block"
  },
  {
    "ParameterValue": "3",
    "ParameterKey": "NodeAutoScalingGroupMaxSize"
  },
  {
    "ParameterValue": "my-ssh-keypair-name",
    "ParameterKey": "KeyName"
  },
  {
    "ParameterValue": "ami-0a54c984b9f908c81",
    "ParameterKey": "NodeImageId"
  },
  {
    "ParameterValue": "arn:aws:iam::123456789012:role/EKS-Service-Role",
    "ParameterKey": "ServiceRole"
  },
  {
    "ParameterValue": "192.168.160.0/19",
    "ParameterKey": "Subnet05Block"
  },
  {
    "ParameterValue": "20",
    "ParameterKey": "NodeVolumeSize"
  },
  {
    "ParameterValue": "192.168.96.0/19",
    "ParameterKey": "Subnet03Block"
  },
  {
    "ParameterValue": "ExampleCluster",
    "ParameterKey": "ClusterName"
  },
  {
    "ParameterValue": "",
    "ParameterKey": "BootstrapArguments"
  },
  {
    "ParameterValue": "myBucket",
    "ParameterKey": "S3BucketName"
  },
  {
    "ParameterValue": "192.168.192.0/19",
    "ParameterKey": "Subnet06Block"
  }
]

```


- At the end of this process you will have a running EKS Cluster and you can apply the configmap to authorize the Worker Node IAM Role
