---
title: High Availability for IBM MQ
toc: false
sidebar: labs_sidebar
folder: pots/mq-ha
permalink: /mq_ha_pot_overview.html
summary: High Availability for IBM MQ
---

# Overview

If you want to operate your IBM® MQ queue managers in a high availability (HA) configuration, you can set up your queue managers to work either with a high availability manager, such as PowerHA® for AIX® (formerly HACMP™ ) or the Microsoft Cluster Service (MSCS), or with IBM MQ multi-instance queue managers. With IBM MQ v9.0.4 on Linux systems, you can also deploy replicated data queue managers (RDQMs), which use a quorum-based group to provide high availability.

You need to be aware of the following configuration definitions:

## Queue manager clusters

Groups of two or more queue managers on one or more computers, providing automatic interconnection, and allowing queues to be shared among them for load balancing and redundancy.

## HA clusters

HA clusters are groups of two or more computers and resources such as disks and networks, connected together and configured in such a way that, if one fails, a high availability manager, such as HACMP ( UNIX ) or MSCS ( Windows ) performs a failover. The failover transfers the state data of applications from the failing computer to another computer in the cluster and re-initiates their operation there. This provides high availability of services running within the HA cluster. The relationship between IBM MQ clusters and HA clusters is described in Relationship of HA clusters to queue manager clusters.

## Multi-instance queue managers

Instances of the same queue manager configured on two or more computers. By starting multiple instances, one instance becomes the active instance and the other instances become standbys. If the active instance fails, a standby instance running on a different computer automatically takes over. You can use multi-instance queue managers to configure your own highly available messaging systems based on IBM MQ, without requiring a cluster technology such as HACMP or MSCS. HA clusters and multi-instance queue managers are alternative ways of making queue managers highly available. Do not combine them by putting a multi-instance queue manager in an HA cluster.

## Replicated data queue managers (RDQMs)

Instances of the same queue manager configured on each node in a group of three Linux servers. One of the three instances is the active instance. Data from the active queue manager is synchronously replicated to the other two instances, so one of these instances can take over in the event of some failure. The grouping of the servers is controlled by Pacemaker, and the replication by DRBD. 

## Differences between multi-instance queue managers and HA clusters

Multi-instance queue managers and HA clusters are alternative ways to achieve high availability for your queue managers. Here are some points that highlight the differences between the two approaches.

Multi-instance queue managers include the following features: 

* Basic failover support integrated into IBM MQ
* Faster failover than HA cluster
* Simple configuration and operation
* Integration with IBM MQ Explorer

### Limitations of multi-instance queue managers include:

* Highly available, high performance networked storage required
* More complex network configuration because queue manager changes IP address when it fails over

### HA clusters include the following features:

* The ability to coordinate multiple resources, such as an application server or database
* More flexible configuration options including clusters comprising more than two nodes
* Can failover multiple times without operator intervention
* Takeover of queue manager's IP address as part of the failover

### Limitations of HA clusters include:

* Additional product purchase and skills are required
* Disks which can be switched between the nodes of the cluster are required
* Configuration of HA clusters is relatively complex
* Failover is rather slow historically, but recent HA cluster products are improving this
*Unnecessary failovers can occur if there are shortcomings in the scripts that are used to monitor resources such as queue managers

## Relationship of HA clusters to queue manager clusters

Queue manager clusters provide load balancing of messages across available instances of queue manager cluster queues. This offers higher availability than a single queue manager because, following a failure of a queue manager, messaging applications can still send messages to, and access, surviving instances of a queue manager cluster queue. However, although queue manager clusters automatically route new messages to the available queue managers in a cluster, messages currently queued on an unavailable queue manager are not available until that queue manager is restarted. For this reason, queue manager clusters alone do not provide high availability of all message data or provide automatic detection of queue manager failure and automatic triggering of queue manager restart or failover. High Availability (HA) clusters provide these features. The two types of cluster can be used together to good effect. For an introduction to queue manager clusters, see Designing clusters.


For the latest and complete discussion of high availability for IBM MQ refer to the link below:  

[High Availability for IBM MQ](https://www.ibm.com/support/knowledgecenter/SSFKSJ_9.0.0/com.ibm.mq.con.doc/q017820_.htm)

