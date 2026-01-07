---
icon: gear
---

# Integrations

The open source integrations page lists all of the database integrations that we currently support:

[!ref](/integrations/README.md)

We can quickly add any integration listed on the [SQLAlchemy dialects](https://docs.sqlalchemy.org/en/20/dialects/) web page. To request a new integration be added, please email support@basejump.ai with the same email you used to create your account or open a PR in the [Basejump open source](https://github.com/basejump-ai/basejump).

# SSL/TLS Encryption

All database connections with Basejump AI are encrypted by default. If your database does not offer encryption due to a missing server certificate, Basejump AI will refuse to connect. 

There are 3 levels of TLS encryption available, referred to as SSL modes in the app:
- Required: This creates an encrypted connection, but does not verify the CA cert
- Verify CA: This creates an encrypted connection and verifies the CA cert
- Verify Full: This creates an encrypted connection, verifies the CA cert, and verifies the host name in the CA cert

Verify full is most secure since it not only encrypts the connection and verifies the certificate, but also confirms the user is connecting to the correct source, which protects against man-in-the-middle attacks. However, this does come with some additional latency. We borrowed these classifications from the Postgres SSL definitions found [here](https://www.postgresql.org/docs/current/libpq-ssl.html) and standardized these same three categories to all of our database connections.

SSL is no longer in use and has been replaced with TLS, however, SSL is still commonly used to refer to an encrypted connection. All references to SSL throughout this documentation are referring to a TLS connection.

For more advanced encryption options such as mTSL or SSH tunneling, please contact us.

# Setting up an Encrypted Connection

When on the datasources page, click 'Add Database' to add a connection. You will see the SSL Mode dropdown that allows you to set your level of preferred protection.

![SSL Mode Configuration](/images/datasources/ssl_modes.png)

In order to use the Verify CA or Verify Full SSL Modes, the User needs to upload the root CA file which has the public key needed to verify the TLS certificate. If a public certificate authority (CA) was used to generate the server certificate, the User can go to the CA website and download their root certificate. If your certificate is self-signed, you will need to provide your server certificate with the certificate chain included so the root certificate can be verified.

If your DBMS is not self-hosted, DBMS providers usually provide their CA certificates for download. Please refer to the database-specific page under integrations for more details regarding downloading the proper certificate.