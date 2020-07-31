---
layout: post
title: "Kubernetes: Deploying a PHP Pod"
description: Learn how to deploy a PHP application to a pod in Kubernetes
categories:
- kubernetes
- ops
- k8s
- php
tags:
- kubernetes
- ops
- k8s
- php
status: publish
type: post
published: true
mainimage: "kubernetes_php.jpeg"
image_url: ""
image_author: ""
---

In this tutorial you will learn how to deploy a PHP application to Kubernetes.
The goal is to have a PHP container running inside a POD and accessible from
outside the cluster.

Kubernetes has a couple gotchas that kinda make sense after you get used to it.
Ones does not simply "deploy a container to k8s" and can then access it from
outside. No, no. It is a bit more complicated than that. A container is "deployed"
inside a POD, a POD is then then exposed using a SERVICE and a SERVICE is finally
exposed to outside the cluster using an INGRESS.

This is what we will have in the end:

![External can access the pod via ingress and a service](/assets/images/kubernetes/pod_service_ingress.png)

The "PHP App" is only one script that shows the current time on the container
and the hostname, more information on the section **Building the image** below.

You can either build the docker image yourself or you can use the one I'm using
from [Dockerhub](https://hub.docker.com/r/infog/php-app-hostname).

## Building the docker image

You can skip this part and head to **Creating the Pod** if you do not want to
create the docker image. I do recommend creating the image, specially if you
are not so familiar with Docker.

In order to push the created image to the image registry you will need an account
on [Dockerhub](https://hub.docker.com/r/infog/php-app-hostname). So, go ahead and
create one.

Now create a directory on your computer, I named mine **php-app-pod**, you can
use the same name to make it easier to follow this tutorial. Inside this
directory you will need another directory named **app** containing a PHP file
named **index.php** with the following contents:

```php
<?php

echo sprintf(
    "Welcome to the app. Current time: %s. The app is running on %s",
    date('Y-m-d H:i:s'),
    gethostname()
);
```

As you can see it is only a bit of information printed by this script, but this
is enough to show us PHP is working. Later on it will also help us visualising
a **deployment** is working properly on Kubernetes, but this is a topic for the
next post on this series.

The Docker image will run Apache HTTP server and for that we need to set it up
to run PHP. Save the configuration bellow on a file named **host.conf** in the
**php-app-pod** directory:

```
<VirtualHost *:80>
    DocumentRoot /app

    <Directory "/app">
        AllowOverride all
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

And finally we need a file named **Dockerfile** with the following contents:

```
FROM php:apache

COPY host.conf /etc/apache2/sites-available/000-default.conf
COPY app /app

WORKDIR /app
```

The final structure should look like this:

```
├── app
│   └── index.php
├── Dockerfile
└── host.conf
```

Now you can build the image using Docker:

```
docker build -t php-app-hostname -f Dockerfile .
```

You can use any name you want for the tag but it will be easier to tag it
**php-app-hostname** to follow this tutorial.

After building the image you need to tag and push it to Dockerhub, be sure
to log in to Dockerhub before pushing the image. Also, please replace **infog**
with your username on Dockerhub.

```
docker tag php-app-hostname infog/php-app-hostname
docker login
docker push infog/php-app-hostname:latest
```

You can test the image running the following command:

```
docker run -p 8080:80 infog/php-app-hostname:latest
```

Again, replace **infog** with your username on Dockerhub. You should be able to
see the following output on your browser when you access **localhost:8080**:

```
Welcome to the app. Current time: 2020-04-21 07:21:59. The app is running on 5cb2ea2e779e
```

Now we are all se to create the Pod on Kubernetes.

## Creating the Pod

Now it is time to focus on Kubernetes. If you skipped building the image on
the section above you can use the same image I'm using, otherwise please replace
**infog** with your username on Dockerhub.

In this tutorial I'm assuming you already have **Minikube** (or other local or remote
Kubernetes cluster) and **kubectl**.

**Minikube** is a simple way to have a local Kubernetes cluster. Need help
installing it? I wrote a step by step that you can follow.

**kubectl** is the command line cliente for Kubernetes. I also wrote a step by step
to set it up.

As you can see on the image above a Pod is what will contain the running container.
We are creating all the needed objects starting from the inner layer, the image
to run the container, to the outer layer that will be Ingress.

A Pod is one of the smallest objects on Kubernetes. A pod will usually run
a container or more containers and will expose some kind of service, like
the Apache HTTP server for our PHP application.

Kubernetes has a declarative interface that lets us create workloads that will
create objects like Pods. It is possible to use both **yaml** and **json** to
declare new workloads. Personally I believe **json** is easier to read and follow
then **yaml** but the Kubernetes community decided to use **yaml**. Some may even
joke Kubernetes professionals are **yaml** developers ;-)

Anyway, I will use json for the examples on this post because I believe it is
more readable, I will show some yaml examples too.

Here is the json to declare a workload to create a pod using the image we created:

```json
{
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "php-app-pod",
    "labels": {
      "app": "php-app-pod"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "php-app-pod",
        "image": "infog/php-app-hostname:latest",
        "ports": [
          {
            "containerPort": 80,
            "name": "phpapppodport"
          }
        ]
      }
    ]
  }
}
```

It seems like a lot, but we can break it down to single lines to make it easier
to understand.

- **apiVersion** is Kubernetes' API version to be used. Some features are available
  only in the beta API, for example.
- **kind** is what the workload is about. In this case we want to create a Pod.
- **metadata** contains the name and a label to help identifying the Pod later.
- **spec** has the specification for what the object will run. There we declare
  a container pointing to that image on Dockerhub. We also declare the port the
  container is exposing, this will be used later.

Save the contents of the json above on a file names **pod.json**. You can save
this file anywhere on your computer, but I do recommend keeping it inside the
**php-app-pod** directory we are working on so far.

Now it is time to use **kubectl** to command Kubernetes to create the Pod. To
achieve this run the following command:

```
kubectl create -f pod.json
```

The output should be the following:

```
pod/php-app-pod created
```

You can even see the status of the Pod using the command **get pods**:

```
kubectl get pods
NAME          READY   STATUS              RESTARTS   AGE
php-app-pod   0/1     ContainerCreating   0          7s
```

After some point you should see the status as **Running**:

```
kubectl get pods
NAME          READY   STATUS    RESTARTS   AGE
php-app-pod   1/1     Running   0          1h
```

Nice, the pod is up and running. The next step is creating a Service to expose
this Pod.

## Creating the Service

The next layer we need to create is the Service. A service exposes a Pod and is
necessary to make it available.

A Service is necessary because Pods are not persistent and can be replaced at any
time when there is a problem. If a Pod misbehaves Kuberenetes will simply remove it
and create a new one (When using deployments, we will get the on the next post).
The Service will keep track of that and can even serve as a balancer to send
traffic to the Pods.

Just like the Pod, the Service is also created using a declarative interface.
This is the **json** used to create a service:

```json
{
  "apiVersion": "v1",
  "kind": "Service",
  "metadata": {
    "name": "php-app-pod-service"
  },
  "spec": {
    "type": "ClusterIP",
    "selector": {
      "app": "php-app-pod"
    },
    "ports": [{
      "protocol": "TCP",
      "port": 8085,
      "targetPort": "phpapppodport"
    }]
  }
}
```

Let's check what are the options all about:

- **kind** this workload will create a Service.
- **metadata** contains identification for the service.
- **spec.type** ClusterIP says this service will expose the Pod to other objects
  inside the cluster.
- **spec.selector** is used to target which Pods will be exposed by the service.
- **spec.ports** contains the port the service will expose (8085) and which port
  to target on the Pods. In this case we are using a named port defined on the Pod
  creation.

To create the service save the contents of the json above into a file named
**service.json** and run the following command:

```
ubectl create -f service.json
service/php-app-pod-service created
```

You can check the services using:

```
kubectl get services
NAME                  TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
kubernetes            ClusterIP   10.96.0.1        <none>        443/TCP    53d
php-app-pod-service   ClusterIP   10.106.139.165   <none>        8085/TCP   46m
```

And there is our service! It accepts connections on port **8085** on IP
**10.106.139.165**. This IP is internal to the cluster, so we still cannot
access the application from outside. This will be done on the next step using
**Ingress**.

## Creating the Ingress

Ingress is the object that will route the external traffic into the cluster. It
is also the outer layer on our chart!

Just like the Pod and the Service, creating an Ingress can be done using a json
or yaml file. Here is the example to create an Ingress object:

```json
{
  "apiVersion": "extensions/v1beta1",
  "kind": "Ingress",
  "metadata": {
    "name": "php-app-pod-ingress"
  },
  "spec": {
    "backend": {
      "serviceName": "default-http-backend",
      "servicePort": 80
    },
    "rules": [
      {
        "host": "php-app-pod.local",
        "http": {
          "paths": [
            {
              "path": "/",
              "backend": {
                "serviceName": "php-app-pod-service",
                "servicePort": 8085
              }
            }
          ]
        }
      }
    ]
  }
}
```

Explaining the lines:

- **apiVersion**: Ingress is still in beta, so we need to explicit that.
- **kind**: The object we want to create is an Ingress.
- **metadata**: Data to identify the Ingress.
- **spec.backend**: Ingress needs a backend service to run, this is the default one.

And inside **spec.rules**:

- **host**: The URL to be used as a domain name for the service.
- **http**: The this one means the **/** (root) endpoint will point to our service
  named **php-app-pod-service** on port 8085.

Save the json above in a file named **ingress.json** and run **kubectl** to create
the workload that will create the **ingress** object:

```
kubectl create -f ingress.json
ingress.extensions/php-app-pod-ingress created
```

Then you can check the ingress objects:

```
kubectl get ingresses
NAME                  CLASS    HOSTS               ADDRESS   PORTS   AGE
php-app-pod-ingress   <none>   php-app-pod.local             80      12s
```

We can now finally access the running application from outside the cluster! Ok,
but how? This is done using the cluster's IP and since we using **minikube** the
way to find out the IP is running the following command:

```
minikube ip
192.168.99.100
```

Now edit the hosts file **/etc/hosts** to add an entry for the domain used on
the Ingress setup:

```
# /etc/hosts
192.168.99.100  php-app-pod.local
```

Now access **php-app-pod.local** on your browser and you should see the text from
the running PHP application on the pod:

```
Welcome to the app. Current time: 2020-04-24 17:09:22. The app is running on php-app-pod
```

And there you have it: A PHP application deployed to a Kubernetes cluster.

## Let's recap

Kubernetes can be complicated to learn and understand, mainly to understand, but
when we break the parts into smaller parts and try to understand how everything
is linked together, we have a better chance. Next is a summary of what we did:

- A Docker Image is the center of everything. Make your application run inside
  Docker as the first step.
- A Pod will run the Docker image on a container.
- Since Pods are ephemeral we need Services to expose them inside the cluster.
- An Ingress will expose the Service outside the cluster and also serve as DNS

It seems like a lot of work only to have an application running and having no
real benefit over, let's say, a more traditional deployment on a private server
or a shared one.

This step is important to understand Kubernetes' concepts. On the next post I
will cover how to use a deployment to have several copies of the Pod and to even
scale the infrastructure up and down when needed, stay tuned.

InFog
