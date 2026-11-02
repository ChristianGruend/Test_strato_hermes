# Hermes Strato — Agent-Setup & Modell-Specs

Dieses Repo dokumentiert das Setup des Hermes-Agenten (Profil `qwen38`) und die
aktiven Modell-Parameter, mit denen dieser Agent läuft.

## Status (Stand: 02.11.2026)

| Punkt | Stand |
|---|---|
| Hermes Agent | ✅ läuft auf `buerozorin` |
| Modell | ✅ `qwen3.8-27b`, **voll lokal** — keine Cloud-API im Einsatz |
| Agent-Test | ✅ Erste README-Version hat der Agent selbst erstellt, committet und gepusht |
| GitHub-Anbindung | ✅ `gh` über das Terminal-Tool funktioniert (Commit + Push) |
| Nachbearbeitung | Status-Abschnitt und Provider-Angabe manuell ergänzt |

## Architektur

```
┌──────────────────────────────────────────────┐
│  Hermes Desktop App (GUI)                   │
│  └─ Profile: qwen38                         │
│     ├─ Skills      (prozedurales Wissen)    │
│     ├─ Memory      (persistente Fakten)    │
│     ├─ Tools       (terminal, browser, ...)│
│     └─ LLM Backend (lokal, qwen3.8-27b)    │
└──────────────────────────────────────────────┘
```

- **Runtime:** Hermes Agent (Nous Research), installiert unter `~/.hermes/hermes-agent/`
- **CLI:** `~/.local/bin/hermes`
- **Profil:** `qwen38` — lesbar/schreibbar unter `~/.hermes/profiles/qwen38/`
- **Host:** `buerozorin` (Linux, AMD RX 6700 XT)

## Aktives Modell

| Feld | Wert |
|---|---|
| Modellname | `qwen3.8-27b` |
| Provider | `custom` — lokaler Endpoint auf `buerozorin` |
| Parameter | Standard (Temperatur etc. nicht hier gesetzt) |
| Kontextfenster | ~128k Tokens (Qwen-3.8-27B-Klasse) |
| Sprache | Deutsch / Englisch (spiegelt Gesprächssprache) |

## Konfigurations-Prinzipien

- **Keine Secrets im Repo** — API-Keys leben in `~/.hermes/.env` und `auth.json`.
- **Skills-first:** wiederkehrende Workflows werden als Skills gepflegt, nicht als Chat-Historie.
- **Memory klein halten:** nur faktenbasierte, sitzungsübergreifende Notizen; prozedurales Wissen gehört in Skills.
- **Verifikation:** jede Aussage über Remote-Zustände (CI, Merges, Issues) wird mit frischen `gh`/API-Reads belegt.

## Werkzeuge (Auswahl)

| Tool | Zweck |
|---|---|
| `terminal` | Shell-Befehle, Foreground/Background |
| `browser_exec` | Browser-Automation (Browser Use CLI) |
| `web_search` / `web_extract` | Web-Research |
| `gh` (via terminal) | GitHub: Repos, PRs, Issues, CI |
| `skill_manage` | Skills erstellen/pflegen |
| `memory` | Persistente Fakten speichern |

## Hinweise

- Dies ist ein **Test-Repo** — es enthält keine produktiven Secrets oder Code.
- Änderungen an diesem Dokument: einfach commiten & pushen.
