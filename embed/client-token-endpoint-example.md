> [!important]
> This example is meant for educational purposes only and not for production use.

> [!note]
> If you are developing in a local environment without a publicly accessible address, you'll need to use a tunneling service such as ngrok to expose your local server to the internet over https. When you do this, you'll need to update the `Embed-Origin` header in the example to match the ngrok url.

```python ~Python/Flask Example~

import requests
import logging
from flask import redirect

logger = logging.getLogger(__name__)

# --- Configuration ---
BASEJUMP_API_URL = "https://api.basejump.ai/v1"
BASEJUMP_EMBED_URL = "https://app.basejump.ai/embed"
BASEJUMP_API_CLIENT_SECRET = "YOUR_API_KEY_CLIENT_SECRET"
BASEJUMP_API_OWNER_ACCESS_TOKEN = "YOUR_API_OWNER_ACCESS_TOKEN"
BASEJUMP_CLIENT_UUID = "YOUR_CLIENT_UUID"
BASEJUMP_TEAM_UUID = "YOUR_TEAM_UUID"


# --- Simulated User Class (Use your own user/session logic) ---
class User:
    def __init__(self, username, email, is_authenticated, basejump_user_uuid=None):
        self.username = username
        self.email = email
        self.is_authenticated = is_authenticated
        self.basejump_user_uuid = basejump_user_uuid

    def save(self):
        # Simulate saving the user to a database
        print(f"User {self.username} saved with Basejump UUID: {self.basejump_user_uuid}")


# --- Example request object (substitute this with real user/session logic) ---
user = User(username="joel", email="joel@example.com", is_authenticated=True)


# --- Logic starts here ---
if not user.is_authenticated:
    print({"error": "Unauthorized"})
    exit(1)

# If user does not yet have a basejump_user_uuid
if not user.basejump_user_uuid:
    # 1. Create new Basejump user
    request_url = BASEJUMP_API_URL + "/account/user/"

    response = requests.post(
        request_url,
        headers={
            "Content-Type": "application/json",
            "Client-Secret": BASEJUMP_API_CLIENT_SECRET,
        },
        params={
            "username": user.username,
            "email": user.email,
            "role": "MEMBER",
        }
    )

    if response.status_code != 200:
        logger.error("Failed to create Basejump user: %s", response.text)
        print({"error": "Unauthorized"})
        exit(1)

    user.basejump_user_uuid = response.json().get("user_uuid", "")
    user.save()

    # 2. Add user to Basejump team
    request_url = (
        BASEJUMP_API_URL
        + f"/account/user/{user.basejump_user_uuid}/team/{BASEJUMP_TEAM_UUID}/"
    )

    response = requests.post(
        request_url,
        headers={
            "Content-Type": "application/json",
            "Authorization": f"Bearer {BASEJUMP_OWNER_ACCESS_TOKEN}",
        },
    )

    if response.status_code != 200:
        logger.error("Failed to add Basejump user to team: %s", response.text)
        print({"error": "Unauthorized"})
        exit(1)

# 3. Get embed auth redirect URL
BASEJUMP_USER_UUID = user.basejump_user_uuid

response = requests.post(
    BASEJUMP_EMBED_URL + "/get-embed-redirect-url/",
    headers={
        "Content-Type": "application/json",
        "Client-Secret": BASEJUMP_API_CLIENT_SECRET,
        "Embed-Origin": "https://myapp.com",
    },
    data={
        "client_uuid": BASEJUMP_CLIENT_UUID,
        "user_uuid": BASEJUMP_USER_UUID,
        "team_uuid": BASEJUMP_TEAM_UUID,
        "view": "chat",
        # Optional - inline or floating
        "display_type": "floating",
        # Username is required for service users
        # "username": "subuser1",
    },
)

if response.status_code != 200:
    logger.error("Failed to request embed URL: %s", response.text)
    print({"error": "Unauthorized"})
    exit(1)

embed_redirect_url = response.json().get("redirect_url", "")
if not embed_redirect_url:
    logger.error("embed_redirect_url is required")
    print({"error": "embed_redirect_url is required"})
    exit(1)

# Redirect user to the embed_redirect_url
return redirect(embed_redirect_url)
```