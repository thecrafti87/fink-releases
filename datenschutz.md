# 🔒 Fink — Datenschutz & Netzwerk-Transparenz

> Diese Seite erklärt **genau**, was Fink auf deinem Rechner tut, wann es (wenn
> überhaupt) ins Internet geht und **wie du das selbst nachprüfen kannst** — ohne
> uns einfach glauben zu müssen.

---

## Das Wichtigste in einem Satz

**Deine Stimme und deine Texte werden auf deinem Gerät verarbeitet.** Die
Spracherkennung und das lokale Sprachmodell brauchen **kein Internet**. Fink
enthält **keine Telemetrie, kein Analytics, kein Tracking** — nichts läuft im
Hintergrund zu uns.

---

## Prüf es selbst (der beste Beweis)

Du musst uns nicht vertrauen — du kannst es **messen**:

### 1. Der Firewall-Test (2 Minuten)

1. Öffne die **Windows Defender Firewall** → „Erweiterte Einstellungen" →
   „Ausgehende Regeln" → „Neue Regel".
2. Sperre für `Fink.exe` **alle ausgehenden Verbindungen** (oder zieh einfach
   den Netzstecker / schalte WLAN aus).
3. **Diktiere etwas.** Es funktioniert weiter.

> Würde Fink deine Stimme an einen Server schicken, könnte es das jetzt nicht.
> Der Test beweist: Diktat, Spracherkennung und das lokale LLM laufen **ohne
> Internet**.

### 2. Live mitschauen, wohin Fink verbindet

Installiere einen Netzwerk-Monitor und beobachte Fink in Echtzeit:

- **Windows:** GlassWire, TCPView (Microsoft Sysinternals) oder der eingebaute
  **Ressourcenmonitor** → Tab „Netzwerk".
- **macOS:** Little Snitch oder LuLu.

Beim reinen Diktieren siehst du **keine** Verbindung nach außen.

### 3. Der eingebaute Offline-Modus

In **Einstellungen → Privatsphäre** (oder im Tray-Menü) gibt es einen Schalter
**„🔒 Offline-Modus"**. Ist er an, **blockt Fink jede Außenverbindung** technisch
selbst — und protokolliert sichtbar jeden (versuchten) Internet-Zugriff. So
siehst du schwarz auf weiß, ob und wann Fink online geht.

---

## Was Fink (wann) nach außen sendet — vollständig

Wir behaupten **nicht** „nichts verlässt je den Rechner" — das wäre falsch und
beim ersten Wireshark-Blick widerlegt. Ehrlich ist diese Liste:

| Verbindung | Wann | Was wird gesendet |
|---|---|---|
| **Spracherkennung (Stimme → Text)** | immer | **nichts** — 100 % lokal |
| **Lokales LLM (Ollama, Standard)** | immer | **nichts** — läuft auf `localhost` |
| **Update-Prüfung** | im Hintergrund | nur die Frage „gibt es eine neue Version?" an GitHub — **keine Nutzerdaten**, nur App-Name + Versionsnummer |
| **Web-Recherche** | nur wenn der Agent sucht | die Suchanfrage (an DuckDuckGo) + Abruf der Trefferseiten |
| **Cloud-KI** (Claude, GPT, Gemini …) | **nur wenn du selbst** einen Anbieter + eigenen Schlüssel einträgst | dein Prompt (das ist der Zweck) |
| **Modell-/Stimmen-Download** | einmalig, auf deine Aktion | nichts Persönliches (lädt nur das Modell bzw. die TTS-Stimme) |
| **Home Assistant** | nur Einkauf-Modus, wenn eingerichtet | nur in deinem **lokalen Heimnetz** |

**Standard-Installation:** Diktat, Textbearbeitung, Spracherkennung und das
lokale LLM laufen ohne Internet. Alles Cloud-seitige ist **opt-in** und sichtbar
— es passiert nur, wenn du einen Anbieter samt Schlüssel selbst hinterlegst.

---

## Keine versteckten Kanäle

- **Keine Telemetrie / kein Analytics / kein Crash-Reporting-SDK.** Es gibt keine
  Mitschnitt- oder Nutzungsdaten, die irgendwohin gesendet werden.
- **Kein Konto, keine Anmeldung.** Fink funktioniert ohne Login.
- **Die Update-Prüfung sendet keine persönlichen Daten** — sie fragt nur die
  öffentliche GitHub-Releases-Liste ab (wie jeder Browser, der die Seite öffnet).
  Sie lässt sich mit dem Offline-Modus komplett abschalten.

---

## Für technische Prüfer (Code-Audit)

Der Quellcode ist überschaubar, und **alle** Netzwerk-Stellen sind an einer Hand
abzuzählen — sie laufen über `httpx` bzw. `urllib` und sind im Code klar benannt
(`fink/websearch.py`, `fink/updater.py`, `fink/llm_providers/*`,
`fink/tts_backends/piper.py`). Der zentrale **Netzwerk-Wächter**
(`fink/netguard.py`) ist der eine Punkt, der entscheidet, ob eine Außenverbindung
überhaupt zustande kommt, und der jeden Zugriff protokolliert.

Auf Anfrage geben wir vertrauenswürdigen Prüfern **Lese-Zugriff auf das
Code-Repository**, um jede dieser Stellen selbst zu kontrollieren.

---

## Ehrlich zu den Grenzen

Wir können nicht *mathematisch garantieren*, dass nirgends ein Fehler steckt —
das kann **keine** Software, auch keine von großen Firmen. Aber: Es gibt **kein
Tracking**, die Netz-Verbindungen sind **wenige und benannt**, du kannst per
**Offline-Modus jede Außenverbindung erzwingen-abschalten**, und du kannst mit
einem Firewall- oder Monitor-Test **selbst messen**, dass beim Diktieren nichts
hinausgeht.

*Stand: Beta. Fragen zum Datenschutz sind ausdrücklich willkommen.*
