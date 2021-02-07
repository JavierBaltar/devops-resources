# devops-resources


<center>
<table>
  <tr>
    <td align="center"><a href="#ansible"><img src="images/ansible.png" width="75px;" height="75px;" alt="ansible"/><br /><b>Ansible</b></a></td>
    <td align="center"><a href="#docker"><img src="images/docker.png" width="70px;" height="75px;" alt="Docker"/><br /><b>Docker</b></a></td>
    <td align="center"><a href="#kubernetes"><img src="images/kubernetes.png" width="70px;" height="75px;" alt="Kubernetes" /><br /><b>Kubernetes</b></a></td>
    <td align="center"><a href="#jenkins"><img src="images/jenkins.png" width="85px;" height="85px;" alt="Jenkins"/><br /><b>Jenkins</b></a></td>
    <td align="center"><a href="#git"><img src="images/git.png" width="80px;" height="75px;" alt="Git"/><br /><b>Git</b></a></td>
    <td align="center"><a href="#AWS"><img src="images/aws.png" width="80x;" height="75px;" alt="AWS"/><br /><b>AWS</b></a></td>
    <td align="center"><a href="#linux"><img src="images/linux.png" width="75x;" height="75px;" alt="Linux"/><br /><b>Linux</b></a></td>
    <td align="center"><a href="#terraform"><img src="images/terraform.png" width="70px;" height="75px;" alt="Terraform"/><br /><b>Terraform</b></a></td>
    <td align="center"><a href="#python"><img src="images/python.png" width="70px;" height="75px;" alt="Python"/><br /><b>Python</b></a></td>
    <td align="center"><a href="#cicd"><img src="images/cicd.png" width="80px;" height="75px;" alt="CI/CD"/><br /><b>CI/CD</b></a></td>
  </tr>
</table>  
</center> 


## Ansible

<details>
<summary>Ansible</summary><br><b>


</b></details>

## Docker

<details>
<summary>Docker</summary><br><b>

Concepts

The Linux kernel has a number of features that allow a process to be isolated. Container engines such as Docker use two main kernel features to isolate processes: Cgroups and Namespaces. 
- Namespaces
- Cgroups

LXC

Libcontainer

Dockerfile

Each Dockerfile is a script, composed of various commands and arguments listed successively to automatically perform actions on a base image (or from scratch) in order to create a new one.

```bash
# Usage: ADD [source directory or URL] [destination directory]
ADD /my_app_folder /my_app_folder
```

Best practices for writing Dockerfiles [here](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)



</b></details>

## Kubernetes

<details>
<summary>Kubernetes</summary><br><b>

Kubernetes Basics

- Pod is a group of linked containers which shares a unique IP address. 
- Labels are key-value pairs attached to resources that contain information that helps to identify them. 
- ReplicaSet is a resource that templates the creation of pods. NOTE: ReplicaSet replaces the ReplicaController
- Deployment are used to gracefully roll out new versions of ReplicaSets.
- Services give a way of accessing services within our Kubernetes cluster. 

Kubernetes Components:

Architecture

API server

Controller manager

Scheduler

Kubelet

etcd


Basic Commands:

kubectl set image

kubectl get pods

kubectl delete pod XX

kubectl scale XX

Configuration as Code:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

service.yaml

EKS Cluster Setup

IAM

Helm

Planning for Production Deployments
</b></details>

<details>
<summary>EKS</summary><br><b>
</b></details>

## Jenkins

<details>
<summary>Jenkins</summary><br><b>
  


</b></details>

## Git

<details>
<summary>Git</summary><br><b>

Git rebase details [here](https://git-scm.com/docs/git-rebase)


</b></details>

## AWS

<details>
<summary>AWS</summary><br><b>


</b></details>

## Linux

<details>
<summary>Linux</summary><br><b>


</b></details>


## Terraform

<details>
<summary>Terraform</summary><br><b>


</b></details>

## Python

<details>
<summary>Python</summary><br><b>

For more info please read [here](https://www.google.com)

</b></details>

## CICD

<details>
<summary>CICD</summary><br><b>

For more info please read [here](https://www.google.com)

</b></details>
