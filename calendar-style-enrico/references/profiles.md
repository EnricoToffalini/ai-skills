# Profili, formati ed esempi

Il nominativo cercato è `TOFFALINI ENRICO`. Tutti gli eventi di questo file vanno in **Lectures_Testing** (`c_2c6f8ed8d81c943a18f8f5713f24db35fe09ff30790cf35b1575cab10978981e@group.calendar.google.com`), salvo dove indicato diversamente.

## Regole di parsing per PDF di lauree e PPV

- Leggere il **documento completo**, non solo le prime pagine. Cercare `TOFFALINI ENRICO` (e varianti `TOFFALINI`, `Prof. TOFFALINI`) in modo robusto rispetto a spazi multipli e layout a colonne. Verificare che compaia nella **commissione**: il nome può comparire anche nei campi `CONTRORELATORE` di tesi che appartengono a un'unica commissione.
- Per i confini delle commissioni usare le intestazioni `DD/MM/YYYY HH:MM - HH:MM`, `aula ... edificio ...` e la sezione `Commissione`. Ruolo e aula sono attributi della sessione, non dell'intera giornata.
- Nei layout a due colonne non associare per errore un laureando a un membro della commissione che si trova sulla stessa riga.
- Se una sessione continua nella pagina successiva, integrarla senza crearne una nuova.
- Ruoli: `Presidente`, `Effettivo/a`, `Supplente`. Distinguere `Esperto Non Componente` e le annotazioni tra parentesi; un esperto non va qualificato come componente effettivo.
- Per le `Mie tesi` leggere i blocchi `LAUREANDA/LAUREANDO`, `TITOLO TESI`, `RELATORE/RELATRICE`, `CONTRORELATORE/CONTRORELATRICE`, conservando il titolo per esteso. Se Enrico compare solo come correlatore, non trattarlo come relatore; segnalarlo a parte.
- Testo estratto illeggibile o ambiguo: confrontarlo con la pagina visiva o chiedere. Non scrivere dati incerti.

## Profilo A — Richiesta di disponibilità per le lauree

Riconoscere ad esempio `Richiesta disponibilità comm. proclamatrici lauree triennali/magistrali`. Si tratta di una richiesta, non di un'assegnazione.

- **Default: non creare eventi di disponibilità.** Creare solo la scadenza in **Deadlines** (`Scadenza disponibilità lauree <tipo> <mese>`, link al modulo in descrizione) e mettere tra le "Azioni che restano a te" l'invio della disponibilità.
- Solo se Enrico lo chiede (es. "segna le fasce" o "blocca le date") creare in Lectures_Testing un evento per **ogni** coppia data-fascia, intitolato `Lauree Triennali [disponibilità]` o `Lauree Magistrali [disponibilità]`, senza aula se non indicata. In descrizione scrivere che la disponibilità non è definitiva.

## Profilo B — Richiesta di disponibilità PPV

Riconoscere ad esempio `richiesta disponibilità Commissioni Prove Pratico-Valutative PPV – <MESE>`.

- Stesso default del profilo A: scadenza in Deadlines (`Scadenza disponibilità PPV <mese>`) e azione per Enrico.
- Su richiesta: un evento `PPV [disponibilità]` per **ogni** intervallo (anche tre fasce nello stesso giorno), con l'appello in descrizione.

## Profilo C — Calendario definitivo PPV

- Cercare **sempre e automaticamente** `TOFFALINI ENRICO` nella sezione `Commissione` lungo tutto il documento. Se non c'è, non creare eventi per quella sessione.
- Creare un evento per commissione o sessione, non per laureando.
- Titolo: `Commissione PPV [<ruolo>] - <EDIFICIO> <AULA>` (es. `Commissione PPV [supplente] - CLA 1G`), con ruolo `presidente`, `effettivo` o `supplente`. La parte finale è la sigla dell'edificio seguita dall'aula, **senza** la parola "aula".
- Luogo: edificio e indirizzo completo (es. `Edificio CLA, Via Venezia 16, Padova`).
- Descrizione: commissione completa con i ruoli (schema sotto) e riga `[cal-enrico]`.
- **Se il ruolo è supplente: `colorId = "8"` (grigio Graphite)**, non l'arancione predefinito. Vale per tutti i profili con commissioni (C, D, esami, defense).

## Profilo D — Calendario definitivo lauree triennali e magistrali

- Stessa selezione del profilo C: creare eventi solo per le commissioni che includono `TOFFALINI ENRICO`.
- Titolo: `Commissione Lauree Triennali [effettivo] - CLA T4`, `Commissione Lauree Magistrali [presidente] - PSICO2 2D`. Per le proclamatrici TEMPS: `Commissione Proclamatrice TEMPS [<ruolo>] - <EDIFICIO> <AULA>`.
- Descrizione: **tutti** i componenti con i rispettivi ruoli; gli `Esperti non componenti` in una sezione separata; le annotazioni rilevanti.
- Supplente: colore grigio (`colorId = "8"`), come nel profilo C.
- **Nella stessa sessione** cercare le tesi in cui Enrico è `RELATORE` o `CONTRORELATORE` e elencarle sotto `Mie tesi` con ruolo, laureando/a e titolo integrale, senza creare altri eventi. Se non ce ne sono, omettere la sezione.

