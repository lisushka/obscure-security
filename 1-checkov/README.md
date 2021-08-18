# Step 1: Scanning cluster CloudFormation files with Checkov

Now that we're in the process of spinning up our EKS cluster, let's use an infrastructure as code scanner to have a look at the CloudFormation templates that we're using.  [Checkov](https://www.checkov.io/) is an open-source security scanner for IaC files.  It's cloud-agnostic; CloudFormation, ARM templates, Terraform, Kubernetes, and Docker files can all be run through Checkov before deployment.

## Installing Checkov on Cloud9

NOTE: Checkov requires Python 3.7 or later to run.  If you're using it on your own machine, please check your version of Python before installing it.

```bash
pip3 install checkov
```
    
## Scanning CloudFormation files

Run the following command to scan the CloudFormation templates from Step 0:

```bash
checkov --directory obscure-security/0-templates
```

When the results come back, you'll see that there are two failures.  The first one is in our control plane file; we don't have Kubernetes secrets encrypted, which means that anyone with access to the cluster can go in and copy them.  The second one is on the node group, as a result of the template not encrypting the EBS volume where we store our launch configuration for the nodes.  The company that developed Checkov provides links to their documentation, which explain how to remediate the issue both in code (CloudFormation, Terraform, etc) and through the AWS control panel.  Go and have a look at this documentation, and try modifying the files in the `0-templates` folder to resolve the issue.  Then, run the scan again.

Next step: [Security benchmarking with `kube-bench`](../2-kube-bench/README.md)

[Back to home](../README.md)
