---
id: mysql
title: Mysql Set Up
sidebar_label: Mysql Configuration
---


## Setup Database (MySQL)

```shell
$ sudo apt-get update
$ sudo apt-get install mysql-server

```
Set Username =root and Password =root

## Create database (Database name: iimbx)

```shell
$ wget https://github.com/fresearchgroup/Collaboration-System/raw/master/collaboration.sql
$ mysql -u root -p
Enter password as root
mysql> create database collaboration;
mysql> use collaboration;
mysql> source collaboration.sql

```
## Provide permissions to remote nodes or external users -
Execute the following commands for allowing remote django machines to connect to database , change the ip addresses and give remote django machine ip addresses

```shell
$ mysql -u root -p
mysql> use collaboration;
mysql> GRANT ALL ON *.* TO edx@'10.129.28.102' IDENTIFIED BY 'edx123'
mysql> flush privileges;
mysql> GRANT ALL ON *.* TO edx@'10.129.26.103' IDENTIFIED BY 'edx123'
mysql> flush privileges;

```
