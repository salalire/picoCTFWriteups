# Failure Failure

## Category

General Skills

## Difficulty

Medium

## Challenge Information

- **Author:** Darkraicg492
- **Platform:** picoCTF
- **Year:** 2026
- **Challenge Name:** Failure Failure
- **Target URL:** `http://chatelaine.cylabacademy.net:16935/`
- **Files Provided:** `haproxy.cfg`, `app.py`

## What I Learned

- How a load balancer distributes traffic between backend servers.
- How high availability and automatic failover work.
- How to inspect application source code and configuration files to understand a challenge.
- How rate limiting can affect server availability.
- How HTTP status codes influence load balancer health checks.
- How to use `curl` to send HTTP requests and Bash loops to automate repeated requests.
- How a misconfiguration between an application and a load balancer can expose information available on a backup server.

## Approach

### 1. Understand the Challenge

The challenge presented a web application behind an HAProxy load balancer.

Initially, the primary server did not reveal the flag. The challenge also provided the HAProxy configuration and Python application source code.

The goal was to understand how the load balancer selected a backend server and determine how to trigger failover to the backup server.

### 2. Inspect the Application Code and HAProxy Configuration

I reviewed the provided `app.py` and `haproxy.cfg` files to understand the application's behavior and the load balancer's failover conditions.

The important findings were:

- The primary application server enforced a limit of 300 requests per minute.
- When the rate limit was exceeded, the application returned HTTP `503 Service Unavailable`.
- HAProxy used health checks to determine whether the primary server was healthy.
- The backup server could return the flag when HAProxy routed traffic to it.

This revealed that exceeding the rate limit could make the primary server appear unhealthy and trigger failover.

### 3. Send Repeated Requests

I used a Bash loop with `curl` to send repeated requests to the challenge endpoint.

First, I sent 320 requests:

    for i in {1..320}; do curl -s http://chatelaine.cylabacademy.net:16935/ > /dev/null; done

Then, I sent another 350 requests:

    for i in {1..350}; do curl -s http://chatelaine.cylabacademy.net:16935/ > /dev/null; done

**Command explanation:**

- `for i in {1..320}` iterates through 320 values.
- `curl -s` sends an HTTP request without displaying the progress meter.
- `> /dev/null` discards the response body.
- `done` marks the end of the loop.

These commands automated repeated requests to exercise the application's rate limit.

### 4. Trigger Failover

Once the primary server began returning HTTP 503 responses because of the rate limit, HAProxy could interpret those responses as failed health checks.

After detecting that the primary server was unhealthy, HAProxy could route requests to the backup server.

The important relationship was:

1. Repeated requests exceeded the primary server's rate limit.
2. The primary server returned HTTP 503 responses.
3. HAProxy detected the failed health checks.
4. Traffic was routed to the backup server.
5. The backup server returned the flag.

### 5. Retrieve the Flag

After triggering the failover, the challenge revealed the flag:

    academy{f41l0v3r_f0r_7h3_w1n_ff05bda3}

## Commands / Tools Used

- `wget URL` — downloads challenge files.
- `cat app.py` — displays the Python application's source code.
- `cat haproxy.cfg` — displays the HAProxy configuration.
- `curl -s URL` — sends an HTTP request quietly.
- `for i in {1..320}; do ...; done` — automates repeated requests using a Bash loop.
- `> /dev/null` — discards command output.

## Key Concepts

### Load Balancer

A load balancer distributes incoming requests across backend servers according to its configuration.

In this challenge, HAProxy directed traffic to a primary server and used a backup server when the primary was considered unhealthy.

### High Availability and Failover

High availability aims to keep a service accessible when a component fails.

Failover is the process of switching traffic to another server when the primary server becomes unavailable or fails its health checks.

### Rate Limiting

Rate limiting restricts how many requests a client or group of clients can make during a specified period.

The primary application enforced a limit of 300 requests per minute. Exceeding that limit caused it to return HTTP 503 responses.

### HTTP 503 Service Unavailable

HTTP 503 indicates that a server cannot currently handle a request.

In this challenge, the application returned 503 when its rate limit was exceeded. Because HAProxy used successful HTTP responses to assess backend health, these responses could contribute to triggering failover.

### Health Checks

Health checks help a load balancer determine whether a backend server is available to handle traffic.

A configuration that allows ordinary rate-limited requests to affect health checks can create unintended interactions between application behavior and infrastructure routing.

## Security Lessons Learned

- Rate limits should be designed so that normal traffic cannot easily manipulate infrastructure health decisions.
- Health checks should be carefully separated from application-level rate limiting where appropriate.
- Backup servers must enforce the same security controls as primary servers.
- Sensitive information should not become accessible simply because a load balancer switches to a different backend.
- Application code and infrastructure configuration should be reviewed together because vulnerabilities can arise from their interaction.

## Result

Successfully triggered the challenge's failover behavior and retrieved the flag from the backup server.

## Flag

academy{f41l0v3r_f0r_7h3_w1n_ff05bda3}