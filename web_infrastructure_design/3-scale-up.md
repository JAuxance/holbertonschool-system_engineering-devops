# 3. Scale up

![Scale up](./nom-de-mon-image.png)

This design splits the components so that each one runs on its **own dedicated
server**, and adds a **second load balancer** clustered with the first.

- **Web server (Nginx)** → its own server
- **Application server** → its own server
- **Database (MySQL)** → its own server
- **Two load balancers (HAProxy)** configured as a **cluster**

## Why each additional element is added

- **Additional server / dedicated servers:** by giving the web server, the
  application server and the database each its own machine, every component can
  be **scaled independently** (add more of whichever tier is the bottleneck),
  failures are **isolated** to a single role, and the hardware can be
  **optimized per role** (e.g. more RAM for the database, more CPU for the
  application server).
- **Second load balancer (clustered with the first):** the two load balancers
  are set up as a **cluster** (for example, in Active-Passive with a floating
  IP). This removes the load balancer as a single point of failure and provides
  **high availability** — if one load balancer goes down, the other takes over.
- **Splitting the components:** separating the web server, application server
  and database improves **scalability** (each tier scales on its own),
  **fault isolation** (a problem in one tier does not directly take down the
  others) and **resource optimization** (each server is tuned for its specific
  workload).

## Application server vs web server

- **Web server (Nginx):** handles the **HTTP layer**. It receives client
  requests, serves **static** content directly (HTML, CSS, JS, images) and
  forwards **dynamic** requests to the application server. It does not run the
  application's business logic.
- **Application server:** **executes the application code** and the business
  logic. It processes the dynamic requests forwarded by the web server, talks
  to the database, builds the dynamic response and returns it to the web server,
  which sends it back to the client.

In short: the web server delivers content and routes traffic, while the
application server runs the program that produces the dynamic content.
