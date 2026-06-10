# Infrastructure Self-Audit

# VPS Infrastruktur Architektur

![VPS Infrastruktur Architektur](vps-infrastruktur-architektur-de.png)

<p align="center">
  <img src="docs/certifications/linux-essentials-certificate.png" width="180">
</p>

<p align="center">
  🏆 Linux Essentials (LPI) • Certified 2026
</p>

Eine Self-Hosted-Infrastruktur, die ursprünglich als privates VPN-Gateway konzipiert wurde und sich zu einem mehrschichtigen Stack aus Diensten, Monitoring und Reverse-Proxy-Routing weiterentwickelt hat.

<p align="center">
  <span style="font-size: 24px;">🌐 🔒 🐳 🚀 ⚡ 📊 🛡️</span>
</p>

### 📋 Übersicht

Der Server wurde ursprünglich als privates VPN-Gateway für Familienmitglieder bereitgestellt. Im Laufe der Zeit entwickelte sich die Infrastruktur zu einem mehrschichtigen, selbst gehosteten Stack, der auf folgenden Säulen aufbaut:

* ✅ **Xray Reality Ingress** (vLESS über TLS)
* ✅ **Nginx** als Reverse Proxy und Backend-Routing-Instanz
* ✅ **Containerisierte** Anwendungen und Dienste (Docker)
* ✅ **Monitoring und Observability** (Systemüberwachung)
* ✅ **Hosting für Websites** und PHP-Anwendungen
* ✅ **Security Hardening** (Keine offenliegenden Admin-Ports)

### 🗺️ Architektur-Übersicht

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
    VPN["🔑 🔑 🔑<br><b>VPN-Clients</b><br>Familienzugriff"] -.-> Xray
    Xray --> Nginx["🚀 🚀 🚀<br><b>Nginx Gateway</b><br>Reverse Proxy"]

    %% Конечные бэкенды с тройными иконками
    Nginx --> MainWeb["🖥️ 🖥️ 🖥️<br><b>Websites</b><br>Öffentliche Domains"]
    Nginx --> Docker["🐳 🐳 🐳<br><b>Docker Apps</b><br>Container"]
    Nginx --> PHP["🐘 🐘 🐘<br><b>PHP Hosting</b><br>PHP-FPM Apps"]
    Nginx --> Mon["📊 📊 📊<br><b>Monitoring</b><br>Metriken & Logs"]

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

### 🛡️ Edge-Routing & Security Hardening

Um automatisierte Scans, Zensur und aktives Probing (Active Probing) zu verhindern, folgt die Infrastruktur einer strikten **Single-Exposed-Port-Policy (nur TCP-Port 443 ist nach außen offen)**. Allen Administrations-Panels und Backend-Diensten wurden die öffentlichen Ports in der Cloud-Firewall (IONOS-Richtlinie) entzogen; sie sind ausschließlich an lokale Schnittstellen (localhost) gebunden.

Konkret wurden alle externen Inbound-Regeln für zentrale Infrastrukturdienste – einschließlich **Portainer (TCP 9000)**, **Uptime Kuma (TCP 3001)**, **3X-UI (TCP 9999/2096)** und benutzerdefinierten Backend-APIs (TCP 8081/9443) – vollständig entfernt und auf Ebene der Edge-Firewall blockiert. Dadurch wird eine Zero-Visibility-Netzwerkstruktur gegenüber öffentlichen Internet-Scannern erreicht.

#### 🔍 Fallstudie: Absicherung des 3X-UI Admin-Panels
Zuvor war das VPN-Verwaltungspanel über einen dedizierten öffentlichen Port (`TCP 9999`) erreichbar, was es anfällig für Fingerprinting machte. Die Architektur wurde angehoben, um vollständige Tarnung (Stealth) zu erreichen:

1. **Firewall Drop**: Port `9999` wurde auf Ebene der externen Cloud-Firewall (IONOS-Richtlinie) komplett gesperbt.
2. **Encrypted Fallback Loop**: Externer Traffic trifft auf `Port 443` (Xray Core Ingress) auf. Normaler Web-Traffic (kein VPN) wird über einen Fallback-Mechanismus an den lokalen `Nginx` auf Port `8443` weitergeleitet.
3. **Nginx Upstream Routing**: Nginx wertet die eingehende Subdomain (`subexample.example.com`) zusammen mit einem kryptografisch sicheren, zufälligen URL-Pfad aus.
4. **Interner SSL-Proxy**: Nginx leitet die Anfrage sicher über lokales HTTPS (`https://127.0.0.1:9999`) weiter. Interne Weiterleitungsschleifen (Redirect Loops) werden vermieden, indem hartcodierte `X-Forwarded-Proto https`-Header übergeben und WebSocket-Upgrades dynamisch verarbeitet werden.

### 📝 Aktueller Stand & Ausblick

Die bestehende Infrastruktur ist im Laufe der Zeit organisch gewachsen und verfügt nun über mehrere Routing-Ebenen. Dieses Repository dokumentiert die Architektur, die Konfiguration, den Sicherheitsstatus sowie potenzielle Bereiche für zukünftige Optimierungen.
