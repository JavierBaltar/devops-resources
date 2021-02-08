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
    <td align="center"><a href="#cicd"><img src="images/cicd.png" width="80px;" height="70px;" alt="CI/CD"/><br /><b>CI/CD</b></a></td>
    <td align="center"><a href="#APM"><img src="images/apm.gif" width="90px;" height="65px;" alt="APM"/><br /><b>APM</b></a></td>
  </tr>
</table>  
</center> 


## Ansible

<details>
<summary>Ansible</summary><br><b>
  
- Inventory

The Ansible inventory file defines the hosts and groups of hosts upon which commands, modules, and tasks in a playbook operate. The file can be in one of many formats depending on your Ansible environment and plugins. 

The default location for the inventory file is /etc/ansible/hosts. If necessary, you can also create project-specific inventory files in alternate locations.

The inventory file can list individual hosts or user-defined groups of hosts. For example, if you are managing one or more data centers, you can create Ansible groups for those components that require the same set of operations.


- YAML

YAML stands for "YAML Ain't Markup Language" (Please refer to: https://yaml.org ). 
it is basically a human-readable structured data format. It is less complex and ungainly than XML or JSON, but provides similar capabilities.
There are some rules that YAML has in place to avoid issues related to ambiguity. 

These rules make it possible for a single YAML file to be interpreted consistently, regardless of which library is being used to interpret it.

YAML files should end in .yaml.
YAML is case sensitive.
YAML uses a fixed indentation scheme to represent relationships between data layers.
Dictionary keys are represented in YAML as strings terminated by a trailing colon. Values are represented by either a string following the colon, separated by a space.
To represent lists of items, a single dash followed by a space is used. Multiple items are a part of the same list as a function of their having the same level of indentation.

The following example represents a YAML playbook:
```yaml
- name: configure interface settings
  ios_config:
    lines:
      - description test interface
      - ip address 172.31.1.1 255.255.255.0
    parents: interface Ethernet1

- name: configure ip helpers on multiple interfaces
  ios_config:
    lines:
      - ip helper-address 172.26.1.10
      - ip helper-address 172.26.3.8
    parents: "{{ item }}"
  with_items:
    - interface Ethernet1
    - interface Ethernet2
    - interface GigabitEthernet1

- name: load new acl into device
  ios_config:
    lines:
      - 10 permit ip host 1.1.1.1 any log
      - 20 permit ip host 2.2.2.2 any log
      - 30 permit ip host 3.3.3.3 any log
      - 40 permit ip host 4.4.4.4 any log
      - 50 permit ip host 5.5.5.5 any log
    parents: ip access-list extended test
    before: no ip access-list extended test
    match: exact

- name: check the running-config against master config
  ios_config:
    diff_against: intended
    intended_config: "{{ lookup('file', 'master.cfg') }}"

- name: check the startup-config against the running-config
  ios_config:
    diff_against: startup
    diff_ignore_lines:
      - ntp clock .*

- name: save running to startup when modified
  ios_config:
    save_when: modified
    
```

- Configuration File

Certain settings in Ansible are adjustable via a configuration file (ansible.cfg). The stock configuration should be sufficient for most users, but there may be reasons you would want to change them.
Configuration file which will be processed in the following order:
Environment variable: ANSIBLE_CONFIG
Actual directory "ansible.cfg" file.
Home directory "ansible.cfg" file.
Configuration file stored in "/etc/ansible/ansible.cfg".

| Option | Default Value | Description |
| --- | ----------- | -------- |
| inventory | /etc/ansible/hosts | Inventory location |
| forks | 5 | Specify number of parallel processes to use |
| remote_port | 22 | Remote SSH port |
| host_key_checking | true | Check host key installed |

| timeout | 10 | SSH connection timeout in seconds |
| remote_user | root | Remote connection user |
| become | false | Run operations with become (does not imply password prompting) |
| become_method | sudo | Privilege escalation method to use |
| pipelining | false | Reduces the number of network operations required to execute a module on the remote server, by executing many Ansible modules without actual file transfer.This can result in a very significant performance improvement when enabled |

Please refer to Ansible documentation for more details: https://docs.ansible.com/ansible/latest/reference_appendices/config.html

- Playbooks
Playbooks are Ansible’s configuration, deployment, and orchestration language. Playbooks are designed to be human-readable and are developed in a basic text language. There are multiple ways to organize playbooks and the files they include.

- Modules
Ansible ships with a number of modules (called the ‘module library’) that can be executed directly on remote hosts or through playbooks. Users can also write their own modules. These modules can control system resources, like services, packages, or files , or handle executing system commands.
Ansible modules: https://docs.ansible.com/ansible/latest/modules/list_of_all_modules.html 


The following command displays the list of available modules:
ansible-doc -l | more


Narrow down modules related to ASA devices:
ansible-doc -l | more | grep asa


Show actions that a module can perform:
ansible-doc -s module_name

- Commands







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

- FROM

FROM directive is probably the most crucial amongst all others for Dockerfiles. It defines the base image to use to start the build process. It can be any image, including the ones you have created previously. If a FROM image is not found on the host, Docker will try to find it (and download) from the Docker Hub or other container repository. It needs to be the first command declared inside a Dockerfile.


```bash
# Usage: FROM [image name]
FROM ubuntu
```

- ADD

The ADD command gets two arguments: a source and a destination. It basically copies the files from the source on the host into the container’s own filesystem at the set destination. If, however, the source is a URL (e.g. http://github.com/user/file/), then the contents of the URL are downloaded and placed at the destination.


```bash
# Usage: ADD [source directory or URL] [destination directory]
ADD /my_app_folder /my_app_folder
```
- CMD

The command CMD, similarly to RUN, can be used for executing a specific command. However, unlike RUN it is not executed during build, but when a container is instantiated using the image being built. Therefore, it should be considered as an initial, default command that gets executed (i.e. run) with the creation of containers based on the image.

To clarify: an example for CMD would be running an application upon creation of a container which is already installed using RUN (e.g. RUN apt-get install …) inside the image. This default application execution command that is set with CMD becomes the default and replaces any command which is passed during the creation.


```bash
# Usage 1: CMD application "argument", "argument", ..
CMD "echo" "Hello docker!"
```

- ENTRYPOINT

ENTRYPOINT argument sets the concrete default application that is used every time a container is created using the image. For example, if you have installed a specific application inside an image and you will use this image to only run that application, you can state it with ENTRYPOINT and whenever a container is created from that image, your application will be the target.

If you couple ENTRYPOINT with CMD, you can remove “application” from CMD and just leave “arguments” which will be passed to the ENTRYPOINT.

```bash
# Usage: ENTRYPOINT application "argument", "argument", ..
# Remember: arguments are optional. They can be provided by CMD
#           or during the creation of a container.
ENTRYPOINT echo

# Usage example with CMD:
# Arguments set with CMD can be overridden during *run*
CMD "Hello docker!"
ENTRYPOINT echo
```

- ENV

The ENV command is used to set the environment variables (one or more). These variables consist of “key value” pairs which can be accessed within the container by scripts and applications alike. This functionality of Docker offers an enormous amount of flexibility for running programs.
```bash
# Usage: ENV key value
ENV SERVER_WORKS 4
```

- EXPOSE

The EXPOSE command is used to associate a specified port to enable networking between the running process inside the container and the outside world (i.e. the host).

```bash
# Usage: EXPOSE [port]
# Usage: EXPOSE [port]
EXPOSE 8080
```

- MAINTAINER

One of the commands that can be set anywhere in the file - although it would be better if it was declared on top - is MAINTAINER. This non-executing command declares the author, hence setting the author field of the images. It should come nonetheless after FROM.


```bash 
# Usage: MAINTAINER [name]
MAINTAINER authors_name
```

- RUN

The RUN command is the central executing directive for Dockerfiles. It takes a command as its argument and runs it to form the image. Unlike CMD, it actually is used to build the image (forming another layer on top of the previous one which is committed).



```bash
# Usage: RUN [command]
RUN aptitude install -y riak
``` 

- USER

The USER directive is used to set the UID (or username) which is to run the container based on the image being built.

```bash
# Usage: USER [UID]
USER 751
``` 

- VOLUME

The VOLUME command is used to enable access from your container to a directory on the host machine (i.e. mounting it).


```bash
# Usage: VOLUME ["/dir_1", "/dir_2" ..]
VOLUME ["/my_files"]
``` 

- WORKDIR

The WORKDIR directive is used to set where the command defined with CMD is to be executed.

```bash
# Usage: WORKDIR /path
WORKDIR ~/
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

1. Listing resources

```bash
kubectl get nodes
kubectl get pods
kubectl get services, deployments
```

2. Deleting resources

```bash
kubectl delete namespaces my-namespace

#Force deletion of a pod
kubectl delete pod my-pod --grace-period=0 --force

#Delete all pods in a namespace
kubectl delete pods --all --namespace my-namespace
```

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

<details>
<summary>GKE</summary><br><b>

Create a cluster
```bash
gcloud container clusters create mycluster
```

</b></details>

## Jenkins

<details>
<summary>Jenkins Cluster Installation AWS EC2</summary><br><b>
</b></details>

<details>
<summary>Jenkins</summary><br><b>
  
Jenkinsfile to compile and test across two different nodes.

```groovy
pipeline {
  agent none
  environment {
      JUNIT_REPORTS_FOLDER = "**/target/surefire-reports/*.xml" /* set junit reports folder variable */
  }
  options {
      skipDefaultCheckout true /* skips the default repository checkout for testing the 'stash/unstash' feature behaviour */
  }
  stages {
      stage('Checkout code by slave-01') {
          agent {
              label 'slave-01' /* this stage executor and workspace is allocated in slave-01 node */
          }  
          steps {
            checkout scm /* checkout source repository */
            stash includes: '**', name: 'repository_code' /* stores code to be handed over to slave-02 */
          }
      }
      stage('Maven compile by slave-01') {
          agent {
              label 'slave-01' /* this stage executor and workspace is allocated in slave-01 node */
          }
          steps {
              echo "-----------------------------------------------------------------------------------------------------------------"
              echo "Maven Compile by Slave 01 "
              echo "-----------------------------------------------------------------------------------------------------------------"
              sh 'mvn compile' /* compile source code */
          }
          post {
              always {
                  deleteDir() /* workspace clean up */
              }
          }
      }  
      stage('Maven testing by slave-02') {
          agent {
              label 'slave-02' /* this stage executor and workspace is allocated in slave-02 node */
          }
          steps {
              echo "-----------------------------------------------------------------------------------------------------------------"
              echo "Maven Application Testing by Slave 02"
              echo "-----------------------------------------------------------------------------------------------------------------"
              unstash 'repository_code' /* retrieves code stored by slave-01 */
              sh 'mvn test' /* test the compiled source code using unit testing framework */
          }
      }
      stage('Publish testing reports by slave-02') {
          agent {
              label 'slave-02' /* this stage executor and workspace is allocated in slave-02 node */
          }
          steps {
              echo "-----------------------------------------------------------------------------------------------------------------"
              echo "Publish Testing Reports by Slave 02"
              echo "-----------------------------------------------------------------------------------------------------------------"
          }
          post {
              always {
                  junit "${JUNIT_REPORTS_FOLDER}" /* publish unit testing reports */
                  deleteDir() /* workspace clean up */
              }
          }
      }
   }
}
```
  


</b></details>

## Git

<details>
<summary>Git</summary><br><b>
  
Git is a distributed Version Control system. It can track changes to a file and allows you to revert back to any particular change.
Its distributed architecture provides many advantages over other Version Control Systems (VCS) like SVN one major advantage is that it does not rely on a central server to store all the versions of a project’s files. Instead, every developer “clones” a copy of a repository I have shown in the diagram below with “Local repository” and has the full history of the project on his hard drive so that when there is a server outage, all you need for recovery is one of your teammate’s local Git repository.
There is a central cloud repository as well where developers can commit changes and share it with other teammates as you can see in the diagram where all collaborators are commiting changes “Remote repository”.
  
Branching strategies

- Feature branching: 
A feature branch model keeps all of the changes for a particular feature inside of a branch. When the feature is fully tested and validated by automated tests, the branch is then merged into master.

- Task branching:
In this model each task is implemented on its own branch with the task key included in the branch name. It is easy to see which code implements which task, just look for the task key in the branch name.

- Release branching:
Once the develop branch has acquired enough features for a release, you can clone that branch to form a Release branch. Creating this branch starts the next release cycle, so no new features can be added after this point, only bug fixes, documentation generation, and other release-oriented tasks should go in this branch. Once it is ready to ship, the release gets merged into master and tagged with a version number. In addition, it should be merged back into develop branch, which may have progressed since the release was initiated.

Revert a commit

```bash
#Remove or fix the bad file in a new commit and push it to the remote repository
git commit -m “commit message”
```

```bash
#Create a new commit that undoes all changes that were made in the commit to be reverted
git revert <name of commit to be reverted>
```

Squash commits

There are two options to squash last N commits into a single commit.

```bash
#If you want to write the new commit message from scratch use the following command
git reset –soft HEAD~N &&
git commit
```
```bash
#If you want to start editing the new commit message with a concatenation of the existing commit messages then you need to extract those messages and pass them to Git commit for that I will use
git reset –soft HEAD~N &&
git commit –edit -m”$(git log –format=%B –reverse .HEAD@{N})”
```

Git rebase

Rebase is a command which will merge another branch into the branch where you are currently working, and move all of the local commits that are ahead of the rebased branch to the top of the history on that branch. For example, if a feature branch was created from master, and since then the master branch has received new commits, Git rebase can be used to move the feature branch to the tip of master.

The command effectively will replay the changes made in the feature branch at the tip of master, allowing conflicts to be resolved in the process. When done with care, this will allow the feature branch to be merged into master with relative ease and sometimes as a simple fast-forward operation.

Git rebase details [here](https://git-scm.com/docs/git-rebase)


</b></details>

## AWS

<details>
<summary>AWS</summary><br><b>
  
AWS DevOps Blog [here](https://aws.amazon.com/blogs/devops/)

</b></details>

<details>
<summary>EC2</summary><br><b>
</b></details>

<details>
<summary>CloudFormation</summary><br><b>
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

Python online IDE [here](https://repl.it/languages/python3)

</b></details>

## CICD

<details>
<summary>CICD</summary><br><b>
  
The Software Development Life Cycle (SDLC) model covers the following phases:

1. Planning
2. Implementation
3. Testing
4. Documentation
5. Deployment and maintenance
6. Maintaining

  
Some of the advantages are:

- Speed of deployment
- Faster testing and analysis
- Smaller code changes
- Better and faster fault isolation
- Increased code coverage
- Automatic deploy to production
- Never ship broken code
- Process is repeatable
- Faster mean time to resolution
- Smaller backlog
- Improved customer satisfaction
- Tons of open source tools available

The disadvantages of CI/CD are:

- New skill sets must be learned
- Big upfront investment
- Legacy systems rarely support CI/CD
- High degree of discipline and dedication to quality

For more info please read [here](https://www.google.com)

</b></details>

## APM

<details>
<summary>Elastic Stack</summary><br><b>

For more info please read [here](https://www.google.com)
</b></details>
<summary>Grafana</summary><br><b>

</b></details>
