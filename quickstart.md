---
icon: rocket
---

# Quickstart

> [!TIP]
> This section is the same as on the Github open source page found [here](https://github.com/basejump-ai/basejump/tree/main)

A demo starter project has been created under basejump-demo to help you get started quickly.

### Dependencies
To run the demo, you will need the following:
- Either Azure and/or AWS account with access to LLM AI models
- Docker installed on your computer

> [!NOTE]
> Azure is required since only Azure embeddings are currently supported.
> However, Claude Sonnet can still be used as the primary agent LLM.
> We hope to add more embedding options soon!

### Steps
Follow the following steps to get the demo set up:
1. Clone this repo
2. Copy `basejump-demo/.env.example` to `basejump-demo/.env` and fill in your credentials
3. Run the demo:
```bash
cd basejump-demo
docker compose up -d
docker compose exec app python main.py
```

That's it! You should also be able to run code outside the container using localhost to refer to the postgres and redis instances running in docker.
After completing these steps, you should see the AI respond to your question based on the basejump database schema.

### Example usage
A complete working example can be found in `basejump-demo/main.py`. Here's the core functionality in just 10 lines:

```python
async with service.run_session() as (core_session, db):
    service_context = service.create_service_context(core_session)
    user_info = await service.create_internal_user_info(db, service_context)
    connection = await service.setup_database(db, service_context, user_info, client_conn_params)
    await service.chat(
        db,
        "Provide a report of all clients.",
        service_context,
        user_info,
        connection,
    )
```