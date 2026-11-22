# Guida alla configurazione e checklist per la pubblicazione

## Prima dell'importazione

- [ ] Predisponi un'istanza n8n che supporti i tipi e le versioni dei nodi presenti nel workflow, oppure aggiornali secondo necessità.
- [ ] Crea un bot Telegram e prepara l'accesso API OpenAI, una rubrica Airtable, Gmail OAuth2 e Google Calendar OAuth2.
- [ ] Durante le prime verifiche utilizza account di prova e contatti fittizi.

## Dopo aver importato `workflow/ai-personal-assistant.json`

- [ ] Nel nodo **If → Conditions → right value**, sostituisci `REPLACE_WITH_YOUR_TELEGRAM_CHAT_ID`.
- [ ] Nel nodo **Telegram** per la revisione umana, sostituisci `REPLACE_WITH_YOUR_TELEGRAM_CHAT_ID` nel campo **Chat ID**.
- [ ] Seleziona base e tabella Airtable per sostituire i valori `REPLACE_WITH_YOUR_AIRTABLE_...`.
- [ ] Seleziona il tuo Google Calendar al posto di `REPLACE_WITH_YOUR_CALENDAR_ID`.
- [ ] Ricollega le credenziali Telegram a **Telegram Trigger**, **Get a file**, **Send a text message** e **Telegram** (revisione umana).
- [ ] Ricollega le credenziali OpenAI a **OpenAI Chat Model** e **Transcribe a recording**.
- [ ] Ricollega le credenziali Airtable, Gmail e Google Calendar.
- [ ] Controlla i collegamenti dei tool dell'**AI Agent**: Airtable direttamente all'agente; Gmail e Calendar attraverso la revisione umana; il nodo di revisione collegato come tool all'agente.
- [ ] Verifica che nel **System Message** dell'AI Agent i nomi degli strumenti corrispondano a quelli effettivi. Il prompt esportato cita `Send a message in Gmail`, mentre il nodo Gmail si chiama `Invio email Gmail`: è consigliabile uniformarli.
- [ ] Controlla il fuso orario del calendario e l'espressione `$now.setZone('Europe/Rome')` usata dall'agente.
- [ ] Verifica la struttura della tabella Airtable e che l'agente riesca a trovare un contatto di prova.

## Verifica del funzionamento

- [ ] Invia una richiesta **testuale** e verifica la risposta su Telegram.
- [ ] Invia una richiesta **vocale** e controlla il flusso `Get a file → Transcribe a recording → AI Agent`.
- [ ] Verifica che la ricerca dei contatti utilizzi effettivamente i record Airtable, senza inventare dati.
- [ ] Prepara un messaggio Gmail e verifica sia la richiesta di conferma in conversazione sia i pulsanti separati **Approva/Rifiuta** su Telegram.
- [ ] Rifiuta un'operazione e verifica che non venga eseguita.
- [ ] Approva un'operazione di prova e controlla il risultato direttamente in Gmail o Google Calendar.
- [ ] Invia un messaggio da un Chat ID non autorizzato e verifica che il nodo **If** interrompa il flusso.
- [ ] Prova espressioni temporali relative e controlla che il modello riceva la data corrente corretta nel fuso di Roma.
- [ ] Pubblica/attiva il workflow soltanto dopo aver completato le verifiche.

## Prima di rendere pubblico il repository

- [ ] Utilizza soltanto `workflow/ai-personal-assistant.json` incluso in questo progetto, **mai l'esportazione originale**.
- [ ] Controlla tutti i testi, le schermate e i PDF per evitare la diffusione di indirizzi email, Chat ID, token, dati delle esecuzioni e URL privati.
- [ ] Aggiungi `docs/presentation.pdf` soltanto dopo averne controllato metadati e collegamenti incorporati.
- [ ] Pubblica soltanto schermate che hai diritto di condividere, oscurando eventuali informazioni personali.
- [ ] Valuta l'aggiunta di una licenza e dei topic GitHub: `n8n`, `ai-agent`, `automation`, `telegram`, `openai`, `human-in-the-loop`.
