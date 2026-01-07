# Microsoft SQL Server

We support integrating with Microsoft SQL Server, for more information see: https://www.microsoft.com/en-us/sql-server

## SSL/TLS Certificates

Microsoft enforces TLS encrpytion by default on SQL Server products such as Azure SQL Server, however, we also provide higher certification levels than the encryption required level. For more information on encryption by default on Azure SQL Server, please see: https://learn.microsoft.com/en-us/azure/azure-sql/database/security-overview?view=azuresql

For verify-ca and verify full modes, Microsoft uses a public certificate authority that is already available in most trusted certificate defaults. However, if a self-signed certificate is used, a certificate can still be uploaded for these modes where check on the server certificate and host name is wanted.