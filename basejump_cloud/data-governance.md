# Data Governance

Due to the democratization of access to the database that the Basejump AI platform will enable, Users will generate data objects faster than ever. This effect of improved access leading to increased utilization is known as [Jevon's paradox](https://en.wikipedia.org/wiki/Jevons_paradox).

Because of this, an AI data analytics solution is incomplete without data governance. We provide tools for User's to easily share their data objects and compare them to understand their differences. Traditional BI tools have made dashboards a priority with typically no data governance included. This led to a proliferation of dashboards with no easy way to compare them except to ask the data analysts why towo dashboards are showing different numbers for the same metric.

It is imperative for an AI data analytics solution to provide means to compare and understand all of the data that is being retrieved and not miss an opportunity for built-in data governance.

One tool we provide to help understand the data is every piece of retrieved data has the original SQL query included. For User's on the same Team to compare their data objects, they can select the context menu within a data object and select 'Compare'.

![Showing the 'Compare' selection on a metric](/images/data/compare_metric.png)

Our AI tool will then compare the data in the two data objects and explain to the user how they compare using one of 4 designations (in order of similarity - most similar first):

Similarity   | Description
---    | ---
Identical | There are no differences between the queries used to retrieve the data.
Equivalent | The output and tables are the same, but queries are structured differently.
Similar | The queries share some or all tables, but the output is different.
Different |  The queries share no tables.

![Comparing two data objects](/images/data/data_comparison.png)

We're offering the capability for organizations to go from first principles and original data sources to curate unique insights for the business that will transform the business into a truly data-driven enterprise like never before. Data governance does not have to mean restricting which metrics can be used, but rather improved transparency on the data that is being used and shared.

## Metadata

A fundamental aspect of good data governance is documentation. We provide the option to add metadata to every table and column in your data and define how they relate to each other. This not only improve the documentation on your data sources, but also improves the context for the AI in order to retrieve the most relevant data.

![Editing metadata](/images/datasources/edit_metadata.png)

## Data Modeling

In order to be most successful using the Basejump AI platform, the tables you provide need to be clear enough that you can document the relationships clearly. Not all tables in your database ned to be added to Basejump, just the most clean tables at the end of your ETL pipeline that you want to provide to users.

The relationships you define will be shown as an ERD diagram in our 'Explore' page to help users understand relationships between tables.

![Image of the ERD diagram](/images/explore/explore_erd_diagram.png)

For more information, please refer to the explore page:

[!ref](/basejump-cloud/sidebar-options/member-options/explore.md)

## Verification

### Verified Results

Users can mark a result as 'verified'. When Users mark a result as verified, it will add a checkmark to the result. Verification indicates that the user has reviewed the output and verifies that it is correct.

![Verified result example](/images/chat/verified_result.png)

Verifying a result will add that result to the cache, which means it will return instantly for other users once it has been added. 

There are 2 types of semantically similar results that can be returned in the cache:
- Identical: These results will return the same information as was originally cached if it is current within the last day. If it is older than 1 day, then the result is refreshed.
- Similar: These results will return different information, but the SQL query only differs in the where clause being applied. For example, if someone asks 'how many bagels are there?' and someone else asks, 'how many sesame seed bagels are there', the 2nd query is similar enough to be verified (we know how to count bagels), but will be updated to filter to sesame seed bagels only.

Other details to be aware of:
- If a verified result is returned and is older than 1 day, the SQL query is re-ran in order get the latest information. 
- The checkmark symbol used to indicate if a result is verified is outlined if it was by a Member and solid if it was verified by an Admin
- An Admin can confirm the verification of a Member to promote that verification to an admin

Verified results is a great initial step to getting common consensus around common metrics. Every time a result is returned, users can verify the output and other members will get the same query ran for them as well.

### Unverifying a Result

These verified results can also be unverified if another user disagrees that this information looks correct. However, a user has to be at the same RBAC role level or greater as the other user to unverify. For example, if the user is a Member, they can't unverify an Admin's verified result.

Once a result is unverified, prior verified results that were returned as verified based on that verified data object, will be unverified for anyone who received them. This ensure the highest level accuracy and agreement possible for human-verified information from the AI.

### Security Implications

Identical verified results are only returned for users who share a database connection through their teams. Similar results are only returned for an organization if two users share the same database, but not necessarily the same connection. This is important for situations where Users rely on jinjafied schemas. The query is re-ran to get the information relevant to the other user's connection, but the query itself remains verified.

This setup ensures that only those who have access to shared connections are able to view semantically similar information and keeps the data secure.