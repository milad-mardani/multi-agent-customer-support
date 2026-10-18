# 🤖 Multi-Agent Customer Support & Credit Allocation System

An advanced, production-ready multi-agent customer support workflow built using **LangGraph**, **LangChain**, **Ollama (Llama 3.2)**, and **RAG (Retrieval-Augmented Generation)**. This system intelligently routes customer inquiries, evaluates account statuses, retrieves technical documentation, monitors sentiment, and implements a Human-in-the-Loop escalation mechanism.

---

## 🌟 Architecture & Overall Flow

The system is structured as a stateful graph (`StateGraph`) where specialized agents collaborate to handle customer requests efficiently:

![Overall Architecture](overall_architecture/0.png)

---

## 🔍 Detailed Node Breakdown & Mechanics

### 1. Triage Node
Classifies incoming customer messages into specific departments (`Billing`, `Technical`, `General`) using Pydantic structured output.
![Triage Node](overall_architecture/1.png)

### 2. Billing Node
Manages subscription statuses, payments, and transaction queries using custom tools and mock databases.
![Billing Node](overall_architecture/2.png)

### 3. Technical Node (RAG Pipeline)
Answers complex technical troubleshooting questions by performing semantic search over local documentation (`FAISS` vector store + HuggingFace embeddings).
![Technical Node](overall_architecture/3.png)

### 4. General Node
Handles polite greetings, general inquiries, and basic customer requests.
![General Node](overall_architecture/4.png)

### 5. Sentiment Analysis Node
Evaluates the emotional tone (`Positive`, `Neutral`, `Negative`) of the conversation to detect angry or dissatisfied users.
![Sentiment Node](overall_architecture/6.png)

### 6. Human-in-the-Loop / Control Node
Automatically interrupts the workflow on strongly negative sentiment or angry customer tones, allowing a human manager to review draft responses and provide overrides or manual resolutions via LangGraph `interrupt` and `Command(resume=...)`.
![Human Node](overall_architecture/7.png)

---

## 📊 Compiled LangGraph Execution Flow

The compiled state graph execution and routing logic:
![Compiled Graph](overall_architecture/5.png)

---

## 📁 Project Structure

```text
├── Multi Agent.ipynb              # Complete implementation of graph, agents, RAG, and tests
├── overall_architecture/          # Architecture and node workflow diagrams
│   ├── 0.png ... 7.png
└── README.md                      # Project documentation
