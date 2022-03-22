- [Installation](#installation)
    - [PRE-FLIGHT CHECK](#pre-flight-check)
    - [STEP 1: MiniKube install](#step-1-minikube-install)
    - [STEP 2: Start MiniKube](#step-2-start-minikube)
    - [STEP 3: Setting kubectl](#step-3-setting-kubectl)
    - [(optional step) Point your docker daemon](#optional-step-point-your-docker-daemon)
  
# Installation

This is a brief guide for `up and running` a K8s cluster  using Minikube. This guide will go through 
- [x] installing Minikube and selecting appropriate driver
- [x] starting a multi-node cluster using Minikube
- [x] point Docker daemon on host to minikube cluster

### PRE-FLIGHT CHECK 

- First thing to do is check if you have virtualization support enabled. To check if you have virtualization enabled run the below command. If it is enabled it should return a number greater than 0 (&ge; 1). In our case, we have to have virtualization support enabled because we will be running the nodes as vm inside our host.
```console
$ lscpu | egrep -c 'vmx|svm'
```

- Have libvirt installed(if you are running Linux). <!--  On this guide, we won't on how to install livirt. Maybe in the future we can link to a guide that shows how to install libvirt -->


### STEP 1: MiniKube install

Head over to [Minikube's website](https://minikube.sigs.k8s.io/docs/start/) and download the binary that matches your operating system and architecture.

### STEP 2: Start MiniKube

Go over to Minikube's [driver's page](https://minikube.sigs.k8s.io/docs/drivers/) and look up the appropriate driver for your OS and use case. For this guide, I assume you are running Linux and going to be using KVM. 

Hence, the driver is going to be `kvm2`. You can set the default driver using the following command 

```console
minikube config set driver kvm2
```

To start (init) run the following command.
```console
minikube start --nodes=3 -p multi-node-demo --driver=kvm2
```
The above command will start a 3 node cluster. 1 control plane node and 2 worker nodes. We are calling our cluster `multi-node-demo`.

<!-- TODO: Explain the size of vm's -->
<!-- TODO: You might encounter problem where libvirt won't allow you to create vm through minikube -->

<!-- Make the new profile the default one -->
I recommend you switch over to the new profile we created so that you won't  have to specify the profile every time you start your minikube cluster.
```console
minikube profile multi-node-demo
```

### STEP 3: Setting kubectl

You can use `minikube kubectl --` command to administer your cluster but I prefer installing the `kubectl` binary allows object tab completion. Follow the [guide](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) to install kubectl.

To enable bash-completion you need to have the package `bash-completion` installed on your system(obviously!)
```console
kubectl completion bash | sudo tee /etc/bash_completion.d/kubectl > /dev/null
```

<!-- Is it better to install kubectl binary? I think it gives object completion -->
### (optional step) Point your docker daemon 

> This part assumes you have docker installed on your host machine.

To make your development seamless you can have docker point to your Minikube cluster. This makes building images easier by allowing you to directly push to the local registry on the your cluster.

```console
eval $(minikube docker-env)
```
Note: This command must be re-run in a new terminal. 

[Read more](https://minikube.sigs.k8s.io/docs/handbook/pushing/)


Hope you enjoyed the guide!