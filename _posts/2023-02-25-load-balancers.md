---
layout: post
title: "Load balancers"
subtitle: "An introduction to workload distribution"
comments: true
categories: "system-design"
tags: "english"
---

Load balancers are responsible to distribute the work among a pool of workers, aiming to scale the job across multiple machines and avoid too many work for only one server.

Load balancers are considered a single point of failure but usually they are deployed using multiple instances or even a cluster

## Global vs Local

There are two types of load balancers, the global and the local ones. Global Load balancers are responsible for traffic distribution across multiple geographical regions. It uses user geographical location, the number of servers per data-center and hit's health.

Local load balancing refer to work distribution within a datac-enter. Focusing on efficiency and better resource utilization 

DNS servers can be considered a Global load balancer with limitations. Knowing that a DNS can answer multiple IP addresses, the order that it's answered matters and with simple techniques, the list can be reordered. Resulting in different users accessing different servers.

This reordering list uses a round-robing mechanism that doesn't consider the ISP size, location or healthy as `Application delivery controllers (ADCs)` and `cloud-based load balancing` do. Resulting in an uneven load distribution or even distribution to crashed servers.

Also, the DNS limitations in Global load balancing are:
- The DNS packet size (512 Bytes) isn't enough to include all possible IP addresses of the servers
- There's limited control over the client's behavior. Clients may select arbitrarily from the received set of IP addresses.
- Clients can't determine the closest address to establish a connection with.
- In case of failures, recovery can be slow due to the caching mechanism, specially when TTL values are longer.

## Algorithms

Some algorithms used in load balancers are:
- Round-robin scheduling that uses chooses a specific and cyclic sequence 
- Weighted round robin to schedule more requests to a specific target
- Least connections that assign new requests to servers with fewer existing connections
- Least response time that considers the server response time to assign new connections
- IP hash that provides different features for different ips. Usually used in geo-location restrictions
