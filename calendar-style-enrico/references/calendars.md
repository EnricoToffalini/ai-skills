# Calendari di Enrico: ID, finalità, convenzioni

Account `enrico.toffalini@unipd.it`, fuso `Europe/Rome` per tutti i calendari.
Le convenzioni sono ricavate dagli eventi reali (aprile 2026 – inizio 2027).

## Come risolvere gli ID

- Il calendar ID da passare agli strumenti è la stringa `c_…@group.calendar.google.com`.
- Nelle impostazioni web di Google Calendar l'URL contiene lo stesso ID **codificato in base64**: `https://calendar.google.com/calendar/u/0/r/settings/calendar/<base64>`. Basta decodificare il base64 per riottenere l'ID.
- Se un ID non funziona: elencare i calendari dell'account con lo strumento disponibile e cercare per nome esatto (sotto). **Non usare mai `primary` come ripiego.**
- Nei dati importati il campo `organizer.displayName` può essere una sola lettera ("A", "U", "L", "D", "C"). È un residuo dell'importazione dell'11/09/2026, non un altro calendario.

## Calendari scrivibili (accessRole: owner)

### University
- **ID**: `c_37cc77e0dfd21ee92b0321aa17ff5563f76e2ee16d0ce1d61bb898a69f4901f6@group.calendar.google.com`
- **URL impostazioni (base64)**: `Y18zN2NjNzdlMGRmZDIxZWU5MmIwMzIxYWExN2ZmNTU2M2Y3NmUyZWUxNmQwY2UxZDYxYmI4OThhNjlmNDkwMWY2QGdyb3VwLmNhbGVuZGFyLmdvb2dsZS5jb20`
- **Promemoria predefinito**: popup 30 minuti.
- **Contenuto**: attività accademica non di docenza diretta, cioè riunioni di progetto (PRIN Carretti, DOR, LAG, Arcade), Lab Meeting, Psicostat meeting, HandZone, Comitato Etico, Collegio Docenti Dottorato, Consiglio Corso di Studi, gruppi di lavoro (semplificazione, data stewards, terza missione), incontri con laureandi e dottorandi, colloqui postdoc, interviste, workshop di altri.
- **Lezioni di colleghi: di regola non vanno in calendario.** Si inseriscono solo se Enrico deve esplicitamente presenziare (es. le lezioni TEMPS della collega Mioni "Lezione TEMPS introduttiva" e "TEMPS ultima lezione"). In quel caso vanno in University, perché Enrico non fa lezione.
- **Ricevimento** ricorrente: mercoledì 10:00–12:00, Zoom `https://unipd.zoom.us/j/5749565733`. Non duplicarlo.
- **Titoli**: `Meeting <persona/progetto/tema>` (es. "Meeting PRIN Carretti", "Meeting laureanda Giorgia Dore", "Meeting Cossovel Airipa"), oppure il nome dell'organo ("Comitato Etico", "Collegio Docenti Dottorato", "Lab Meeting", "Psicostat meeting", "HandZone <tema>").
- **Luogo**: il link Zoom/Meet/Teams se presente, altrimenti l'aula o l'edificio. La descrizione contiene ordine del giorno, relatori o link utili, se presenti.

