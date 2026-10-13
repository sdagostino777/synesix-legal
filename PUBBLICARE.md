# Pagine legali di Synesix — come pubblicarle

Questa cartella contiene le pagine legali dell'app, in HTML statico. Non hanno risorse
esterne — un solo `style.css` accanto — quindi si aprono anche da `file://` e si possono
ospitare ovunque, senza build e senza dipendenze.

Servono perché **App Store Connect pretende un URL pubblico** per l'informativa sulla
privacy (obbligatorio in ogni localizzazione) e per l'URL di supporto. Le pagine dentro
l'app non bastano: Apple vuole poterle aprire dal browser.

---

## I file

Per **ognuna delle cinque lingue** (it, en, es, de, fr) ci sono quattro pagine. L'italiano
non ha suffisso; le altre lingue hanno il codice ISO.

| Lingua | Privacy | Termini | Avvertenza | Indice |
| :--- | :--- | :--- | :--- | :--- |
| Italiano | `privacy.html` | `terms.html` | `disclaimer.html` | `index.html` |
| Inglese | `privacy.en.html` | `terms.en.html` | `disclaimer.en.html` | `index.en.html` |
| Spagnolo | `privacy.es.html` | `terms.es.html` | `disclaimer.es.html` | `index.es.html` |
| Tedesco | `privacy.de.html` | `terms.de.html` | `disclaimer.de.html` | `index.de.html` |
| Francese | `privacy.fr.html` | `terms.fr.html` | `disclaimer.fr.html` | `index.fr.html` |

Più `style.css`, condiviso da tutte le pagine, e questo `PUBBLICARE.md`.

Ogni pagina ha in fondo il collegamento alle altre tre della **stessa lingua** e alle
lingue alternative: chi arriva dalla scheda tedesca resta in tedesco.

**Il link all'EULA di Apple** (`https://www.apple.com/legal/internet-services/itunes/dev/stdeula/`)
sta nella sezione 11 dei *termini* di tutte e cinque le lingue. Non è decorativo: la stessa
voce deve comparire **anche nella Descrizione** della scheda App Store, altrimenti la
revisione si ferma (linea guida 3.1.2). È il rifiuto già preso una volta su un'altra app
dello stesso sviluppatore: non rimuoverlo.

**I prezzi e il rinnovo** stanno nella sezione 7 dei *termini*, in tutte e cinque le lingue.
Dal 13 ottobre 2026 il PRO ha **due** prodotti, non più uno: l'acquisto una volta sola
(69,99 €) e l'abbonamento annuale con rinnovo automatico (24,99 € all'anno). La sezione 6
dice che il piano gratuito non ha limiti e non scade e che tutti i valori si vedono sempre;
la sezione 7 dice prezzi, rinnovo, disdetta e rimborsi. Se cambia uno dei due prezzi, o la
periodicità, vanno aggiornate **cinque** pagine (`terms.*`), più le due voci in `index.*`
che rimandano ai termini.

---

## Dove pubblicarle: GitHub Pages

È il modo già collaudato sull'altra app dello stesso sviluppatore, che ha un repository
dedicato alle sole pagine legali. Per Synesix si fa la stessa cosa, con un repository
separato — così le pagine legali hanno una storia di modifiche propria e non si mescolano
al codice dell'app.

1. Crea un repository **pubblico** chiamato `synesix-legal` sull'account GitHub dello
   sviluppatore (`sdagostino777`).
2. Da questa cartella:

   ```bash
   cd /Users/simonedagostino/Documents/DeepSeek/APP/Synesix/Store/legal
   git init
   git add .
   git commit -m "Pagine legali di Synesix"
   git branch -M main
   git remote add origin https://github.com/sdagostino777/synesix-legal.git
   git push -u origin main
   ```

3. Su GitHub: **Settings → Pages → Source: Deploy from a branch → Branch: `main` /
   `/ (root)` → Save**. Dopo un minuto le pagine rispondono.
4. Gli indirizzi diventano:

   ```
   https://sdagostino777.github.io/synesix-legal/            → index.html (italiano)
   https://sdagostino777.github.io/synesix-legal/privacy.html
   https://sdagostino777.github.io/synesix-legal/privacy.en.html
   ```

   e così via per le altre lingue.

Gli aggiornamenti si fanno con un commit: Pages ricostruisce da solo. HTTPS è incluso e
non c'è niente da pagare.

