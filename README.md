# Obscure Security on AWS EKS

Kubernetes is a container orchestration system that's very popular, and still increasing in use.  Security for Kubernetes isn't very intuitive if you don't come from a background of working with containerised workloads; in addition, as with any other specialised software, the control plane itself is very complex to secure.

In this workshop, we'll demonstrate four tools that can be used to secure your Kubernetes cluster and the workloads on it.  They cover three different areas: code scanning (both code and IaC), security benchmarking, and runtime threat detection.

**NOTE:** This lab has a small cost attached (US$1-2 an hour).  When you're done, follow the cleanup steps to ensure that you don't end up with cost overruns.

- [0: Set up EKS cluster](0-templates/README.md)
- [1: Infrastructure as Code scanning with Checkov](1-checkov/README.md)
- [2: Security benchmarking with `kube-bench`](2-kube-bench/README.md)
- [3: Code scanning with SonarQube](3-sonarqube/README.md)
- [4: Runtime threat detection with Falco](4-falco/README.md)
- [5: Cleanup](5-cleanup/README.md)
