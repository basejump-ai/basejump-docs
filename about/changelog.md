# Changelog

## Basejump AI is Now Source Available
_January 7, 2026_

We’re excited to announce that Basejump AI is now source available! This has been a long time coming and we decided to start off 2026 by releasing Basejump under a source available license. You can check it out in our Github repo [here](https://github.com/basejump-ai/basejump).

## TLDR
- ✅ Accuracy: Uses SQLglot to parse and validate queries, preventing hallucinated tables, columns, or filters
- 🔒 Security: Role-based access control ensures users and AI agents only access provisioned data
- ⚡ Fast Indexing: Redis vector database integration for rapid semantic search
- 🗄️ Full Tracking: Pre-configured schema tracks chat history, clients, teams, users, and query results
- 💾 Smart Caching: Support semantic caching for retrieval of datasets based on similar questions
- 📦 Result Storage: Saves data results for later reference and auditing

Basejump also now supports embeds!

### Summary
Going forward, the changelog will have 3 separate sections: one for source available releases, one for API releases, and one for the UI releases.

==- Source available
**Release v0.31.4**

_January 7, 2026_

### Features
- Refactoring of the code base to prepare for the source available launch
- Upgrade to pydantic V2
- Added support for Athena

### Bugs
- Database column quoting is now working properly when there are mixed case names or other instances where columns need to be quoted
- Fixing column verification bug

### Breaking Changes
- Many functions were put into classes, most notably: ResultStore, QueryRunner, and QueryRecorder. This was released in v0.31.0, but putting here to catch up on changelog entries.

===

==- API
**Release v1.2.1**

_January 7, 2026_

### Features
- The PUT `/connection/database/{db_uuid}/` has been updated so that the index is updated and new tables are scanned when this endpoint is used.
- Added ability for end users to change the preferred LLM
- Created and supported service members
- Separated basejump into source available, internal, and API packages

#### New Endpoints
- PUT `/account/client/settings/`

### Bugs
- None

### Breaking changes
- None
===

==- UI

_January 7, 2026_

### Features
- Basejump now supports embeds

===

## Improved Accuracy, Feedback, and Private Storage
_April 10, 2025_

This release we improved AI accuracy, added thumbs up/down on user messages, and added private storage options for data retrieved from the database.

## TLDR
- :dart: Accuracy was improved by enforcing no hallucinated columns or filter values
- :+1: Users can now provide feedback to the AI using thumbs up/down on a message
- :file_cabinet: Users can store saved data results in their own private storage

### Summary

We're proud of what we have been able to accomplish this past month. Users will notice improved accuracy in the AI responses due to code added to ensure no hallucinated columns or filters. This adds to our already existing guarantee of no hallucinated tables as well as enforcement of valid SQL queries in general. The next feature we will add is enforcement of joins if they are defined in the metadata.

We also added a way for users to provide feedback to the AI. Users can now use the thumbs up/down reactions on a given message to improve accuracy of the AI responses over time.

![Thumbs up example](/images/changelog/thumbs_up_2025_04_10.png)

More information about message thumbs up/down reactions can be found here: [!ref](/basejump_cloud/sidebar-options/member-options/chat.md)

Finally, for users that want improved security, they can store the AI result responses in their own private AWS object storage via S3. This security enhancement will ensure no spreadsheets from the user database is ever stored within Basejump. In order to add private storage, go to the Company -> Advanced section.

![Private storage option screenshot](/images/changelog/private_storage_option_2025_04_10.png)

More information about private storage can be found here: [!ref](/basejump_cloud/sidebar-options/owner-options/company.md)

### API Release

==- API
**Release v1.2.0**

_April 10, 2025_

### Features
- Filter verification: the AI is now unable to filter by invalid values
- Added team and datasource descriptions to improve AI context
- Added SQL query planning so the AI will plan ahead when creating the SQL query and self-reflect
- Added S3 private storage option if customers want to save their own data in their private data store
- Added thumbs up/down reactions in chat to provide feedback to the AI
- Enforcement of columns was added so the AI is never able to use an invalid column name or one that has been ignored
- Changed the message dropdown from 'SQL' to 'Audit'

#### New Endpoints
- PUT /chat/message/{parent_msg_uuid}/thumbs-up/
- PUT /account/team/{team_uuid}/
- GET /connection/storage/list/
- POST /connection/storage/
- GET /connection/storage/migration-status/
- GET /connection/storage/{storage_uuid}/
- PUT /connection/storage/activate/{storage_uuid}/
- PUT /connection/storage/{storage_uuid}/
- DELETE /connection/storage/{storage_uuid}/

### Bugs
- Fixed issue while chatting where if two prompts were submitted simultaneously, then the prompt that completes first would cancel the other from completing


### Breaking Changes
- Changed all endpoint paths with underscores in the name to dashes
  - For example GET /database/{db_uuid}/index_status/ -> /database/{db_uuid}/index-status/

===

## New Integrations: Snowflake and MS SQL Server
_March 11, 2025_

We're excited to add 2 new integrations this week: MS SQL Server and Snowflake!

![Snowflake and SQL Server integration announcement](/images/changelog/sql_server_and_snowflake_integrations_20250311.png)

### API Release

==- API
**Release v1.1.0**

_March 11, 2025_

### Features
- Added the SQL Server and Snowflake database integrations!
- Made the port field optional when connecting your database (providers like Snowflake don't require it)

### Bugs
- Fixed inability to verify the demo objects
- Updated verification so any descendant verified result is unverified if the parent it came from or other descendants are unverified
- If foreign schemas for a given table weren't included in the accepted list of schemas, it would previously throw an error. Now that relationship is ignored and fills in None values if that foreign schema is not available as part of the database connection setup.
- Child partitions are excluded from indexing for redshift and postgres

### Breaking Changes
- None

===

## AI Generated, Human Verified
_March 6, 2025_

This launch is all about improving the trust that users have in the results that they are getting from the Basejump AI application. 

## TLDR
- :white_check_mark: Users can mark results as verified, which will then be returned to other users for semantically similar queries.

### Summary

Users can now mark a result as 'verified'. When Users mark a result as verified, it will add a checkmark to the result. 

![Verified result example](/images/changelog/verified_result_2025_03_06.png)

### Verified Results

Verifying a result will add that result to the cache, which means it will return instantly for other users once it has been added. These verified results can also be unverified if another user disagrees that this information looks correct. However, a user has to be at the same RBAC role level or greater as the other user to unverify. For example, if the user is a Member, they can't unverify an Admin's verified result.

There are 2 types of semantically similar results that can be returned in the cache:
- Identical: These results will return the same information as was originally cached if it is current within the last day. If it is older than 1 day, then the result is refreshed.
- Similar: These results will return different information, but the SQL query only differs in the where clause being applied. For example, if someone asks 'how many bagels are there?' and someone else asks, 'how many sesame seed bagels are there', the 2nd query is similar enough to be verified (we know how to count bagels), but will be updated to filter to sesame seed bagels only.

Other details to be aware of:
- If a verified result is returned and is older than 1 day, the SQL query is re-ran in order get the latest information. 
- The checkmark symbol used to indicate if a result is verified is outlined if it was by a Member and solid if it was verified by an Admin
- An Admin can confirm the verification of a Member to promote that verification to an admin

Verified results is a great initial step to getting common consensus around common metrics. Every time a result is returned, users can verify the output and other members will get the same query ran for them as well.

#### Security Implications

Identical verified results are only returned for users who share a database connection through their teams. Similar results are only returned for an organization if two users share the same database, but not necessarily the same connection. This is important for situations where Users rely on jinjafied schemas. The query is re-ran to get the information relevant to the other user's connection, but the query itself remains verified.

This setup ensures that only those who have access to shared connections are able to view semantically similar information and keeps the data secure.

### API Release

==- API
**Release v1.0.0**

_March 6, 2025_

### Features
- Added verification feature and semantic caching
- Added changing storage location via API


#### New Endpoints
- update_verify_mode `PUT /account/client/verify_mode/`
  - This endpoint allows you to change the verify mode. 
  - Verify modes control what the users are able to see.
    - STRICT means only results with similarly previously verified outputs will be returned.
    - EXPLORE means any result can be returned.
    - Both modes show verify status for all results regardless.
- get_client `GET /account/client/`
  - See the verify mode, client name, and client UUID
- setup_client_storage `POST /connection/storage/`
  - Connect S3 storage for storing results from the AI
- get_client_s3_conn `GET /connection/storage/`
  - Connect a client's S3 bucket to the database for storing results from chatting with the AI
- Update result `PUT /result/{result_uuid}/
  - Update a result. This endpoint currently is only for updating the verification status of a result.
More parameters to update will likely be added in the future.

### Bugs
- Fixed uncaptured timeout error for chats
- Fixed only top 10 tables being used for ERD diagram
- Fixed queries for other connections with jinja values not executing due to unresolved jinja

### Breaking Changes
- 1 breaking change for a changed endpoint

#### Changed Endpoints 
- save_result `POST /result/save/
  - Added the team_uuid, verified, and verified_user_uuid fields
===

## Visualizations, HIPAA Compliance, AI Internal Docs Tool, and New User Experience
_February 4, 2025_

We are proud to be launching on Product Hunt again for this release! The last time we launched on Product Hunt was Sept. 2024 and so much has changed since then.

### TLDR
- :bar_chart: A long-awaited feature was incorporating visualizations.
- :stethoscope: We're HIPAA compliant! We enforce encryption via our SSL mode options when connecting your database.
- :wrench: We gave our AI Data Assistant access to our docs. Users can now ask the AI any questions about how to use the Basejump AI app.
- :world_map: We're introducing guided tutorials which will help new users understand how to use our app.

### Summary
The primary focus was adding visualizations and our product hunt launch. So many great features were added in addition to visualizations, such as the internal docs tool for the AI, SSL support (for HIPAA compliance), and improved onboarding for new users via data objects.

![Visualization example](/images/changelog/bar_chart_2025_02_07.png)

### Highlights
- Added visualizations, internal docs tool, stop chat feature, and updated demo account creation w/data objects
- Focus on this release was adding SSL support with required as the minimum + fixing visualization-related bugs

### API Release

==- API
**Release v0.29.0**

_February 4, 2025_

### Features
- Updated stop chat to send webhook messages indicated chat has been stopped
- Added data objects to be created on account creation
- Added internal docs tool to the Basejump agent
- Added visualization support! 📊
- Enforcing SSL required to enforce encrypted connections for improved security + HIPAA compliance

#### New Endpoints
- Added DB test endpoint POST /connection/database/test/
- DELETE /result/saved/{saved_result_uuid}/
- POST /result/save/{saved_result_uuid}/
  - Notice this is just called save as opposed to all the other endpoints using saved

### Bugs
- Updated the create_chat endpoint to not allow chats created by those who don't belong to the team being passed in
- Updated code to throw error if there is a DB alias conflict

### Breaking Changes
- Result objects changed the name of the titles, subtitles, and descriptions to use a 'result_' prefix
- All of the result endpoints have changed. Most have been changed to focus on saved results as opposed to results or visual results. There are now 3 classifications of results (each with their own uuid):
  - saved_result_uuid: This is a result that was saved using POST /result/save/
  - result_uuid: This is the initial SQL query results. It is not part of a saved result until it is saved via the POST endpoint mentioned above
  - visual_result_uuid: This is the visualization related to the result_uuid. Visual results and data results (aka results) both can be used to created a saved result

#### Changed Endpoints
- GET /result/visual/{visual_result_uuid}/ -> DELETED
  - This was deleted
POST /result/visual/search/ -> DELETED
  - This was deleted
- POST /result/search/ -> POST /result/saved/search/
  - Renamed to POST /result/saved/search/
- PUT /result/{result_uuid}/ -> PUT /result/saved/{saved_result_uuid}/
  - Renamed to /result/saved/{saved_result_uuid}/
  - Removed the 'saved_result' option in the body. To save a result, you now must use the POST /result/save/- {saved_result_uuid}/ endpoint
- Removed drivername from POST /connection/database/
  - This is something configured server-side
- Any endpoints returning the GetResultHistory schema object now have an 'orphan_type'. This has two values: one for orphaned results due to connections being deleted, and the other due to teams being deleted
  - DELETE `/result/{result_uuid}/
  - GET /result/{result_uuid}/
  - PUT /result/{result_uuid}/  
===

## Redesigned Data Page, Free Accounts, Documentation, Community, and API Release
_January 14, 2025_

There were so many changes this release! We're proud of all the changes that we managed to accomplish and share with all of you.

### TLDR
- :sparkles: There is a fresh new design for data objects
- :free: We have a new free tier! Check out the [pricing page](https://basejump.ai/pricing) for details.
- :scroll: We have new [API documentation](https://docs.basejump.ai/api/api-reference/) and Basejump AI documentation
- :space_invader: Join our [Community Discord](https://discord.gg/fUucrZyP7D)!

### Redesigned Data Page

Our data page has been redesigned along with anywhere else there is a data object throughout the app. This is what the next data page looks like:

![Redesigned data page](/images/changelog/data_page_2025_01_14.png)

We focused on designing the data page to have a modern feel that also highlights the data at the top of the data tile. We set the default to the tile view to make it easy to see your metrics at a glance. 

The color of each tile indicates whether the data object is a metric (green), record (orange), or dataset (purple). We also added icons in the tabular view that represent each of these three data object types.

![Redesigned data tabular page](/images/changelog/data_tabular_page_2025_01_14.png)

The redesign should make it easier to browse the various data objects that have been retrieved from the Basejump data agent.

### Documentation

There was a huge focus on getting our documentation improved to make using our application simple and intuitive. The improvements in documentation include:
- API documentation overhaul. API documentation can be found here: [API Reference](https://docs.basejump.ai/api/api-reference/)
- Publishing Basejump AI documentation publicly (this documentation that you're reading)
- Creating an interactive tutorial when the user logs in to the app

The interactive tutorial can be activated by clicking the 'Tutorials' toggle under the profile drop-down menu. A graduation cap will appear in the header with relevant tutorials that the User can explore. 

![Interactive tutorials](/images/changelog/interactive_tutorials_2025_01_14.png)

### Free Tier

We now have free accounts! There are 2 tiers: free and developer. The developer tier comes with access to the API.

Both accounts come with 50 Basejump credits included. Once billing has been set up, the User will get another 50 free credits. After the free credits have been used, additional credits can be purchased in blocks of 500 credits. Please refer to the pricing page for more information and the differences between the tiers: [Pricing Page](https://basejump.ai/pricing).

### Community

We made a big effort to work on improving our community. We're adding the following features to improve our community focus:
- Free accounts
- [API documentation](https://docs.basejump.ai/api/api-reference/)
- [Community Discord](https://discord.gg/fUucrZyP7D)
- Basejump AI Documentation
- Roadmap
- Community board
- Public API release

The goal of all of these improvements it to get rapid feedback and involve the community with the Basejump AI application that we're building. We would love your feedback and participation!

### API Release

The UI now has an API management section which allows Users to create and delete API keys to access our API. The API was also improved by adding RBAC for token endpoints. Finally, we made our API documentation public so others can see how to use our API before even starting to use our documentation. It's part of our commitment to build a community and increase transparency.

==- API
**Release v0.28.0**

_January 14, 2025_

### Summary
The focus of this release was on improving security as well as documentation. RBAC was introduced to the API with clear roles, including:
- Account owner
- Administrator
- Member

### Highlights
- Added the OWNER-level role, added fields to chat responses, and created ability to bulk get results
- Created new client secret mgmt endpoints
- Improved security and updated the documentation
- Improved RBAC controls for the API, added feature to stop AI thoughts, and updated the API docs

### Breaking Changes
- GET /connections/database/{}/index_status/ endpoint now returns only a status enum: "queued" "started" "finished" "stopped" "scheduled" "canceled" "failed"
- PUT /account/client/reset_secret/
  - This has been deleted
- An `/auth' prefix has been added to the POST /token/ and POST /access_token/ endpoints 
- There were updates to endpoints to remove client UUIDs for the following endpoints:
  - POST `/account/team/`: Removed client_uuid as a parameter
  - GET `/account/team/`: Removed client_uuid as a parameter
  - POST `/account/user/`: Removed client_uuid as a parameter
  - PUT `/account/client/reset_secret/`: Removed {client_uuid} as a path parameter
- Not breaking, but potentially changing behavior that will break functionality as intended. The `include_all_client_info` has been added to the following endpoints - results are now restricted to only the user unless this parameter has been set to true:
  - Result endpoints
    -  compare_results
    - get_result
    - get_result_csv
    - get_user_results
  - Chat endpoints
    - get_messages
    - get_chat_message
    - get_chat
- Changed paths for all of the account tag endpoints by adding a /account prefix
- All result endpoints no longer have a `/chat/` prefix
- create_chat (POST /chat/team/{team_uuid}/) requires an object instead of an array directly for prior chat_history. It now expects JSON with a 'messages' parameter. The prior array is the value for that new key.
- update_result (PUT /result/{result_uuid}/ ) now expects the parameters to update in the Body instead of the query parameters
- withdraw_credits (DELETE /billing/credits/) endpoint path has been changed from `DELETE /billing/credits/{sub_uuid}/` to `DELETE /billing/credits/`
- Not necessarily a breaking change, but I added a default when creating a subscription plan for Basejump credit blocks to be 500 credits
- User roles are now enforced for access tokens - this means that any existing refresh tokens will be labeled as MEMBER level access. `. This will only go into effect after the access token has been refreshed.
- Docs no longer require an access token to view. Docs have now been moved to /api/api-reference/.
- The GET /{db_uuid}/mermaidjs/ is now /{db_uuid}/mermaidjs/erd/
===