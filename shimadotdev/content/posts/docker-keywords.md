+++
title = 'Docker Guide for Beginners: Keywords in Docker'
description = "This article offers a beginner-friendly guide to Docker, covering core concepts such as the Docker Engine, Dockerfile, images, and containers. It explains the roles of volumes and the Union File System in Docker's architecture."
date = 2018-08-21
tags = ["Docker For Beginners", "UnionFS", "Dockerfile"]
draft = false
+++

## Docker Engine

The Docker Engine is the layer on which Docker runs, and its task is to manage containers, images, building, etc. This layer sits right above the host machine's operating system and performs its tasks by receiving commands from the client (for example, the terminal).

## Dockerfile

A Dockerfile is where the necessary instructions for building an image are written. If you take a look at existing Dockerfiles, you will see sample commands like `RUN apt-get install something`; these commands allow us to install necessary packages for running software in an isolated container environment, assign ports, or define directories.

### Sample Dockerfile:
```dockerfile
#This is a sample Image 
FROM ubuntu 
MAINTAINER nina@dobrev.com

RUN apt-get update 
RUN apt-get install –y nginx 
CMD [“echo”,”Image created”] 
```

## Image

Images are read-only templates created through the commands written in the Dockerfile.

## Container

Containers are created using images. A container provides an isolated space containing everything an application needs to run, from the operating system to system libraries and application code. By creating a container, Docker establishes an interface for networking so that the container can communicate with the local host, assign an IP, and so on.

For a better understanding of the relationship between image and container, you can think of it in terms of object-oriented programming. If an image is considered a class, then a container is an object instantiated from this class. Hundreds of containers can be created from a single image.

## Volume

A volume can be thought of as a virtual disk. This part of the container stores and shares container data (between the container and the host or between multiple containers). We have two main types of volumes:

a. Persistent: Data is naturally stored in the host machine's file system. So, in case of destruction, updates, and rebuilding of the container, this part of the data remains untouched.

b. Ephemeral: In this type, data in the container created is shared with other containers and exists as long as the containers use it. However, as soon as the containers are gone, that part of the data is also gone.

## Union File System

The most interesting part related to Docker is the use of the Union File System. Before anything, it's necessary to understand what the Union File System is. In [UnionFS](https://en.wikipedia.org/wiki/UnionFS), directories and files, grouped from separate file systems in branches, allow them to create a unified file system by stacking them on top of each other.

![The Structure of the Union File System in Docker](/images/overlay_constructs.jpg)
*The Structure of the Union File System in Docker*

Docker uses this feature to structure the layers of images (each instruction in an image forms a layer that is added on top of the underlying layers). Therefore, when a specific layer needs modification in an image, a copy of the layer is created, and the modifications are made on it, not the original layer. In the end, all these layers are stacked on top of each other for the container to use.

It's worth knowing that this process is referred to as [Copy On Write (COW)].

With this feature, when creating a new container from another image, there is no need to copy all the files again. Instead, it will have a pointer to the original location, so container initialization operations are performed quickly and at minimal cost.

On the other hand, when you change an image, Docker only updates the specific changed layer, making its operation faster.

In the next post, which is likely the last post in this series, we will focus on "Defining a Dockerfile, Building an Image, and Launching a Container" in a practical exercise.
