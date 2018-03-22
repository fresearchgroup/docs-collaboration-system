---
id: cache
title: Memcache Configuration
sidebar_label: Memcache Configuration
---

## Configuring Memchached for Django backend

Install memcached on all django servers:

```shell
$ sudo apt-get install memcached
```
Install Python API for communication between your application and Memcached daemon:

```shell
$ sudo apt-get install python-memcache
```
This one depends from the Django version that you use. For 1.2.5 and prior the next code should be added in your settings file(settings.py). One excellent feature of Memcached is its ability to share a cache over multiple servers. This means you can run Memcached daemons on multiple machines, and the program will treat the group of machines as a single cache, without the need to duplicate cache values on each machine. To take advantage of this feature, include all server addresses in LOCATION, either as a semicolon or comma delimited string, or as a list. In this example, the cache is shared over Memcached instances running on IP address 172.19.26.240 and 172.19.26.242, both on port 11211

```
CACHES = {
           'default': {
           'BACKEND': 'django.core.cache.backends.memcached.MemcachedCache',
           'LOCATION': [  '172.19.26.240:11211',
                          '172.19.26.242:11211',
                       ]
                  }
            }
```
