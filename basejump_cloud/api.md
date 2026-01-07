---
icon: code
---

# API

The API documentation can be found using the following link: [API Reference](https://docs.basejump.ai/api/api-reference/)

The API can be used to automate interaction with the Basejump AI application and integrate the Basejump AI data agent with other software tools. It's also intended to allow the User flexibility to use the Basejump product using a different UI that they build themselves in addition to integrating the Basejump AI agent into another existing tool.

Besides offering capability to augment the intraction and automation experiences internal to a company, the API also allows companies to use Basejump AI as an AI data analytics vendor to supplement a service they already provide.

## Versioning and Releases

As releases are made, we will make announcements on our various social media platforms as well as via our newsletter. We use semantic versioning for our releases internally, however, the API will just refer to the major version (v1, v2, etc...). The API endpoints include the API version in their endpoint paths.

We will only support, at most, the latest 2 API releases at any given time. We will provide deprecation warnings to anyone that has not upgraded to a new API version that the prior version will soon be deprecated.

## Quickstart example

This example illustrates how to create a new user, request an access token, connect your database, and then ask a question.

```python
import os
import requests

base_url = "https://api.basejump.ai/api/v1"

# Create an ADMIN user
response = requests.post(
    url=base_url + "/account/user/",
    params={
        "username": "new_user",
        "role": "ADMIN",
    },
    headers={"client-secret": os.environ["API_KEY"]},
)
assert response.status_code == 200
response_dict = response.json()
user_uuid = response_dict["user_uuid"]

# Get the refresh token
response = requests.post(
    url=base_url + "/auth/token/",
    params={
        "user_uuid": user_uuid,
    },
    headers={"client-secret": os.environ["API_KEY"]},
)
assert response.status_code == 200
new_refresh_token = response.json()["refresh_token"]

# Get the access token
headers = {
    "Authorization": f"Bearer {new_refresh_token}",
    "Content-Type": "application/json",
}
response = requests.post(
    url=base_url + "/auth/access_token/",
    params={"user_uuid": user_uuid},
    headers=headers,
)
assert response.status_code == 200
access_token = response.json()["access_token"]
headers = {
    "Authorization": f"Bearer {access_token}",
    "Content-Type": "application/json",
}

# Create a team
response = requests.post(
    url=base_url + "/account/team/",
    params={"team_name": "pytest_team"},
    headers=headers,
)
assert response.status_code == 200
response_dict = response.json()
team_uuid = response_dict["team_uuid"]

# Add a database connection to index
conn_params = {
    "database_type": "postgres",
    "username": os.environ["HR_DEMO_DB_USER"],
    "password": os.environ["HR_DEMO_DB_PASSWORD"],
    "host": os.environ["DEMO_DB_HOST"],
    "port": int(os.environ["DEMO_DB_PORT"]),
    "database_name": os.environ["HR_DEMO_DB_NAME"],
    "query": {},
    "schemas": [{"schema_nm": "hr_demo_db"}],
    "data_source_desc": """
        A select only role for the HR demo database.
""",
    "ssl_mode": "require",
    "database_desc": """
        Human Resources (HR) demo database with employee and dependent information.
""",
    "include_default_schema": False,
}
response = requests.post(
    url=base_url + "/connection/database/",
    json=conn_params,
    headers=headers,
)
assert response.status_code == 200
conn_uuid = response.json()["conn_uuid"]
db_uuid = response.json()["db_uuid"]

# Add team to connection
response = requests.post(
    url=base_url + f"/connection/{conn_uuid}/team/",
    json={"team_uuids": [team_uuid]},
    headers=headers,
)
assert response.status_code == 200

# Add user to team
response = requests.post(url=base_url + f"/account/user/{user_uuid}/team/{team_uuid}/", headers=headers)
assert response.status_code == 200

# Create a chat
response = requests.post(url=base_url + f"/chat/team/{team_uuid}/", headers=headers)
assert response.status_code == 200
chat_uuid = response.json()["chat_uuid"]

# Ask the AI a question about your data
response = requests.post(
    url=base_url + f"/chat/{chat_uuid}/message/",
    headers=headers,
    json={"prompt": "How many employees are there?"},
)
print(response.text)
```

