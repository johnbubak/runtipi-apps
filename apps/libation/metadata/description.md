# Libation (Runtipi-App)

[Libation](https://getlibation.com/) (GPL, kostenlos) im Browser — Docker-Image
`ceramicwhite/libation` (KasmVNC, Chardonnay-Build). Die freie Alternative zu
OpenAudible für Audible-Hörbücher.

## Was die App tut

- Libation-GUI auf Port 3000 (Container) bzw. `${APP_PORT}` (Host, Default `8834`).
- Daten in `${APP_DATA_DIR}/data` (= `/config` im Container):
  - `Books/` — befreite Hörbücher (M4B/MP3)
  - `Libation/` — Settings, Datenbank, Logs
- Erster Start: Libation wird ggf. nachinstalliert/aktualisiert, dauert 1–2 Minuten.

## Audible → Audiobookshelf („mit allem drum und dran")

Zwei Wege, kombinierbar:

**A) Auto-Upload (empfohlen, per API):** In Libation unter
Settings → Audiobookshelf aktivieren, Server-URL `http://192.168.178.72:13378`
(API-Token aus ABS-Benutzereinstellungen). Jedes befreite Buch landet
automatisch in ABS. Details: <https://getlibation.com/docs/features/audiobookshelf>

**B) Geteilter Ordner (bereits verdrahtet):** `Books/` ist zusätzlich im
Audiobookshelf-Container unter `/libation` eingehängt (read-only,
user-config-Override). In ABS eine Library auf `/libation` zeigen → Scan.

## Hinweise

- Nur **ein Viewer gleichzeitig** (KasmVNC-Limit).
- `seccomp:unconfined` ist Pflicht (wie OpenAudible).
- Bei Audible einloggen erforderlich (eigenes Konto, in der Libation-GUI).
- Update: Image neu pullen + Restart, `Books/` + Settings bleiben erhalten.
