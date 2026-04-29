# Banking Intelligence & Retention Platform (BIRP)

> Plataforma de dados em nuvem para análise de churn bancário e efetividade de campanhas de retenção, construída com Azure Data Lake Gen2, Azure Databricks, ADF e Power BI.

[![CI/CD](https://github.com/SEU_USUARIO/banking-retention-platform/actions/workflows/ci.yml/badge.svg)](https://github.com/SEU_USUARIO/banking-retention-platform/actions)
[![Delta Lake](https://img.shields.io/badge/Delta%20Lake-3.x-blue)](https://delta.io)
[![Databricks](https://img.shields.io/badge/Azure-Databricks-red)](https://azure.microsoft.com/en-us/products/databricks)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## Problema de negócio

Bancos e fintechs perdem entre 15% e 25% da base de clientes ao ano por churn. Identificar clientes em risco com antecedência e avaliar a efetividade das campanhas de retenção são desafios críticos que exigem uma plataforma de dados confiável, escalável e bem documentada.

Este projeto demonstra como construir essa plataforma do zero em cloud.

---

## Objetivo técnico

Construir uma plataforma end-to-end capaz de:

- Ingerir dados de múltiplas fontes (histórico de clientes, transações e campanhas)
- Transformar e modelar os dados em camadas de qualidade crescente (medallion architecture)
- Calcular score de risco de churn por cliente
- Entregar insights via dashboard executivo e API REST
- Operar com CI/CD, monitoramento e qualidade de dados automatizados

---

## Arquitetura da solução

```
Fontes (CSV + Sintético)
        │
        ▼ Azure Data Factory
┌───────────────────────────────┐
│     Azure Data Lake Gen2      │
│  raw → bronze → silver → gold │
│        (Delta Lake)           │
└───────────────┬───────────────┘
                │ Azure Databricks / PySpark
                ▼
        Serving Layer
   ┌────────────────────┐
   │  Power BI Dashboard│
   │  FastAPI (churn API)│
   └────────────────────┘
```

> Diagrama detalhado: [`docs/architecture.md`](docs/architecture.md)

---

## Stack

| Categoria | Ferramenta |
|-----------|-----------|
| Orquestração | Azure Data Factory |
| Processamento | Azure Databricks + PySpark |
| Armazenamento | Azure Data Lake Gen2 |
| Formato | Delta Lake |
| Linguagens | Python, PySpark, SQL |
| Serving | Power BI, FastAPI |
| CI/CD | GitHub Actions + Databricks CLI |
| Versionamento | GitHub |
| Qualidade | Great Expectations |

---

## Fontes de dados

| Fonte | Tipo | Conteúdo | Caminho |
|-------|------|----------|---------|
| Kaggle Bank Churn | CSV público | Histórico de churn (10k clientes) | `data/raw/kaggle/` |
| Sintético Python | Gerado | Transações mensais por cliente | `data/raw/transactions/` |
| Sintético Python | Gerado | Campanhas de retenção e respostas | `data/raw/campaigns/` |

> Script de geração dos dados sintéticos: [`src/data_generation/generate_synthetic_data.py`](src/data_generation/generate_synthetic_data.py)

---

## Estrutura do repositório

```
banking-retention-platform/
│
├── README.md
├── LICENSE
│
├── docs/
│   ├── architecture.md          # Diagrama e decisões de arquitetura
│   ├── data-dictionary.md       # Dicionário de dados das camadas
│   ├── ADR-001-stack-choice.md  # Por que essas ferramentas
│   ├── ADR-002-infra-setup.md   # Decisões de infraestrutura
│   └── runbook-incidents.md     # Como responder a falhas
│
├── data/
│   └── samples/                 # Amostras pequenas para referência
│
├── src/
│   ├── data_generation/         # Scripts Python para dados sintéticos
│   ├── ingestion/               # Notebooks de ingestão (raw → bronze)
│   ├── transformation/          # Notebooks de transformação (bronze → silver → gold)
│   ├── serving/                 # API FastAPI e queries de serving
│   └── quality/                 # Validações Great Expectations
│
├── pipelines/
│   └── adf/                     # Templates JSON do Azure Data Factory
│
├── infra/
│   └── setup-azure.sh           # Script de provisionamento inicial
│
├── .github/
│   ├── workflows/
│   │   ├── ci.yml               # Lint, testes e validação em PRs
│   │   └── cd.yml               # Deploy em merge na main
│   └── CODEOWNERS
│
└── tests/
    ├── unit/                    # Testes unitários de transformações
    └── integration/             # Testes de pipeline end-to-end
```

---

## Como executar localmente

```bash
# Clone o repositório
git clone https://github.com/SEU_USUARIO/banking-retention-platform.git
cd banking-retention-platform

# Instale as dependências
pip install -r requirements.txt

# Gere os dados sintéticos
python src/data_generation/generate_synthetic_data.py

# Configure as variáveis de ambiente
cp .env.example .env
# edite o .env com suas credenciais Azure
```

---

## Backlog de evolução

- [x] Setup inicial do repositório e documentação
- [ ] Pipeline de ingestão raw → bronze
- [ ] Camada silver com qualidade de dados
- [ ] Camada gold com métricas de churn
- [ ] Dashboard Power BI
- [ ] API REST de scoring
- [ ] CI/CD com GitHub Actions
- [ ] Observabilidade e alertas

---

## Decisões arquiteturais

| ADR | Decisão | Status |
|-----|---------|--------|
| [ADR-001](docs/ADR-001-stack-choice.md) | Escolha da stack principal | ✅ Aceito |
| [ADR-002](docs/ADR-002-infra-setup.md) | Estrutura de infraestrutura Azure | 🔄 Em revisão |

---

## Aprendizados e trade-offs

> Seção atualizada ao final de cada ciclo. Registra decisões reais, erros cometidos e como foram resolvidos.

- **Ciclo 1**: *a preencher após conclusão*

---

## Autor

**[Seu Nome]**  
Data Engineer | 10+ anos de experiência em dados  
[LinkedIn](https://linkedin.com/in/andregomesvs) · [GitHub](https://github.com/andregomesvs)
