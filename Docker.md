# Docker

## <font color="Red">How to install Docker for CentOS</font>

Installing docker needs CentOS v.7  
Refer to [install Docker CE][1]

## <font color="Red">Linux Container(LXC)</font>

Docker's idea is based on LXC.

### <font color="orange">Feature</font>

LXC is technology that separete each resources for OS to use. This technology don't simulate hardware like OS, so there is no overhead to virtulize. In addition to it, launching and stopping virtual machine is fast, because it does not have to boot and shutdown.

### <font color="orange">Detail</font>

LXC is realized by cgroups. it is mechanism for manage resources OS use. The way to manage is grouping resource, regulating priority and usable resources in each groups, and each groups are invisible.

## <font color="orange">Containerization</font>

The use of LXC to deploy application is called contanarization.

### <font color="orange">containers feature (that is, LXC's feature)</font>

1. Even the most complex applications can be containerized
1. Containers leverage and share host kernel
1. Containerization can deploy updates on-the-fly
1. build locally, deploy to the cloud, and run anywhere
1. Containerization can increase and automatically destribute container replicas

### <font color="orange">images and containers</font>

A container is launched by running an image. An image is an executable package that includes everything to run an application.

A container is a runtime instance of an image.

[1]:https://docs.docker.com/install/linux/docker-ce/centos/#docker-ee-customers
