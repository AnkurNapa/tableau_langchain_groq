# Tableau Langchain + Groq API Integration

[![PyPI version](https://badge.fury.io/py/langchain-tableau.svg)](https://badge.fury.io/py/langchain-tableau)
[![GitHub Repo](https://img.shields.io/badge/GitHub-Repository-blue?logo=github)](https://github.com/Tab-SE/tableau_langchain)

This project builds Agentic tools from Tableau capabilities for use within the [Langchain](https://www.langchain.com/) and [LangGraph](https://langchain-ai.github.io/langgraph/tutorials/introduction/) frameworks. I’ve implemented this using **Groq API** instead of OpenAI for blazing-fast performance with models like **Mixtral**.

Solutions such as Tools, Utilities, and Chains are published to the PyPi registry under [langchain-tableau](https://pypi.org/project/langchain-tableau/) following conventions for [integrations](https://python.langchain.com/docs/contributing/how_to/integrations/) to Langchain.

![tableau logo](experimental/notebooks/assets/tableau_logo_text.png)

```bash
pip install langchain-tableau
```

To see live demos of Agents using Tableau, visit:

* [EmbedTableau.com](https://www.embedtableau.com/) | [Github Repository](https://github.com/Tab-SE/embedding_playbook) | [@stephenlprice](https://github.com/stephenlprice)

---

# Table of Contents

* [Tableau Langchain + Groq API Integration](#tableau-langchain--groq-api-integration)
* [Getting Started](#getting-started)

  * [Published Solutions](#published-solutions)
  * [Experimental Sandbox](#experimental-sandbox)
* [About This Project](#about-this-project)

  * [Published Solutions](#published-solutions-1)
  * [Experimental Sandbox](#experimental-sandbox-1)
  * [Security](#security)
* [Contributors](#contributors)

![area chart](experimental/notebooks/assets/vizart/area_chart_banner.png)

# Getting Started

The easiest way to start with `tableau_langchain` is to try the Jupyter Notebooks in the `experimental/notebooks/` folder. These examples will guide you through different use cases and scenarios with increasing complexity.

## Published Solutions

To use the solutions available at [langchain-tableau](https://pypi.org/project/langchain-tableau/) in notebooks and your code, do the following:

### 1. Install `langchain-tableau`

```bash
pip install langchain-tableau
```

### 2. Use Groq API instead of OpenAI:

```python
from langchain_groq import ChatGroq  # Groq LLM wrapper
from langgraph.prebuilt import create_react_agent
from langchain_tableau.tools.simple_datasource_qa import initialize_simple_datasource_qa

# Setup Groq LLM
llm = ChatGroq(model="mixtral-8x7b-32768", api_key="your_groq_api_key")

# Setup Tableau data agent
analyze_datasource = initialize_simple_datasource_qa(
    domain='https://your-tableau-cloud-url.com',
    site='your-site-name',
    jwt_client_id='your-client-id',
    jwt_secret_id='your-secret-id',
    jwt_secret='your-secret-value',
    tableau_api_version='api-version',
    tableau_user='your-tableau-username',
    datasource_luid='datasource-luid',
    tooling_llm_model='mixtral-8x7b-32768'
)

tools = [analyze_datasource]
tableauAgent = create_react_agent(llm, tools)

messages = tableauAgent.invoke({"messages": [("human", "Which regions had the highest sales growth in Q4?")]})
print(messages)
```

## Experimental Sandbox

To develop and test solutions for the `langchain-tableau` package:

```bash
git clone https://github.com/Tab-SE/tableau_langchain.git
cd tableau_langchain
pip install -e .
pip install langgraph-cli[inmem]
```

1. Copy and configure your `.env` file:

```bash
cp .env.template .env
```

2. Run agent locally:

```bash
python main.py
```

3. Run Langgraph server (Docker must be running):

```bash
langgraph dev
```

---

# About This Project

This repository is a monorepo with two components:

* `experimental/`: for development
* `pkg/`: for production-ready packages published to PyPi

## Published Solutions

* `simple_datasource_qa.py`

  * Enables natural language queries on Tableau Datasources
  * Uses Tableau’s VizQL Data Service
  * Secure, scalable, no SQL injection risk

## Security

* Tableau access is secured via Connected Apps (JWT auth)
* Use `.env` to store sensitive keys (Groq + Tableau)

Learn more in the [Security Guide](.github/SECURITY.md)

---

# Contributors

Original Authors:

* Stephen Price [@stephenlprice](https://github.com/stephenlprice)
* Joe Constantino [@joeconstantino](https://github.com/joeconstantino)
* Joseph Fluckiger [@josephflu](https://github.com/josephflu)
* Will Sutton [@wjsutton](https://github.com/wjsutton)
* Cristian Saavedra [@cristiansaavedra](https://github.com/cristiansaavedra)
* Antoine Issaly [@antoineissaly](https://github.com/antoineissaly)

Please consider contributing to this project and help advance the intersection of Tableau and Agentic AI workflows.

![dual axis area chart](experimental/notebooks/assets/vizart/rounded-bars-blue-dark.png)
