# Snowflake

We support integrating with Snowflake, for more information see: https://www.snowflake.com/

## SSL/TLS Certificates

Snwoflake enforces TLS encryption by default, for more information please refer to: https://docs.snowflake.com/en/user-guide/security-encryption-end-to-end

For verify-ca and verify full modes, Snowflake uses a public certificate authority that is already available in most trusted certificate defaults. However, if a self-signed certificate is used, a certificate can still be uploaded for these modes where check on the server certificate and host name is wanted.

## Connecting Snowflake as a Datasource

When connecting Snowflake, pass the Account number in as the host. A specific database name is required for this host. A port is not necessary since Snowflake uses port 443: https://docs.snowflake.com/en/user-guide/client-connectivity-troubleshooting/common-issues