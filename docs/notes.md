# Consigli utili per Smart Fan Controller

Queste note raccolgono alcuni consigli pratici basati sulla realizzazione e sull’utilizzo reale del progetto.

---

## Posizionamento del dispositivo
- Posiziona la scatola in un punto dove la ventola possa muovere l’aria senza ostacoli.
- Evita che il DHT11 sia troppo vicino al calore della ventola: meglio montarlo sul fronte della scatola.
- Assicurati che l’ESP abbia una buona copertura Wi-Fi.

---

## Alimentazione
- Alimenta la ventola a 12V e usa lo **step-down** per fornire 5V all’ESP.
- Lo step-down deve essere fissato bene e non deve toccare superfici metalliche.
- Assicurati che lo step-down eroghi abbastanza corrente (almeno 1A).

---

## Ventola PWM
- La ventola deve supportare PWM standard (solitamente 25 kHz).
- Il filo **PWM (blu)** va all’ESP (pin configurato come PWM).
- Il filo **TACH (verde)** deve essere filtrato per avere RPM stabili.

---

## Filtro RC per lettura RPM
Per ottenere letture stabili degli RPM è utile aggiungere:

- **10 kΩ** in serie al filo TACH  
- **100 nF** tra TACH e GND  

Questo riduce il rumore elettrico e rende la lettura molto più stabile.

---

## Relè di accensione
- Il relè taglia o ripristina la linea a 12V della ventola.
- Usalo per spegnere completamente la ventola quando non serve.
- Il relè deve essere da **12V** per funzionare correttamente.

---

## Suggerimenti per Home Assistant
- Imposta le soglie di temperatura in modo da non fare partire la ventola troppo spesso.
- Usa la modalità automatica per mantenere un ambiente stabile senza dover intervenire.
- La modalità manuale è utile per test o per situazioni particolari.

---

## Sicurezza
- Controlla bene i collegamenti prima di alimentare il sistema.
- Non lasciare fili esposti dentro la scatola.
- Fissa tutto con colla a caldo o fascette per evitare corti.

---

## Manutenzione
- Ogni tanto pulisci la ventola: la polvere può ridurre il flusso d’aria.
- Se gli RPM diventano instabili, controlla i cavi del TACH e il filtro RC.
- Se il DHT11 inizia a dare valori strani, sostituiscilo (sono sensori economici e delicati).

---

## Note finali
Il progetto funziona bene in ambienti dove serve un controllo intelligente dell’aria o della temperatura.  
È semplice da espandere e può essere migliorato aggiungendo sensori o un display.
