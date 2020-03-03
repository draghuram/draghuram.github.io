---
layout: post
title:  "Containers and Virtualization"
date:   2020-03-03
categories: kubernetes docker kata containers virtualization
---

While reading an interesting blog post about 
[kata containers](https://platform9.com/blog/kata-containers-docker-and-kubernetes-how-they-all-fit-together/),
the following sentence caught my attention:

> Unlike virtual machines, which can take a minute or two to start and
> waste a fair amount of hardware resources on isolation, Kata
> containers aim to start just as fast and consume resources just as
> efficiently as other containers. 

This rang a bell because when 
[Hardware
virtualization](https://en.wikipedia.org/wiki/Hardware_virtualization)
was getting popularized by
[vSphere](https://www.vmware.com/products/vsphere.html) and other
solutions, one of the advantages frequently mentioned was that usage
of physical servers wastes resources and by running multiple VMs on a
single host, you will utilize it more, thus reducing such wastage.

It is interesting to see that almost same reason is now being given
for switching to containers from VMs themselves. To me, this
highlights the fact that we (as in *software field*) are making constant
progress towards having better utilization of servers as well as
having a very flexible and powerful way of building and deploying apps
(using VMs and Containers). 

Going back to the main point of the 
[blog](https://platform9.com/blog/kata-containers-docker-and-kubernetes-how-they-all-fit-together/),
the concept of 
[kata containers](https://katacontainers.io) sounds very intriguing. I
heard about them before but haven't spent much time exploring. But I am
curious now to see how I can take advantage of the fact that each 
*kata container* runs in a dedicated kernel (unlike 
[Docker](https://www.docker.com/) and other container
runtimes). Specifically, I want to know if they allow containerizing
[ZFS](https://en.wikipedia.org/wiki/ZFS). Since 
[ZFS](https://en.wikipedia.org/wiki/ZFS) is implemented as a
combination of a kernel module and userland utilities, it is not
possible to containerize it using 
[Docker](https://www.docker.com/). For example, a pool created in one
[Docker](https://www.docker.com/) container will make it visible in
other containers as well. But with [kata
containers](https://katacontainers.io) running a dedicated kernel, it
may be possible to fully containerize
[ZFS](https://en.wikipedia.org/wiki/ZFS). 

Just to be clear, this is just a theory and I haven't tested the
hypothesis. I do hope to spend some time understanding and exploring
[kata containers](https://katacontainers.io) though.

