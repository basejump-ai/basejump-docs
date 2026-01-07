> [!important]
> In order to use the Basejump embed code, you will need to generate an OWNER-level [API Key](/sidebar-options/owner-options/api-keys.md).

### Generating an Embed Code

To generate a unique embed code, visit the **Embed Code** tab within the **Developer** section of the sidebar.

Copy the embed code in the example or click **preview** to test the embed code output in a new tab. The preview uses a unique client token endpoint which only works while logged into the Basejump web app. **Do not use this client token endpoint in your embed code as it will not work.**

Your embed code will look something like this:

```html ~Example embed code:~
<link
  rel="stylesheet"
  type="text/css"
  href="https://cdn.basejump.ai/css/embed.min.css"
/>
<script
  type="text/javascript"
  src="https://cdn.basejump.ai/js/embed.min.js"
></script>
<script type="text/javascript">
  window.addEventListener("DOMContentLoaded", function () {
    const embed = new BJEmbed({
      public_key: "YOUR_PUBLIC_KEY",
      client_token_endpoint: "YOUR_CLIENT_TOKEN_ENDPOINT",
      container: document.querySelector("#bjai-embed"),
      view: "chat",
      // optional
      theme: "light",
      basejump_iframe_url: "https://app.basejump.ai",
      assistant_name: "AI Data Agent",
      colors: {},
      display_type: "floating", // floating, inline
      username: "subuser1", // required for service members
    });
  });
</script>
<div id="bjai-embed"></div>
```

### Customizing the Embed Code

You will need to update the values `YOUR_PUBLIC_KEY` and `YOUR_CLIENT_TOKEN_ENDPOINT` in the embed code, all others can be left as default if you choose.

Here are all the arguments available for the embed code:

**Required:**

- **public_key:** The public key generated alongside your API key. You can access this in the API keys tab by selecting the key and copying it from the key details.
- **client_token_endpoint:** The path to a unique endpoint on your applications server, ex: `https://myapp.com/basejump-client-token-endpoint`
- **container:** The container element to render the embed into. By default this is set to the first element with the id `bjai-embed`.
- **view:** The view to display after authentication. Currently only supports **chat**.

**Optional:**

- **assistant_name:** The name of the assistant you wish to use for the Basejump Data Agent. This is the name that will be displayed in the chat interface. By default this is set to "AI Data Agent".
- **colors:** An object containing the colors to use for the chat interface. By default this is set to the Basejump color scheme.

  ```json ~Example colors object:~
  {
    "text-primary": "#6d28d9",
    "icon": "#f59e42",
    "icon-hover": "#e67c19",
    "button": "#3b82f6",
    "button-text": "#ffffff",
    "button-hover": "#e5e7eb",
    "button-primary": "#ff69b4",
    "button-primary-hover": "#ff1493",
    "button-secondary": "#50fa7b",
    "button-secondary-hover": "#22c55e",
    "chat-bubble": "#b4f8ff",
    "chat-bubble-primary": "#a78bfa",
    "chat-bubble-text": "#212121",
    "chat-bubble-thoughts-text": "#ffffff",
    "chat-bubble-primary-text": "#fff7fb",
    "success": "#a78bfa",
    "error": "#ef4444",
    "warning": "#f59e42",
    "info": "#38bdf8"
  }
  ```

- **theme:** The theme to use for the chat interface. Options are "light" or "dark". By default this is set to "light".

- **display_type:** The display type to use for the chat interface. Options are "floating" or "inline". By default this is set to "floating".

- **username:** The username for the service member sub member. This is required if you are providing a user_uuid for a service member.

Once you have updated these values you can place the embed code into your application. Place the code within the page or component where you wish to have the chat ui accessible.
