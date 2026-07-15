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
- [ ] **DNS**: puntare `relaquantix.com` e `www` alla VPS (record A) — gestito lato Coolify/altra sessione.
- [ ] **SSL**: certificato Let's Encrypt automatico via Coolify.
- [ ] **Revisione legale**: far controllare `privacy.html` e `note-legali.html` da un professionista prima di considerarle definitive.
- [ ] **Privacy per l'app**: prima della submission su App Store, estendere `privacy.html` con la sezione sui dati trattati dall'app.
- [ ] **Hosting/dati**: verificare la region del data center Hostinger e allineare la frase sui trasferimenti extra-UE nella privacy.
- [ ] (Opzionale) Upgrade tipografico con web font self-hosted per un tocco ancora più premium.
- [ ] (Opzionale) Immagine `og:image` 1200×630 per anteprime social.

## Storico
- 15/07/2026 — Prima versione completa del sito (direzione B), pronta per il deploy.
