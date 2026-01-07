---
icon: star
---

# Getting Started

## Installation
Create a virtual environment and then install from PyPI:
```bash
pip install basejump
```

This installs the core basejump library and common packages.

## Quickstart
To get started quickly, refer to the quickstart here:

[!ref](/quickstart.md)

## Open source project package layout

The Basejump project is a layered architecture. It consists of (in order):
- common: This is the highest layer and contains common modules for use throughout the library
- models: Contains models defining schemas using things like pydantic and SQLAlchemy.
- database: Logic for connecting to the database to store history and other information.
- service: Business logic layer that uses all of the above layers. This is the final layer before the API.

## Key Concepts

At the most fundamental level, Basejump is built on a few concepts. At its core, Basejump relies on:
- An LLM
- Data stored in a database
- A relational database
- A vector database

The `ServiceContext` class is helpful for understanding the necessary components to running the basejump project:

```python
class CoreSession(BaseModel):
    sql_engine: AsyncEngine
    redis_client_async: RedisAsync
    model_config = ConfigDict(arbitrary_types_allowed=True)


class ServiceContext(CoreSession):
    large_model_info: ModelInfo
    small_model_info: ModelInfo
    embedding_model_info: AzureModelInfo 
```

Here is a quick summary of each item:
- sql_engine: The SQL engine is the app engine. 
- redis_client_async: The Redis client is used to access the vector database.
- large_model_info: This is the primary LLM used by Basejump to answer user questions.
- small_model_info: This is a smaller and faster model used for JSON output validation or summaries.
- embedding_model_info: This is the embedding model for storing the information in your vector database.

### Basejump AI Agents
Basejump provides 2 AI data agents currently:
- DataChatAgent: The DataChatAgent is the primary agent used in Basejump. It connects with one or many database connections and can talk with your data.
- MermaidAgent: The MermaidAgent creates ERD diagrams based on your database index.

==- Agent Tools
The DataChatAgent is given 2 tools currently, a SQL tool and a visualize tool. 

The SQL tool checks the output of the agents SQL query and guides the agent through a workflow to creating a query. The visualize tool allows the agent to visualize the information from the SQLQuery using plotly.
===

### Data
The AI data agent needs access to your data. The way it does this is via an indexed database. 

This section covers the fundamentals of data access and storage for the client's database. Within Basejump, anything dealing with accessing the client database is in either the /database/client/ or /service/database/client/ packages. Client database is used to differentiate from the app database where things like CRUD operations are stored.

==- Data Profiling

This is handled by the `BaseInspector` class within Basejump. Every database supported by Basejump has an inspector class. Here is the abstract class for all databases:

```python
class BaseInspector(ABC):
    """Implements the same methods as SQLAlchemy inspector so that it can be used in
    place of the SQLAlchemy inspector for drivers which may not be compatible with
    SQLAlchemy 2
    """

    @abstractmethod
    def inspect(cls, conn: sa.Connection):
        pass

    @abstractmethod
    def get_table_names(
        self,
        schema: Optional[str] = None,
        include_views: bool = False,
        include_materialized_views: bool = False,
        include_partitioned_tbls: bool = False,
    ) -> list[str]:
        pass

    @abstractmethod
    def get_permitted_table_names(
        self,
        schema: Optional[str] = None,
        include_views: bool = False,
        include_materialized_views: bool = False,
        include_partitioned_tbls: bool = False,
    ):
        pass

    @abstractmethod
    def get_permitted_schema_names(self) -> list[str]:
        pass

    @abstractmethod
    def get_table_comment(self, table_name: str, schema: Optional[str] = None):
        pass

    @abstractmethod
    def get_columns(self, table_name: str, schema: Optional[str] = None):
        pass

    @abstractmethod
    def get_foreign_keys(self, table_name: str, schema: Optional[str] = None):
        pass
```
===
==- Indexing
A single function ised used to index a database called `index_db`. This is within the index module within the `database/client/` package.
===
==- Storage
The `ResultStore` class is used to data storage. There are currently 2 options: local storage or AWS S3 storage. Explore the store module in `basejump-core/basejump/core/database/result/store.py` for more information
===



