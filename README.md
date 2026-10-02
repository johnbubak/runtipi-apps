# runtipi-store — Custom App Store (ZimaCube / Runtipi)

Minimaler Custom-Store für Runtipi ≥ 4.5.0. Enthält aktuell: **OpenAudible**.

## Struktur

```
runtipi-store/
  apps/
    openaudible/
      config.json
      docker-compose.yml
      metadata/
        description.md
        logo.jpg
```

`id` in `config.json` = Ordnername (`openaudible`). Pflichtdateien pro App:
`config.json` + `docker-compose.yml` + `metadata/logo.jpg` + `metadata/description.md`.

## Store in Runtipi einbinden (.72)

1. Runtipi-Dashboard öffnen → **App Store** → **Custom Store hinzufügen**.
2. Repo-URL dieses Projekts eintragen (Branch `main`, Pfad `runtipi-store`).
3. Store aktivieren → App **OpenAudible** erscheint → **Install**.
4. Port prüfen (Default `8833`): `http://192.168.178.72:8833`.

## CLI (auf .72, User mit Docker-Rechten)

```bash
./runtipi-cli app install openaudible:custom
./runtipi-cli app start openaudible:custom
./runtipi-cli app logs openaudible:custom --tail 50
```

Store-Name (`custom`) ggf. anpassen: `./runtipi-cli app list` zeigt installierte Stores.

## Neue App aus GitHub-Repo ableiten (Kurzform)

1. Upstream-README + `docker-compose.yml` lesen (Image, interner Port, Volumes, Env, `security_opt`).
2. Ordner `apps/<id>/` anlegen, `config.json` nach `apps/nginx`-Schema schreiben
   (`id` = Ordner, `port` frei z. B. 88xx, `dynamic_config: true`, `amd64` wenn x86-Image).
3. `docker-compose.yml` im Nginx-Label-Stil schreiben:
   `ports: ["${APP_PORT}:<intern>"]`, Volume `${APP_DATA_DIR}/data:/<container-pfad>`,
   Env aus `form_fields` (`${VAR:-default}`), Netzwerk `tipi_main_network`, Traefik-Labels kopieren.
4. `metadata/description.md` + `metadata/logo.jpg` (512×512) anlegen.
5. Lokal validieren: `python3 -c json.load(config.json)` + `docker compose config`.
6. Pushen → Store-Update in Runtipi → Install testen.

Details: `.project-docs/runtipi-git-install.md`, Skill: `.opencode/skills/runtipi-git-install/SKILL.md`.
