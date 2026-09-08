# 🍰 Vava Doces — Data Lakehouse & Modern Data Pipeline (v2.0)

[![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)](https://www.python.org/)
[![Polars](https://img.shields.io/badge/Polars-Fast_DataFrames-CD7F32.svg)](https://pola.rs/)
[![DuckDB](https://img.shields.io/badge/DuckDB-OLAP_Engine-FFF000.svg)](https://duckdb.org/)
[![dbt](https://img.shields.io/badge/dbt-Transformations-FF694B.svg)](https://www.getdbt.com/)
[![Architecture](https://img.shields.io/badge/Docs-C4_Model_&_ADRs-green.svg)](docs/)

> **Pipeline de Engenharia de Dados de alta performance para apuração de custo operacional, margem de contribuição e Unit Economics do ecossistema Vava Doces.**

---

## 📌 Contexto & Evolução do Projeto (v1.0 vs v2.0)

Este repositório representa a **Versão 2.0 (Refatoração para Engenharia de Dados)** do sistema de gestão financeira e custos operacionais da doceria.

* 🔗 **[Acessar Repositório v1.0 (Legado)](https://github.com/GilJSantana/vava_doces):** Aplicação inicial desenvolvida para prototipagem rápida da interface e regras de negócio usando Pandas e Streamlit.
* 🚀 **Versão 2.0 (Este Repositório):** Re-arquitetado sob o paradigma do **Modern Data Stack (MDS)** e **Data Lakehouse Local**, com foco em processamento colunar vetorizado, concorrência OLAP, idempotência e governança de dados.

---

## 🎯 O Problema de Negócio

Garantir o cálculo preciso de **Unit Economics** (custo por grama/unidade de insumo, margem de contribuição real por produto, taxa de perda de insumos na produção e ponto de equilíbrio) através do processamento automatizado e seguro de fontes de dados operacionais e financeiras.

---

## 🛠️ Tech Stack & Decisões Arquiteturais

| Componente | Tecnologia | Papel no Pipeline |
| :--- | :--- | :--- |
| **Ingestão & Carga** | **Polars** | Leitura vetorizada com *Lazy Evaluation* e pré-processamento de alta performance. |
| **Data Quality (Ingestão)** | **Pandera / Pydantic** | Validação rigorosa de schemas e contratos de entrada em tempo de execução. |
| **Data Warehouse OLAP** | **DuckDB** | Engine analítica colunar em memória para execução de consultas complexas. |
| **Transformação & Testes** | **dbt (dbt-duckdb)** | DML modular em SQL, linhagem de dados (*Data Lineage*) e testes de integridade. |
| **Modelagem de Dados** | **Kimball (Star Schema)** | Organização da camada Gold em Tabelas Fato e Dimensões. |
| **Armazenamento Final** | **Apache Parquet** | Formato de arquivo colunar aberto e altamente compactado. |

---

## 📂 Estrutura do Repositório

```text
vava_doces_lakehouse-v2/
├── docs/                      # Documentação de Arquitetura (C4 Model) e ADRs
│   ├── adr/                   # Architecture Decision Records
│   └── architecture/          # Diagramas de arquitetura em Mermaid
├── data/
│   ├── raw/                   # Camada Bronze (Arquivos brutos CSV/Excel)
│   └── processed/             # Camada Gold (Parquet / DuckDB)
├── src/
│   ├── ingestion/             # Scripts de carga e pipeline Polars
│   └── quality/               # Validadores de contrato de dados (Pandera)
├── dbt_project/               # Projeto dbt integrado ao DuckDB
│   ├── models/                # Camadas Silver (Staging) e Gold (Marts)
│   └── tests/                 # Testes automáticos do dbt
├── tests/                     # Testes unitários em Python (Pytest)
└── README.md
```

Como Executar o Projeto Localmente

Pré-requisitos:
- Python 3.11+
- Git

Passo a Passo

1. Clone o repositório:
   ```bash
   git clone [https://github.com/GilJSantana/vava_doces_lakehouse-v2.git](https://github.com/GilJSantana/vava_doces_lakehouse-v2.git)
    cd vava_doces_lakehouse-v2
    ```
2. Crie e ative um ambiente virtual:
   ```bash
   python -m venv venv
   source venv/bin/activate  # Linux/Mac
   venv\Scripts\activate     # Windows
   ```

3. Instale as dependências:
   ```bash
   pip install -r requirements.txt
   ```

Práticas de Engenharia de Software Adotadas

- Conventional Commits: Padrão claro de mensagens(feat:, fix:, chore:, docs:, refactor:).
- GitHub Flow: Desenvolvimento isolado em branches por funcionalidade(feature/1-docs...).
- Code Review & PRs: Pull Requests vinculados a issues do repositório pata rastreabilidade.
- Data Governance: Documentação de linhagem de dados e testes automatizados de dados.

Autor

Desenvolvido po Gil Santana - [Linkedin](https://www.linkedin.com/in/giljsantana/) | [GitHub](https://github.com/GilJSantana)