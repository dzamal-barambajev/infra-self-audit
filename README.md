# Infrastructure Self-Audit

A self-hosted infrastructure built as a private VPN gateway and evolved into a layered stack of services, monitoring, and reverse proxy routing.

![Self-Hosted](https://shields.io) ![VPN](https://shields.io) ![Docker](https://shields.io) ![Nginx](https://shields.io) ![Xray](https://shields.io) ![Monitoring](https://shields.io) ![Reverse Proxy](https://shields.io)

### Overview

The server was originally deployed as a private VPN gateway for family members. Over time, the infrastructure evolved into a layered self-hosted stack built around:

- [x] **Xray Reality ingress** (vLESS over TLS)
- [x] **nginx** reverse proxy and backend routing
- [x] **Dockerized** applications and services
- [x] **Monitoring and observability** stack
- [x] **Hosting for websites** and PHP applications

### Architecture Overview

```mermaid
graph LR
    classDef box fill:#fff,stroke:#777,stroke-width:1px,round;

    Internet((Internet)) --> Ingress[443 public]
    Ingress --> Xray[Xray VLESS + Reality]
    
    VPN[VPN Clients] -.-> Xray

    Xray --> Fallback[127.0.0.1:8443]
    Fallback --> Nginx[nginx]

    Nginx --> Main[Main Site]
    Nginx --> Wife[Wife Site]
    Nginx --> Mon[Monitoring]
    Nginx --> Docker[Docker Apps]

    class Xray,Nginx,Main,Wife,Mon,Docker,Fallback,VPN,Ingress box;
```

### Current Understanding

The current infrastructure grew incrementally over time and now contains multiple routing layers. 
This repository documents its architecture, configuration, security posture, and areas for improvement.
