# Matrice Interattiva delle Minacce per Sistemi di Intelligenza Artificiale

[![Live Demo](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-5b3cf5.svg)](https://tavardt-italia.github.io/ai-threat-matrix-it/)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

***

Matrice interattiva delle minacce e motore di valutazione della postura difensiva per Grandi Modelli Linguistici e agenti IA sviluppato da **TAVARDT**. Basato sugli standard OWASP Top 10 for LLM Applications e sul framework MITRE ATLAS, lo strumento verifica le vulnerabilità, quantifica punteggi di robustezza ed esporta blueprint di mitigazione mirati.

***

## Funzionalità Principali e Architettura Difensiva

* **Valutazione Adattiva all'Architettura**: Calibra l'analisi delle minacce su quattro modelli applicativi specifici, inclusi agente autonomo, pipeline RAG, chat interattiva e API di backend.
* **Quantificazione Metrica della Postura**: Determina un punteggio difensivo calibrato da 0 a 100 punti combinando coefficienti di rischio ponderati e controlli di protezione attivi.
* **Esportazione di Piani di Mitigazione**: Produce blueprint operativi in formato Markdown che illustrano le carenze rilevate, i gap critici e le misure correttive necessarie.

***

## Vettori di Rischio e Impatto Operativo

Implementare modelli di linguaggio senza un modello formale delle minacce espone l'ambiente di produzione a manipolazione dei dati, exploit laterali e perdita di controllo dei processi. Il valutatore monitora dieci vettori critici lungo l'intero ciclo di vita operativo dell'IA:

* **Iniezione di Prompt Diretta e Indiretta (OWASP-LLM01)**: Intercetta input manipolativi strutturati per violare i vincoli del sistema o imporre comportamenti non autorizzati (Peso: 15 punti).
* **Divulgazione di Informazioni Riservate (OWASP-LLM02)**: Rileva la trasmissione accidentale di dati personali, parametri proprietari o registri sensibili all'interno delle risposte (Peso: 12 punti).
* **Vulnerabilità della Supply Chain (OWASP-LLM03)**: Controlla dipendenze da modelli base di terze parti, plugin non verificati e dataset esterni per fine-tuning (Peso: 10 punti).
* **Avvelenamento di Dati e Modelli (OWASP-LLM04)**: Identifica alterazioni malevole nei dati di addestramento o nelle fonti informative utilizzate per il recupero documentale (Peso: 10 punti).
* **Gestione Inadeguata dell'Output (OWASP-LLM05)**: Verifica risposte generate non sanificate trasmesse direttamente a interpreti di sistema, browser o webhook (Peso: 12 punti).
* **Autonomia e Permessi Eccessivi (OWASP-LLM06)**: Protegge contro agenti con privilegi non vincolati capaci di intraprendere operazioni distruttive su database collegati (Peso: 14 punti).
* **Estrazione del Prompt di Sistema (OWASP-LLM07)**: Contrasta interrogazioni volte a carpire le istruzioni riservate di configurazione e le regole interne di guardia (Peso: 8 punti).
* **Debolezze nei Vettori e negli Embedding (OWASP-LLM08)**: Analizza rischi di contaminazione semantica e interrogazioni non controllate nei database vettoriali (Peso: 7 punti).
* **Allucinazione e Disinformazione (OWASP-LLM09)**: Identifica elaborazioni errate o prive di riscontro oggettivo non supportate da citazioni affidabili (Peso: 6 punti).
* **Consumo Incontrollato di Risorse (OWASP-LLM10)**: Previene attacchi di esaurimento delle risorse causati da contesti eccessivi o loop ricorsivi tra agenti (Peso: 6 punti).

La postura complessiva viene classificata in **HARDENED** (da 85 a 100), **DEVELOPING** (da 60 a 84) o **VULNERABLE** (inferiore a 60). Le difese verificate ottengono l'intero punteggio, le coperture parziali il 50%, mentre i vettori esposti assegnano 0 punti.

***

## Installazione ed Esecuzione CLI

Valutate la sicurezza dei modelli in ambiente locale o integrate gate automatizzati nelle pipeline di rilascio tramite Python:

```bash
# Clonare il repository ufficiale
git clone https://github.com/TAVARDT-Italia/ai-threat-matrix-it.git

# Accedere alla directory di lavoro
cd ai-threat-matrix-it

# Valutare la postura tramite il profilo agente autonomo
python threat_matrix_evaluator.py -a agent

# Esportare un piano di hardening dettagliato in Markdown
python threat_matrix_evaluator.py -a agent -e blueprint.md

# Eseguire una verifica rigorosa con emissione JSON
python threat_matrix_evaluator.py -a agent -s -j
```

***

## FAQ Tecniche

### Quale metodologia impiega la Matrice delle Minacce di IA per valutare la postura del modello?

Il motore di valutazione correla i controlli difensivi alle dieci categorie dello standard OWASP Top 10 per LLM tramite coefficienti di rischio ponderati pari a 100 punti. In base alle difese rilevate, il sistema classifica l'architettura in HARDENED per valori pari o superiori a 85, DEVELOPING tra 60 e 84, o VULNERABLE sotto i 60 punti.

### In che modo i profili architetturali influenzano la valutazione dei rischi nel toolkit?

L'interfaccia CLI calibra il contesto di controllo su quattro profili operativi comprendenti agente autonomo, pipeline RAG, chat interattiva e interfacce API. La selezione del modello architetturale tramite l'opzione -a consente di concentrare le misure difensive sui flussi di dati caratteristici dell'applicazione.

### Come supporta le squadre di ingegneria il generatore di piani di irrobustimento?

L'esecuzione del valutatore con il parametro -e genera un piano di hardening in formato Markdown indicando i vettori scoperti e le azioni di bonifica richieste per ciascuna minaccia. Questo prospetto strutturato collega l'analisi di sicurezza alle pipeline operative definendo priorità di implementazione inequivocabili.

### Quali rischi operativi derivano da un eccesso di autonomia e permessi (LLM06)?

Assegnare facoltà operative illimitate ad agenti autonomi consente a iniezioni indirette di prompt di compiere operazioni non autorizzate su database e sistemi integrati. L'applicazione di whitelist restrittive per le chiamate e gate di convalida umana vincola le capacità dell'agente al principio del minimo privilegio.

### Il toolkit di valutazione può fungere da controllo automatizzato nelle pipeline CI/CD?

La CLI elabora file di profilo JSON tramite il parametro -p e interrompe la compilazione con codice di errore 1 quando la modalità rigorosa -s rileva vettori esposti. Unitamente all'opzione -j per l'esportazione di dati JSON strutturati, i team di sviluppo possono bloccare automaticamente il rilascio di codice vulnerabile.

***

## Link Utili

* **Portale Aziendale:** https://ag.tavardt.com/it/
* **Suite di Diagnostica:** https://tools.tavardt.com/it/
* **Contatto Tecnico:** https://ag.tavardt.com/it/contatto/

***

### Licenza
Rilasciato sotto Licenza MIT. Consultare [LICENSE](LICENSE) per tutti i dettagli.

***

© 2026 TAVARDT. Tutti i diritti riservati.
