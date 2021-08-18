# Step 5: Cleanup

In the [CloudFormation UI](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks), spin down the stacks in the following order:

* `obscure-security-node-group`
* `obscure-security-control-plane`
* `obscure-security-cloud9`

The fourth stack, which is created by the Cloud9 deployment, will spin down when the Cloud9 stack is deleted.

[Back to home](../README.md)
