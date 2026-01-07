# Security

Security is important to us so we have a few measures in place to ensure we are shipping secure software. There are many different aspects of security that we elaborate below to help explain our internal policies. We use multiple industry standard tools to ensure the security of our application.

## 1. RBAC (Role-Based Access Control)
To help organizations provide access to only the data that should be seen by an individual, we use role-based access control. This is achieved through multiple methods at Basejump. One method is by using Teams. A Team is a group created by an administrator to limit data access. Each team may have access to different database connections. This is controlled by an administrator. Reports can only be shared within teams to ensure that requisite access has been provided to view the information. 

Additionally, when a database is added, the role associated with the username and password will be used to query the information. Therefore, the given database connection assigned to teams can only access the information based on that database role. 

Finally, when indexing the information to provide to our AI, we only index the metadata and not the table information itself. The AI also only will see the same tables that a user has permission to see. This ensures that the AI is unable to provide any information that a user is not permitted to access.

## 2. AI
We only partner with AI providers who do not train on customer data. We only use the database metadata to inform the AI and never index the rows from your data sources.

## 3. API Access
Access to our API is provided using authentication and refresh tokens. All endpoints are secured using these tokens to ensure only authorized access. There are 4 levels of token access (in order of most to least access):
- API level
- Account Owner
- Admin
- Member

Using tokens ensures that API secrets are not used frequently. Refresh tokens are required to be refreshed every 90 days and authentication tokens need to be refreshed every 15 minutes. 

## 4. SCA (Software Composition Analysis)

SCA is our first-line of defense to help write secure code. We scan our code as we’re writing it within our coding environment. Before we merge to production, we push our code to a staging environment. We ensure that the code has no vulnerabilities and any found vulnerabilities from our tool are resolved. We connect it to our Github staging repo so it can find any vulnerabilities before they make it to production. Only when all issues are resolved do we ship the code to production. Our tool also scans the code our software is dependent upon as well. This helps to ensure our code is not vulnerable due to security issues with other software. Before shipping to production, we also use a DAST tool to ensure the code is secure.

## 5. DAST (Dynamic Application Security Testing)

DAST ensures that our application, regardless of the software used, is secure. It is our final security measure and uses pentesting methods to probe our app for vulnerabilities in the same way a malicious actor might. Before shipping to production, we run an automated scan on our staging application for both the web app and the API. We resolve all alerts that are above the ‘informational’ alert level. This test probes the web app unauthenticated. We then use a manual pentest scan within the tool as an authenticated user. As new features are deployed, we use the authenticated user pentest to test the security of the new feature.

## 6. Sensitive Information Storage and Encryption

Any sensitive data is encrypted at rest. Currently, this is most pertinent in regards to credentials for database connections. All information is provided using HTTPS and SSL/TLS to ensure data encryption in transit as well.

Any database connection requires SSL/TLS support since the Basejump app won't connect if an encrypted connection can't be made. For more information on SSL/TLS support for your database, please see refer to the integrations page [!ref](/integrations/README.md)

## 7. Firewall

Internal servers and databases use private IP addresses to communicate and transmit information using a virtual private cloud (VPC). The private IPs enable the information to be communicated using local servers not connected to the internet. Access to our internal servers are white-listed by IP address. Any server connected and accessible to the internet requires authentication.

## 8. Security Reporting

Security reports are available upon request for paid customers.

This information can also be found listed on our website: [Basejump Security Policy](https://basejump.ai/security)

## 9. Whitelisting

Please reach out to support@basejump.ai if our server IP addresses are needed so you can whitelist them on your servers.