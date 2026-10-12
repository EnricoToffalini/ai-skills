---
name: calendar-style-enrico
description: Read Enrico Toffalini's Gmail (enrico.toffalini@unipd.it) and, when asked, autonomously add the events suggested by emails or attachments to the right Google Calendar among his several calendars (University, Lectures_Testing, Activities (general), Deadlines, B-days), following his naming conventions, then report every action for verification. Use when Enrico asks to put something from an email into the calendar, to screen recent emails for meetings, deadlines, committees, exams, lectures, talks or conferences he may have missed, or to check whether email commitments are already in his calendar. Also covers university availability requests and final schedules for graduation committees (lauree) and PPV.
metadata:
  author: Enrico Toffalini
  credits: Based on calendar-batch-manager by Filippo Gambarota (see CREDITS.md)
---

# Calendar Style Enrico

## Impostazioni fisse

- Account: `enrico.toffalini@unipd.it`, sia Gmail sia Google Calendar. Fuso `Europe/Rome`; date italiane `DD/MM/YYYY`.
- La skill funziona in Claude, ChatGPT e Codex. I nomi degli strumenti cambiano da un ambiente all'altro: vedi **Ambiente e strumenti** più sotto.
- **Ci sono più calendari: scegliere sempre quello giusto.** Gli ID completi, le finalità e le convenzioni sono in [references/calendars.md](references/calendars.md): **leggerlo sempre prima di scrivere**. Tabella rapida:

| Calendario | Calendar ID | Uso |
|---|---|---|
| University | `c_37cc77e0dfd21ee92b0321aa17ff5563f76e2ee16d0ce1d61bb898a69f4901f6@group.calendar.google.com` | riunioni, organi, comitati, progetti, lab, studenti, eventi universitari a cui Enrico partecipa senza condurli (lezioni di colleghi solo se deve esplicitamente presenziare) |
| Lectures_Testing | `c_2c6f8ed8d81c943a18f8f5713f24db35fe09ff30790cf35b1575cab10978981e@group.calendar.google.com` | ciò che Enrico **conduce**: lezioni, esami, commissioni di laurea/PPV, talk e seminari tenuti da lui |
| Activities (general) | `c_2b315a12c879a3ba6d3888259c0360dde56a70afe43d84159a372075167b20bd@group.calendar.google.com` | convegni (all-day, liberi), personale/casa, Supervisione, attività esterne miste |
| Deadlines | `c_257164ecd12fef4342ca983e293743f6a11139871a4f2334d390ef613eb7ec39@group.calendar.google.com` | scadenze (invii, iscrizioni, domande, rinnovi) |
| B-days | `c_b8e8fb46d61c44e5e912905c23fd9c192b75478252660399f99297dffdb09279@group.calendar.google.com` | compleanni |
| Calendario di Direzione | `c_2a30f618b6922006fcb89da467991c45a651100352ef273d5c842c8ba00eafa5@group.calendar.google.com` | **sola lettura**, gestito dalla Direzione: consultarlo, mai scriverci |
| primary | `enrico.toffalini@unipd.it` | riceve solo inviti esterni: **non scriverci** |

