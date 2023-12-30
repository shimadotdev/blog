+++
title = 'Docker Guide for Beginners: What is Docker?'
description = 'In recent years, we have frequently heard the name “Docker.” The following article is a simple and easy guide to familiarize beginners with Docker and its basic concepts, along with exercises. Join us on this journey.'
date = 2018-05-04
tags= ["Docker For Beginners", "Containerization", "DevOps"]
draft = false
+++

In recent years, we have frequently heard the name "Docker." The following article is a simple and easy guide to familiarize beginners with Docker and its basic concepts, along with exercises. Join us on this journey.

*I would like to remind you that this series consists of three posts, and two other articles titled "Docker Guide for Beginners: Key Terms in Docker" and "Docker Guide for Beginners: Defining Dockerfile, Building Images, and Running Containers" are also available.*

**What is Docker?**

According to Docker itself, Docker is a tool for building, shipping, and running applications easily. One of the key concepts in Docker is the container. Containers use virtualization at the operating system level to isolate resources. Containers and virtual machines operate similarly, but containers isolate resources at the operating system level, while virtual machines do so at the hardware level, leading to differences in performance and behavior. We will try to better understand the concept of containers by comparing these two tools.

**Differences Between Virtual Machines and Containers**

Virtual machines, with the help of a hypervisor, abstract one server into multiple servers. The hypervisor is a software, middleware, or hardware monitor for virtual machines, placed directly on the host machine's hardware, distributing resources like RAM and CPU among virtual machines.

These virtual machines are referred to as guest machines. A guest machine includes the application and everything needed to run it, from system management to necessary libraries and the entire hardware stack, including CPU, RAM, etc., virtually allocated to it. Virtual machines each have their own separate operating system, with libraries and applications placed on top.

Now, containers. Like virtual machines, containers have their own isolated space for processing, including libraries, allocated resources such as CPU, RAM, and network. However, containers differ in that they share the host machine's operating system kernel, which enhances their performance.

Containers require less space compared to virtual machines, allowing them to divide available resources among a greater number of applications.

Below are images from the Docker website to help us better understand.

- ![Virtual Machine Configuration](/images/container-vm-whatcontainer_2-1.png)
- ![Docker and Container Configuration](/images/docker-containerized-appliction-blue-border_2.png)

**Why Use Docker?**

a. Docker has made the process easy for everyone by providing tools and clients to build applications quickly and easily on personal computers. This allows anyone to run their applications rapidly without the need for modifications on cloud servers or elsewhere.

b. As mentioned earlier, Docker's high speed and lightweight nature make it a suitable option for work due to sharing the operating system kernel, allocating fewer resources while creating a separate and isolated space.

c. On the other hand, Docker's extensive community (Docker Hub), ready-made images, and the layered structure of these images - which we will explain later - make container creation and development easier.

d. Additionally, with the ability to create separate containers for software components (breaking down the application into various modules: Redis, MySQL, etc.) and the ease of communication between these components, Docker enables their independent development in the future.

*In the next post titled "Docker Guide for Beginners: Key Terms in Docker," we will become familiar with concepts and keywords used in Docker.*

