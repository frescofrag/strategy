# 🏗️ Hardware Specification: The Architect Node v2.0

> **System Status**: OPERATIONAL | **Architecture**: DUAL-LAPTOP HYBRID (Cloud + Local Encoding)

Questa sezione documenta l'infrastruttura fisica utilizzata per le operazioni di **FrescoFrag**. Il setup è progettato per garantire la massima stabilità del segnale (FTTH 1Gbps) e la separazione dei carichi tra il nodo di gioco e il nodo di trasmissione.

---

## 💻 Gaming Node (Laptop Sinistra)

*Ruolo: Terminale ad alte prestazioni per GeForce NOW (Cloud Gaming).*

| Componente | Specifica Tecnica | Note Operative |
| :--- | :--- | :--- |
| **CPU** | Intel i7-8650U (4C/8T) | Gestione fluida del client GFN. |
| **RAM** | 32 GB DDR4 Kingston | Sovradimensionata per stabilità multitasking. |
| **Network** | Ethernet FTTH 1 Gbps | Connessione diretta (Low Jitter). |
| **Output** | HDMI to Capture Card | Ingestione del segnale video a 1080p/60fps. |

---

## 🖥️ Monitoring & Display Layer

*Il centro di comando tattico per la visualizzazione latency-free.*

| Periferica | Specifica | Funzione Logica |
| :--- | :--- | :--- |
| **Monitor Centrale** | BenQ GL2780 (1080p) | **Primary Display**: Collegato in Pass-through. |
| **Capture Card** | External USB 3.0 | Interfaccia di acquisizione tra i due nodi. |

---

## 🎙️ Streaming & Encoding Node (Laptop Destra)

*Ruolo: Host OBS Studio, Encoding Video (QuickSync) e gestione AI Audio.*

| Componente | Specifica Tecnica | Note Operative |
| :--- | :--- | :--- |
| **CPU** | Intel i7-1165G7 (11th Gen) | Core dedicato all'encoding Iris Xe. |
| **RAM** | 64 GB DDR4 Crucial | Gestione massiva di buffer e browser sources. |
| **Microfono** | **Blue Yeti** (USB) | Acquisizione vocale con filtri RNNoise AI. |
| **OS** | Windows 11 | Ambiente ibrido per script di automazione. |

---

## 🧪 Analisi dell'Infrastruttura (Architect Insights)

L'uso di due laptop indipendenti permette di isolare i potenziali crash: un "System Failure" sul nodo di gioco non interrompe mai la trasmissione sul nodo di streaming, garantendo la continuità del servizio (High Availability).

---
*FrescoFrag Architect - Hardware Specification SEALED.*
