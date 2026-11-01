# Next.js blueprint

Starting point for Next.js apps made with `dev --stack nextjs <name>` (claude-dev kit).
Same deploy contract as `seitenschwung/template` (port 8080, `/healthz`, `/version.txt`, hardened
image), shared pipeline `seitenschwung/template/.github/workflows/pipeline.yml@v1`. The deploy
setup (Coolify, secrets, `COOLIFY_APP_UUID`) is the one in the README of `seitenschwung/template`.

Replace this README with one about the project.

## Lokal starten

Voraussetzung: Node.js (22 oder neuer) und npm.

```bash
npm ci               # Abhängigkeiten installieren
npm run dev          # Dev-Server auf http://localhost:8080 (Port 8080, Host 0.0.0.0)
```

## Prüfen und testen

```bash
npm run lint         # ESLint und tsc --noEmit
npm test             # Vitest (einmaliger Lauf)
npm run build        # Produktions-Build (standalone)
```

Den Build lokal starten (ohne `PORT` und `HOSTNAME` lauscht der Server auf Port 3000 und dem Hostnamen der Maschine):

```bash
cp -r .next/static .next/standalone/.next/static
cp -r public .next/standalone/public
PORT=8080 HOSTNAME=0.0.0.0 node .next/standalone/server.js
```

Danach liefern `GET /healthz` (200) und `GET /version.txt` (Wert von `APP_VERSION`) die Deploy-Checks.
