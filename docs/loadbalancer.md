---
id: loadbalancer
title: Load Balancer Configuration
sidebar_label: Load Balancer Configuration
---


## Install haproxy

```shell
$ sudo apt-get update
$ sudo apt-get install haproxy -y

```

## Enable haproxy

```shell
$ sudo vi /etc/default/haproxy

```
The variable ‘Enabled’ is set 0. Set it to 1.
ENABLED=1
.Save and exit

## Configure haproxy

```shell
$ sudo vi /etc/haproxy/haproxy.cfg

```

Add the following lines at the end of file

```
#frontend haproxy_in
frontend http_front
        bind *:80
        default_backend http_back

#backend haproxy_http
backend http_back
        balance roundrobin
        mode http
        server vm1 10.129.26.103:80 check
        server vm2 10.129.28.102:80 check

```

Change the variables as per your configuration.

## Restart and Test haproxy
```shell
$ sudo /etc/init.d/haproxy restart

```
