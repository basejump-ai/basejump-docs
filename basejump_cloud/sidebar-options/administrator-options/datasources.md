# Datasources

The datasources page shows all available datasources that have been added for the company.

## Adding a New Datasource

In order to get started chatting with your own data, you will need to add a datasource on the datasources page. You can see that two database sources have already been added, the 'HR Database' and the 'Shop Database'. To add your own database, follow these steps:

![The Datasources page](/images/datasources/datasource_page.png)

1. Click the 'Add Database' button

![The Add Database view](/images/datasources/add_database_modal.png)

2. Fill in your database credentials in the modal window. To include any additional schemas besides the default schema, add them in the 'Accessible Schemas' section. The database role you provide needs to have a SELECT permission to the tables you want to give access.

3. Your database comes with the initial connection that you provided. You can add additional connections with different usernames and passwords by selecting the connection number on the database line. Access to Users is provisioned at the connection level and not at the database level.

![Click the Connection number tile to manage connections](/images/datasources/manage_connections.png)

## Database Metadata

One of the most important steps is that you supplement the automatic profiling of your database for the Basejump AI data agent with metadata.

### Editing Metadata

If you have not edited the metadata, you will get a caution symbol indicating it needs to be updated and/or reviewed. To remove this caution symbol, either click the caution icon or navigate to the edit option under metadata in the context menu.

![Selecting the edit metadata button](/images/datasources/select_edit_metadata.png)

After selecting the edit option, you will see each table in the modal window sidebar. For each table, you have a few options for information that you can supplement. 

![Editing database metadata](/images/datasources/edit_metadata.png)

**Table Metadata**
Metadata Setting   | Description
---    | ---
Ignore | This option will tell the AI to ignore the table and not use it when providing answers to Users. 
Table Description | Providing a description of the table will help the AI find relevant information for Users.
Primary Keys | Primary keys will help ensure that the outputs are distinct and avoid the possibility of duplicates in the output.

**Column Metadata**
Metadata Setting   | Description
---    | ---
Ignore | Same behavior as ignore for tables, but at the columnar level of detail.
Column Description | Providing a description of the columnb will help the AI find relevant information for Users.
Foreign Key | Fill out this field with another table that has this column. This information is used to help the AI join tables together.
Distinct Values | Add distinct values using a comma-seperated list for the column for columns with low cardinality (i.e. there are only a few options such as 'Male', 'Female' for example)

## Templated Schemas

Database connections can have access to different schemas, but these different schemas are based on the exact same database table layout. This setup is more common with SQL workflows powered by dbt or using some variant where Jinja and SQL are combined.

In order to set up templated schemas, add a database on the database page.

![Using templated schemas](/images/datasources/templated_schemas.png)

You can see in the image above that templated schema was added. It includes a key for the templated schema listed as 'db_type'. This creates an input box down below to fill in the value for that particular connection that appears after submitting.

![The templated schema input](/images/datasources/required_templated_schema.png)

For this one we will put 'demo'. So the full schema name will resolve to 'hr_demo_db'.

Then whenever a new connection is added, it will also prompt you for the 'jinjafied' schema. Adding a new connection now looks like this:

![Image showing what adding a new conection would look like](/images/datasources/adding_conn_w_templated_schema.png)

## Bulk Add Connections

A tall is shown by the database name with the connection count.

![Click the Connection number tile to manage connections](/images/datasources/manage_connections.png)

Clikcing this button for managing connections will take you to the Connections page. Click 'Bulk Import' to import many connections at once. This allows you to create many connections with each one associated with a unique username, password, and optional schema (your database user login).

![Bulk importing Connections](/images/datasources/bulk_import_connections.png)

This is really important for those may have many different user roles all with different schemas. Instead of inputting them manually, you can upload the connections using a CSV.

## Bulk Manage Team Access

Many teams can be given access to a connection at once by clicking the team count tally on the connection page. A tooltip will appear with the text 'Manage Teams'.

![Click the Team number tally to manage Teams](/images/datasources/select_manage_teams_connections.png)

Using the checkboxes on the pop-up modal, you can easily provision or remove access to database connections.

![Managing team connections](/images/datasources/manage_team_connections.png)
