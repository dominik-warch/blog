---
title: "Geoserver mit Docker hinter Nginx-Proxy-Manager"
date: 2022-05-11T16:01:46+02:00
draft: false

tags: ["GIS", "GeoServer", "Docker", "Nginx Proxy Manager"]
author: "Dominik Visca"
---

Docker und der [Nginx Proxy Manager](https://nginxproxymanager.com/) sind für mich ein _Match made in Heaven_. Die Möglichkeit, per Docker nahezu beliebige Dienste auf meine Server zu packen das Grundsystem nicht mit unübersichtlichen und schwer zu dokumentierenden Konfigurationen zu verändern, ist an sich schon großartig. Diese ganzen Dienste aber mit einer aufgeräumten und gut funktionierenden Weboberfläche nach außen verfügbar zu machen erleichtert einiges an Arbeit.

Für unser [Forschungsprojekt](https://i3mainz.hs-mainz.de/projekte/rafviniert/) gibt es Bedarf, räumliche Daten zu visualisieren. Um das dienstebasiert zu erreichen, gibt es u.a. Projekte wie den [GeoServer](https://geoserver.org/), um die Daten standardisiert als WMS- oder WFS-Dienst zu veröffentlichen. Bisher war ich mehr der Freund des QGIS-Servers, für Endanwender scheint mit der GeoServer aber komfortabler zu sein, also sollte es dieser werden.

Das Unternehmen [Kartoza](https://www.kartoza.com/) stellt auf GitHub viele Dockerfiles und `docker-compose.yml`-Dateien zur Verfügung, um unkompliziert die gängigen FOSS-GIS-Tools zu verwenden, [auch für den GeoServer](https://github.com/kartoza/docker-geoserver).

Per Docker Compose und der angepassten `.env`-Datei ist das Ganze dann innerhalb weniger Minuten gestartet und einsatzbereit. Die Einbindung einer passenden Subdomain über den Nginx Proxy Manager funktionierte augenscheinlich reibungslos, bis dann doch einige Problemchen aufgetreten sind:

1. Obwohl eine aktive SSL-Verschlüsselung im Browser angezeigt wurde, gibt u.a. das Login-Formularfeld die Warnung an, dass die Daten unverschlüsselt versendet werden.
2. Das Wechseln von Menü-Reitern im GeoServer mündet in einem 404-Fehler, die entsprechenden JavaScript-Skripte um die Reiter zu wechseln, können nicht geladen werden.

Es hat ein wenig gedauert bis eine Lösung gefunden war. Wäre ich fitter bei der Konfiguration vom GeoServer, wäre das vermutlich schneller gegangen, die Problematik wird in der (ansonsten recht umfangreichen) Dokumentation des Dockerfiles und der möglichen Umgebungsvariablen von Kartoza nicht thematisiert. Die Lösung des Ganzen? Die Umgebungsvariablen `GEOSERVER_CSRF_WHITELIST` und `PROXY_BASE_URL` mit passenden Werten der entsprechenden Domain egänzen. In der `docker-compose.yml` sieht der Abschnitt dann wie folgt aus:

```yml
geoserver:
  image: kartoza/geoserver:${GS_VERSION}
  container_name: geoserver
  volumes:
    - geoserver-data:/opt/geoserver/data_dir
  restart: on-failure
  environment:
    - GEOSERVER_DATA_DIR=${GEOSERVER_DATA_DIR}
    - GEOWEBCACHE_CACHE_DIR=${GEOWEBCACHE_CACHE_DIR}
    - GEOSERVER_ADMIN_PASSWORD=${GEOSERVER_ADMIN_PASSWORD}
    - GEOSERVER_ADMIN_USER=${GEOSERVER_ADMIN_USER}
    - INITIAL_MEMORY=${INITIAL_MEMORY}
    - MAXIMUM_MEMORY=${MAXIMUM_MEMORY}
    - GEOSERVER_CSRF_WHITELIST=geoserver.example.com
    - PROXY_BASE_URL=https://geoserver.example.com/geoserver
  depends_on:
    db:
      condition: service_healthy
  healthcheck:
    test: curl --fail -s http://localhost:8080/ || exit 1
    interval: 1m30s
    timeout: 10s
    retries: 3
  networks:
    - nginx-proxy-manager_default
```

Damit mich das in Zukunft nicht noch einmal Lebenszeit kostet, dient das hier auch als Dokumentation für mich selbst. 😄
