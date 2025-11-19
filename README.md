# Smart Fan Controller (ESP8266 + PWM PC Fan)

Questo progetto permette di controllare una ventola PWM da 12V (ventola da PC a 4 fili) usando un **ESP8266**, un sensore **DHT11** e Home Assistant.  
Il sistema misura temperatura e umidità, regola la velocità tramite il filo PWM, legge gli RPM dal filo tachimetrico e utilizza un relè per accendere e spegnere la ventola.

La ventola e lo step-down vengono alimentati a 12V, mentre l’ESP riceve 5V tramite il convertitore.  
Il tutto è installato all’interno di una **scatola impermeabile**, con il DHT11 montato sulla facciata per misurare correttamente l’ambiente.

---

## Funzionalità principali

- Controllo velocità ventola tramite PWM (3 livelli)
- Accensione/spegnimento ventola tramite relè 12V
- Lettura RPM tramite filo TACH
- Lettura temperatura e umidità (DHT11)
- Modalità **Automatica** basata sulla temperatura
- Modalità **Manuale** da Home Assistant
- Automazioni configurabili direttamente dalla dashboard
- Installazione compatta e alimentazione unificata a 12V

---

## Componenti utilizzati

- **ESP8266** (Wemos D1 Mini / NodeMCU)
- **Ventola PWM 12V a 4 fili**
- **DHT11**
- **Relè 12V**
- **Step-down 12V → 5V**
- Alimentatore 12V
- Scatola impermeabile

---

## Come funziona

1. La ventola è alimentata a 12V.
2. Lo step-down converte i 12V in 5V per alimentare l’ESP8266.
3. Il **relè 12V** accende o spegne completamente la ventola (taglia la linea dei 12V).
4. Il filo **PWM** è collegato direttamente a un pin dell’ESP e controlla la velocità.
5. Il filo **TACH** della ventola fornisce impulsi che rappresentano gli RPM.
6. Il DHT11 misura temperatura e umidità.
7. Tutte le letture e i controlli sono disponibili in Home Assistant tramite ESPHome.

Da Home Assistant si può:

- modificare le soglie di temperatura
- forzare manualmente la velocità
- scegliere tra modalità automatica o manuale
- vedere temperatura, umidità e RPM in tempo reale

---

## Modalità automatica

La ventola si regola così:

- **Temperatura sotto la soglia minima** → ventola spenta  
- **Tra soglia minima e massima** → velocità bassa/media/alta  
- **Oltre la soglia massima** → velocità massima

Le soglie sono configurabili direttamente da Home Assistant tramite slider dedicati.

---

## Filtraggio del segnale RPM (TACH)

Per ottenere una lettura degli RPM stabile, è stato aggiunto un piccolo filtro sul filo TACH della ventola.  
Il tachimetro delle ventole PWM genera impulsi molto rapidi e spesso con rumore, per questo senza filtraggio i valori possono essere instabili.

Il filtro usato è una semplice rete RC:

- **10 kΩ in serie** sul filo TACH  
- **100 nF** collegato tra TACH e massa (GND)

Questa combinazione stabilizza gli impulsi e permette all’ESP8266 di leggere gli RPM in modo affidabile.

---

## Struttura del progetto

```text
smart-fan-controller/
│
├─ esphome/
│   └─ smart-fan-controller.yaml
│
├─ schematics/
│   └─ schema_elettrico.png
│
├─ docs/
│   └─ notes.md
│
├─ LICENSE
└─ README.md
```
Posizionamento e installazione:
Montare tutto in una scatola stagno per evitare polvere e umidità.
Tenere l’ESP in una zona dove il Wi-Fi è stabile.
Posizionare il DHT11 sul fronte della scatola, lontano dal calore della ventola.
Assicurarsi che lo step-down sia fissato bene e non tocchi parti metalliche.

Note utili:
La maggior parte delle ventole PWM lavora bene a 25 kHz di frequenza PWM.
Se la ventola non parte, controllare la linea a 12V o il relè.
Il DHT11 ha una precisione limitata, ma è sufficiente per il controllo ventola.
Se gli RPM oscillano, verificare i collegamenti del filtro RC.
