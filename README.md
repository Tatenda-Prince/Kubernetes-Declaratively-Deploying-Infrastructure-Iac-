# Kubernetes-Declaratively-Deploying-Infrastructure-Iac-
"Declaring the Kube"

![image alt](https://github.com/Tatenda-Prince/Kubernetes-Declaratively-Deploying-Infrastructure-Iac-/blob/a0634811090a8eb2acdda088c320645fa80bfe1b/images/Screenshot%202024-12-29%20153511.png)

# Intro

Let’s say you have multiple houses that you want to manage, each with their own set of unique features and requirements. It would be a difficult and time-consuming task to manage all of them manually, making sure that everything is running smoothly and making changes as needed.

This is where Kubernetes comes in. Kubernetes is like a property manager that helps you manage multiple houses at once. Just like a property manager oversees the maintenance and operations of multiple properties, Kubernetes helps you manage and orchestrate multiple Docker containers at scale.

In this example, Kubernetes would be like the property manager who oversees multiple houses. Each house would be a Docker container that contains all the necessary components to run the application. Kubernetes would help you manage and automate the deployment, scaling, and monitoring of all these containers, making sure that everything is running smoothly and efficiently.

So if one of the houses needs some maintenance work done, like fixing a leaky faucet. With Kubernetes, you can automatically spin up a new container with the fixed faucet, while the old container is taken down for maintenance.

This ensures that the application remains available and operational, even while maintenance work is being done.

Now let’s get into the more technical concepts of Kubernetes.

# Kubernetes Info

# Kubernetes

Kubernetes is an open-source container orchestration tool at heart. It helps automate managing and deploying containerized applications, making it easier for developers to build, deploy and manage their applications.

# Minikube

Minikube is very lightweight Kubernetes application that deploys a Kubernetes cluster on a virtual machine hosted on a local system. It supports all major operation systems (Mac, Windows and Linux).

# Pod
A Pod is the smallest deployable unit in Kubernetes and represents a single instance of a running process in a cluster. It can contain one or more containers that share the same network namespace and are deployed and managed together.

# Service

A Service provides a stable IP address and DNS name for a set of Pods and allows for the expose of these Pods to be accessed by other parts of the application or by external clients.

# Deployment

A Deployment manages a set of replicas of a Pod and allows you to declaratively define and manage the desired state of a group of Pods. It can also automatically create or delete replicas to match the desired state.

# ConfigMap

A ConfigMap stores configuration data as key-value pairs or as plain text files in a data volume. It allows you to separate configuration data from your application code and makes it easier to manage configuration changes without redeploying your application.


# Kubernetes Commands

# kubctl get

Kubectl get retrieves information about Kubernetes resources, such as Pods, Services, Deployments, ConfigMaps etc.

# kubctl apply

kubctl apply is used to apply configuration changes to Kubernetes resources. It takes a YAML or JSON file that defines the desired state of a resource and applies the changes to the cluster.

# Kubectl deploy

Kubectl deploy is used to deploy a new version of an application to a Kubernetes cluster. It creates a new Deployment resource with the desired number of replicas and updates the running Pods to match the new version of the application.

# Kubctl create

Kubectl create is used to create new Kubernetes resources, such as Pods, Services, Deployments, ConfigMaps, etc. It also takes a YAML or JSON file that defines the desired state of the resource and creates the resource in the cluster.

# Kubctl describe

Kubectl describe is used to display detailed information about a Kubernetes resource, such as the resource’s labels, annotations, events and status. It is also useful for troubleshooting and debugging issues with Kubernetes resources.

# Prerequisites

Basic knowledge and understanding of Containerization and Docker

Basic Linux command line knowledge

Basic knowledge and use of an Interactive Development Environment (IDE).

# Objectives

1. Deploy a sidercar container that watches  a remote Git Repo, and synch the changes to the share volume and the main app container will update the webpage.


# Step 0: Setup Kubernetes environment with miniKube

1.Run the following command to install miniKube —
brew install minikube

2.Now, run the command below to install Hyperkit, a hypervisor for Windows systems —

brew install hyperkitbrew install hyperkit

3.Finally, run the following command to start miniKube with hyperkit as the driver —

Minikube Start 

You should observe miniKube running through a series of steps to create the Kubernetes Cluster and node, as seen below.

![image alt](https://github.com/Tatenda-Prince/Kubernetes-Declaratively-Deploying-Infrastructure-Iac-/blob/36e953bd1e392ae99a97d18d84a18d5dbf04f530/images/Screenshot%202024-12-29%20155541.png)

Run the followings commands in succession to verify the a node and default ClusterIP service was created when deploying the Kubernetes cluster —

~ kubectl get all

~ kubectl get nodes

You will see similar results as shown below. One default Service of type “ClusterIP” and one “minikube” Node that is the master/control plane.

![image alt](https://github.com/Tatenda-Prince/Kubernetes-Declaratively-Deploying-Infrastructure-Iac-/blob/72a50ba0d4a0c286753a605a8483c5aecd1ec186/images/Screenshot%202024-12-29%20155626.png)

Now that we’ve set up our environment, let’s proceed to Step 1 — Creating the Kubernetes deployment files using YAML to leverage IaC.


# Step 1: Create Kubernetes deploying Multi-container Pod - sidecar container using a YAML manifest file.

Sidecar containers are regular containers that run at the same time as application
containers for the entire lifecycle of the Pod.

The job of a sidecar container is to add functionality to an app without having to
implement it in the actual app. Common examples include sidecars that scrape logs,
sync remote content, broker connections, and munge data. They’re also heavily used
by services meshes where the sidecar intercepts network traffic and provides traffic
encryption and telemetry.

As we proceed, use a preferred text editor in your local command line interface to create each YAML file.

Here I will use the nano text editor to create a Kubernetes Service resource YAML file by running the following command —

~ nano sidecarpod.yml

A text editor window should open. Copy and paste the code into the text editor.

![image alt](https://github.com/Tatenda-Prince/Kubernetes-Declaratively-Deploying-Infrastructure-Iac-/blob/37fb2a22ab1fb71f0937b67e73ef94ab6970cd4f/images/Screenshot%202024-12-29%20170039.png)


The main app container is called ctr-web. It’s based on an NGINX image and serves a
static web page loaded from the shared html volume.
The second container is called ctr-sync and is the sidecar. It watches a GitHub repo and
syncs changes into the same shared html volume.
When the contents of the GitHub repo change, the sidecar copies the updates to the
shared volume, where the app container notices and serves an updated version of the

web page.

We’ll walk through the following steps to see it in action:
1. Fork the GitHub repo
2. Update the YAML file with the URL of your forked repo
3. Deploy the app
4. Connect to the app and see it display This is version 1.0
5. Make a change to your fork of the GitHub repo
6. Verify your changes appear on the web page

 Go to GitHub and fork the following repo. You’ll need a GitHub account to do this.

 https://github.com/Tatenda-Prince/ps-sidecar
 
Come back to your local machine and edit the sidecarpod.yml. Change the GIT_SYNC_-
REPO value to match the URL of your forked repo, and save your changes.
Run the following command to deploy the application. It will deploy the Pod as well as a
Service you’ll use to connect to the app.

~ kubectl apply -f sidecarpod.yml

~ kubectl get all

~ kubecttl get service 

You should received similar outputs after running all the command as show below —


![image alt](https://github.com/Tatenda-Prince/Kubernetes-Declaratively-Deploying-Infrastructure-Iac-/blob/fd524081d6b97c337dbfc68c2ff6e461b72a7bf0/images/Screenshot%202024-12-29%20171933.png)


Check the status of the Pod with a kubectl get pods command.
As soon as the Pod enters the running state, run a kubectl get svc and copy the value
from the EXTERNAL-IP column. It might show as ‘ localhost ‘ if you’re running a Docker
Desktop cluster or another local option.
Paste the value into a new browser tab to see the web page. It will display This is
version 1.0.

![image alt](https://github.com/Tatenda-Prince/Kubernetes-Declaratively-Deploying-Infrastructure-Iac-/blob/3e7fee3857e21b16d25dbe2ce63261f57d896f6d/images/Screenshot%202024-12-29%20172055.png)


Be sure to complete the following step against your forked repo.Go to your forked repo and edit the index.html file. Change the H1 line to something
different and save your changes.Refresh the app’s web page to see your updates.


![image alt](https://github.com/Tatenda-Prince/Kubernetes-Declaratively-Deploying-Infrastructure-Iac-/blob/84082a9133392d6af96abf7e9cc9411ab9158d9b/images/Screenshot%202024-12-29%20172817.png)

Congratulations. The sidecar container successfully watched a remote Git repo, synced
the changes to a shared volume, and the main app container updated the web page.
Feel free to run the kubectl get pods and kubectl describe pod commands to see
how multi-container Pods appear in the outputs.

# Clean up

~ kubectl delete -f sidecarpod.yml 




























