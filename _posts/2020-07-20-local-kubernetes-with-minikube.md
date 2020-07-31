---
layout: post
title: Local Kubernetes cluster with Minikube
description: Follow this short tutorial to have Minikube running locally to start learning Kubernetes.
categories:
- kubernetes
- ops
- k8s
- minikube
tags:
- kubernetes
- ops
- k8s
- minikube
status: publish
type: post
published: true
mainimage: "kubernetes.jpeg"
image_url: ""
image_author: ""
---

If you are using Docker for local development it is natural to move to the next
step and also have it in production, but it surely is a total different situation
having local containers for development and a production enviroment with containerized
applications.

Kubernetes is the de facto tool for managing the deployment and management of
containerized applications.

The easiest approach to start learning Kubernetes is to have it running on your
local computer, but this can be tricky, since Kubernetes requires a cluster of
servers to run on.

This is where [Minikube](https://github.com/kubernetes/minikube) can help!

Minikube sets up a virtual cluster on your local machine with little effort when
compared to setting up a cluster.

Minikube makes use of a Virtual Machine to setup a local Kubernetes cluster, in
this tutorial we will be using VirtualBox as the driver. KVM and Docker are also
available as possible drivers. Using Docker as driver is not really recommended
as it can result in some security issues for the host, your local machine.

This guide covers Minikube installation on a Debian based GNU/Linux distro, like
Ubuntu, for example.

## Installing VirtualBox

The first thing we need is [VirtuaBox](https://www.virtualbox.org/). Install it
using **apt-get**, **aptitude** or the Software application on the desktop.

To install using **apt-get** run the following command as root (Or using **sudo**):

```
apt-get install virtualbox
```

Then you need to add your user to the **vboxusers** group. This is necessary to
give your user permission to create virtual machines using VirtualBox. In order
to do so run the following command as root (Or using **sudo**):

```
adduser USER vboxusers
```

Replace **USER** with your username.

Now you have to login in again so the group change will be valid. You can simply
logout of your session or even restart your computer (Restarting is not necessary,
only logging out and in again from your current session).

After logging back in it is time to install Minikube.

## Installing Minikube

The easiest way to install Minikube is downloading
[the latest release](https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64).

This can be done using your Browser or a **curl** command:

```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```

Now you need to give execution permission to the downloaded file, so it can be
used as a command:

```
chmod -x minikube
```

I personally prefer moving this file to a system available directory that is
already on the PATH (possible directories where to find commands):

```
mv minikube /usr/local/bin/
```

This should be done as root or with sudo.

And it is done! You have the Minikube command installed.

Another way to install it is using a package for your distribution. To do so
head to [the releases page](https://github.com/kubernetes/minikube/releases) and
find the suitable one, like [minikube_1.9.2-0_amd64.deb](https://github.com/kubernetes/minikube/releases/download/v1.9.2/minikube_1.9.2-0_amd64.deb).

Download it and install using **dpkg**:

```
pkg -i minikube_1.9.2-0_amd64.deb
```

## Starting the cluster

Now you can start the local cluster using Minikube's command. Run **minikube start**
and you should see the output like the following:

```
minikube start
🙄  minikube v1.9.2 on Ubuntu 19.10
✨  Using the virtualbox driver based on existing profile
👍  Starting control plane node m01 in cluster minikube
🏃  Updating the running virtualbox "minikube" VM ...
🐳  Preparing Kubernetes v1.18.0 on Docker 18.09.8 ...
🌟  Enabling addons: default-storageclass, storage-provisioner
🏄  Done! kubectl is now configured to use "minikube"
```

This is the output for an already setup local cluster. On the first run Minikube
will create a new Virtual Machine on VirtualBox named minikube, so it will take
a bit longer.

To verify that Minikube is running you can run the dashboard:

```
minikube dashboard
🔌  Enabling dashboard ...
🤔  Verifying dashboard health ...
🚀  Launching proxy ...
🤔  Verifying proxy health ...
🎉  Opening http://127.0.0.1:34977/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/ in your default browser...
```

Use **ctrl+c** to stop the dashboard.

To stop minikube use **minikube stop**:

```
minikube stop
✋  Stopping "minikube" in virtualbox ...
🛑  Node "m01" stopped.
```

And that is it. You now have Minikube running a local Kubernetes cluster.
Next step is to install **kubectl**, the Kubernetes command line client to interact
with the cluster.

InFog
