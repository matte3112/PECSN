# Cloud RAN-based Cellular System Simulation

Questo repository contiene il progetto finale per il corso di **Performance Evaluation of Computer Systems and Networks (PECSN)** presso l'**Università di Pisa** per l'Anno Accademico 2023/2024.

L'obiettivo dello studio è analizzare le prestazioni di un sistema cellulare basato su architettura **Cloud-RAN (C-RAN)** al variare di diversi parametri di configurazione. Il simulatore ad eventi discreti è stato interamente sviluppato sfruttando il framework **OMNeT++**.

---

## 🧐 Panoramica del Progetto

Il cuore del progetto consiste nel valutare l'efficacia della **compressione dei pacchetti** all'interno della rete per ottimizzare il **ritardo end-to-end (end-to-end delay)** tra la generazione del traffico e la cella di destinazione. 

Il sistema modella il seguente flusso di rete:
* **AS (Application Server)**: Genera i pacchetti a intervalli di tempo regolati da una distribuzione esponenziale. La dimensione dei pacchetti segue invece una distribuzione esponenziale o lognormale.
* **BBU (Baseband Unit)**: Riceve i pacchetti dall'AS e gestisce l'instradamento verso i vari moduli RRH tramite una coda con politica FIFO. Se la modalità di compressione è attiva, riduce istantaneamente la dimensione del pacchetto prima di trasmetterlo sul link a banda limitata.
* **RRH (Remote Radio Head)**: Riceve i pacchetti dalla BBU. Se il pacchetto è compresso, l'RRH esegue una fase di decompressione che richiede un tempo non nullo prima di inoltrare il dato. Per gestire l'attesa, ogni RRH è dotato di una propria coda FIFO.
* **CELL**: Rappresenta l'elemento finale della rete che riceve il pacchetto e si occupa di misurare e memorizzare le statistiche sul ritardo complessivo.

---

## 📊 Scenari Esplorati e Risultati Chiave

Il comportamento del sistema è stato validato sia teoricamente (attraverso modelli di code M/M/1, M/D/1 e M/G/1) sia sperimentalmente per verificarne la stabilità e la coerenza.

Dall'analisi approfondita degli scenari emergono due conclusioni fondamentali:
* **Quando NON comprimere (Link Veloci / Basso Carico)**: Se la velocità del link di trasmissione è molto alta rispetto alla dimensione dei pacchetti, le code alla BBU sono quasi nulle. In questo caso la compressione è svantaggiosa perché introduce solo il ritardo di decompressione nell'RRH senza portare benefici reali.
* **Quando COMPRIMERE (Link Lenti / Alto Carico)**: Quando il tasso di utilizzo della BBU è elevato e si generano code consistenti, la compressione diventa fortemente consigliata. La riduzione del tempo di attesa nella coda della BBU compensa ampiamente il successivo tempo speso dall'RRH per decomprimere il pacchetto.

---

## 👥 Membri del Gruppo
* Matteo Halilaga
* Lorenzo Mancinelli
* Rocco Giuseppe Pastore
