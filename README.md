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
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#ffffff', 'edgeLabelBackground':'#ffffff'}}}%%
graph LR
    %% Palette Definitions
    classDef internetStyle fill:#E1F5FE,stroke:#0288D1,stroke-width:2px,rx:8px,ry:8px;
    classDef xrayStyle fill:#FCE4EC,stroke:#C2185B,stroke-width:2px,rx:8px,ry:8px;
    classDef nginxStyle fill:#E8F5E9,stroke:#2E7D32,stroke-width:2px,rx:8px,ry:8px;
    
    classDef webStyle fill:#EDE7F6,stroke:#4527A0,stroke-width:1.5px,rx:6px,ry:6px;
    classDef dockerStyle fill:#E0F7FA,stroke:#006064,stroke-width:1.5px,rx:6px,ry:6px;
    classDef phpStyle fill:#E8EAF6,stroke:#1A237E,stroke-width:1.5px,rx:6px,ry:6px;
    classDef monStyle fill:#FFFDE7,stroke:#F57F17,stroke-width:1.5px,rx:6px,ry:6px;
    classDef vpnStyle fill:#FFF3E0,stroke:#E65100,stroke-width:1.5px,rx:6px,ry:6px;

    %% Ingress Core Pipeline
    Internet(["Internet"]) --> Xray["Xray Core<br>vLESS + Reality<br>🔒 443"]
    VPN["VPN Clients<br>Family Access"] -.-> Xray
    Xray --> Nginx["nginx<br>Proxy Gateway<br>🔒 8443"]

    %% Super Compact Subgraph Cluster for Backends
    subgraph Hosted_Services_Stack [" HOSTED SERVICES STACK "]
        MainWeb["Websites<br>Public Domains"]
        Docker["Docker Apps<br>Containers"]
        PHP["PHP Hosting<br>PHP-FPM Apps"]
        Mon["Monitoring<br>Metrics & Logs"]
    end

    %% Tight Routing Connections with Massive Icons on Lines
    Nginx ==>|🌐 Websites| MainWeb
    Nginx ==>|🐳 Docker| Docker
    Nginx ==>|🐘 PHP| PHP
    Nginx ==>|📊 Monitoring| Mon

    %% Style Injection
    class Internet internetStyle;
    class Xray xrayStyle;
    class Nginx nginxStyle;
    class MainWeb webStyle;
    class Docker dockerStyle;
    class PHP phpStyle;
    class Mon monStyle;
    class VPN vpnStyle;
```

### Current Understanding

The current infrastructure grew incrementally over time and now contains multiple routing layers. 
This repository documents its architecture, configuration, security posture, and areas for improvement.
