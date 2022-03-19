# Installation

This is a brief guide for `up and running` a K8s cluster  using Minikube. This guide will go through 
- [x] installing Minikube and selecting appropriate driver
- [x] starting a multi-node cluster using Minikube
- [ ] point Docker daemon on host to minikube cluster

### PRE-FLIGHT CHECK 

- First thing to do is check if you have virtualization support enabled. To check run the below command. If it is enabled it should return a number greater than 0 (&ge; 1). In our case, We have to have virtualization support enabled because we will be running the nodes as vm inside our host.
```console
$ lscpu | egrep -c 'vmx|svm'
```

- Have libvirt installed. <!--  On this guide, we won't on how to install livirt. Maybe in the future we can link to a guide that shows how to install libvirt -->


### STEP 1: MiniKube install

Head over to [Minikube's website](https://minikube.sigs.k8s.io/docs/start/) and download the binary that matches your operating system and architecture.

### STEP 2: Start MiniKube

Go over to Minikube's [driver's page](https://minikube.sigs.k8s.io/docs/drivers/) and find out the appropriate driver for your OS and use case. For this guide, I assume you are running Linux and going to be using KVM. 

Hence, the driver is going to be `kvm2`. You can set the default driver using the following command 

```console
$ minikube config set driver kvm2
```

To start (init) run the following command.
```console
$ minikube start --nodes=3 -p multi-node-demo --driver=kvm2
```
<!-- Explain what each command does -->
<!-- TODO: Explain the size of vm's -->
<!-- TODO: You might encounter problem where libvirt won't allow you to create vm through minikube -->

<!-- Make the new profile the default one -->
I recommend you switch over to the new profile we created so that you won't  have to specify the profile every time you start your minikube cluster.
```console
$ minikube profile multi-node-demo
```

### STEP 3: Setting kubectl

<!-- configure kubectl, and enable tab-completion -->
```text
alias kubectl="minikube kubectl --"
```

<!-- Is it better to install kubectl binary? I think it gives object completion -->
### (optional step) Point your docker daemon 



Hope you enjoyed the guide!