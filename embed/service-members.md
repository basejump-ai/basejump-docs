# Service Members

> [!note]
> At this time, service members can only be generated through the Basejump web app by an OWNER.

`SERVICE_MEMBER` is a special user role that cannot log in to the Basejump web app. Their main purpose is to simplify the number of users an external application needs to create and manage. For example: a single service member could be shared by multiple users within an application. **Permissions given to the service member are shared with any user accessing the embed with the same service member.**

### Creating a Service Member

To create a service member, visit the **Company Settings** page:

1. Scroll to the **Invite Company Members** form
2. Select **Service Member** from the **Role** dropdown.
3. Choose whether to add this member to all teams or select a specific team.
4. After submitting the form, you will see a new **Service Member** added to the list of company members. Copy the **User UUID** of the service member and use it in the [client token endpoint](/embed/client-token-endpoint.md) request.

### Using Service Members in the Embed Client Token Endpoint

To use a service member in the [client token endpoint](/embed/client-token-endpoint.md), you will need to include the **User UUID** of the service member in the request body.

You will also need to include the `username` key in the request body. In the background, Basejump will create a new service `SUB_MEMBER` with the username you provide and use this to authenticate the user as well as segment the user's data from other users accessing the embed with the same service member. **The username that you provide should be static and unique to your application user.**

> [!note]
> The settings for the service member are shared with all child sub members.

```json ~Example request body~
{
    "team_uuid": "YOUR_BASEJUMP_TEAM_UUID",
    "user_uuid": "YOUR_BASEJUMP_USER_UUID",
    "username": "subuser1",
    "display_type": "floating", // optional - inline or floating
}
```