- Indicare **sempre** esplicitamente il calendar ID di destinazione. Se un calendario non è accessibile o scrivibile, fermarsi su quel record e segnalarlo: non ripiegare mai su `primary` o su un altro calendario.
- Lingua degli eventi: italiano, salvo titoli ufficiali in inglese (es. corsi TEMPS). Non aggiungere ospiti, Google Meet, ricorrenze, inviti o dettagli che la fonte non contiene. Quindi: nessun partecipante, nessun link Meet generato, nessuna notifica, promemoria predefiniti del calendario, fuso `Europe/Rome` con orari locali (o con l'offset corretto +01:00/+02:00 se lo strumento lo richiede).
- **Prevenire copie in `primary`.** Nei calendari secondari, non basta passare una lista ospiti vuota: verificare anche che lo strumento non aggiunga implicitamente Enrico come partecipante. Per il connettore ChatGPT usare `attendees: []` e `self_attendance: "omit"`; impostare `add_google_meet: false` salvo esplicita richiesta. Se non e possibile disabilitare l'aggiunta automatica dell'utente, fermarsi prima di scrivere e segnalare il limite.

## Cosa può e non può fare

- **Lettura**: cercare e leggere email, thread e allegati; leggere tutti i calendari.
- **Scrittura**: solo creazione di eventi, e aggiornamento solo di eventi già creati da questa skill (riconoscibili dalla riga `[cal-enrico]` nella descrizione). Solo nei calendari scrivibili sopra.
- **Mai**: rispondere a email, accettare o rifiutare inviti, cancellare o spostare eventi esistenti, modificare eventi non creati dalla skill, applicare etichette o segnare come letto, compilare moduli di disponibilità (es. link APEX). Per tutte queste cose: segnalare e proporre.

## Modalità

Capire dalla richiesta quale modalità si applica.

1. **Mail indicata + "mettilo in calendario"** (o simili): leggere la mail indicata ed eseguire **autonomamente**. Non serve chiedere conferma per i record ad alta confidenza.
2. **Screening** ("controlla se mi è sfuggito qualcosa", "guarda le mail dell'ultima settimana"): ricerca ampia, vedi [references/screening.md](references/screening.md). **Per default solo proposta**, senza scrivere. Scrivere autonomamente solo se Enrico lo ha chiesto esplicitamente (es. "e inserisci quello che manca").
3. **Solo analisi o controllo** ("c'è già in calendario?", "cosa dice questa mail?"): nessuna scrittura.

In caso di dubbio sulla modalità, trattare la richiesta come solo proposta. Una richiesta che chiede solo di analizzare non autorizza la scrittura.

## Procedura

1. **Trovare la fonte.** Cercare la mail con la sintassi di ricerca Gmail, usando parole chiave salienti, mittente e data, non l'oggetto intero. Leggere l'intero thread in testo semplice, perché le mail successive possono spostare, annullare o correggere. Usare il messaggio più recente come stato attuale.
2. **Leggere gli allegati** pertinenti (PDF, Excel, Word, immagini) con gli strumenti disponibili nell'ambiente. Di norma basta leggerli direttamente dalla mail. Solo se in quell'ambiente il contenuto non è accessibile, provare le alternative: lo stesso file su Google Drive, una copia locale, il browser. Se nessuna funziona, fermarsi su quel record e chiedere il file.
   **Non dedurre mai il contenuto dal nome del file.** Leggere il documento completo, comprese le continuazioni di pagina.
3. **Estrarre i record**, uno per ogni sessione o fascia oraria distinta, con questi campi: `fonte` (oggetto, mittente, data, link), `tipo`, `ruolo di Enrico`, `data`, `inizio`, `fine`, `luogo`, `link online`, `note`, `confidenza` (alta/media/bassa). Non dedurre orari mancanti.
4. **Decidere se Enrico è coinvolto.** Una circolare a tutti i docenti non coinvolge automaticamente Enrico. Una convocazione a un organo di cui fa parte sì. Per i PDF con commissioni, cercare `TOFFALINI ENRICO` (anche `TOFFALINI`, `Prof. TOFFALINI`, `Toffalini Enrico`) come indicato in [references/profiles.md](references/profiles.md).
5. **Scegliere il calendario e applicare le convenzioni** di [references/calendars.md](references/calendars.md) e i profili di [references/profiles.md](references/profiles.md). Se il calendario è incerto (es. University o Activities), scegliere quello più coerente con i precedenti e dichiararlo nel report.
6. **Controllare i duplicati.** Leggere **tutti** i calendari scrivibili, più primary, Direzione e psicostat-events, nell'intervallo della data (giorno intero, con paginazione). Un evento equivale a un duplicato se ha lo stesso tipo, la stessa data e orari uguali o molto vicini, anche con titolo diverso o in un altro calendario. Esempi: un invito già presente in primary; una riunione di Dipartimento già nel Calendario di Direzione; un seminario Psicostat già in University o in psicostat-events. Non creare duplicati. Le sovrapposizioni con altri impegni vanno **segnalate**, mai risolte da sola. **Verifica tecnica:** usare intervalli e fuso espliciti, esaurire ogni pagina e distinguere un elenco veramente vuoto da errori o risposte incomplete. Se non si riesce a verificare l'assenza di duplicati, non creare l'evento.
7. **Applicare le soglie di confidenza:**
   - **alta** (data, ora e coinvolgimento espliciti; calendario chiaro): creare l'evento nelle modalità che lo autorizzano;
   - **media** (es. orario di fine mancante ma deducibile da prassi nota, calendario discutibile): creare solo se Enrico ha chiesto l'inserimento, e segnalarlo con ⚠ nel report;
   - **bassa** (data o ora ambigue, coinvolgimento incerto, contenuto dell'allegato non letto): **non creare**; elencare tra le proposte con la domanda precisa.
   - Un evento solo **ipotetico** o in attesa di conferma altrui con dati chiari non è a confidenza bassa: si crea con `???` nel titolo (vedi **Regole speciali**).
8. **Scrivere** con lo strumento di creazione eventi e il calendar ID esplicito, applicando le **Regole speciali** (`???` e colore grigio per le supplenze). In ChatGPT, per gli eventi senza invitati impostare esplicitamente `attendees: []`, `self_attendance: "omit"`, `add_google_meet: false` (quando supportati), senza usare i default. La descrizione termina sempre con la riga di tracciabilità:
   `[cal-enrico] Da email: "<oggetto>" — <mittente>, <data> — <viewUrl>`
9. **Verificare.** Dopo la scrittura rileggere ogni evento creato per confermare calendario, data, orari e colore (se impostato). **Ricercare inoltre lo stesso evento in `primary`**, confrontando ID, titolo e orario: lo stesso ID in `primary` e nel calendario secondario puo indicare una copia dovuta all'auto-invito, non due creazioni distinte. In tal caso segnalarlo espressamente e non dichiarare la creazione priva di duplicazioni. Se una creazione fallisce, non dichiararla riuscita.
10. **Fare il report** nel formato sotto.

## Regole speciali (importanti)

- **Eventi ipotetici o in attesa di conferma altrui** (es. "forse martedì", "attendo conferma da X", una data proposta e non ancora accettata da tutti): se l'inserimento è autorizzato, creare l'evento con **`???` alla fine del titolo**, ad esempio `Meeting PRIN Carretti ???`. In descrizione indicare chi deve confermare. Quando arriva la conferma, togliere `???` (se l'evento è stato creato dalla skill) e riportarlo nel report. Questo vale per un'incertezza sulla **conferma dell'evento**. Se invece sono ambigui i dati (data, ora o coinvolgimento poco chiari), il record ha confidenza bassa e non si crea.
- **Ruolo di supplente** in commissioni di laurea, PPV, esame o altro: evento in **Lectures_Testing** con **colore grigio**, cioè Google Calendar `colorId = "8"` (Graphite). Non va lasciato il colore predefinito arancione del calendario: serve proprio a distinguere a colpo d'occhio le supplenze. Il titolo contiene comunque `[supplente]`. Dopo la creazione verificare che il colore sia stato applicato. Se lo strumento non permette di impostarlo, **non creare l'evento**: chiedere a Enrico come procedere (vedi **Ambiente e strumenti**).

## Ambiente e strumenti

La procedura è descritta per azioni, non per nomi di strumenti. Usare gli strumenti equivalenti disponibili:

| Azione | Claude (connettori claude.ai) | ChatGPT / Codex |
|---|---|---|
| cercare email | `search_threads` (Gmail) | connettore o app Gmail (ricerca) |
| leggere thread o mail | `get_thread` / `get_message` (`PLAIN_TEXT`) | lettura messaggio del connettore Gmail |
| elencare i calendari | `list_calendars` | connettore Google Calendar, oppure gli ID di calendars.md |
| leggere eventi | `list_events` (con `calendarId`, intervallo, `fullText`) | ricerca o lista eventi del connettore |
| creare evento | `create_event` (con `calendarId`) | creazione evento del connettore, se esiste |
| aggiornare evento | `update_event` | aggiornamento evento del connettore, se esiste |

**All'avvio controllare che cosa permette l'ambiente.** Le capacità necessarie sono: leggere Gmail e gli allegati; leggere tutti i calendari elencati; scrivere nel calendario di destinazione corretto; impostare il colore (per le supplenze).

**Se anche una sola manca, non intraprendere azioni.** In questo caso:
1. dire chiaramente che cosa manca (es. "il connettore Calendar di questo ambiente scrive solo nel calendario principale", "non posso impostare il colore", "non vedo gli allegati");
2. presentare comunque l'analisi: gli eventi individuati con calendario, titolo, orari, colore e fonte, come nel report alla voce ❓;
3. suggerire le alternative possibili, ad esempio:
   - incollare o allegare la mail o i file;
   - generare file `.ics`, uno per calendario di destinazione, da importare (Google Calendar → Impostazioni → Importa ed esporta), ricordando che il colore grigio va poi impostato a mano;
   - creare solo gli eventi possibili e lasciare gli altri come elenco;
   - inserimento manuale da parte di Enrico;
4. **chiedere conferma e attendere la risposta** prima di proseguire. Anche in modalità 1 (inserimento autorizzato), un'autorizzazione data senza sapere del limite non vale: serve una nuova conferma.

Non scrivere mai in un calendario diverso da quello giusto come ripiego. Non dichiarare mai creato un evento che non è stato scritto e verificato.

## Report finale (obbligatorio, anche se non è stato scritto nulla)

Va scritto in modo che Enrico possa ricontrollare tutto rapidamente.

```
Fonti lette: N email (elenco: oggetto — mittente — data — link), allegati letti/non letti

✅ Creati (N)
| Calendario | Titolo | Data | Orario | Luogo | Colore (se non predefinito) | Fonte | Link evento |

⚠ Creati con assunzioni (N): evento — assunzione fatta (es. "fine stimata 2h")

⏭ Saltati perché già presenti (N): evento — dove si trova (calendario, titolo esistente)

❓ Proposti / da confermare (N): evento — cosa manca o perché non l'ho inserito — calendario suggerito

🚫 Ignorati (N, solo nello screening): mail — motivo breve (newsletter, non coinvolto, passato…)

⚡ Conflitti e sovrapposizioni: evento nuovo ↔ evento esistente (calendario)

📌 Azioni che restano a te: es. compilare disponibilità APEX entro il 13/10, rispondere all'invito, ecc.
```

Le sezioni vuote si omettono, ma va sempre detto esplicitamente se nessun evento è stato creato.

## Aggiornamenti e calendari definitivi

- Quando arriva un calendario definitivo dopo una richiesta di disponibilità, non cancellare le disponibilità `[disponibilità]` precedenti. Creare l'evento definitivo e proporre nel report di rimuovere le disponibilità ormai superate.
- Se una mail sposta o annulla un evento creato dalla skill (riga `[cal-enrico]`), aggiornarlo in modalità autorizzata e riportare il prima e il dopo. Se l'evento non è stato creato dalla skill, solo proporre la modifica.
- Per le richieste di sincronizzazione presentare un piano `crea / aggiorna / lascia / proponi rimozione` ed eseguire solo crea/aggiorna nei limiti sopra.

## Estensibilità

Per tipi di evento nuovi seguire il flusso comune e i precedenti osservati nel calendario: cercare eventi simili con una ricerca testuale nei calendari e imitarne titolo, calendario e formato. Non estendere ad altri tipi di evento la regola di filtro sulle commissioni.
