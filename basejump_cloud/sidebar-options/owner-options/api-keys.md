# API Keys

In the API, API keys are referred to as client secrets. A client secret is an API key that is extremely sensitive and should not be widely shared since the client secret is used to create users within the organization along with other privileged actions that manage access to the application. Client secrets have a role associated with them. A user can only create client secrets below their current privilege level. However, only the OWNER role currently is allowed to create client secrets. An OWNER can only create an OWNER level client secret through the Basejump UI.

A client secret given to a user from an OWNER allows that user to create other users if that client secret role is an ADMIN. Just like creating a client secret, users can only create other users below their current role. This means only the OWNER role can create an ADMIN. Both the OWNER and ADMIN roles can create a MEMBER. If the client secret role is a MEMBER, the MEMBER can't create users since they are already the least privileged role. However, the client secret can be used to create their own MEMBER-level refresh and access tokens.

## Adding an API Key

Navigate to the API key management page within the Basejump UI. Only the account owner will see the API key page. To start using the API, a client secret is needed, which can be generated on this page:

![The API Key management page](/images/api_keys/api_keys_page.png)

Click the 'Generate New Key' button to pull up a window to create your API key. On this window you can name the API key as well as provide a description. 

![The API Key modal window](/images/api_keys/add_api_key_modal.png)

You can also specify the access level. For more information on the various use roles, please refer to the concepts page:

[!ref](/basejump_cloud/getting-started/concepts.md)

Finally, make sure to copy your client secret since it won't be shown again.

![Image with generated client secret](/images/api_keys/generated_api_key.png)

The client secret can now be used to access the API. Keys can also be given to other developers. A developer is unable to use a key above their member role.

## Revoking an API Key

Revoking API keys allows any access granted using that client secret to be revoked. This is very useful for removing access to the application quickly (access tokens expire every 15 minutes). 

To revoke an API key, go to the API Key management page and click the ellipsis associated with the row of the API key you want to revoke. Select the 'Revoke' option.

## Accessing the API

For more information about API keys and using them within the API, please refer to the [API Reference](https://docs.basejump.ai/api/api-reference/). The API page in the docs also has high-level information regarding using the API:

[!ref](/basejump_cloud/api.md)