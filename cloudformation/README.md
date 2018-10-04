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

$ aws cloudformation create-stack --stack-name ExampleEKS --parameters file://./parentparameters.json --template-body file://./parent.yaml

- At the end of this process you will have a running EKS Cluster and you can apply the configmap to authorize the Worker Node IAM Role
