# Trigger A6100 — versione WebUSB (senza Pi, senza Termux)

Questa versione fa scattare la Sony A6100 **direttamente dal browser del
telefono**, via WebUSB + web-gphoto2 (WebAssembly). Nessun Raspberry Pi,
nessun PC, nessun server locale — solo il telefono e un cavo USB-OTG.

--------------------------------------------------------------------
SETUP (una tantum)
--------------------------------------------------------------------

1. Scarica il file `coi-serviceworker.js` dalla fonte ufficiale — NON è
   incluso in questa cartella perché va servito così com'è, dalla stessa
   origine del sito, senza modifiche:

     https://raw.githubusercontent.com/gzuidhof/coi-serviceworker/master/coi-serviceworker.js

   Salvalo nella STESSA cartella di `index.html`.

   (Questo script serve solo per far funzionare SharedArrayBuffer su
   GitHub Pages, che non permette di impostare header di risposta
   personalizzati — è una libreria open source di terze parti, non
   scritta da me: la trovi qui per riferimento
   https://github.com/gzuidhof/coi-serviceworker)

2. Crea un repository pubblico su GitHub (es. "flash-trigger").

3. Carica in quel repository tutti i file di questa cartella, PIÙ il
   coi-serviceworker.js scaricato al punto 1:
     - index.html
     - manifest.json
     - icon-192.png
     - icon-512.png
     - icon-512-maskable.png
     - coi-serviceworker.js

4. Nel repository: Settings → Pages → Source → seleziona il branch
   principale (main/master) e la cartella "/ (root)" → Save.

5. Dopo un minuto o due, GitHub Pages ti dà un indirizzo tipo:
     https://<tuo-utente>.github.io/flash-trigger/

   Apri quell'indirizzo su Chrome per Android.

--------------------------------------------------------------------
USO
--------------------------------------------------------------------

1. Collega la A6100 al telefono con un cavo/adattatore USB-OTG.
2. Sulla fotocamera: Menu → Impostazioni USB → "Collegamento PC remoto".
3. Nell'app: menu ☰ → Fotocamera → "Connetti" → scegli la A6100 dal
   selettore USB nativo del browser.
4. Torna alla schermata Flash (o Intervallo / Alba-Tramonto), regola
   soglia/raffica/filtro scena dall'icona ⚙, premi ARMA.

--------------------------------------------------------------------
DIFFERENZE RISPETTO ALLA VERSIONE PI5
--------------------------------------------------------------------
- Statistiche, intervallo e alba/tramonto sono calcolati e salvati
  interamente sul telefono (localStorage), non più su un server —
  restano quindi legati a QUESTO telefono/browser specifico.
- Serve connessione internet al primo caricamento della pagina (per
  scaricare l'app da GitHub Pages e il modulo web-gphoto2 da CDN).
  Le sessioni successive possono beneficiare della cache del browser,
  ma non è garantito un funzionamento offline al 100% come con il
  Pi5 in modalità hotspot — se ti serve zero-internet garantito sul
  campo, quella resta l'opzione più solida.
- web-gphoto2 non è più mantenuto attivamente dai suoi autori (Google
  Chrome Labs ha archiviato il repository) — il codice funziona ancora,
  ma non aspettarti aggiornamenti futuri.
