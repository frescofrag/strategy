# Streaming Stack: Infrastruttura Logica

Configurazione software e routing del segnale tra Gaming Node e Streaming Node.

## 🏗️ Visual Architecture (Data Flow)

```text
[ GAMING NODE ]                    [ STREAMING NODE ]
(Laptop Sinistra)                  (Laptop Destra)
      |                                   |
      |--- [ GeForce NOW ]                |--- [ OBS Studio ]
      |      (1080p/60fps)                |      (QuickSync H.264)
      |                                   |             ^
      |           [ Capture Card ]        |             |
      +----------> (USB External) --------+-------------+
                          |               |
                   [ PASS-THROUGH ]       |--- [ Yeti Mic ] (Audio Input)
                          |               |--- [ StreamElements ] (Overlays)
                          v               |--- [ PowerShell Script ] (Automation)
                   [ MONITOR CENTRALE ]
                     (27″ 1080p / 60Hz)
```

## 🔗 Capture Architecture

| Elemento | Specifica | Note |
| :--- | :--- | :--- |
| **Capture Card** | Esterna USB (1080p @ 60fps) | Interfaccia tra Laptop Sinistra e Destra |
| **Monitor Centrale** | HDMI Pass-through | Visualizzazione latency-free per il gaming |
| **Encoding Node** | Laptop Destra (Iris Xe) | Hardware encoding dedicato |

## 🎥 Software Stack

| Tool | Funzione | Configurazione Tecnica |
| :--- | :--- | :--- |
| **GeForce NOW** | Gaming (Performance Plan) | Eseguito sul Laptop Sinistra. |
| **OBS Studio** | Streaming Host (QuickSync) | 1080p @ 60fps, 6000 Kbps (CBR) |
| **StreamElements** | Alert & Bot | Integrazione via Browser Source |
| **PowerShell Script** | Media Automation | Symlink Watcher per Instant Replay (120s) |

## 📊 SaaS Data Stack (Game Intelligence)

Strumenti esterni per l'analisi dei dati in background (fondamentali per workflow su GeForce NOW).

| Tool | Funzione | Integrazione Tattica |
| :--- | :--- | :--- |
| **Dune Gaming Tools** | Build Simulator | [Dune: Awakening Skill Builder](https://dune.gaming.tools) |
| **Steam Overlay** | Data Source | Browser interno per consultazione rapida wiki/mappe |

### ⚙️ OBS Deep Dive (Streaming Node)

- **Encoder**: QuickSync H.264 (Hardware)
- **Rate Control**: CBR @ 6000 Kbps
- **Target Usage**: TU1 (Slower - Massima Qualità)
- **Profile/Keyframe**: High / 2s
- **Recording**: Matroska (.mkv) per resilienza ai crash
- **Replay Buffer**: 120s (attivo per "Instant Clips")
- **Audio Sample Rate**: 48 kHz (Standard professionale)

### 🎙️ Audio Processing Chain (Yeti Microphone)

La catena è ottimizzata per la chiarezza vocale e l'abbattimento del rumore ambientale (typing/ventole).

1. **RNNoise**: Soppressione rumore basata su AI.
2. **Noise Gate**: Soglie -40dB/-35dB per isolare la voce.
3. **Compressor**: Ratio 4:1, Soglia -18dB. Livella i picchi e i sussurri.
4. **Limiter**: Soglia -3dB (Hard Ceiling per evitare clipping).

### 🎮 Game Audio & Ducking (Capture Card)

1. **Sidechain Compressor**: Ratio 8:1 con **Yeti** come sorgente. Abbassa automaticamente il volume del gioco quando l'utente parla (Ducking).
2. **Limiter**: Soglia -15dB per mantenere il gioco sempre in sottofondo rispetto alla voce.

## 🧪 Analisi del Rischio (Technical Debt)

1. **Bottleneck USB**: Verificare se la scheda di acquisizione condivide il controller USB con altre periferiche critiche sul Laptop Destra.
2. **Latenza Cloud**: La combinazione GeForce NOW + Capture Card + OBS aggiunge diversi layer di latenza.
3. **Audio Desync**: Il processing pesante può introdurre un leggero ritardo audio. Verificare se è necessario un "Sync Offset" (ms).

---
*FrescoFrag Architect - Infrastructure Documentation SEALED.*
