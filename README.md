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
%%{init: {'theme': 'base', 'themeVariables': { 'fontFamily': 'Helvetica', 'primaryColor': '#ffffff', 'edgeLabelBackground':'#ffffff'}}}%%
graph LR
    %% Style Profiles
    classDef mainNode fill:#fff,stroke:#4A90E2,stroke-width:1.5px,rx:8px,ry:8px;
    classDef secNode fill:#fff,stroke:#7B1FA2,stroke-width:1.2px,rx:6px,ry:6px;
    classDef outlineNode fill:#fff,stroke:#555,stroke-width:1.2px,rx:6px,ry:6px;

    %% Elements and Icons definition
    Internet(["🌐 <br> Internet"])
    Xray["<div style='color:#00796B; font-weight:bold;'>Xray Core</div><div style='font-size:11px; color:#555;'>Reality + vLESS</div><div style='font-size:11px; color:#00796B;'>🔒 :443 (TLS)</div>"]
    Nginx["<div style='color:#0D47A1; font-weight:bold;'>nginx</div><div style='font-size:11px; color:#555;'>Reverse Proxy</div><div style='font-size:11px; color:#0D47A1;'>🔒 :8443</div>"]
    Web["<div style='color:#1A237E; font-weight:bold;'>Websites</div><div style='font-size:11px; color:#555;'>Public & Private<br>Domains</div>"]
    
    VPN["📦 <br> <b>VPN Clients</b><br><span style='font-size:11px; color:#555;'>Family / Remote<br>Access</span>"]
    Docker["🐳 <br> <b>Docker Apps</b><br><span style='font-size:11px; color:#555;'>Containerized<br>Services</span>"]
    PHP["🐘 <br> <b>PHP Hosting</b><br><span style='font-size:11px; color:#555;'>PHP-FPM<br>Applications</span>"]
    Mon["📊 <br> <b>Monitoring Stack</b><br><span style='font-size:11px; color:#555;'>Metrics, Logs<br>& Alerts</span>"]

    %% Flow Connections
    Internet --> Xray
    Xray --> Nginx
    Nginx --> Web
    
    VPN -.-> Xray
    Nginx -.-> Docker
    Nginx -.-> PHP
    Nginx -.-> Mon

    %% Assigning Style Classes
    class Xray,Nginx,Web mainNode;
    class Docker,PHP,Mon secNode;
    class Internet,VPN outlineNode;
```

### Current Understanding

The current infrastructure grew incrementally over time and now contains multiple routing layers. 
This repository documents its architecture, configuration, security posture, and areas for improvement.
