# Matrice Interattiva delle Minacce per Sistemi di Intelligenza Artificiale

[![Live Demo](https://img.shields.io/badge/GitHub%20Pages-Live%20Demo-38bdf8?style=for-the-badge)](https://tavardt-italia.github.io/ai-threat-matrix-it/)
[![Standard](https://img.shields.io/badge/Standard-OWASP%20LLM%20%26%20MITRE-3b82f6?style=for-the-badge)](https://tavardt-italia.github.io/ai-threat-matrix-it/)
[![Privacy](https://img.shields.io/badge/Privacy-100%25%20Client--Side-10b981?style=for-the-badge)](https://tavardt-italia.github.io/ai-threat-matrix-it/)
[![License](https://img.shields.io/badge/License-MIT-slate?style=for-the-badge)](LICENSE)

Matrice interattiva delle minacce e guida di mitigazione per modelli linguistici e sistemi di IA. Basato su OWASP LLM e MITRE ATLAS.

Progettato per organizzazioni, ricercatori e team di ingegneria in **Italia**, questo repository fornisce una matrice strutturata per la valutazione della postura difensiva e la generazione di blueprint di blindatura per modelli linguistici e agenti autonomi di Intelligenza Artificiale.

---

## Modalità di Utilizzo

### 1. Applicazione Web nel Browser (GitHub Pages)
Accedi alla versione interattiva direttamente tramite browser:
- **Indirizzo Ufficiale**: [https://tavardt-italia.github.io/ai-threat-matrix-it/](https://tavardt-italia.github.io/ai-threat-matrix-it/)
- **Privacy Integrata**: Elaborazione eseguita al 100% nel motore JavaScript del browser. Nessun dato architetturale o risultato viene trasmesso a server remoti.

### 2. Utilità da Riga di Comando (CLI)
Per verifiche automatizzate nelle pipeline CI/CD o controlli locali:

```bash
# Valutazione standard con profilo agente autonomo
python threat_matrix_evaluator.py --arch agent

# Esportazione del Blueprint Difensivo in formato Markdown
python threat_matrix_evaluator.py --arch rag --export-blueprint hardening-blueprint.md

# Validazione mediante file di profilo dei controlli difensivi
python threat_matrix_evaluator.py --profile profile.json --strict

# Output strutturato in formato JSON per integrazioni
python threat_matrix_evaluator.py --arch agent --json
```

---

## 10 Vettori Critici di Rischio (OWASP Top 10 for LLMs)

1. **Iniezione di Prompt (Diretta e Indireta)**: Manipolazione delle istruzioni del modello tramite input ingannevoli o contesto esterno.
2. **Fuga di Informazioni Riservate**: Diffusione involontaria di dati sensibili o credenziali nelle risposte generate.
3. **Vulnerabilità della Supply Chain**: Librerie non verificate, estensioni vulnerabili o modelli privi di tracciabilità.
4. **Avvelenamento di Dati e Modelli**: Alterazione fraudolenta dei dataset di addestramento o delle basi documentali.
5. **Gestione Inadeguata dell'Output**: Inoltro diretto dell'output del modello a interpreti di script o motori database.
6. **Eccessiva Autonomia degli Agenti**: Strumenti dotati di permessi critici privi di presidio umano o limiti di esecuzione.
7. **Fuga del Prompt di Sistema**: Estrazione non autorizzata delle istruzioni riservate configurate nel prompt iniziale.
8. **Debolezze negli Embedding e Vettori**: Inserimento di record malevoli nel database vettoriale del RAG per manipolare il recupero.
9. **Allucinazioni e Disinformazione Critica**: Generazione di dati falsi in processi decisionali o operativi critici.
10. **Consumo Illimitato di Risorse**: Esaurimento delle risorse di calcolo o costi anomali causati da query massive.

---

## Integrazione CI/CD (GitHub Actions)

Esempio di pipeline per la verifica continua della postura di sicurezza:

```yaml
name: AI Threat Matrix Gate
on: [push, pull_request]

jobs:
  evaluate-ai-security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'
      - name: Run AI Threat Matrix Assessment
        run: |
          python threat_matrix_evaluator.py --arch agent --strict
```

---

## Conformità e Standard Tecnici

- **Giurisdizione**: Italia
- **Standard Normativo**: OWASP Top 10 per Applicazioni LLM e MITRE ATLAS
- **Organizzazione Responsabile**: [TAVARDT-Italia](https://github.com/TAVARDT-Italia)

## Portali Ufficiali

- **Portale Istituzionale**: [https://ag.tavardt.com/it/](https://ag.tavardt.com/it/)
- **Centro Strumenti**: [https://tools.tavardt.com/it/](https://tools.tavardt.com/it/)
- **Canale di Supporto Tecnico**: [https://ag.tavardt.com/it/contatto/](https://ag.tavardt.com/it/contatto/)

---

### Licenza
Rilasciato sotto Licenza MIT. Consultare il file [LICENSE](LICENSE) per i dettagli completi.
