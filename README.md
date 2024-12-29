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

kubectl get all

kubectl get nodes

You will see similar results as shown below. One default Service of type “ClusterIP” and one “minikube” Node that is the master/control plane.

![image alt]()

Now that we’ve set up our environment, let’s proceed to Step 1 — Creating the Kubernetes deployment files using YAML to leverage IaC.






