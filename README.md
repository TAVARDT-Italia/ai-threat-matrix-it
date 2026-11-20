# Matrice Interattiva delle Minacce per Sistemi di Intelligenza Artificiale

[![Live Demo](https://img.shields.io/badge/GitHub%20Pages-Live%20Demo-38bdf8?style=for-the-badge)](https://tavardt-italia.github.io/ai-threat-matrix-it/)
[![Standard](https://img.shields.io/badge/Standard-OWASP%20LLM%20%26%20MITRE-3b82f6?style=for-the-badge)](https://tavardt-italia.github.io/ai-threat-matrix-it/)
[![Privacy](https://img.shields.io/badge/Privacy-100%25%20Client--Side-10b981?style=for-the-badge)](https://tavardt-italia.github.io/ai-threat-matrix-it/)
[![License](https://img.shields.io/badge/License-MIT-slate?style=for-the-badge)](LICENSE)

Matrice interattiva delle minacce e guida di mitigazione per modelli linguistici e sistemi di IA. Basato su OWASP LLM e MITRE ATLAS.

Sviluppato per organizzazioni e professionisti in **Italia**, questo repository fornisce una matrice specialistica per la valutazione della sicurezza e la formulazione di piani di blindatura per sistemi con intelligenza artificiale generativa e modelli linguistici.

---

## Modalita Operative

### 1. Applicazione Web nel Browser (GitHub Pages)
Interfaccia visiva accessibile direttamente dal browser web:
- **Indirizzo Ufficiale**: [https://tavardt-italia.github.io/ai-threat-matrix-it/](https://tavardt-italia.github.io/ai-threat-matrix-it/)
- **Riservatezza Totale**: Esecuzione interamente nel motore JavaScript locale. Nessuna informazione architetturale viene trasmessa a server esterni.

### 2. Strumento da Linea di Comando (CLI)
Per pipeline di integrazione continua (CI/CD) o verifiche locali:

```bash
# Valutazione di base per profilo di agente autonomo
python threat_matrix_evaluator.py --arch agent

# Esportazione di Blueprint Difensivo in formato Markdown
python threat_matrix_evaluator.py --arch rag --export-blueprint hardening-blueprint.md

# Modalita rigorosa per gate di sicurezza (esce con codice 1 se vi sono vulnerabilita)
python threat_matrix_evaluator.py --profile profile.json --strict

# Esportazione in formato JSON
python threat_matrix_evaluator.py --arch agent --json
```

---

## 10 Vettori di Minaccia Ispezionati (OWASP Top 10 for LLMs)

1. **Iniezione di Prompt (Diretta e Indiretta)**: Manipolazione delle istruzioni del modello tramite input ingannevoli o contesto esterno.
2. **Fuga di Informazioni Riservate**: Diffusione involontaria di dati sensibili o credenziali nelle risposte generate.
3. **Vulnerabilita della Supply Chain**: Librerie non verificate, estensioni vulnerabili o modelli privi di tracciabilita.
4. **Avvelenamento di Dati e Modelli**: Alterazione fraudolenta dei dataset di addestramento o delle basi documentali.
5. **Gestione Inadeguata dell Output**: Inoltro diretto dell output del modello a interpreti di script o motori database.
6. **Eccessiva Autonomia degli Agenti**: Strumenti dotati di permessi critici privi di presidio umano o limiti di esecuzione.
7. **Fuga del Prompt di Sistema**: Estrazione non autorizzata delle istruzioni riservate configurate nel prompt iniziale.
8. **Debolezze negli Embedding e Vettori**: Inserimento di record malevoli nel database vettoriale del RAG per manipolare il recupero.
9. **Allucinazioni e Disinformazione Critica**: Generazione di dati falsi in processi decisionali o operativi critici.
10. **Consumo Illimitato di Risorse**: Esaurimento delle risorse di calcolo o costi anomali causati da query massive.

---

## Integrazione con GitHub Actions

```yaml
name: AI Threat Matrix Gate
on: [push, pull_request]

jobs:
  evaluate-ai-security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Installa Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'
      - name: Esegui Valutazione della Matrice di Minacce
        run: |
          python threat_matrix_evaluator.py --arch agent --strict
```

---

## Standard Istituzionali e Conformita

- **Giurisdizione**: Italia
- **Quadro Normativo**: Linee Guida Nazionali ed Europee per la Sicurezza dell IA e OWASP LLM
- **Organizzazione**: [TAVARDT-Italia](https://github.com/TAVARDT-Italia)

## Portali e Risorse TAVARDT

- **Portale Principale**: [https://ag.tavardt.com/it/](https://ag.tavardt.com/it/)
- **Strumenti di Sicurezza Informatica**: [https://tools.tavardt.com/it/](https://tools.tavardt.com/it/)
- **Contatto Tecnico**: [https://ag.tavardt.com/it/contatto/](https://ag.tavardt.com/it/contatto/)

---

### Licenza
Rilasciato sotto licenza MIT. Per maggiori dettagli consultare il file [LICENSE](LICENSE).
