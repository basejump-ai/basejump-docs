---
icon: home
---

# What is Basejump?

Basejump first and foremost is an open source project that allows you to chat with your data **reliably**. Basejump indexes a database and connects it with an AI data agent to chat with your data. We use deterministic tools to check the LLM output and ensure the data can be trusted.

Not only do we provide the agents, but also the complete framework to quickly connect AI to your data and track the results.

## Key Features
* ✅ **Accuracy**: Uses SQLglot to parse and validate queries, preventing hallucinated tables, columns, or filters
* 🔒 **Security**: Role-based access control ensures users and AI agents only access provisioned data
* ⚡ **Fast Indexing**: Redis vector database integration for rapid semantic search
* 🗄️ **Full Tracking**: Pre-configured schema tracks chat history, clients, teams, users, and query results
* 💾 **Smart Caching**: Support semantic caching for retrieval of datasets based on similar questions
* 📦 **Result Storage**: Saves data results for later reference and auditing

## Why Basejump?
**Reliability, Reproducibility, and Robustness** (yes, we forced the alliteration).

We provide a data agent with features designed for robustness:
- **Deterministic validation** using SQLglot to parse and verify every query
- **Multi-level access control** supporting RBAC through clients, teams, and users
- **Complete audit trail** with queries and results saved in a pre-configured database schema

## Ready to Get Started?
Read the "Getting Started" section next to explore fundamental concepts in the open source project:

[!ref](/getting_started.md)

Or go to the Basejump cloud section to learn more about our hosted offering:

[!ref](/basejump_cloud/README.md)