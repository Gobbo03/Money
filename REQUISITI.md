# Da Niko Ortofrutta — Requisiti del progetto

App e sito per prenotare la spesa online, con consegna a domicilio o ritiro in negozio.
Risposte date dal titolare il 10/11/2026. Le voci marcate **[ipotesi]** sono scelte provvisorie
da confermare.

## 1. Il negozio
| # | Domanda | Risposta |
|---|---------|----------|
| 1 | Nome | **Da Niko ortofrutta**. Città e indirizzo: **da comunicare** |
| 2 | Punti vendita | Uno solo, per ora |
| 3 | Numero prodotti | Oltre 200 |
| 4 | Categorie | Tutte tranne i detersivi: frutta, verdura, latticini e uova, formaggi, salumi, pasta e riso, pane e forno, dispensa, bevande |
| 34 | Esempi a cui ispirarsi | Easy Coop, Esselunga e simili |

## 2. Tipo di app
| # | Domanda | Risposta |
|---|---------|----------|
| 5 | Sito o app negli store | Si parte da un **sito installabile sul telefono** (PWA). In futuro anche **Play Store e App Store** |
| 35 | Sito | Sì, anche un sito web (vetrina + negozio online) |
| 6 | Lingua | Solo italiano |

## 3. Clienti
| # | Domanda | Risposta |
|---|---------|----------|
| 7 | Dati richiesti | Nome, telefono, email; indirizzo solo per la consegna a domicilio |
| 8 | Accesso | Email e password, oppure Google |
| 9 | Approvazione | Nessuna: si registra chiunque |
| 18 | Tessera fedeltà / punti | No, per ora |

## 4. Prodotti e prezzi
| # | Domanda | Risposta |
|---|---------|----------|
| 10 | Unità di vendita | Sia al kg sia al pezzo |
| 11 | Prezzo dei prodotti a peso | Il prezzo finale si calcola **dopo la pesatura** in negozio |
| 12 | Prodotto mancante | Si **chiama il cliente** e si sostituisce solo se è d'accordo |
| 13 | Magazzino | Basta un interruttore **disponibile / esaurito** |
| 14 | Foto | Le scatta il negozio |

## 5. Offerte e stagionalità
| # | Domanda | Risposta |
|---|---------|----------|
| 15 | Offerte | Sconti e promozioni (es. caldarroste) |
| 16 | Prodotti di stagione | **Entrambi**: calendario stagionale automatico + scelta manuale |
| 17 | Notifiche ai clienti | Sì |

## 6. Consegna a domicilio
| # | Domanda | Risposta |
|---|---------|----------|
| 19 | Raggio | 10 km dal negozio |
| 20 | Termine ordini | Entro le 18 per il giorno stesso |
| 21 | Capacità | **4 consegne all'ora** |
| — | Costo consegna | **[ipotesi]** € 3,50, gratis sopra € 40, ordine minimo € 15 (modificabile dal pannello) |
| — | Giorni | **[ipotesi]** lunedì–sabato, domenica chiuso |

## 7. Ritiro in negozio
| # | Domanda | Risposta |
|---|---------|----------|
| 22 | Fasce e orari | Nessun limite di ritiri. Orari **8:00–13:00 e 15:30–19:30** (fasce da 30 minuti) |
| 23 | Termine ordini | Ore 18 |
| 24 | Modifica / annullamento | Possibile **finché il negozio non inizia a preparare** l'ordine |

## 8. Pagamenti
| # | Domanda | Risposta |
|---|---------|----------|
| 25 | Metodi | Carta online; alla consegna o al ritiro anche **contanti** (e POS) |
| 26 | Conto pagamenti | Da aprire (consigliato **Stripe**) |
| 27 | Documenti | Scontrino; **fattura** su richiesta (il cliente inserisce CF / P.IVA) |

Con carta e prodotti a peso: si **blocca** l'importo stimato + 10% e si addebita il totale esatto
dopo la pesatura (funzione standard di Stripe, "pre-autorizzazione").

## 9. Pannello negozio e fattorino
| # | Domanda | Risposta |
|---|---------|----------|
| 28 | Pannello | Tutto: ordini del giorno, lista per preparare, pesature, giro consegne, incassi, prodotti, offerte |
| 29 | Avviso nuovi ordini | Email + notifica |
| 30 | Ruoli | Titolare + **app per il fattorino** |

## 10. Aspetti pratici
| # | Domanda | Risposta |
|---|---------|----------|
| 31 | Dominio | Non ancora (da registrare, es. `daniko.it`) |
| 32 | Budget mensile | Basso |
| 33 | Tempi | Prima un **prototipo di prova** |

---

## Piano tecnico (proposta)
Scelto per costi bassi e per arrivare agli store senza riscrivere tutto.

- **Frontend:** un'unica app web (React o Vue) installabile come PWA. In seguito si impacchetta con
  **Capacitor** per Play Store e App Store, riusando lo stesso codice.
- **Backend:** **Supabase** (piano gratuito per partire): database, login email/password e Google,
  archivio foto prodotti.
- **Pagamenti:** Stripe (nessun canone, solo commissione per transazione).
- **Email:** Resend o simili (piano gratuito). **Notifiche:** web push dalla PWA.
- **Hosting:** Netlify / Vercel / Cloudflare Pages (gratuito) + dominio (~10–15 €/anno).
- **Tre interfacce, stesso sistema:** cliente, negozio (titolare), fattorino.
- **Costi fissi stimati all'inizio:** dominio + eventuale piano a pagamento solo quando cresce il traffico.
  Account sviluppatore: Google Play 25 $ una tantum, Apple 99 $/anno (solo quando si va negli store).

## Fasi
1. **Prototipo** (cartella `prototipo/`): funziona nel browser, i dati restano sul telefono di chi prova. ✅
2. **Versione 1:** backend reale, login vero, ordini condivisi tra cliente/negozio/fattorino, email, foto.
3. **Pagamenti con carta** (Stripe) e notifiche push.
4. **App negli store** (Capacitor).

## Da chiedere / confermare
- Indirizzo, città, telefono ed email del negozio (per sito, mappe e calcolo dei 10 km).
- Costo della consegna, soglia per la consegna gratis, ordine minimo.
- Giorni di apertura (domenica? festivi?) e se le consegne seguono gli stessi orari del negozio.
- Logo e colori, se esistono.
