# OpenAudible (Runtipi-App)

[OpenAudible](https://openaudible.org/) im Browser — auf Basis von
[openaudible/openaudible_docker](https://github.com/openaudible/openaudible_docker)
(KasmVNC-Container, experimentell).

## Was die App tut

- OpenAudible-Desktop als Web-GUI auf Port 3000 (Container) bzw. `${APP_PORT}` (Host).
- Daten persistent in `${APP_DATA_DIR}/data` (= `/config/OpenAudible` im Container):
  Bücher, Metadaten, Settings überleben Restarts/Updates.
- Erster Start dauert 1–2 Minuten (OpenAudible wird beim Start geladen).

## Installieren

1. Custom App Store `runtipi-store` in Runtipi einbinden (Repo-URL dieses Projekts).
2. App **OpenAudible** installieren (Port-Vorschlag `8833`, änderbar).
3. Öffnen: `http://<runtipi-host>:8833` oder via Runtipi-Dashboard/Traefik.

## Hinweise

- Nur **ein Viewer gleichzeitig** (KasmVNC-Limit, Upstream-Known-Limitation).
- Kein Passwort by default; `seccomp:unconfined` ist Pflicht (sonst startet OpenAudible nicht).
- `OA_BETA=false` = stable; auf `true` setzen für Beta.
- Vor Container-Löschung in OpenAudible per Control-Menü ausloggen (virtuelles Audible-Device löschen).
- Hörbücher liegen auf dem Host unter `<app-data>/openaudible/data/` (`books/`, `m4b/`, …).

## Update

App in Runtipi updaten bzw. `docker pull openaudible/openaudible:latest` + Restart.
Daten bleiben im Volume erhalten.
