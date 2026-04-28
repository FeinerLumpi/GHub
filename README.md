# Genesys Agent Script – iFrame Demo

Eine schlanke, statische HTML-Seite zum Einbetten als iFrame in **Genesys Cloud Agent Scripts**. Sie liest Kontextdaten (z. B. `interactionId`, `ani`, `queue`, `agent`) aus URL-Parametern und stellt sie übersichtlich dar.

> ⚠️ **Hinweis:** Dieses Projekt dient ausschließlich Test- und Demonstrationszwecken. Für den Produktivbetrieb (Authentifizierung, Datenschutz, API-Integration) ist eine eigene Implementierung notwendig.

## Zweck

- Schnelles Prototyping einer iFrame-Komponente in Genesys Cloud Agent Scripts
- Anzeige von Interaktionskontext aus URL-Parametern
- Beispiel für eine Aktion (Button → `console.log` und Toast)
- Vorlage für eigene Erweiterungen

## Live-Demo

Nach Aktivierung von GitHub Pages (siehe unten) erreichbar unter:

```
https://feinerlumpi.github.io/GHub/
```

## Nutzung in Genesys Cloud Agent Scripts

1. **Web-Komponente** im Script Designer hinzufügen (z. B. `Web Page` / `Iframe`).
2. **URL** auf die GitHub-Pages-Adresse setzen und Script-Variablen einbinden:

   ```
   https://feinerlumpi.github.io/GHub/?interactionId={{Scripter.Interaction Id}}&ani={{Scripter.ANI}}&queue={{Scripter.Queue Name}}&agent={{Scripter.Agent Name}}
   ```

   Die Platzhalter in geschweiften Klammern sind Beispiele für Genesys-Cloud-Variablen und werden zur Laufzeit ersetzt.

3. Beim Öffnen einer Interaktion zeigt die iFrame-Komponente die übergebenen Werte an.

### Unterstützte URL-Parameter

| Parameter       | Beschreibung                                |
| --------------- | ------------------------------------------- |
| `interactionId` | Eindeutige Kennung der aktuellen Interaktion |
| `ani`           | Rufnummer / Identität des Anrufers           |
| `queue`         | Aktive Warteschleife                         |
| `agent`         | Name oder ID des Agenten                     |

Nicht erkannte Parameter werden ignoriert.

## Projektstruktur

```
.
├── index.html      Komplette Seite (HTML, CSS und JS in einer Datei)
├── README.md       Diese Datei
└── LICENSE         MIT-Lizenz
```

## Technische Eigenschaften

- Reines statisches HTML, keine Build-Tools, keine Frameworks
- Keine externen Abhängigkeiten (CDN-frei)
- Responsives Layout (mobil bis Desktop)
- Light/Dark Mode automatisch über `prefers-color-scheme`
- iFrame-tauglich: kein `top`-Redirect, keine restriktiven Header
- URL-Parameter werden ausschließlich per `textContent` gesetzt (kein HTML-Injection-Vektor)

## GitHub Pages aktivieren

1. Im Repository auf **Settings → Pages**.
2. Bei **Source** den Branch `main` und Ordner `/ (root)` auswählen.
3. **Save** klicken.
4. Nach kurzer Wartezeit ist die Seite unter `https://<user>.github.io/<repo>/` erreichbar (siehe Hinweis oben in der Pages-Einstellung).

Alternativ per CLI:

```bash
gh repo edit --enable-pages --pages-branch main --pages-path /
```

## Lokal testen

Einfach `index.html` im Browser öffnen oder einen kleinen Webserver starten:

```bash
# Python
python -m http.server 8080

# Node
npx serve .
```

Anschließend `http://localhost:8080/?interactionId=abc&ani=+49301234567&queue=Support&agent=Erika` aufrufen.

## Lizenz

[MIT](./LICENSE) © 2026 FeinerLumpi
