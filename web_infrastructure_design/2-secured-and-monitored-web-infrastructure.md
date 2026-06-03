# 2. Secured and monitored web infrastructure

![Secured and monitored web infrastructure](./nom-de-mon-image.png)

This design takes the distributed infrastructure from Task 1 and adds **three
firewalls**, an **SSL certificate** to serve traffic over HTTPS, and **three
monitoring clients** (for example, a Sumologic agent on each server).

## Why each additional element is added

- **Firewalls (3):** one per machine (load balancer + the two servers) to
  control and filter network traffic, only allowing legitimate connections in
  and out.
- **SSL certificate:** to serve traffic over **HTTPS**, encrypting data
  exchanged between users and the infrastructure.
- **Monitoring clients (3):** one agent per server to collect data and report
  the health and performance of each machine to a monitoring service.

## What are firewalls for?

A firewall is a security system (hardware or software) that monitors and
filters incoming and outgoing network traffic based on a set of rules. It
blocks unauthorized access and only lets through the traffic you explicitly
allow, protecting servers from attacks and intrusions.

## Why is traffic served over HTTPS?

HTTPS encrypts the data exchanged between the user's browser and the server
using SSL/TLS. This protects sensitive information (passwords, personal data,
session cookies) from being intercepted or tampered with, and guarantees the
integrity and authenticity of the communication.

## What is monitoring used for?

Monitoring is used to continuously observe the infrastructure: server health,
resource usage (CPU, memory, disk), traffic, errors and performance. It helps
detect problems early, troubleshoot incidents, send alerts when something goes
wrong, and make informed decisions about scaling.

## How does the monitoring tool collect data?

Each server runs a **monitoring agent** (the monitoring client). This agent
collects logs and metrics locally on the server and **pushes** them to the
monitoring service (e.g. Sumologic), where the data is aggregated, stored,
visualized and used to trigger alerts.

## How to monitor the web server QPS

QPS (Queries Per Second) measures how many requests the web server handles each
second. To monitor it, configure the monitoring agent to read **Nginx access
logs** (each line is one request) and count the number of requests over time,
or expose a request-count metric from Nginx that the agent reports to the
monitoring service. Dividing the request count by the time window gives the QPS.

## Issues with this infrastructure

- **SSL termination at the load balancer:** if SSL is terminated at the load
  balancer, traffic between the load balancer and the backend servers travels
  **unencrypted (in clear text)**, which is a security risk inside the
  infrastructure.
- **Single MySQL write node:** only the Primary MySQL server can accept
  **writes**. It is a single point of failure for write operations — if it
  fails, the application can no longer write data.
- **Identical servers:** every server runs all components (web server,
  application server, database). This makes it hard to scale a single component
  independently and does not optimize hardware usage per role.
