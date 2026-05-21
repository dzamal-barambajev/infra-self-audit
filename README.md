# Infrastructure Self-Audit

A self-hosted infrastructure built as a private VPN gateway and evolved into a layered stack of services, monitoring, and reverse proxy routing.

<p align="center">
  <span style="font-size: 24px;">🌐 🔒 🐳 🚀 ⚡ 📊 🛡️</span>
</p>

### Overview

The server was originally deployed as a private VPN gateway for family members. Over time, the infrastructure evolved into a layered self-hosted stack built around:

* ✅ **Xray Reality ingress** (vLESS over TLS)
* ✅ **nginx** reverse proxy and backend routing
* ✅ **Dockerized** applications and services
* ✅ **Monitoring and observability** stack
* ✅ **Hosting for websites** and PHP applications

### Architecture Overview

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'fontFamily': 'Helvetica', 'primaryColor': '#ffffff', 'edgeLabelBackground':'#ffffff'}}}%%
graph LR
    %% Компактные пастельные стили
    classDef internetStyle fill:#E1F5FE,stroke:#0288D1,stroke-width:2px,rx:12px,ry:12px;
    classDef xrayStyle fill:#FCE4EC,stroke:#C2185B,stroke-width:2px,rx:12px,ry:12px;
    classDef nginxStyle fill:#E8F5E9,stroke:#2E7D32,stroke-width:2px,rx:12px,ry:12px;
    
    classDef webStyle fill:#EDE7F6,stroke:#4527A0,stroke-width:2px,rx:10px,ry:10px;
    classDef dockerStyle fill:#E0F7FA,stroke:#006064,stroke-width:2px,rx:10px,ry:10px;
    classDef phpStyle fill:#E8EAF6,stroke:#1A237E,stroke-width:2px,rx:10px,ry:10px;
    classDef monStyle fill:#FFFDE7,stroke:#F57F17,stroke-width:2px,rx:10px,ry:10px;
    classDef vpnStyle fill:#FFF3E0,stroke:#E65100,stroke-width:2px,rx:10px,ry:10px;

    %% Ядро входа с тройными иконками
    Internet(["🌐 🌐 🌐<br><b>WAN Internet</b>"]) --> Xray["🔒 🔒 🔒<br><b>Xray Core Ingress</b><br>vLESS + Reality"]
    VPN["🔑 🔑 🔑<br><b>VPN Clients</b><br>Family Access"] -.-> Xray
    Xray --> Nginx["🚀 🚀 🚀<br><b>Nginx Gateway</b><br>Reverse Proxy"]

    %% Конечные бэкенды с тройными иконками
    Nginx --> MainWeb["🖥️ 🖥️ 🖥️<br><b>Websites</b><br>Public Domains"]
    Nginx --> Docker["🐳 🐳 🐳<br><b>Docker Apps</b><br>Containers"]
    Nginx --> PHP["🐘 🐘 🐘<br><b>PHP Hosting</b><br>PHP-FPM Apps"]
    Nginx --> Mon["📊 📊 📊<br><b>Monitoring</b><br>Metrics & Logs"]

    %% Применение стилей
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
