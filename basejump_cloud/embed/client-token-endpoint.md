The client token endpoint is a unique endpoint on **YOUR APPLICATION SERVER** whose primary role is to authenticate users within **YOUR APPLICATION** and then redirect authenticated users to a unique url on **app.basejump.ai**.


### Understanding Embed Authentication Flow

To ensure the security of your client token endpoint, it's important to understand the authentication process used in embed code integrations.

**At a high-level, the authentication process works as follows:**

1. When your application window is loaded, the basejump embed script will generate an iframe and embed it within your application window
2. The iframe is initially pointed to a [client token endpoint](/basejump_cloud/embed/client-token-endpoint.md) which is hosted on your application server
3. The client token endpoint authenticates users within your application
4. The client token endpoint requests a unique redirect url from Basejump and then redirects the user to that url. 
5. Basejump authenticates the user using an encrypted token included in the redirect url
6. If authenticated successfully, a Basejump web app session is created and the user is redirected to the Basejump chat interface. If not, an error is displayed or the iframe is destroyed.


> [!Note]
> If the iframe ancestor does not match the Embed-Origin, the embed session will not authenticate.

### Requesting a Redirect URL

> [!important]
> The following assumes that you have a valid **API key client secret** and a valid **team UUID**. If you do not have a valid API key, please refer to the [API Keys](/basejump_cloud/sidebar-options/owner-options/api-keys.md) documentation for more information. We also have a [client token endpoint example](/basejump_cloud/embed/client-token-endpoint-example.md) which you can checkout for greater clarification.

To request a unique embed redirect url, make a POST request to the `https://app.basejump.ai/embed/get-embed-redirect-url/` endpoint:

```json ~Example request headers~
{
    "Content-Type": "application/json",
    "Client-Secret": "YOUR_API_KEY_CLIENT_SECRET",
    "Embed-Origin": "YOUR_APPLICATION_URL"
}
```

```json ~Example request body~
{
    "team_uuid": "YOUR_BASEJUMP_TEAM_UUID",
    "user_uuid": "YOUR_BASEJUMP_USER_UUID",
    "username": "subuser1", // optional - required for service members
    "display_type": "floating", // optional - inline or floating
}
```

If your request is unsuccessful the response body will be a json object containing an `error` key.

```json ~Example 403 response~
{
    "error": "Unauthorized"
}
```

If your request is successful the response body will be a json object containing a `redirect_url` which itself contains a short lived `embed_token`.

```json ~Example 200 response~
{
    "redirect_url": "https://app.basejump.ai/embed/auth/chat/?embed_token=SHORT_LIVED_TOKEN_VALUE",
    "instructions": "Use this url to redirect the user to complete embed authentication"
}
```


### Redirecting the User

Once you have a redirect url, you can redirect the user to it. The user will be authenticated and redirected to the Basejump chat interface.

That's it! Your embed is complete and users can now access the Basejump chat interface within your application.

### Service Members

Basejump has created a special user role called a **Service Member** for external applications to use with the embed code. Service members are a special user role that cannot login to the Basejump web app. Their main purpose is to simplify the number of users an external application needs to create and manage, for example: a single service member could be shared by multiple users within an application. 

To learn more about service members, [click here](/basejump_cloud/embed/service-members.md).

