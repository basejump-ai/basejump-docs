---
icon: gear
---

# Integrations

Basejump relies on both database profiling and AI models in order to function. This section gives some information on what is currently supported.

Don't see an integration? We welcome any community contributions! Go to our [open source project](https://github.com/basejump-ai/basejump) to open a PR.

## Databases
The Basejump AI platform currently integrates with 6 DBMS types:
- MS SQL Server
- MySQL
- Postgres
- Redshift
- Snowflake
- Athena

However, adding a new one is relatively simple. The inspector classes in Basejump open source are where this is handled and can be found in `basejump-core/basejump/core/database/inspector/`. These are built on top of SQLAlchemy's [Inspector class](https://docs.sqlalchemy.org/en/20/core/reflection.html#sqlalchemy.engine.reflection.Inspector).

For a list of supported databases via SQLAlchemy, you can go to their website [here](https://docs.sqlalchemy.org/en/20/dialects/).

## AI Models
Basejump requires an AI model to run. Right now we support AI models hosted on either AWS or Azure. Any model that LlamaIndex supports, Basejump can hypothetically support. 

To add a new model to Basejump, just update the `AIModelSchema` in `basejump.core.models.schemas` and submit a PR. Make sure to test your new model before submitting the new PR.