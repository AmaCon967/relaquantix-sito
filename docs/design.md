# Sito Relaquantix — decisioni di design e note operative

Documento di sintesi del progetto: cosa è stato deciso, i dati usati e i punti
ancora da chiudere. Fa da spec e da promemoria operativo.

## Obiettivo
Sito aziendale ufficiale di **Relaquantix S.r.l.** su `relaquantix.com`, da usare
come sito da collegare all'iscrizione **Apple Developer Program come organizzazione**.
Doppio uso: presenza aziendale + pagine legali che coprono i requisiti App Store
(Privacy Policy URL = `privacy.html`, Support URL = `supporto.html`).

## Decisioni
| Ambito | Scelta |
|---|---|
| Struttura | One-page (`index.html`) + pagine legali/supporto |
| Lingua | Italiano (predisposto per aggiungere `/en/` in futuro) |
| Tecnologia | HTML/CSS/JS statico, zero build, zero dipendenze |
| Direzione visiva | **B · Luce editoriale** — avorio, indaco + oro antico, serif |
| Font | Sistema: Baskerville/Georgia (titoli) + system-ui (testo). Nessun font esterno (GDPR-clean) |
| Cookie/analytics | Nessuno → nessun banner cookie |
| Deploy | Coolify (build pack Static) su VPS Hostinger |
| Repo | GitHub pubblico `AmaCon967/relaquantix-sito` |

### Palette (direzione B)
- Avorio `#f6f2e9` / carta `#fffdf8`
- Inchiostro `#1a1b22`
- Indaco `#26306b` (accento primario)
- Oro antico `#a87b22` / `#c19233` (accento secondario)
- Hairline `#e3dccb`

### Concept di marca
Rela + Quantix = relatività + quantistica. In assenza di una teoria del tutto
che unisca le due grandi teorie della fisica, l'azienda le unisce nel proprio nome.
Filo conduttore visivo: motivo "orbita" (ellissi + nodo).

## Dati legali (da Visura CCIAA Sud Est Sicilia, 24/10/2024)
- Denominazione: **Relaquantix S.r.l.**
- Sede legale: Viale della Regione 77, 95040 Motta Sant'Anastasia (CT)
- P.IVA / C.F.: 06106470872 — REA CT-467450
- Capitale sociale: € 20.000,00 interamente versato
- PEC: relaquantix@pec.it
- Costituzione: 04/06/2024 — iscrizione 14/06/2024
- Amministratore Unico: rappresentante con pieni poteri (nome NON pubblicato sul sito — scelta voluta, non richiesto da Apple)
- D-U-N-S: 508186135

## Contenuti
Home: hero → L'azienda (visione + storia del nome + esperienza trentennale del
fondatore, senza nome) → Cosa facciamo (4 divisioni: e-commerce/abbigliamento,
app mobili [generico], editoria, formazione) → Contatti → footer legale (art. 2250 c.c.).

**Nota:** l'app specifica (Roma Aeterna) NON è mostrata finché non è pubblicata sugli
store — decisione presa per non anticiparla. La divisione "App per dispositivi mobili"
resta generica. A pubblicazione avvenuta si aggiunge una sezione showcase con i link store.

## Punti aperti / TODO operativi
- [ ] **Creare le caselle email** `info@relaquantix.com` e `supporto@relaquantix.com` su Hostinger (il sito le usa già ovunque).
- [x] **DNS**: `relaquantix.com` e `www` puntano alla VPS. ✅ 16/07/2026
- [x] **SSL**: Let's Encrypt attivo, scade 13/10/2026 con rinnovo automatico. ✅ 16/07/2026
- [x] **Deploy automatico** dal push. ✅ 16/07/2026 — vedi sezione sotto
- [ ] **Revisione legale**: far controllare `privacy.html` e `note-legali.html` da un professionista prima di considerarle definitive.
- [ ] **Privacy per l'app**: prima della submission su App Store, estendere `privacy.html` con la sezione sui dati trattati dall'app.
- [ ] **Hosting/dati**: verificare la region del data center Hostinger e allineare la frase sui trasferimenti extra-UE nella privacy.
- [ ] (Opzionale) Upgrade tipografico con web font self-hosted per un tocco ancora più premium.
- [ ] (Opzionale) Immagine `og:image` 1200×630 per anteprime social.

## Deploy automatico (webhook GitHub → Coolify)

Ogni push su `main` ri-pubblica il sito da solo, in ~25 secondi. La catena è:
`git push` → webhook GitHub → Coolify verifica la firma → build → live.

Configurazione attiva:
- **Webhook GitHub** (repo → Settings → Webhooks): URL
  `https://coolify.ordinaryangels.cloud/webhooks/source/github/events/manual`,
  content type `application/json`, solo evento `push`.
- **Coolify**: `Auto Deploy` acceso (Configuration → Advanced) e **secret** impostato
  in Configuration → Webhooks → *GitHub Webhook Secret*.

⚠️ **Trappola da ricordare:** con il build pack "Public Repository" il **secret è
obbligatorio e deve essere identico** nei due campi (Coolify e GitHub). Lasciarlo vuoto
da entrambe le parti **non** disattiva la verifica: Coolify calcola comunque la firma,
non trova quella di GitHub e scarta il push rispondendo `200` con
`{"status":"failed","message":"Invalid signature."}` — quindi **sembra funzionare
ma non fa nulla, senza errori visibili**.

Per diagnosticare, la risposta di Coolify si legge dal lato GitHub:
```
gh api repos/AmaCon967/relaquantix-sito/hooks --jq '.[0].id'
gh api repos/AmaCon967/relaquantix-sito/hooks/<id>/deliveries
gh api repos/AmaCon967/relaquantix-sito/hooks/<id>/deliveries/<delivery-id> --jq '.response.payload'
```

## Cache dei file statici — IMPORTANTE

Nginx serve CSS e JS senza header `Cache-Control`, quindi i browser li tengono in cache
a lungo. Per questo `index.html` e le altre pagine richiamano gli asset **con un numero
di versione**:

```html
<link rel="stylesheet" href="/assets/css/style.css?v=2">
<script src="/assets/js/main.js?v=2" defer></script>
```

⚠️ **Ogni volta che modifichi `style.css` o `main.js`, incrementa `?v=` in TUTTE e quattro
le pagine** (`index`, `privacy`, `note-legali`, `supporto`). Se te ne dimentichi, i
visitatori che hanno già aperto il sito continuano a vedere la grafica vecchia mescolata
all'HTML nuovo — con risultati visibilmente rotti (è già successo: una colonna vuota nelle
statistiche dopo aver rimosso il capitale sociale).

## Storico
- 15/07/2026 — Prima versione completa del sito (direzione B), pronta per il deploy.
- 16/07/2026 — Sito online su relaquantix.com con HTTPS. Rimosso il capitale sociale
  dalle statistiche della home (resta nel footer per obbligo di legge).
  Attivato il deploy automatico dal push.
