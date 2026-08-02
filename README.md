# portfolio.mumelter.org

Portfolio-Seite mit den Arbeitsproben von Svenja Mumelter.

Statische Seite, ausgeliefert als Cloudflare Worker mit Static Assets — gleiches
Muster wie `dashboard.mumelter.org` und `orbit.mumelter.org`.

## Aufbau

```
public/
  index.html                                   Die komplette Seite (Styles inline)
  assets/royalshrimp-logo.png                  Logo aus der Original-Slide, inkl. Alphamaske
  assets/royalshrimp-qr.png                    QR-Code aus der Original-Slide
  assets/fonts/*.woff2                         Cormorant Garamond + Lora, selbst gehostet
  Arbeitsprobe_1_RoyalShrimp_Svenja_Mumelter.pdf
  Arbeitsprobe_2_Cuply_Svenja_Mumelter.pdf     (noch zu ergänzen)
wrangler.jsonc                                 Worker-Konfiguration + Custom Domain
```

## Gestaltung

Der Kopfbereich bildet die Original-Slide „Arbeitsprobe RoyalShrimp.de" in Code
nach. Farben, Schriftgrößen und Rasterabstände sind aus der PDF ausgelesen; bei
1440 px Viewportbreite messen die Textblöcke exakt dieselben Werte wie im
Original (Fließtext 841 px, Linkkasten 786 px). Darunter folgen der
Shop-Walkthrough, die zweite Arbeitsprobe (Cuply) und der Kontaktblock in
derselben Gestaltung.

Die Schriften liegen als woff2 im Repo, statt über Google Fonts eingebunden zu
werden. Eingebettete Google Fonts übertragen die IP der Besucher ohne
Einwilligung an Google (LG München I, 3 O 17493/20) — auf einer Bewerbungsseite
ein unnötiges Risiko.

## Verlinkte Dateien

Die Download-Buttons zeigen exakt auf diese beiden Dateinamen. Nicht umbenennen,
sonst brechen die Links:

- `Arbeitsprobe_1_RoyalShrimp_Svenja_Mumelter.pdf`
- `Arbeitsprobe_2_Cuply_Svenja_Mumelter.pdf`

Fehlt eine der beiden PDFs auf dem Server, greift der in `data-fallback`
hinterlegte Link (Google Drive). Gibt es keinen, schaltet die Seite den Button
auf „folgt in Kürze", statt ins Leere zu verlinken.

**Cloudflare erlaubt maximal 25 MiB pro einzelner Asset-Datei.** Größere PDFs
vorher komprimieren oder über Drive verlinken.

## Video

Der Shop-Walkthrough (81 MB, zu groß fürs Selbsthosten) liegt auf Google Drive
und wird erst beim Klick geladen — vorher geht keine Anfrage an Google raus.

Das Umstellen auf ein unlisted YouTube-Video sind zwei Attribute am Play-Button
in `public/index.html`:

```html
data-provider="youtube"
data-video-id="<YouTube-ID>"
```

## Lokal ansehen

```sh
npm install
npm run dev
```

## Deployen

Der Deploy läuft über die Git-Integration von Cloudflare Workers: Ein Push auf
`main` baut und veröffentlicht automatisch.

Manuell geht es mit einem Cloudflare-API-Token:

```sh
npx wrangler deploy
```
