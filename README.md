# Veebiraamistike API

See on valmis Cloudflare Worker + D1 API. Muuda näidisandmed enda sündmusteks ja juuruta API oma Cloudflare'i kontole.

## 1. Paigalda

```bash
npm install
```

## 2. Asenda näidisandmed

Ava `migrations/0001_create_events.sql` ja asenda `INSERT INTO events` järel olevad näidisread oma sündmustega.

Pane sündmuste pildid kausta `public/images/`. Kirjuta andmetesse pildi tee kujul:

```text
/images/minu-pilt.webp
```

Vähemalt üks sündmus võib olla ilma pildita. Selle `image_url` väärtus on `NULL`.

## 3. Käivita kohapeal

```bash
npm run db:local
npm run dev
```

Ava <http://localhost:8787/api/events>.

## 4. Loo enda andmebaas

```bash
npx wrangler login
npx wrangler d1 create events-db
```

Kopeeri käsu väljundist `database_id` faili `wrangler.jsonc` rea `ASENDA_OMA_DATABASE_ID` asemele.

## 5. Juuruta

```bash
npm run db:remote
npm run deploy
```

Wrangler kuvab API aadressi. Kontrolli seda, lisades lõppu `/api/events`:

```text
https://events-api.SINU-ALAMDOMEEN.workers.dev/api/events
```

## Mida võib muuta?

Seminaris 3 muuda ainult:

- `migrations/0001_create_events.sql` sündmuste ridu;
- `public/images/` pilte;
- `wrangler.jsonc` välja `database_id`.

Ära muuda veel faili `src/index.ts`. API loomise, muutmise ja kustutamise lõpp-punkte kasutame seminaris 5.
