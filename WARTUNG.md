# 📝 Wartungsprotokoll: Infrastruktur-Audits und Optimierungen

Hier werden alle technischen Wartungsarbeiten, Fehlerbehebungen und Konfigurationsänderungen an der Server-Infrastruktur dokumentiert.

---

## Nginx-Optimierung & Fehlerbehebung

**Status:** Erfolgreich abgeschlossen (`nginx -t`: clean status)

### 🛠 Durchgeführte Änderungen:

1. **Behebung von Protokollkonflikten auf Port `8443` (Xray Fallback):**
   * **Problem:** In der Konfiguration `portainer` war der Port als `listen 8443 ssl http2;` definiert, in `monitoring` (Grafana/Prometheus) jedoch nur als `listen 8443;`. Dies führte zu der Warnung `protocol options redefined`.
   * **Lösung:** Die Direktiven für Port `8443` wurden in allen Dateien vereinheitlicht: `listen 8443 ssl http2;`. Der interne Datenverkehr von Xray wird nun korrekt verschlüsselt.

2. **Behebung von Namenskonflikten (`server_name`-Duplikate auf Port `80`):**
   * **Problem:** Die Domains `netzvirtuell.com` und `://netzvirtuell.com` waren für HTTP-Traffic gleichzeitig in den Dateien `barambajev` und `3x-ui` aktiv. Nginx ignorierte daher einen Teil der Einstellungen.
   * **Lösung:** Der doppelte Block wurde aus der Konfiguration `3x-ui` entfernt. Die primäre HTTP-Weiterleitung (Port 80) wird nun zentral von `barambajev` (Production Site) gesteuert.

3. **Stabilitätstest:**
   * Der Zugriff auf das **3X-UI Web-Dashboard** (über Port `8443` und den geheimen Location-Pfad) bleibt voll funktionsfähig und läuft ohne Redirect-Schleifen.
   * Die Konfiguration wurde mit `sudo systemctl reload nginx` erfolgreich live geschaltet.


---

## Behebung von SSE-Verbindungsabbrüchen in Prometheus

**Datum:** 26.05.2026
**Status:** Erfolgreich behoben (Nginx-Proxy optimiert)

### 🛠 Durchgeführte Änderungen:
* **Problem:** Die Fehlermeldung `Real-time notifications interrupted` trat im Prometheus-Webinterface auf, da Nginx die Server-Sent Events (SSE) blockierte.
* **Lösung:** In der Datei `sites-available/monitoring` wurden die Parameter `proxy_buffering off;`, `proxy_cache off;` und ein erweitertes `proxy_read_timeout 24h;` für das Prometheus-Target hinzugefügt. Die Echtzeit-Synchronisation läuft nun stabil.
