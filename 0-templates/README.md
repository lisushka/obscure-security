# Step 0: Setting up the Kubernetes cluster

First of all, we need to spin up a Kubernetes cluster to run our test workloads on.  We'll do this using CloudFormation templates, which make the deployment process simple and repeatable.

## Creating an EC2 key pair

We need a key pair to be able to SSH onto our Kubernetes worker nodes in the event of any issues.  Go to the [EC2 Key Pairs page](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#KeyPairs), and click Create key pair.  The key pair type should be RSA, and the private key file format should be `.ppk`.  Save this key to your local machine.

## Spinning up the Kubernetes cluster

In order to spin up the Kubernetes cluster that we're going to use, we need to deploy two separate CloudFormation templates.  It is possible to deploy an EKS cluster in a single template, but for the purposes of this workshop, we're going to use a modified version of the samples from the [EKS User Guide](https://github.com/awsdocs/amazon-eks-user-guide).  [The first template](amazon-eks-control-plane.yaml) will create IAM roles and network infrastructure that the cluster need to run, as well as the EKS control plane.  [The second template](amazon-eks-nodegroup.yaml) will create three nodes, each one running on a separate instance, that we can use to deploy resources into the cluster.

Click the following links to deploy the EKS cluster into the `us-west-2` region of your account.  You'll need to wait for the control plane to create before you spin up the worker nodes.  For the worker nodes template, you'll need to get the name of the cluster's control plane from the [EKS console](https://us-west-2.console.aws.amazon.com/eks/home?region=us-west-2#/clusters).  The VPC name, security group name, and four subnets all begin with `obscure-security-control-plane`.  Use the key pair from the earlier step, and `--use-max-pods` for the bootstrap script.  Leave everything else as the default.

1. [Control Plane](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/quickcreate?templateUrl=https://obscure-security.s3.us-west-2.amazonaws.com/templates/amazon-eks-control-plane.yaml&stackName=obscure-security-control-plane)
2. [Worker Nodes](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/quickcreate?templateUrl=https://obscure-security.s3.us-west-2.amazonaws.com/templates/amazon-eks-nodegroup.yaml&stackName=obscure-security-node-group)

## Setting up a Cloud9 environment

It is highly recommended to provision a Cloud9 environment for this lab, as Cloud9 comes with most of the basic tools that we need already installed.  The predefined CloudFormation template [here](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/quickcreate?templateUrl=https://obscure-security.s3.us-west-2.amazonaws.com/templates/obscure-security-cloud9.yaml&stackName=obscure-security-cloud9) will launch a Cloud9 instance into a fresh VPC in the `us-west-2` region, which will allow you to easily spin the environment down at the end of the lab.  This will typically take about 5 minutes.

When the CloudFormation template has run, you should see two stacks in the `CREATE_COMPLETE` state.  One is called `obscure-security-cloud9`, and the other will have the name of the underlying EC2 instance running your IDE.  Go to the [Cloud9 management page](https://us-west-2.console.aws.amazon.com/cloud9/home?region=us-west-2#), and use the `Open IDE` button to launch the `workshop-cloud9-instance`.

## Connecting the control plane management role to Cloud9

In order for us to be able to control our Kubernetes cluster on the Cloud9 instance, we need to attach the IAM role that we used to create the control plane.  Open the [EC2 console], and select the `aws-cloud9-workshop-cloud9` instance.  Select it, and click `Actions` > `Security` > `Modify IAM role`.  Then, attach the `obscure-security-control-plane-EKSRole`.

## Checking out the workshop code

In the terminal window at the bottom of Cloud9, run the following command:

```bash
git clone git@github.com:lisushka/obscure-security
```

You should now see the files in this repository in the sidebar of your Cloud9 IDE.

Next step: [Infrastructure as Code scanning with Checkov](../1-checkov/README.md)

[Back to home](../README.md)
