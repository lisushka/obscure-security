# Step 3: Install SonarQube and scan a sample workload

Next, we're going to try installing SonarQube on the Kubernetes cluster itself, so that we can use it to scan all of our hypothetical organisation's code.  In order to do this, we're going to use a deployment management tool for Kubernetes called Helm.

## Install Helm 3 on Cloud9

1. Run the following commands to install Helm 3 in your Cloud9 IDE:
    ```bash
    sudo su
    curl -L https://mirror.openshift.com/pub/openshift-v4/clients/helm/latest/helm-linux-amd64 -o /usr/bin/helm
    chmod +x /usr/bin/helm
    exit
    ```
    
1. Verify that Helm installed correctly:
    ```bash
    helm version
    ```
    The installed version should be Helm `3.6.2`.

## Add public Helm chart for SonarQube to chart repository

```bash
helm repo add oteemocharts https://oteemo.github.io/charts
helm repo update
```

## Deploy SonarQube onto cluster

```bash
helm install oteemocharts/sonarqube
```

To check whether the helm installation worked, run `helm list` to get information about installed releases.

## Testing SonarQube on example code

If you want to test SonarQube on example code, then you'll need to set it up to be accessible outside of the cluster using an NGINX ingress.  The documentation on how to do so is [here](https://docs.sonarqube.org/latest/setup/sonarqube-on-kubernetes/); due to time constraints, we won't be setting this up as part of this lab.  I may run a second lab with instructions on how to do so.

Next step: [Runtime threat detection with Falco](../4-falco/README.md)

[Back to home](../README.md)
