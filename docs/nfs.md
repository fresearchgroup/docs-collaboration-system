---
id: nfs
title: NFS Configuration
sidebar_label: NFS Configuration
---

## Configuring NFS between two Django nodes:

Setting up Server (10.129.26.102)

```shell
$ sudo apt-get update
$ sudo apt-get install nfs-kernel-server

```

Setting up Client (10.129.26.103)

```shell
$ sudo apt-get update
$ sudo apt-get install nfs-common

```

Exporting and Configuring directory on Server (10.129.26.102)

```shell
$ sudo vi /etc/exports
```
Add <Folder path> <client IP>(sharing). Example given below
```
/home/edx/CollaborationSystem/media 10.129.26.103(rw,sync,no_subtree_check)

```
```shell
$ sudo systemctl restart nfs-kernel-server
```

Mounting on Client (10.129.26.103)

```shell
$ sudo mount 10.129.126.102:/home/edx/CollaborationSystem/media /home/edx/CollaborationSystem/media

```
