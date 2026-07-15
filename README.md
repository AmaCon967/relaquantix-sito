# Sito aziendale Relaquantix S.r.l.

Sito vetrina statico di **Relaquantix S.r.l.** — `relaquantix.com`.

Serve come presenza aziendale ufficiale e come sito da collegare all'iscrizione
**Apple Developer Program** (come organizzazione). Le pagine legali coprono anche
i requisiti dell'App Store: `privacy.html` è la **Privacy Policy URL** e
`supporto.html` la **Support URL**.

## Tecnologia
HTML/CSS/JavaScript statico, **zero dipendenze** e zero build. Font di sistema
(Baskerville/Georgia + system-ui), nessun cookie di terze parti, nessun tracciamento.

## Struttura
```
index.html          Home one-page (hero, azienda, cosa facciamo, contatti)
privacy.html        Informativa privacy (GDPR)
note-legali.html    Note legali + cookie policy
supporto.html       Supporto (Support URL per Apple/App Store)
assets/css/style.css
assets/js/main.js   Menu mobile, reveal allo scroll, anno footer
assets/img/favicon.svg
robots.txt · sitemap.xml
docs/design.md      Decisioni di design, dati legali, note operative
```

## Deploy (Coolify)
Il sito è servito da **Coolify** sulla VPS:
`+ Add Resource → Public Repository →` questo repo `→ build pack Static →`
domini `relaquantix.com` + `www.relaquantix.com` `→ SSL → Deploy`.
Se il build pack "Static" chiede una *publish directory*, è la **root** del repo (`/`).

Ogni `git push` sul branch principale fa ri-pubblicare il sito automaticamente.

## Manutenzione
I dati legali nel footer sono ripetuti in tutte le pagine: se cambiano, aggiornali
in `index.html`, `privacy.html`, `note-legali.html`, `supporto.html`.
