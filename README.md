# Célkövető Naptár

Megtakarítási célkövető naptár és átalányadós TB/szocho kalkulátor — egyetlen `index.html` fájlban. A PWA, a macOS és az iOS verzió ugyanezt a fájlt tölti be; ez a repo a PWA-t szolgálja ki GitHub Pages-ről.

## Mit tud

- **Célkövetés havonta**: célösszeg, havi terv, hónapzárás, megtakarítási ráta, mérföldkövek, előrejelzés, kamatprojekció, sorozat (streak).
- **Napi nézet**: megtakarítás / munkanap-bér / bérbeállítás mód; a fejlécben napi bérkövető sáv; a hónap lezárható a ledolgozott keresettel.
- **Átalányadós kalkulátor** (mellékállású egyéni vállalkozó, TB + szocho):
  - Heti legalább 36 órás munkaviszony mellett értelmezett; ez alatt figyelmeztetést ad.
  - Általános költséghányad **45%** → a bevétel **55%-a** számított jövedelem.
  - Éves, göngyölített adómentes jövedelmi keret: **1 936 800 Ft (2026)**. A keret feletti részre **TB 18,5% + szocho 13%** (együtt 31,5%).
  - Alapértelmezések: **4 800 Ft/óra**, **8 h/nap**, **40 h** heti munkaviszony.
  - **Napi bontás (1–31 nap)** és **éves göngyölítés (12 hónap)** táblázat; szerkeszthető ledolgozott óraszám; havi/éves mód.
  - Nem számol SZJA-t, helyi iparűzési adót, könyvelési díjat, kamarai hozzájárulást — ezt a felület jelzi is.
- **Statisztika, előzmények, beállítások**, JSON/CSV export-import.

## Használat a telefonon (PWA)

A Pages-oldal: `https://madaro-kaputto.github.io/goaltracker-pwa/`

1. Nyisd meg a címet az iPhone Safari-jában.
2. **Megosztás → Hozzáadás a kezdőképernyőhöz.**
3. Ettől app-ikonról indul, **offline** működik — nincs 7 napos lejárat, nincs Developer Mode.

Az első megnyitás legyen online, hogy a service worker letöltse az offline másolatot.

## Platformok

| Verzió | Hol | Build |
|---|---|---|
| PWA (ez a repo) | GitHub Pages | `./scripts/deploy-pwa.sh` |
| macOS | `macapp/` | `macapp/build.sh` |
| iOS | `iosapp/` | `iosapp/build.sh` (Xcode kell) |

Mindegyik ugyanazt az `index.html`-t használja: a PWA másolat a `pwa-site/index.html`, a natív appok közvetlenül a gyökérből.

## Frissítés

```bash
./scripts/deploy-pwa.sh   # másolás + commit + push → Pages automatikusan újraépül
macapp/build.sh           # macOS app
iosapp/build.sh           # iOS build (szimulátor)
```

## Tesztek

```bash
npm test       # kalkulátor- és napi/hónapzárás logika (63 check)
npm run syntax # inline script szintaxis-ellenőrzés
```

A számítási logika külön függvényekben él (`flatCalc`, `flatDayRows`, `flatYearRows`); minden összeg forintra kerekített, nincs hardcode-olt eredmény.

## Struktúra

```
index.html       → az alkalmazás (markup + CSS + JS egy fájlban)
macapp/          → macOS WKWebView héj
iosapp/          → iOS WKWebView héj (Xcode projekt)
pwa-site/        → a Pages-deployolt PWA (ez a repo gyökere)
tests/           → node-alapú tesztek
scripts/         → deploy + szintaxis-ellenőrzés
```
