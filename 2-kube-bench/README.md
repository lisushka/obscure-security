# Step 2: Install `kube-bench` and run security benchmarks

By now, your EKS nodes should be up and running.  We're going to use a utility called `kube-bench` to scan the cluster itself for any configuration errors that might present a security issue.  `kube-bench` runs as a job on our Kubernetes cluster, and its results are in the logs of the pod that runs it.

## Installing `kubectl`

1. Download the `kubectl` binary for Kubernetes 1.20:
    ```bash
    sudo su
    curl https://amazon-eks.s3.us-west-2.amazonaws.com/1.20.4/2021-04-12/bin/linux/amd64/kubectl -o /usr/bin/kubectl
    chmod +x /usr/bin/kubectl
    exit
    ```

1. Verify the installation:
    ```bash
    kubectl version --short --client
    ```
    
## Connecting to the Kubernetes cluster

Update your `kubeconfig` file using the command below:

```bash
aws eks --region us-west-2 update-kubeconfig --name obscure-security-eks-cluster
```

## Checking out `kube-bench`

In the terminal window at the bottom of Cloud9, run the following command:

```bash
git clone https://github.com/aquasecurity/kube-bench
```

## Running the `kube-bench` job on the cluster

1. Apply the job file to the cluster:
    ```bash
    kubectl apply -f job-eks.yaml
    ```
    
1. Wait for the pod to finish running:
    ```bash
    kubectl get pods
    ```
    
1. Once the job pod has finished running, get the job logs:
    ```bash
    kubectl get logs <pod-name>
    ```
    
    The pod name will appear in the output of `kubectl get pods`.

Next step: [Code scanning with SonarQube](../3-sonarqube/README.md)

[Back to home](../README.md)
