# Quickstart

Welcome to the Basejump AI quickstart! This video below gives a quick introduction on using the app:

[!embed](https://www.youtube.com/watch?v=mFXwVtsyWTk&ab_channel=BasejumpAI)

When you first log in, you will start on the data page. The data page is initially blank. Here is what the data page looks like once data has been retrieved.

![The Data page](/images/data/data_page.png)

To start generating your own data objects, make sure to select a team from the top of the sidebar menu - it's initially set to the 'Default Team'. Then in order to generate your own data objects, either select the chat page in the sidebar or start chatting with the chat bar that is present throughout the app.

Your chat is scoped to whichever team you currently have selected. Each team has databases that have been provisioned by your company admin. If you are the initial user and created the account, then you will have admin privileges and will see an admin sidebar in addition to the typical sidebar that members see.

## Adding a New Datasource

![The Datasources page](/images/datasources/datasource_page.png)

In order to get started chatting with your own data, you will need to add a datasource on the datasources page. We are focused on chatting with your database so we have built this feature out first. We will soon be adding the ability to upload CSV files as well as adding knowledge store datasources to help provide the AI with more context.

You see that two database sources have already been added, the `HR Database` and the `Shop Database`. To add your own database, follow these steps:

1. Click the 'Add Database' button

![Adding a database](/images/datasources/add_database_modal.png)

2. Fill in your database credentials in the modal window. To include any additional schemas besides the default schema, add them in the 'Accessible Schemas'. For more information on creating templated schemas using Jinja, refer to the 'Datasources' page. The database role you provide needs to have a SELECT permission to the tables you want to give access.

[!ref](/sidebar-options/administrator-options/datasources.md)

3. Your database comes with the initial connection that you provided. You can add additional connections with different usernames and passwords by selecting the connection number on the database line. Access is provisioned at the connection level and not at the database level.

![Managing connections](/images/datasources/manage_connections.png)

4. One of the most important steps is that you supplement the automatic profiling of your database for the Basejump AI data agent with metadata. If you have not edited the metadata, you will get a caution symbol indicating it need to be updated and/or reviewed.

![Showing the context menu to select edit metadata](/images/datasources/select_edit_metadata.png)

You will see each table in the left sidebar in the modal window. You have options to fill out information at the table and column level. If the information was available in the database, it will already be filled in your metadata. This information provides context to the AI and will improve the ability for it to retrieve the correct information based on the user input.

![The edit metadata page](/images/datasources/edit_metadata.png)

## Creating a Team

Now that you have added your first datasource, go to the team page by clicking the team option in the sidebar to provide access to your new datasource connection.

![The Teams page](/images/team/team_page.png)

Follow these steps to create a team and provide access:

1. Click 'Add Team'
2. Provide a unique team name and select a data connection

![Adding a Team](/images/team/add_team.png)

3. Click 'Add Team'

## Chatting with the AI

By this point, you should have added a datasource and given a team access to your information. Before chatting with the AI, you will need to select your team if not already selected. Once selected, select the chat icon in the sidebar.

Use the chat bar at the bottom of the screen to ask the AI a question. As the AI responds, you can see its thoughts as it is thinking through the question and iteratively solving it.

![Adding a Team](/images/chat/chat_page.png)

That's it! You now have set up your account to start chatting with the AI data agent. Start inviting other users to your company and teams to give them access as well. Happy Basejumping!

## API

If you're interested in the API, see the API docs for information for getting started using the API.

[!ref](/api.md)

