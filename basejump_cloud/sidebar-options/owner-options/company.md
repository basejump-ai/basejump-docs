# Company

The company page is only available to the account Owner. The company page provides 3 tabs:
- Members
- Branding
- Advanced

## Members

The members page is used to manage all company members. Members can be added or deleted. To add a member, type in their email and select their role and then click &quot;send invitation&quot;. 

![Invite company members](/images/company/invite_company_members.png)

For an overview of each role, please refer to &quot;User Definitions&quot; on the Concepts page:

[!ref](/getting-started/concepts.md)

## Branding

Company logos can be added to customize the Basejump UI with company branding.

## Advanced

The company display name and ID can be changed in this section.

### Verify Mode

There are two verify modes available:
- EXPLORE
- STRICT

![Verify mode options](/images/company/verify_mode_option.png)

Each of these control how much leniency the AI has to retrieve results.

Explore Mode   | Strict Mode
---    | ---
Allows the AI to make it's best attempt to retrieve the information. Verified results are returned, but that's unverified (non-human reviewed) results can also be returned. | Restricts the AI to only return information that has previously been reviewed and verified. This is for those who need a higher level of assurance and accuracy from what the AI is returning.

More information about verification can be found here: [!ref](/data-governance.md)

### Private Storage

For users that want improved security, they can store the AI result responses in their own private AWS object storage via S3. This security enhancement will ensure no spreadsheets from the user database is ever stored within Basejump. In order to add private storage, go to the Company -> Advanced section.

![Private storage option screenshot](/images/company/private_storage_option.png)

Use the following steps to add your own private storage:
1. Select 'Add Private Storage' and fill out the credentials for your S3 connection

![Screenshot of S3 credentials modal form](/images/company/private_storage_s3_credentials.png)

2. Here is what the successfully added storage should look like

![Private storage row example](/images/company/private_storage_row_example.png)

3. Activate your private storage to start using it. This will migrate any existing results within Basejump to your AWS bucket.

![Activate private storage](/images/company/activate_private_storage.png)

4. You will see a 'Migration started' status. Once that has been completed, the active status will have a checkmark.

![Activate private storage](/images/company/activated_private_storage.png)

This private storage is for the results generated (anything in the Data dropdown in chat) and does not include the text within the message bubble from the AI. This ensures that no spreadsheets of information are stored in Basejump object storage.

#### Deactivating Private Storage

Users can also deactivate their private storage. Once deactivated, a migration will begin to migrate information to Basejump S3 object storage to ensure users can still access their data objects. An alternative to deactivation would be adding another private storage and marking that as active instead. There can only be 1 active private storage connection at a time.