### Le alternative

- **Netlify o Cloudflare Pages** — si trascina la cartella nel browser e si ottiene l'URL.
  Utile se in seguito si vuole collegare un dominio proprio.
- **Dominio proprio** — se un giorno esiste un sito di Simone D'Agostino, i file vanno in
  una sottocartella. L'unica cosa che conta è che gli URL rispondano in HTTPS.

---

## Cosa fare dopo la pubblicazione

1. **Apri ogni URL** e controlla che la pagina si veda con lo stile giusto (fondo scuro,
   testo leggibile): se il CSS non carica, il percorso di `style.css` è sbagliato.
2. **Sostituisci i segnaposto** nei file di `Store/metadata/` con gli indirizzi veri.
   Finché restano segnaposto, la scheda **non si può inviare**.
3. **In App Store Connect**, nella scheda della versione, compila *URL di supporto* e
   *URL per l'informativa sulla privacy* **per ciascuna delle cinque localizzazioni**,
   usando la pagina della lingua corrispondente (non l'inglese per tutte).
4. Aggiorna la data in cima alle pagine quando cambi qualcosa di sostanziale.

---

## Prima di pubblicare: tre controlli

- L'indirizzo postale nei documenti è `Calle Ollerías 20, 29012 Málaga, Spagna`: deve
  corrispondere a quello dichiarato all'Apple Developer Program e alla normativa DSA.
  Se cambia, va aggiornato in **dieci** pagine, non venti: compare solo in `privacy.*` e
  `terms.*`, in tutte e cinque le lingue. In `index.*` e `disclaimer.*` non c'è, ed è
  corretto così — il titolare si dichiara dove si parla di trattamento dei dati e di
  condizioni d'uso, non in una pagina di indice.
- L'email di contatto è `dagostino.simone@icloud.com`: è quella che risponde, e deve
  restare valida per tutto il tempo in cui l'app è in vendita.
- I due prezzi nelle pagine — **69,99 € una volta sola** (`com.dagostinosimone.synesix.premium.lifetime`)
  e **24,99 € all'anno** (`com.dagostinosimone.synesix.premium.annual`) — e la frase sul rinnovo
  automatico con disdetta **almeno 24 ore prima** devono restare identici ai prezzi configurati
  in App Store Connect e alla Descrizione della scheda: la linea guida 3.1.2 confronta le tre
  cose, e un prezzo diverso fra pagina e scheda è un rifiuto. Le pagine dicono che i prezzi sono
  IVA inclusa e che possono cambiare per i nuovi acquisti; per gli abbonamenti in corso valgono
  le regole di Apple sulla comunicazione delle variazioni di prezzo. Se un prezzo cambia, si
  aggiornano **cinque** pagine (`terms.*`), non venti.
- I termini dicono che l'app **non è un dispositivo medico**, che i dati restano sul
  dispositivo e che l'app **non fa richieste di rete**: se un giorno il comportamento
  dell'app cambia, queste pagine vanno riscritte **prima** di pubblicare la versione
  nuova, non dopo.

---

## Una differenza da Emycra, e va tenuta presente

Le pagine di Synesix nominano **un solo numero di emergenza**, non un elenco di linee di
ascolto. È una decisione di Simon del 9 ottobre 2026, spiegata in `CrisisProtocol.swift` e
in `../SPECIFICHE.md` §3.1-bis: l'app non tiene un registro di linee di ascolto, perché
cambiano numero, gestore e orari, e un numero verificato una volta e mai più ricontrollato
è una bugia con la data sopra. Il numero di emergenza invece non invecchia.

Nelle sezioni legali che parlano di questo, l'elenco da riportare è quello dei **numeri di
emergenza** dei quattro paesi dell'app: in Italia il 112, negli Stati Uniti e in Canada il
911, nel Regno Unito il 999, in Australia il 000.

Se qualcuno riscrive queste pagine, **non aggiunga linee di ascolto**: servirebbe anche il
campo per gli orari, il flag di verifica, la data di revisione e il modo di tenerli
aggiornati in cinque lingue.

---

## Nota sulla lingua

Le pagine sono scritte a mano in italiano, inglese, spagnolo, tedesco e francese. Se
modifichi una lingua, controlla le altre quattro: i documenti devono continuare a dire le
stesse cose, perché la revisione Apple confronta la descrizione della scheda con le pagine
collegate e con il comportamento reale dell'app.
