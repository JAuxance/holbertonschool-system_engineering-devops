# Holberton School — System Engineering & DevOps

[![Holberton School](https://img.shields.io/badge/Holberton-School-ff0a78)](https://www.holbertonschool.com/)
[![Made with Markdown](https://img.shields.io/badge/Made%20with-Markdown-1f425f.svg)](https://www.markdownguide.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](#-license)

> A collection of **System Administration**, **Networking** and **DevOps**
> projects completed during the Holberton School curriculum — covering web
> infrastructure design, scripting, automation and server management.

---

## 📑 Table of Contents

- [About](#-about)
- [Projects](#-projects)
- [Repository Structure](#-repository-structure)
- [Requirements](#-requirements)
- [Author](#-author)
- [License](#-license)

---

## 📖 About

This repository gathers the hands-on projects from the **System Engineering &
DevOps** track at Holberton School. Each project lives in its own directory and
focuses on a specific concept — from designing resilient web infrastructures to
shell scripting, networking and server automation.

The goal is to learn, step by step, how to **design, deploy, secure, scale and
monitor** the infrastructure that runs modern web applications.

---

## 🚀 Projects

| Project | Description |
| ------- | ----------- |
| [`web_infrastructure_design`](./web_infrastructure_design) | Whiteboarding exercises designing web stacks of increasing complexity: a simple single-server stack, a distributed infrastructure with a load balancer, a secured & monitored setup, and a fully scaled-up architecture. |

### `web_infrastructure_design`

A series of infrastructure designs, each documented with a diagram and a written
explanation of the components, their roles and the trade-offs involved.

| Task | File | Focus |
| ---- | ---- | ----- |
| 0 | [`0-simple-web-stack.md`](./web_infrastructure_design/0-simple-web-stack.md) | Single LAMP server: DNS, web server, application server and database on one machine. |
| 1 | [`1-distributed-web-infrastructure.md`](./web_infrastructure_design/1-distributed-web-infrastructure.md) | Adding a load balancer (HAProxy) in front of two servers. |
| 2 | [`2-secured-and-monitored-web-infrastructure.md`](./web_infrastructure_design/2-secured-and-monitored-web-infrastructure.md) | Firewalls, HTTPS (SSL) and monitoring on top of the distributed stack. |
| 3 | [`3-scale-up.md`](./web_infrastructure_design/3-scale-up.md) | Splitting components onto dedicated servers and clustering the load balancers for high availability. |

---

## 🗂 Repository Structure

```text
holbertonschool-system_engineering-devops/
├── README.md
└── web_infrastructure_design/
    ├── 0-simple-web-stack.md
    ├── 0-simple_web_stack.png
    ├── 1-distributed-web-infrastructure.md
    ├── 1-distributed_web_infrastructure.png
    ├── 2-secured-and-monitored-web-infrastructure.md
    ├── 2-secured_and_monitored_web_infrastructure.png
    ├── 3-scale-up.md
    └── 3-scale_up.png
```

---

## 🛠 Requirements

- A **Markdown** reader to browse the design documents.
- Familiarity with core infrastructure concepts: **DNS**, **HTTP/HTTPS**,
  **load balancing**, **databases (MySQL)**, **firewalls** and **monitoring**.
- New projects in this track typically run on **Ubuntu 20.04 LTS** and follow
  the [Holberton School coding & documentation standards](https://www.holbertonschool.com/).

---

## 👤 Author

**Auxance Jourdan**

- GitHub: [@JAuxance](https://github.com/JAuxance)

---

## 📝 License

This project is licensed under the **MIT License** — feel free to use it for
learning purposes.