## Schema della descrizione per le commissioni

```text
Commissione
- Nome Cognome (Presidente)
- Nome Cognome (Effettivo/a)
- TOFFALINI ENRICO (Supplente)
...

Esperti non componenti [solo se presenti]
- Nome Cognome (Correlatore/a; altre annotazioni)

Mie tesi [solo se presenti]
- Controrelatore — NOME LAUREANDO/A
  Titolo completo della tesi
- Relatore — NOME LAUREANDO/A
  Titolo completo della tesi

[cal-enrico] Da email: "<oggetto>" — <mittente>, <data> — <viewUrl>
```

## Profili aggiuntivi (casi comuni nella posta di Enrico)

### E — Convocazioni di organi e riunioni (University)
- Collegio Docenti Dottorato, Consiglio Corso di Studi, Comitato Etico, gruppi di lavoro, riunioni di progetto.
- Titolo con il nome dell'organo o `Meeting <tema>`. Il link Zoom va nel luogo; ordine del giorno e link ai documenti in descrizione.
- Giunta, Consiglio di Dipartimento e DPG meeting stanno di solito già nel **Calendario di Direzione**: controllare lì e non duplicare.

### F — Lezioni, esami e appelli (Lectures_Testing)
- Solo se Enrico è il docente o è in commissione d'esame.
- Le lezioni di colleghi **di regola non si inseriscono**. Eccezione: Enrico deve esplicitamente presenziare (richiesta diretta, ruolo assegnato). In quel caso vanno in University.
- Seguire i titoli osservati in calendars.md e mettere l'aula nel luogo.

### G — Talk, seminari, simposi in cui Enrico interviene (Lectures_Testing)
- `Talk - <titolo breve>` o `Seminario <ente> su <tema>`. Mettere in descrizione l'orario esatto del proprio intervento e il programma.
- Se fa parte di un convegno, creare **anche** l'evento convegno all-day in Activities (profilo H), se non c'è già.

### G2 — Discussioni di dottorato (defense) e commissioni esterne
- Enrico **commissario** (anche all'estero, online): Lectures_Testing, `Defense <Nome Cognome>`, link nel luogo. Se è supplente, colore grigio.
- Enrico **solo uditore**: University, stesso titolo.

### H — Convegni, congressi, webinar (Activities (general))
- Convegno su uno o più giorni: evento all-day su tutti i giorni (in Google Calendar la data di fine è esclusiva: verificarla), disponibilità "libero", titolo = sigla o nome con la città se utile.
- Webinar o presentazione puntuale: evento a orario con il link nel luogo.
- Creare solo se Enrico partecipa (iscrizione confermata, contributo accettato, invito accettato). Una semplice call for papers o una newsletter non bastano: al massimo vanno tra le proposte o, se c'è una scadenza utile, in Deadlines.

### I — Scadenze (Deadlines)
- Formato da calendars.md: 30 minuti che terminano all'ora limite, oppure 10:00–10:30.
- Esempi: scadenza disponibilità PPV, scadenza revisione per una rivista (se accettata), domande di progetto, iscrizioni, approvazioni Uniweb richieste entro una data.

### J — Impegni personali (Activities (general))
- Appuntamenti con tecnici, consegne, visite. Titolo breve; indirizzo nel luogo; numero d'ordine o riferimento in descrizione.

## Esempi di eventi ipotetici (`???`)

- "Ci vediamo martedì 14 alle 15, ti confermo domani" → `Meeting <persona> ???` nel calendario appropriato; in descrizione "in attesa di conferma da <persona>".
- Data di lauree o PPV indicata come "probabile" o "da confermare" dalla segreteria → titolo del profilo con ` ???` alla fine.
- Proposta di Enrico non ancora accettata dall'altra parte → `???`.
- Data ambigua ("la settimana prossima", "giovedì" senza riferimento) → **non** `???`: confidenza bassa, solo proposta.

## Esempi anti-duplicato

- Due eventi con stessa data e stessi orari e titoli simili (maiuscole, spazi, descrizione diversi): possibile duplicato, non creare.
- Un'email "Invito: …" di Google Calendar: l'evento è già in primary, quindi non crearlo; segnalare solo se Enrico non ha ancora risposto.
- Una riunione diversa sovrapposta: è un **conflitto**, non un duplicato. Crearla comunque se autorizzata e segnalarla.
- Eventi di disponibilità e sessione definitiva nello stesso giorno: non sono duplicati. Proporre di rimuovere le disponibilità.
