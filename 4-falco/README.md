# Step 4: Install and configure Falco

The other tool that we're going to install directly on our cluster is a tool called Falco, which is used for runtime security.  What this means is that it will constantly scan our cluster for threats; both workloads that may be poorly set up or misconfigured, and also abnormal patterns of external access.

## Add public Falco Helm chart

```bash
helm repo add falcosecurity https://falcosecurity.github.io/charts
helm repo update
```

## Deploy Falco onto cluster

```bash
helm install falco falcosecurity/falco
```

## Using rules files and alert files to configure Falco

One of the advantages of using Falco for runtime security is that it's highly configurable.  We're going to create a rules file and an alert file in our repository to configure Falco, and then walk through the process of applying them.  The documentation for creating rule files is [here](https://falco.org/docs/rules/), and the documentation for alert files is [here](https://falco.org/docs/alerts/).

Next step: [Cleanup](../5-cleanup/README.md)

[Back to home](../README.md)
