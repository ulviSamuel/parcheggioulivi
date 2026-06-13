# Parcheggio Ulivi

![Java](https://img.shields.io/badge/Java-Console%20Application-blue)
![Stato](https://img.shields.io/badge/Stato-Progetto%20scolastico-orange)
![Anno](https://img.shields.io/badge/Anno-2023-lightgrey)
![Storage](https://img.shields.io/badge/Storage-CSV-green)

**Parcheggio Ulivi** è un progetto scolastico realizzato nel **2023** per simulare la gestione di un parcheggio multipiano tramite un'applicazione Java da console.

Il programma utilizza la **programmazione orientata agli oggetti** e file `.csv` come sistema di salvataggio dei dati, permettendo di gestire auto, scooter, auto elettriche, piazzole ordinarie, piazzole affittabili e posti con ricarica.

---

## Indice

- [Descrizione](#descrizione)
- [Funzionalità](#funzionalità)
- [Struttura del parcheggio](#struttura-del-parcheggio)
- [Tecnologie utilizzate](#tecnologie-utilizzate)
- [Struttura del progetto](#struttura-del-progetto)
- [Architettura](#architettura)
- [Formato dei file CSV](#formato-dei-file-csv)
- [Tariffe e ricavi](#tariffe-e-ricavi)
- [Validazione targhe](#validazione-targhe)
- [Esecuzione del progetto](#esecuzione-del-progetto)
- [Note sul progetto](#note-sul-progetto)
- [Possibili miglioramenti futuri](#possibili-miglioramenti-futuri)
- [Autore](#autore)
- [Licenza](#licenza)

---

## Descrizione

L'obiettivo del progetto è gestire in modo semplice un parcheggio multipiano, salvando lo stato delle piazzole su file CSV.

Ogni piazzola contiene informazioni come:

- numero identificativo;
- stato di occupazione;
- targa del veicolo parcheggiato;
- ora e minuto di ingresso;
- eventuale stato di affitto, per le piazzole affittabili.

Il progetto distingue diverse tipologie di veicoli e aree del parcheggio, permettendo una gestione differenziata tra auto ordinarie, auto elettriche e scooter.

---

## Funzionalità

Il gestionale permette di svolgere le principali operazioni legate a un parcheggio:

- inserimento di auto ordinarie;
- inserimento di auto elettriche;
- inserimento di scooter;
- uscita di un veicolo dal parcheggio;
- ricerca di un veicolo tramite targa;
- gestione di piazzole libere e occupate;
- gestione delle piazzole affittabili;
- affitto e disdetta di una piazzola;
- calcolo del costo della sosta;
- aggiornamento dei ricavi giornalieri;
- controllo del formato delle targhe;
- lettura e scrittura dei dati tramite file CSV.

---

## Struttura del parcheggio

Il parcheggio è suddiviso in più piani e settori, ognuno rappresentato da un file CSV.

| File | Area | Descrizione | Numero piazzole |
| --- | --- | --- | ---: |
| `pianoA.csv` | Piano A | Auto con piazzole affittabili | 100 |
| `pianoAScooter.csv` | Piano A Scooter | Area dedicata agli scooter | 50 |
| `pianoB.csv` | Piano B | Auto ordinarie | 90 |
| `pianoBRicarica.csv` | Piano B Ricarica | Auto elettriche con ricarica | 10 |
| `pianoC.csv` | Piano C | Auto ordinarie | 100 |

---

## Tecnologie utilizzate

- **Java**
- **Programmazione orientata agli oggetti**
- **Package Java**
- **Ereditarietà**
- **Classi astratte**
- **Enumerazioni**
- **Gestione file** con `BufferedReader` e `BufferedWriter`
- **File CSV** come database locale
- **Applicazione da console**

---

## Struttura del progetto

```text
parcheggioulivi/
│
├── Main.java
├── Console.java
│
├── bean/
│   ├── Veicolo.java
│   ├── Auto.java
│   ├── Scooter.java
│   ├── Piazzola.java
│   ├── PiazzolaAuto.java
│   ├── PiazzolaAutoAffittabile.java
│   └── PiazzolaScooter.java
│
├── business/
│   ├── BizDataBase.java
│   ├── BizRicavi.java
│   └── BizVeicoli.java
│
├── enumerations/
│   ├── Motore.java
│   ├── Piano.java
│   └── SiNo.java
│
└── util/
    └── Util.java
```

---

## Architettura

Il progetto è organizzato seguendo una separazione logica tra classi modello, logica applicativa, enumerazioni e utility.

### Package `bean`

Contiene le classi che rappresentano gli oggetti principali del dominio.

#### `Veicolo`

Classe astratta di base per tutti i veicoli.

Contiene:

- `targa`

Da questa classe derivano:

- `Auto`
- `Scooter`

#### `Auto`

Rappresenta un'automobile.

Estende `Veicolo` e aggiunge l'informazione relativa al tipo di motore:

- `ELETTRICO`
- `NON_ELETTRICO`

#### `Scooter`

Rappresenta uno scooter e contiene la targa ereditata dalla classe `Veicolo`.

#### `Piazzola`

Classe astratta che rappresenta una piazzola generica del parcheggio.

Contiene:

- numero della piazzola;
- stato di occupazione;
- ora di entrata;
- minuto di entrata.

#### `PiazzolaAuto`

Rappresenta una piazzola destinata alle auto.

#### `PiazzolaAutoAffittabile`

Estende `PiazzolaAuto` e aggiunge la possibilità di indicare se la piazzola è affittata.

#### `PiazzolaScooter`

Rappresenta una piazzola destinata agli scooter.

---

### Package `business`

Contiene la logica principale del programma.

#### `BizDataBase`

Gestisce le operazioni sui dati salvati nei file CSV.

Si occupa di:

- leggere le piazzole dai file;
- cercare veicoli tramite targa;
- parcheggiare auto ordinarie;
- parcheggiare auto elettriche;
- parcheggiare scooter;
- liberare una piazzola all'uscita del veicolo;
- aggiornare i file CSV;
- gestire piazzole affittabili;
- salvare informazioni temporanee utili per il calcolo del pedaggio.

#### `BizRicavi`

Gestisce il calcolo dei ricavi.

Permette di:

- calcolare il pedaggio in base alle ore di sosta;
- aggiungere ricavi giornalieri;
- aggiungere o rimuovere ricavi legati alle piazzole affittate.

#### `BizVeicoli`

Contiene i metodi di validazione delle targhe per auto e scooter.

---

### Package `enumerations`

Contiene le enumerazioni usate nel progetto.

#### `Motore`

Indica il tipo di motore di un'auto:

```java
ELETTRICO,
NON_ELETTRICO
```

#### `SiNo`

Rappresenta valori di tipo sì/no:

```java
SI,
NO
```

#### `Piano`

Rappresenta i piani e le aree del parcheggio:

```java
PIANO_A,
PIANO_A_SCOOTER,
PIANO_B,
PIANO_B_RICARICA,
PIANO_C
```

---

### Package `util`

Contiene classi di supporto.

#### `Util`

Classe pensata per gestire operazioni comuni, come l'inserimento controllato di valori da tastiera tramite `Scanner`.

---

## Formato dei file CSV

I file CSV vengono usati come archivio locale per memorizzare lo stato del parcheggio.

### Piazzole auto ordinarie, scooter e ricarica

Esempio:

```csv
151,NO,NESSUNA,0,0
```

Campi:

| Posizione | Significato | Esempio |
| ---: | --- | --- |
| 1 | Numero piazzola | `151` |
| 2 | Occupata | `NO` |
| 3 | Targa veicolo | `NESSUNA` |
| 4 | Ora di entrata | `0` |
| 5 | Minuto di entrata | `0` |

### Piazzole affittabili del Piano A

Esempio:

```csv
1,NO,NESSUNA,0,0,NO
```

Campi:

| Posizione | Significato | Esempio |
| ---: | --- | --- |
| 1 | Numero piazzola | `1` |
| 2 | Occupata | `NO` |
| 3 | Targa veicolo | `NESSUNA` |
| 4 | Ora di entrata | `0` |
| 5 | Minuto di entrata | `0` |
| 6 | Affittata | `NO` |

---

## Tariffe e ricavi

Il progetto calcola i ricavi in base alla tipologia di veicolo o servizio.

| Tipo | Tariffa |
| --- | ---: |
| Scooter | `1.50 € / ora` |
| Auto ordinaria | `2.00 € / ora` |
| Auto elettrica | `3.00 € / ora` |
| Piazzola affittata | `100.00 €` |

Il calcolo della sosta arrotonda all'ora successiva se sono presenti minuti di permanenza.

---

## Validazione targhe

Il progetto controlla il formato delle targhe prima di svolgere alcune operazioni.

### Formato targa auto

```text
AA000AA
```

Dove:

- i primi due caratteri sono lettere maiuscole;
- i tre caratteri centrali sono numeri;
- gli ultimi due caratteri sono lettere maiuscole.

### Formato targa scooter

```text
AA00000
```

Dove:

- i primi due caratteri sono lettere maiuscole;
- gli ultimi cinque caratteri sono numeri.

---

## Esecuzione del progetto

Il progetto è scritto in Java e può essere aperto con un IDE come:

- IntelliJ IDEA;
- Eclipse;
- NetBeans;
- Visual Studio Code con estensioni Java.

### Compilazione da terminale

Posizionarsi nella cartella principale del progetto ed eseguire:

```bash
javac -d out $(find . -name "*.java")
```

### Avvio

Dopo la compilazione, eseguire la classe principale del progetto:

```bash
java -cp out it.volta.ts.ulivisamuel.parcheggioulivi.Main
```

> **Nota:** il progetto utilizza file CSV locali. È quindi importante mantenere i file `.csv` nella posizione prevista dal codice, oppure aggiornare i percorsi nei metodi di lettura e scrittura.

---

## Note sul progetto

Questo repository contiene un **progetto scolastico del 2023**.

Il progetto è stato realizzato con finalità didattiche, principalmente per esercitarsi su:

- modellazione di classi Java;
- ereditarietà;
- classi astratte;
- enumerazioni;
- gestione di input da console;
- lettura e scrittura su file;
- uso di file CSV come sistema di persistenza;
- separazione tra dati, logica applicativa e classi di supporto.

---

## Possibili miglioramenti futuri

Alcune possibili evoluzioni del progetto potrebbero essere:

- sostituire i file CSV con un database relazionale;
- aggiungere un'interfaccia grafica;
- migliorare la gestione degli errori;
- rendere configurabili i percorsi dei file;
- aggiungere test automatici;
- introdurre una gestione utenti/amministratore;
- salvare lo storico degli ingressi e delle uscite;
- generare report giornalieri dei ricavi.

---

## Autore

Progetto realizzato da **Samuel Ulivi**.

---

## Licenza

Questo progetto è stato sviluppato per scopi scolastici e didattici.
