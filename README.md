# Infrastructure Self-Audit

A self-hosted infrastructure built as a private VPN gateway and evolved into a layered stack of services, monitoring, and reverse proxy routing.

<p align="left">
  <kbd>🌐 Self-Hosted</kbd>
  <kbd>🔒 VPN Gateway</kbd>
  <kbd>🐳 Docker</kbd>
  <kbd>🚀 Nginx</kbd>
  <kbd>⚡ Xray</kbd>
  <kbd>📊 Monitoring</kbd>
  <kbd>🛡️ Reverse Proxy</kbd>
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
graph TD
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

    %% Color definitions for elements (using safe hex codes)
    style Internet fill:#E6F0FA,stroke:#4A90E2,stroke-width:2px;
    style Ingress fill:#F0F4F8,stroke:#9B9B9B,stroke-width:2px;
    style Xray fill:#FFF0F5,stroke:#FF69B4,stroke-width:2px;
    style VPN fill:#FFF5EE,stroke:#FFA500,stroke-width:2px;
    style Fallback fill:#F5F5F5,stroke:#777777,stroke-width:2px;
    style Nginx fill:#E6F4EA,stroke:#34A853,stroke-width:2px;
    style Main fill:#FFFFFF,stroke:#333333,stroke-width:2px;
    style Wife fill:#FFFFFF,stroke:#333333,stroke-width:2px;
    style Mon fill:#FFFDE7,stroke:#FBC02D,stroke-width:2px;
    style Docker fill:#E1F5FE,stroke:#0288D1,stroke-width:2px;
```

### Current Understanding

The current infrastructure grew incrementally over time and now contains multiple routing layers. 
This repository documents its architecture, configuration, security posture, and areas for improvement.
