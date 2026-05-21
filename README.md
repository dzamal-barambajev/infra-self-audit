# Infrastructure Self-Audit

A self-hosted infrastructure built as a private VPN gateway and evolved into a layered stack of services, monitoring, and reverse proxy routing.

<p align="left">
  <img src="https://shields.io" alt="Self-Hosted">
  <img src="https://shields.io" alt="VPN">
  <img src="https://shields.io" alt="Docker">
  <img src="https://shields.io" alt="Nginx">
  <img src="https://shields.io" alt="Xray">
  <img src="https://shields.io" alt="Monitoring">
  <img src="https://shields.io" alt="Reverse Proxy">
</p>

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
    %% Strict theme overrides for GitHub Markdown override
    style Internet fill:#E6E6FA,stroke:#777,stroke-width:2px;
    style Ingress fill:#FFF,stroke:#333,stroke-width:2px;
    style Xray fill:#FFF,stroke:#333,stroke-width:2px;
    style VPN fill:#FFF,stroke:#333,stroke-width:2px;
    style Fallback fill:#FFF,stroke:#333,stroke-width:2px;
    style Nginx fill:#FFF,stroke:#333,stroke-width:2px;
    style Main fill:#FFF,stroke:#333,stroke-width:2px;
    style Wife fill:#FFF,stroke:#333,stroke-width:2px;
    style Mon fill:#FFF,stroke:#333,stroke-width:2px;
    style Docker fill:#FFF,stroke:#333,stroke-width:2px;

    %% Base Layout Configuration
    Internet((Internet)) --> Ingress["443 public"]
    Ingress --> Xray["Xray VLESS + Reality"]
    
    VPN[VPN Clients] -.-> Xray

    Xray --> Fallback["Local 127.0.0.1 8443"]
    Fallback --> Nginx[nginx]

    Nginx --> Main[Main Site]
    Nginx --> Wife[Wife Site]
    Nginx --> Mon[Monitoring]
    Nginx --> Docker[Docker Apps]
```

### Current Understanding

The current infrastructure grew incrementally over time and now contains multiple routing layers. 
This repository documents its architecture, configuration, security posture, and areas for improvement.
