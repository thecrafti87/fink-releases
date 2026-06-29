# 🐦 Fink — Installationsanleitung (Windows)

> Diese Anleitung führt dich Schritt für Schritt durch die Installation. Du
> brauchst **kein Vorwissen**. Für die meisten reichen **Schritt 1–3**.

---

## Überblick: Was wird installiert?

| Was | Wozu | Pflicht? | Größe |
|---|---|---|---|
| **Fink** | das Programm selbst | ✅ ja | ~200 MB (CPU) / ~1,5 GB (GPU) |
| **Ollama** | die lokale KI (Diktat-Aufbereitung + Agent), läuft offline | ⭐ empfohlen | ~700 MB + Modell |
| **Ein KI-Modell** | das „Gehirn" für Ollama | ⭐ empfohlen | 2–9 GB je nach Modell |

> **Ohne Ollama** funktioniert das reine Diktat (Sprache → Text) trotzdem. Die
> Aufbereitung/der Agent brauchen entweder **Ollama (lokal)** *oder* einen
> **Cloud-Anbieter** (Claude/ChatGPT/Gemini) mit eigenem Schlüssel — siehe
> [Schritt 4](#4-ki-einrichten-ollama-lokal-oder-cloud).

---

## 1. Fink herunterladen

1. Öffne die Download-Seite: **<https://github.com/thecrafti87/fink-releases/releases/latest>**
2. Lade unter **„Assets"** das passende Paket:

   | Dein Rechner | Datei |
   |---|---|
   | Windows **ohne** NVIDIA-Grafikkarte | `Fink-windows.zip` |
   | Windows **mit** NVIDIA-Grafikkarte (schneller) | `Fink-windows-cuda.zip` |
   | macOS (Apple Silicon) | `Fink-macos.zip` |

   *Nicht sicher? Nimm `Fink-windows.zip` — das läuft überall.*

## 2. Entpacken & starten

1. Rechtsklick auf die ZIP → **„Alle extrahieren …"**.
2. Öffne den entpackten Ordner und starte **`Fink.exe`** (Doppelklick).
3. **Windows-Warnung „Der Computer wurde geschützt"?** Das ist normal (die App ist
   noch nicht signiert): **„Weitere Informationen" → „Trotzdem ausführen"**.
4. Fink öffnet **kein großes Fenster**, sondern lebt als **Vogel-Symbol unten
   rechts** in der Taskleiste (ggf. auf den kleinen Pfeil `^` klicken). Ein
   Einrichtungs-Assistent startet automatisch.

## 3. Mikrofon erlauben

Beim ersten Diktat fragt Windows nach dem Mikrofon → **Zulassen**. Falls nicht:
**Windows-Einstellungen → Datenschutz → Mikrofon** → für Desktop-Apps aktivieren.

---

## 4. KI einrichten (Ollama lokal **oder** Cloud)

Fink kann die Aufbereitung/den Agent auf zwei Wegen betreiben — **du entscheidest**:

### Variante A — Ollama (lokal, kostenlos, offline) — empfohlen

1. Im Einrichtungs-Assistenten auf **„Ollama jetzt installieren"** klicken.
   **Klappt das nicht automatisch?** → installiere es selbst:
2. Lade Ollama hier: **<https://ollama.com/download>** → **„Download for Windows"**.
3. Starte `OllamaSetup.exe` und klick durch (Weiter → Weiter → Fertig). Ollama läuft
   danach unsichtbar im Hintergrund.
4. Zurück in Fink: im Assistenten **„Erneut prüfen"** klicken — Fink findet Ollama
   jetzt und schlägt ein passendes **Modell** vor (lädt es per Knopfdruck).

   *Modell-Empfehlung:* ohne starke Grafikkarte ein kleines Modell (z. B.
   `qwen2.5:3b`), mit NVIDIA/Apple Silicon gern größer (`qwen2.5:7b`/`14b`).
   Du kannst Modelle jederzeit unter **Einstellungen → KI → Modelle** wechseln.

### Variante B — Cloud (Claude, ChatGPT, Gemini …)

Kein lokales Modell nötig, dafür brauchst du einen eigenen API-Schlüssel:

- **Anthropic Claude:** <https://console.anthropic.com/> → API Keys
- **OpenAI (ChatGPT):** <https://platform.openai.com/api-keys>
- **Google Gemini:** <https://aistudio.google.com/app/apikey>

Den Schlüssel trägst du in **Einstellungen → KI → Modelle** ein (er wird sicher im
Windows-Schlüsselbund gespeichert, nicht im Klartext). Hinweis: Cloud-Anbieter
sehen deine Anfragen — fürs reine Lokal-Setup nimm **Variante A**.

---

## 5. Loslegen

- **Diktieren:** die Diktat-Taste **gedrückt halten**, sprechen, loslassen → der
  Text erscheint, wo dein Cursor steht. (Welche Taste das ist, zeigt die
  Startseite; Standard frei wählbar unter **Einstellungen → Hotkeys**.)
- **Fragen/Recherche, To-Dos, Zeiterfassung, Notizen, Teleprompter:** alles über
  das Vogel-Symbol bzw. das Hauptfenster erreichbar.

---

## ❓ Probleme & Lösungen

| Problem | Lösung |
|---|---|
| **„Ollama jetzt installieren" tut nichts / Fehler** | Lade Ollama manuell von <https://ollama.com/download>, installiere es, dann in Fink **„Erneut prüfen"**. |
| **SmartScreen blockt `Fink.exe` oder den Ollama-Installer** | „Weitere Informationen" → „Trotzdem ausführen". (Beide sind unsigniert, aber unbedenklich.) |
| **Diktat funktioniert, aber Text wird nicht aufbereitet** | Es fehlt die KI: Ollama installieren (Variante A) **oder** Cloud-Schlüssel eintragen (Variante B). |
| **Antivirus/Firmen-Firewall blockt den Download** | Die Datei manuell im Browser von der jeweiligen Seite laden. |
| **Kein Mikrofon erkannt** | Windows-Einstellungen → Datenschutz → Mikrofon erlauben; in Fink unter **Einstellungen → Mikrofon & STT** das richtige Gerät wählen. |

---

## 🔄 Updates & 🔒 Datenschutz

- **Updates:** Fink prüft selbst auf neue Versionen und bietet sie im
  Taskleisten-Menü als **„Update + Neustart"** an (Windows: vollautomatisch).
- **Datenschutz:** Deine Stimme wird **lokal** in Text umgewandelt. Was (wenn
  überhaupt) nach außen geht und wie du es nachprüfst, steht in
  **[datenschutz.md](datenschutz.md)** — inkl. einem **Offline-Modus**, der jede
  Internet-Verbindung abschaltet.

*Stand: Beta. Fragen? Gerne melden — Rückmeldungen sind in der Beta sehr willkommen. 🙌*