### Lectures_Testing
- **ID**: `c_2c6f8ed8d81c943a18f8f5713f24db35fe09ff30790cf35b1575cab10978981e@group.calendar.google.com`
- **URL impostazioni (base64)**: `Y18yYzZmOGVkOGQ4MWM5NDNhMThmOGY1NzEzZjI0ZGIzNWZlMDlmZjMwNzkwY2YzNWIxNTc1Y2FiMTA5Nzg5ODFlQGdyb3VwLmNhbGVuZGFyLmdvb2dsZS5jb20`
- **Promemoria predefinito**: popup 20 minuti.
- **Contenuto**: tutto ciò in cui Enrico **conduce, insegna, esamina o presenta**: lezioni, esami, prove intermedie, commissioni di laurea, PPV e preparatorie, discussioni di dottorato (defense) in cui è commissario, talk e seminari su invito, lezioni nei master e nella formazione continua, simposi in cui interviene.
- **Supplenze** (Enrico supplente in commissioni di tesi, PPV, esami o altro): vanno qui, ma con **colore grigio** (`colorId = "8"`, Graphite) invece dell'arancione predefinito del calendario. È una distinzione importante.
- **Defense o discussioni a cui Enrico assiste soltanto** (non commissario): vanno in University (es. defense Irene Alfarone, 07/07/2026).
- **Titoli tipici osservati**:
  - lezioni: `Psicologia dell'Intelligenza Umana`, `Lezione TEMPS <argomento>` (es. "Lezione TEMPS Memory"), `Lezione Master DSA - Intelligenza`, `Lezione Intelligenza NeuroCare`, `Basics of Python for Data Science`;
  - esami: `Esame TEMPS General Psychology`, `Esame Psicologia Intelligenza (Umana)`, `TEMPS midterm exam`;
  - commissioni: `Commissioni Proclamatrici TEMPS`, `Commissioni Lauree Magistrali`, `Commissione PPV`, `Commissioni Preparatorie Triennali`, `Commissioni Tesi Magistrali`; per le nuove commissioni usare il formato di [profiles.md](profiles.md);
  - interventi: `Talk - <titolo breve>`, `Seminario <ente> su <tema>`, `Simposio <ente>`.
- **Luogo**: l'aula, nel formato della fonte (es. "Aula 4R (informatica)", "aula T3 edificio CLA, via Venezia 16").
- **Descrizione**: composizione della commissione, programma, orario del proprio intervento ("intervento Toffalini: 12:50-13:05").

### Activities (general)
- **ID**: `c_2b315a12c879a3ba6d3888259c0360dde56a70afe43d84159a372075167b20bd@group.calendar.google.com`
- **URL impostazioni (base64)**: `Y18yYjMxNWExMmM4NzlhM2JhNmQzODg4MjU5YzAzNjBkZGU1NmE3MGFmZTQzZDg0MTU5YTM3MjA3NTE2N2IyMGJkQGdyb3VwLmNhbGVuZGFyLmdvb2dsZS5jb20`
- **Promemoria predefinito**: nessuno impostato (si usano quelli di default).
- **Contenuto**:
  - **convegni e congressi** a cui Enrico partecipa: evento **all-day** su più giorni, `availability=FREE`. Titolo = sigla o nome (es. "AIRIPA", "MCLS", "ICAP Conference - Firenze"); link al programma o dettagli delle proprie sessioni in descrizione. Gli interventi specifici di Enrico al convegno vanno **in più** in Lectures_Testing come eventi a orario;
  - **impegni personali e di casa**: tecnici, consegne, ritiri, assemblea condominiale, visite. Titoli brevi e informali ("Tecnici Bosch", "Consegna divano");
  - **Supervisione** ricorrente: martedì 12:00–13:00, Zoom `https://unipd.zoom.us/j/91052088541`. Non duplicarla;
  - attività esterne o istituzionali sparse (es. "Invalsi", "Commissione Ricerca", webinar di associazioni come "Presentazione gruppo tematico AIP Misurazione").
- In caso di dubbio tra University e Activities: le riunioni dell'ateneo di Padova vanno in University; eventi di enti esterni, associazioni, webinar e convegni vanno in Activities.

### Deadlines
- **ID**: `c_257164ecd12fef4342ca983e293743f6a11139871a4f2334d390ef613eb7ec39@group.calendar.google.com`
- **URL impostazioni (base64)**: `Y18yNTcxNjRlY2QxMmZlZjQzNDJjYTk4M2UyOTM3NDNmNmExMTEzOTg3MWE0ZjIzMzRkMzkwZWY2MTNlYjdlYzM5QGdyb3VwLmNhbGVuZGFyLmdvb2dsZS5jb20`
- **Promemoria predefinito**: popup 1440 minuti (il giorno prima).
- **Contenuto**: scadenze come invio documenti, lettere, iscrizioni a convegni, domande, bollo e assicurazione auto.
- **Formato**: evento **a orario di 30 minuti**, non all-day. Se la fonte dà un'ora limite, l'evento **termina** a quell'ora (es. entro le 12:00 → 11:30–12:00). Senza ora: 10:00–10:30.
- **Titoli**: `Scadenza <cosa>` oppure verbo e oggetto ("Invio letter commitment STARS", "Iscrizione Giornate Bologna"). Mettere in descrizione cosa fare e il link o modulo.
- Le scadenze di disponibilità (es. "SCADENZA 13 OTTOBRE: richiesta disponibilità PPV") vanno qui come `Scadenza disponibilità PPV novembre` se Enrico chiede di inserirle o se emergono dallo screening.

