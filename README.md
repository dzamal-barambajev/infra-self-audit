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
%%{init: {'theme': 'base', 'themeVariables': { 'fontFamily': 'Helvetica', 'edgeLabelBackground':'#ffffff'}}}%%
graph LR
    %% Style Profiles with Custom Background Colors
    classDef internetStyle fill:#E1F5FE,stroke:#0288D1,stroke-width:1.5px,rx:8px,ry:8px;
    classDef xrayStyle fill:#FCE4EC,stroke:#C2185B,stroke-width:1.5px,rx:8px,ry:8px;
    classDef nginxStyle fill:#E8F5E9,stroke:#2E7D32,stroke-width:1.5px,rx:8px,ry:8px;
    classDef webStyle fill:#EDE7F6,stroke:#4527A0,stroke-width:1.5px,rx:8px,ry:8px;
    
    classDef vpnStyle fill:#FFF3E0,stroke:#E65100,stroke-width:1.2px,rx:6px,ry:6px;
    classDef dockerStyle fill:#E0F7FA,stroke:#006064,stroke-width:1.2px,rx:6px,ry:6px;
    classDef phpStyle fill:#E8EAF6,stroke:#1A237E,stroke-width:1.2px,rx:6px,ry:6px;
    classDef monStyle fill:#FFFDE7,stroke:#F57F17,stroke-width:1.2px,rx:6px,ry:6px;

    %% Elements and Icons definition with Larger Emojis
    Internet(["<span style='font-size:24px;'>🌐</span><br><b>Internet</b>"])
    Xray["<span style='font-size:22px;'>🛡️</span><br><div style='color:#C2185B; font-weight:bold;'>Xray Core</div><div style='font-size:11px; color:#555;'>Reality + vLESS</div><div style='font-size:11px; color:#C2185B;'>🔒 :443 (TLS)</div>"]
    Nginx["<span style='font-size:22px;'>🚀</span><br><div style='color:#2E7D32; font-weight:bold;'>nginx</div><div style='font-size:11px; color:#555;'>Reverse Proxy</div><div style='font-size:11px; color:#2E7D32;'>🔒 :8443</div>"]
    Web["<span style='font-size:22px;'>🖥️</span><br><div style='color:#4527A0; font-weight:bold;'>Websites</div><div style='font-size:11px; color:#555;'>Public & Private<br>Domains</div>"]
    
    VPN["<span style='font-size:24px;'>🏠</span><br><b>VPN Clients</b><br><span style='font-size:11px; color:#555;'>Family / Remote<br>Access</span>"]
    Docker["<span style='font-size:26px;'>🐳</span><br><b>Docker Apps</b><br><span style='font-size:11px; color:#555;'>Containerized<br>Services</span>"]
    PHP["<span style='font-size:26px;'>🐘</span><br><b>PHP Hosting</b><br><span style='font-size:11px; color:#555;'>PHP-FPM<br>Applications</span>"]
    Mon["<span style='font-size:24px;'>📊</span><br><b>Monitoring Stack</b><br><span style='font-size:11px; color:#555;'>Metrics, Logs<br>& Alerts</span>"]

    %% Flow Connections
    Internet --> Xray
    Xray --> Nginx
    Nginx --> Web
    
    VPN -.-> Xray
    Nginx -.-> Docker
    Nginx -.-> PHP
    Nginx -.-> Mon

    %% Force tight horizontal clustering using invisible connections
    VPN ~~~ Docker
    Docker ~~~ PHP
    PHP ~~~ Mon
    Web ~~~ Docker

    %% Assigning Style Classes
    class Internet internetStyle;
    class Xray xrayStyle;
    class Nginx nginxStyle;
    class Web webStyle;
    class VPN vpnStyle;
    class Docker dockerStyle;
    class PHP phpStyle;
    class Mon monStyle;
```

### Current Understanding

The current infrastructure grew incrementally over time and now contains multiple routing layers. 
This repository documents its architecture, configuration, security posture, and areas for improvement.
