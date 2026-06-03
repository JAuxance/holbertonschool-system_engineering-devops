# 1. Distributed web infrastructure

![Distributed web infrastructure](./nom-de-mon-image.png)

This design adds a **load balancer (HAProxy)** in front of **two servers**.
Each server runs Nginx, the application server and the application files. The
database is set up as a **Primary-Replica (Master-Slave) cluster**.

## Why each additional element is added

- **Load balancer (HAProxy):** distributes incoming traffic across multiple
  servers so no single server is overwhelmed, and provides a single entry point
  for `www.foobar.com`.
- **Second server:** adds capacity (more traffic can be handled) and
  redundancy (if one server fails, the other can keep serving requests).

## Distribution algorithm: Round Robin

The load balancer is configured with the **Round Robin** algorithm. It
forwards each new request to the next server in the list, one after another, in
a rotating order (server 1, then server 2, then server 1 again, ...). This
spreads requests evenly across all servers, regardless of their current load.

## Active-Active vs Active-Passive

This setup is **Active-Active**: both servers are running and actively handling
traffic at the same time, and the load balancer distributes requests to both.

- **Active-Active:** all nodes are live and serve traffic simultaneously,
  increasing total capacity.
- **Active-Passive:** only one node (active) serves traffic while the other
  (passive) stays on standby and only takes over if the active node fails.

## How a Primary-Replica (Master-Slave) database cluster works

The cluster has one **Primary (Master)** node and one or more **Replica
(Slave)** nodes. The Primary handles all **write** operations and records every
change. These changes are continuously replicated to the Replica nodes, which
stay in sync with the Primary and serve **read** operations.

## Difference between Primary and Replica regarding the application

- **Primary node:** the application sends all its **writes** (INSERT, UPDATE,
  DELETE) here. It is the single source of truth.
- **Replica node:** the application sends its **reads** (SELECT) here. Replicas
  hold a copy of the data and offload read traffic from the Primary.

The application is therefore configured to **write to the Primary** and **read
from the Replicas**.

## Issues with this infrastructure

- **SPOF:** the load balancer is a single point of failure — if it goes down,
  the whole site is unreachable. The Primary database is also a SPOF for writes.
- **Security issues:** there is no firewall protecting the servers, and no
  HTTPS, so traffic is not encrypted.
- **No monitoring:** there is no way to know the health, performance or load of
  the infrastructure in real time.