### B-days
- **ID**: `c_b8e8fb46d61c44e5e912905c23fd9c192b75478252660399f99297dffdb09279@group.calendar.google.com`
- **URL impostazioni (base64)**: `Y19iOGU4ZmI0NmQ2MWM0NGU1ZTkxMjkwNWMyM2ZkOWMxOTJiNzU0NzgyNTI2NjAzOTlmOTkyOTdkZmZkYjA5Mjc5QGdyb3VwLmNhbGVuZGFyLmdvb2dsZS5jb20`
- **Formato**: evento a orario 10:00–10:30, ricorrenza annuale (`RRULE:FREQ=YEARLY`), titolo = solo il nome della persona (es. "Sara Caviola", "Fiorella DPC"). È l'unico caso in cui la ricorrenza è ammessa, e solo se Enrico chiede di aggiungere un compleanno.

## Calendari in sola lettura o da non usare per scrivere

### Calendario di Direzione (reader)
- **ID**: `c_2a30f618b6922006fcb89da467991c45a651100352ef273d5c842c8ba00eafa5@group.calendar.google.com`
- **URL impostazioni (base64)**: `Y18yYTMwZjYxOGI2OTIyMDA2ZmNiODlkYTQ2Nzk5MWM0NWE2NTExMDAzNTJlZjI3M2Q1Yzg0MmM4YmEwMGVhZmE1QGdyb3VwLmNhbGVuZGFyLmdvb2dsZS5jb20`
- Gestito dalla Direzione del Dipartimento: Giunta di Dipartimento, Consiglio di Dipartimento (anche straordinari su Zoom), DPG meeting, retreat.
- Serve per il controllo dei duplicati: le convocazioni di Giunta e Consiglio che arrivano per email sono di solito **già qui**. Non ricrearle altrove; segnalare solo se data od ora differiscono.

### Primary
- **ID**: `enrico.toffalini@unipd.it`. Nome visualizzato "-".
- Contiene quasi solo inviti esterni ricevuti (es. intervista Faculti). Un invito Google Calendar ricevuto per email è **già** qui: non duplicarlo in altri calendari. Non scrivere in primary.

### Altri calendari sottoscritti (solo consultazione)
- `psicostat-events`: `c_e2028e282c700c15b439f67706cefdc67966b1bc6820f60dfc4e9d7ed51539f4@group.calendar.google.com` (eventi pubblici Psicostat).
- `TEMPS I anno I Semestre`: `c_jt8lmpshdnpevvs4tthbn9v9so@group.calendar.google.com` (orario del corso).
- `Festività in Italia`: `it.italian#holiday@group.v.calendar.google.com`.

## Regola di scelta rapida

1. Enrico conduce, insegna, esamina o presenta? → **Lectures_Testing**. Se è supplente, colore grigio (`colorId` 8).
2. È una scadenza (qualcosa da fare entro una data)? → **Deadlines**
3. È un convegno, un evento esterno o un impegno personale? → **Activities (general)**
4. È una riunione o un'attività dell'ateneo a cui partecipa? → **University**. Le lezioni di colleghi vanno qui solo se Enrico deve esplicitamente presenziare; altrimenti non si inseriscono.
5. È un compleanno? → **B-days**
6. È già in primary, in Direzione o in psicostat-events? → non creare, segnalare.
7. È ipotetico o in attesa di conferma da altri? → calendario come sopra, con `???` alla fine del titolo.
