---
layout: post
title: Local Kubernetes cluster with Minikube
description: Follow this short tutorial to have Minikube running locally to start learning Kubernetes.
categories:
- kubernetes
- ops
- k8s
tags:
- kubernetes
- ops
- k8s
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

Kubernetes is the de facto tool for managing the deployment and managemente of
containerized applications.

The easiest approach to start lerning Kubernetes is to have it running on your
local computer, but this can be tricky, since Kubernetes requires a cluster of
servers to run on.

This is where [Minikube](https://github.com/kubernetes/minikube) can help!

Minikube sets up a virtual cluster on your local machine with little effort when
compared to setting up a cluster.

Minikube makes use of a Virtual Machine to setup a local Kubernetes cluster, in
this tutorial we will be using VirtualBox as the driver. KVM and Docker are also
available as possible drivers. Using Docker as driver is not really recommended
as it can result in some security issues for the host, your local machine.
