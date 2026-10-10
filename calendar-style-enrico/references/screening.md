# Screening della posta

Si usa quando Enrico chiede di controllare se qualcosa gli è sfuggito. Per default produce solo proposte; scrive solo se richiesto esplicitamente.

## Finestra

- Usare quella indicata da Enrico. Altrimenti: email degli ultimi **14 giorni** (`newer_than:14d`) ed eventi da oggi in avanti.
- Considerare solo eventi futuri, o di oggi non ancora trascorsi. Gli eventi passati vanno al massimo in "Ignorati".

## Query Gmail (in parallelo, `pageSize` 50, con paginazione se serve)

Escludere sempre `-category:promotions -category:social`. Ad esempio:

1. `newer_than:14d (convocazione OR riunione OR "ordine del giorno" OR meeting OR incontro)`
2. `newer_than:14d (commissione OR commissioni OR lauree OR laurea OR PPV OR proclamazione OR appello OR esame)`
3. `newer_than:14d (scadenza OR deadline OR "entro il" OR "entro e non oltre" OR due)`
4. `newer_than:14d (seminario OR webinar OR workshop OR convegno OR congresso OR conference OR symposium OR talk OR invited)`
5. `newer_than:14d (zoom.us OR meet.google OR teams.microsoft OR webex)`
6. `newer_than:14d from:didattica.psicologia@unipd.it`, oltre ad altri mittenti istituzionali che compaiono (segreterie, dottorato, comitato etico)
7. `newer_than:14d in:sent (appuntamento OR incontriamoci OR "ci vediamo" OR "va bene" OR confermo)`: impegni presi da Enrico nelle sue risposte
8. `newer_than:14d is:starred`: le mail stellate sono spesso cose da ricordare

Unire i risultati e deduplicarli per `threadId`. Per i candidati leggere il thread completo (`PLAIN_TEXT`).

## Filtro

Scartare, contando il motivo:
- newsletter, mailing list, pubblicità, promozioni di convegni a cui Enrico non è iscritto;
- comunicazioni generiche a tutti i docenti senza un impegno per Enrico. Eccezione: le scadenze che lo riguardano come docente, come le disponibilità PPV e lauree o le scadenze didattiche;
- lezioni di colleghi, salvo che Enrico debba esplicitamente presenziare;
- eventi già passati;
- inviti già presenti in primary;
- eventi già presenti in un qualsiasi calendario (controllo duplicati come nella procedura principale).

## Output dello screening

Usare il report standard di SKILL.md, con in più per ogni proposta:
- calendario suggerito e titolo proposto;
- confidenza e cosa manca;
- link alla mail.

In fondo indicare quante email sono state esaminate e quante scartate per categoria, così Enrico sa quanto è stato ampio il controllo.
