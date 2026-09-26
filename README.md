# Célkövető Naptár

Megtakarítási célkövető naptár + **átalányadós TB/szocho kalkulátor** (mellékállású egyéni vállalkozóknak). Egyetlen, önálló `index.html` webapp — a natív macOS/iOS verziók és a PWA is ezt a fájlt használja (egyetlen forrás, mindenhol szinkron).

## Funkciók

- **Célkövető naptár** — havi megtakarítási célok, hónapzárás, megtakarítási ráta, mérföldkövek, előrejelzés, kamat-projekció, streak.
- **Napi nézet** — megtakarítás / munkanap-bér / bérbeállítás módok, napi bérkövető sáv a fejlécben, hónap lezárása a ledolgozott keresettel.
- **Átalányadós kalkulátor** (TB + szocho):
  - Heti legalább 36 órás munkaviszony melletti (mellékállású) átalányadózó.
  - 45%-os általános költséghányad → a bevétel 55%-a számított jövedelem.
  - Éves, göngyölített adómentes jövedelmi keret: **1 936 800 Ft (2026)**; a keret feletti részre **TB 18,5% + szocho 13% (együtt 31,5%)**.
  - SZJA-t, IPA-t, könyvelési díjat nem számol (tájékoztatja a felhasználót).
  - Napi bontás (1–31 munkanap) és éves göngyölítés (12 hónap) táblázat.
  - Szerkeszthető „Ledolgozott óra összesen" mező; gyorsválasztás 5–22 munkanap; havi/éves mód.
- **Statisztika, előzmények, beállítások**, JSON/CSV export-import.
- **Offline PWA** — kezdőképernyőről indítható, lejárat és fejlesztői mód nélkül.

## Platformok

| Verzió | Útvonal | Build |
|---|---|---|
| Web / PWA | `pwa-site/` (ez a repo) | `scripts/build-pwa.sh` + push |
| macOS app | `macapp/` | `macapp/build.sh` |
| iOS app | `iosapp/` | `iosapp/build.sh` (Xcode kell) |

Mindegyik ugyanazt az `index.html`-t használja: a PWA a `pwa-site/index.html`-be másolja, a natív appok közvetlenül a gyökérből.

## PWA használata (telefonon)

1. Nyisd meg a Pages-címet a Safari-ban: `https://madaro-kaputto.github.io/goaltracker-pwa/`
2. **Megosztás → Hozzáadás a kezdőképernyőhöz** → app-ikon.
3. Offline, fix nézet, zoom-mentes — nincs 7 napos lejárat, nincs Developer Mode.
4. Frissítéshez: `./scripts/deploy-pwa.sh`, majd a telefonon egyszer újratöltés.

## Frissítés / telepítés

```bash
./scripts/deploy-pwa.sh   # PWA: másolás + commit + push (Pages automatikusan újraépül)
macapp/build.sh           # macOS app → build/Célkövető Naptár.app
iosapp/build.sh           # iOS build (szimulátor), fizikai eszközhöz Xcode kell
```

## Tesztek

```bash
npm test      # unit tesztek a kalkulátor-logikára és a napi/hónapzárás logikára (60+ check)
npm run syntax # inline script szintaxis-ellenőrzés
```

A számítási logika tiszta, újrahasznosítható függvényekben él (`FLAT`, `flatCalc`, `flatDayRows`, `flatYearRows`), minden Ft-kerekített, nincs hardcode-olt eredmény.