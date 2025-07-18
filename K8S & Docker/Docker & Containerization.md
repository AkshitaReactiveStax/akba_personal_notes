
## Containers v/s VMs
## This article covers:

- [What is a container?](https://circleci.com/blog/containers-vs-virtual-machines/#what-is-a-container)
- [What is a VM?](https://circleci.com/blog/containers-vs-virtual-machines/#what-is-a-vm)
- [Containers vs VMs: Which should you use?](https://circleci.com/blog/containers-vs-virtual-machines/#containers-vs-vms-which-should-you-use)
- [Using containers and VMs in CI/CD pipelines](https://circleci.com/blog/containers-vs-virtual-machines/#using-containers-and-vms-in-cicd-pipelines)

Containers and virtual machines (VMs) are two approaches to [virtualization](https://circleci.com/blog/top-6-benefits-of-virtualization/), or the creation of virtual — as opposed to a physical — versions of computer hardware platforms, storage devices, and network resources.

While containers are isolated processes designed to run a single service or application, VMs emulate entire operating systems, offering a more comprehensive environment for running multiple applications and managing complex workloads.

Developers often use VMs and containers in combination, particularly in [CI/CD pipelines](https://circleci.com/blog/what-is-a-ci-cd-pipeline/). Containers provide portability and consistency across different CI/CD stages, while VMs offer deeper isolation and the ability to replicate complex environments. This hybrid approach allows teams to optimize resource utilization, maintain security, and ensure that applications perform reliably in a variety of scenarios.

In this article, you will learn key differences between containers and VMs, including when you should use each and how to incorporate them into your development pipelines.

## What is a container?

A container is a lightweight, self-contained unit that runs one or more processes, keeping them separate from other programs on the same computer. It uses the system’s shared kernel (the part of the operating system [OS] that controls resources and operations) to create this isolation.

Containers operate similarly to regular applications on the host OS, but with restricted access to hardware. While the host OS interacts directly with hardware, containers use virtualized resources. This allows them to run independently while ensuring isolation and portability.

There are two types of containers: application containers and system containers. System containers are much less common now, but were popular before [Docker](https://circleci.com/topics/docker/) made application containers commonplace in 2015. When discussing containers, people most often mean application containers.

Containers are [built from read-only templates called images](https://circleci.com/blog/docker-image-vs-container/) that are pulled from a central repository to run on a host machine.

Typically, containers run on Linux systems within separate [namespaces](https://en.wikipedia.org/wiki/Linux_namespaces), ensuring they don’t directly interact with other processes. Communication between containers and other processes happens through a software interface. Containers on other operating systems follow a similar structure.

### Uses of containers

Containers are useful because they are highly portable. Most common container engines run in multiple environments and are lightweight in resource use. Containers package all the dependencies they need, so they run consistently no matter what compatible system you implement them on. That means that once you build an application from one or multiple containers, you can run it on many different systems.

This portability is particularly valuable for large organizations that need to deploy identical software across multiple machines or networks. Containers can also run multiple instances of the same task simultaneously or divide a larger application into smaller, independent [microservices](https://circleci.com/blog/microservices-architecture/).

Beyond deployment, containers are commonly used to create temporary environments for development, testing, and CI/CD pipelines. These ephemeral environments can be quickly spun up and torn down, providing a clean, isolated setup for automated testing, building applications, and performing security checks. This allows developers to test changes in an environment that closely mirrors production without the hassle of managing long-term infrastructure.

### Container tools

Containers require an engine to run, and several tools make managing containers easier. [Docker](https://circleci.com/topics/docker/), the most popular container orchestration system, uses a daemon to create and manage containers.

Other container systems like Buildah and Kaniko offer daemon-less architecture. Daemon-less architecture doesn’t need root access for full functionality, which may offer greater security. However, these tools alone cannot run or manage containers. Developers may prefer tools like Docker and Podman because they let users build images and run and configure containers.

## What is a VM?

Like a container, a VM is a software-based environment used for virtualization. Unlike containers, which share the host system’s operating system, VMs are built on a software layer called a hypervisor. The hypervisor allows each VM to run its own separate operating system, enabling multiple VMs to operate independently on the same physical server.

Because each VM runs its own complete and separate operating system, VMs have a higher level of isolation and are more versatile than containers. They can handle a wider range of tasks, including running applications, services, or even multiple processes at once, as if they were a standalone physical computer.

While both VMs and containers allow multiple instances to run on the same server, VMs require more resources because each instance includes its own OS. Containers, on the other hand, share the host system’s kernel, making them lighter and faster to spin up, but with slightly less isolation.

### Uses of VMs

Because VMs create a complete computing environment, you can use them for a wider set of use cases. You can install new software on them and change their code down to the OS level. You can even snapshot the VM in a given state to roll it back to that configuration should there be issues later. Like containers, VMs are separate from other software on the same piece of hardware, making them perfect environments for [software testing](https://circleci.com/topics/software-testing/).

VMs allocate resources below the level of a guest OS, which limits the effect a malicious application can have. Malicious code that compromises one VM is unlikely to affect the host OS or access the machine’s firmware. That keeps other VMs running on the same machine safe. And, because your VM can use a different OS than its host device, you can use VMs to test software in different environments.

### VM tools

There are many tools available to build and manage VMs. The most essential are hypervisors, which govern access to the underlying hardware resources (like CPU, memory, and storage) for one or more VMs. There are two types of hypervisors:

- **Type 1 hypervisors** (also known as ***bare-metal hypervisors**) run directly on the physical hardware without an underlying operating system. Examples include VMware ESXi, Microsoft Hyper-V, and Xen. These are typically used in enterprise data centers and cloud environments because they offer high performance and efficiency.
    
- **Type 2 hypervisors** (also called **hosted hypervisors**) run on top of an existing operating system. Examples include Oracle VirtualBox and VMware Workstation. These are more commonly used on personal computers or in smaller environments for development and testing.
    

Other tools help users create and manage many VMs simultaneously. For example, cloud platforms like Amazon Web Services (AWS), Microsoft Azure, and Google Cloud offer services that allow developers to quickly spin up and manage large fleets of VMs with ease. Some developers use pre-configured VMs to ensure they are set up correctly and have all the basic programs they need.

## Containers vs VMs: Which should you use?

VMs and containers are both powerful technologies with specific use cases. Both provide isolated environments to run processes securely, but they differ in their strengths and purposes.

### When to use containers

A containerized application has more direct access to hardware than an application running in a VM. This access makes containers well-suited for lightweight use cases.

Suppose you want to run a single process in multiple separate instances, or run many different processes in isolation from each other. In that case, it makes sense to go with containers. Their small resource footprints make them easy to start up quickly and run at scale.

You can securely examine a container image to know what it will do before creating and running the container itself. That transparency makes containers easy to scan for security flaws, but it comes at a price. You must [scan shared containers for vulnerabilities](https://circleci.com/blog/adding-application-and-image-scanning-to-your-cicd-pipeline/) to avoid replicating those vulnerabilities in the systems where they are used.

It is also easy to update every instance of a containerized application. To do so, you make an updated version of the container image and create new containers from that updated image. Then you can delete out-of-date and less secure containers without affecting other processes. You can even automate the update process and rely on the container’s fast start-up time to make sure updates happen quickly every time.

Containers can make some complex tasks simpler. For example, you can [build a CI/CD pipeline with a Docker image](https://circleci.com/blog/build-cicd-piplines-using-docker/) and a CircleCI config file. The pipeline allows you to quickly test an image and then push it to Docker Hub or another container registry. That lets you move quickly through the CI/CD pipeline from building to deployment.

Containers also facilitate the use of [microservices](https://circleci.com/blog/soa-vs-microservices/). Microservices split larger applications into bite-sized processes, giving greater flexibility to users and securely separating those processes. You would need to spin up a separate VM for every microservice, which is an inefficient allocation of resources. Containers run multiple services on the same VM, which doesn’t have the benefit of isolation.

### When to use VMs

Despite their popularity, containers have not replaced VMs completely. In many cases, containers complement the use of VMs. In fact, VMs offer key advantages in certain scenarios. For example, VMs are ideal when you need to run multiple services on different operating systems while sharing the same hardware.

Since each VM has its own complete operating system, they also provide better isolation and security, making them less vulnerable to potential attacks. If malicious code compromises a container, it could affect the entire system, but with VMs, such risks are isolated to the specific virtual machine.

VMs are also more flexible for performing system-level tasks. For instance, making OS-level changes, such as modifying the system kernel with a `sysctl` command, is straightforward in a VM. In contrast, doing the same within a container requires elevated privileges, which could weaken the container’s security benefits.

For tasks that require complete OS control or more robust isolation, VMs remain a reliable choice, especially in environments where security and system-level access are critical.

## Using containers and VMs in CI/CD pipelines

A major benefit of using VMs and containers in CI/CD pipelines is the standardization of environments. This allows multiple developers to contribute code to a project without encountering environment-related issues. Both VMs and containers ensure consistency, which minimizes errors due to configuration differences.

You can also run containers inside VMs to leverage the benefits of both: containers ensure consistency across environments, while VMs provide control over resources below the OS level. Cloning build environments in this way lets you increase the amount of [automation](https://circleci.com/blog/automation-drives-devops/) in your pipelines, reducing the number of error-prone manual steps in your development process.

Containers are particularly useful in CI/CD automation because they make it easy to move and deploy code between machines. You can build a piece of code as a container image and deploy it as a readable file to a repository or hub. Companies like [Dollar Shave Club](https://circleci.com/case-studies/dollar-shave-club/) integrate containers in CI/CD to automate their testing and deployment pipeline for maximum efficiency.

CI/CD and containers also work well for [vulnerability management](https://circleci.com/blog/how-to-do-vulnerability-management-with-docker-and-ci-cd/). For example, you can use containers as part of an automated, ongoing process of frequent and incremental patch testing. That can be more efficient than releasing extensive updates with less well-understood effects on all parts of your system. Managing vulnerabilities becomes fast, smooth, and distributable among team members.

VMs and containers contribute to a CI/CD pipeline differently. One way they can work together is by using a VM as a machine executor to run more demanding containers. People already using a Docker executor may need to [migrate from Docker to a VM-based machine executor](https://circleci.com/docs/docker-to-machine). The machine executor’s more isolated environment and greater access to system resources can make this a worthwhile effort.

## Conclusion

Containers and virtual machines are essential tools for virtualizing your applications, each offering unique strengths based on your needs. Rather than choosing one or the other, you can use both to create a more flexible, efficient, and secure infrastructure.

By combining the security of virtual machines and the efficiency of containers, you can take advantage of all the benefits of virtualization. Using VMs to secure your applications and containers to move and deploy code between different machines combines the strength of both of their technologies.




# Docker image vs container: What are the differences?


If you are new to [Docker](https://circleci.com/topics/docker/), you may wonder how a Docker image differs from a Docker container. Although Docker images and containers have a similar purpose (to package and deploy software efficiently), they have different uses.

An **image** is a snapshot of an environment, while a **container** runs the software.

Think of a container as a shipping container for software — it holds important content like files and programs so that an application can be delivered efficiently from producer to consumer. An image is more like a read-only manifest or schematic of what will be inside the container. Docker uses images to create containers and containers to run the applications.

This article will explore the differences between Docker images and containers, to help you understand how and when to use each.

## Docker overview

One of the biggest [benefits of containerization](https://circleci.com/blog/benefits-of-containerization/) is that it helps developers to package their apps with all dependencies needed to run on any Linux distribution. Tools like Docker, Flatpak, and Snaps all have the same goal of making it easier to build, manage, and distribute containerized software.

Docker is similar to virtual machines in the way it creates multiple instances of an operating system. However, Docker lets you create containers that run on the _same_ operating system. So, more containers than virtual machines can run on a given hardware combination. Multiple containers can run simultaneously, each based on the same or different images.

Docker containers can even run within virtual machines. Docker provides an additional layer of abstraction and automation versus creating a virtual machine, making it easier to use. You can learn more about containers and virtual machines in [Containers vs virtual machines (VMs): What is the difference?](https://circleci.com/blog/containers-vs-virtual-machines/)

Docker’s popularity has increased among developers and system administrators because it encompasses the application’s complete filesystem with all its dependencies. This setup enables immutable infrastructure. It guarantees that deployments are idempotent — they will stay exactly the same no matter how many times you repeat the operation.

A Docker daemon runs in the background to manage images, containers, and more. A client and the daemon communicate using sockets or through a [RESTful API](https://circleci.com/blog/what-is-api/).

## What is a Docker image?

Images are read-only templates containing instructions for creating a container. A Docker image creates containers to run on the Docker platform.

Think of an image like a blueprint or snapshot of what will be in a container when it runs.

An image is composed of multiple stacked layers, like layers in a photo editor, each changing something in the environment. Images contain the code or binary, runtimes, dependencies, and other filesystem objects to run an application. The image relies on the host operating system (OS) kernel.

For example, to build a web server image, start with an image that includes Ubuntu Linux (a base OS). Then, add packages like Apache and PHP on top.

You can manually build images using a Dockerfile, a text document containing all the commands to create a Docker image. You can also pull images from a central repository called a registry, or from repositories like Docker Hub using the command `docker pull [name]`.

When a Docker user runs an image, it becomes one or multiple container instances. The container’s initial state can be whatever the developer wants — it might have an installed and configured web server, or nothing but a bash shell running as root. In practice, though, most images include some preconfigured software and configuration files.

Docker images are immutable, so you cannot change them once they are created. If you need to change something, you’ll have to start with a new container that includes your updates, and then save these updates as a new image. Alternatively, you can use an existing image to start a new container and make your changes in this new container.

After successfully building an application, Docker can further export images into other images. Images derived from each other are usually called parent and child images.

To distinguish related images, you can use tags like `ubuntu:latest` or `ubuntu:14.04`, for example. An image may have multiple tags, but each tag is unique.

Images themselves do not run, but you can create and run containers from a Docker image.

## What is a container?

A container is an isolated environment where an application runs without affecting the rest of the system and without the system impacting the application.

Because they are isolated, containers are well-suited for securely running software like databases or web applications that need access to sensitive resources, without giving access to every user on the system.

Since the container runs natively on Linux and shares the host machine’s kernel, it is lightweight, so it doesn’t use more memory than other executables. If you stop a container, it will not automatically restart unless you configure it that way.

Containers can be much more efficient than virtual machines because they don’t need the overhead of an entire operating system. They share a single kernel with other containers and boot in seconds instead of minutes.

You can use containers for packaging an application with all the components it needs, then ship it all out as one unit. This approach is popular because it eliminates the friction between development, QA, and production environments, enabling teams to ship software faster.

Building and deploying applications inside software containers eliminates “it works on my machine” problems when collaborating on code with fellow developers. Since containers ensure consistency across various computing environments, users can rest assured that their application will run the same way everywhere, regardless of where it is deployed.

Docker containers can also run on any infrastructure and in any cloud. You can isolate applications and their underlying infrastructure from other applications, giving you enhanced security and control.

## Docker images vs. containers

A Docker image is a blueprint of code that is executed in a Docker container. To use Docker, you add layers of core functionalities to a Docker image that are then used to create a running container.

In other words, a Docker container is a running instance of a Docker image. You can create many containers from the same image, each with its own unique data and state.

Using containers standardizes and simplifies development, operations, and testing. To use containers effectively, make sure developers, operations engineers, and testers create consistent environments.

One of the best ways to ensure consistency across development, testing, and production environments is to automate building, testing, and deployment processes with [continuous integration and continuous delivery (CI/CD)](https://circleci.com/ci-cd/).

With a CI/CD platform like CircleCI, you can automatically build Docker images as part of your development process. This ensures that every code commit triggers an automated workflow that includes building a Docker image, running [automated testing](https://circleci.com/topics/software-testing/) on the image, and, if the tests pass, pushing the image to a Docker registry.

This automation not only speeds up the development cycle but also improves the reliability and consistency of the software being deployed.

CircleCI offers features such as Docker layer caching, which can significantly reduce build times by reusing the unchanged layers of your Docker images across builds. This is particularly useful when working with large images or when frequently updating images with small changes.

For example, CircleCI can [build Docker images and push them to a container image registry](https://circleci.com/blog/using-circleci-workflows-to-replicate-docker-hub-automated-builds/) like Docker Hub. From there, it can instantiate the images into containers in Kubernetes, OpenShift, or elsewhere.

The flow works like this:

1. You commit changes to your Git repo.
2. This commit triggers a CircleCI build job that checks out the source code from Git and runs unit tests on the code.
3. If the unit tests pass, CircleCI pushes the built image to Docker Hub.
4. If the unit tests fail, CircleCI alerts the developer and stops the workflow.

Features like [Docker layer caching](https://circleci.com/blog/config-best-practices-docker-layer-caching/) and [test splitting](https://circleci.com/blog/a-guide-to-test-splitting/) can also help you build and test your images faster, speeding time to deployment. To learn more about the benefits of using a continuous integration platform to orchestrate your Docker builds, tests, and deploys, visit [How to build a CI/CD pipeline with Docker](https://circleci.com/blog/build-cicd-piplines-using-docker/).

## Conclusion

Understanding the distinction between Docker images and containers is essential for developers and system administrators aiming to leverage Docker’s capabilities for efficient software deployment. While Docker images serve as the static blueprints for creating containers, it’s the containers themselves that bring these blueprints to life, running applications in isolated, consistent environments across different infrastructures.



