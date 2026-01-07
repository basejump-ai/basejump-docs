# Chat

The chat page allows the User to chat with their data. The chat is scoped to the current team that is selected. The AI will use the data sources available to that team to answer the User's question.

![The chat page](/images/chat/chat_response.png)

A new chat can be created by selecting the 'Start New' button in the chat bar at the bottom of the screen. To see all chats select 'Recent' -> 'Chat History'.

To rename a chat, select the pencil icon by the chat name at the top of the chat window. Chats can also be renamed in the Chat History view. Names are given automatically based on the initial question in the chat.

![The chat history page](/images/chat/chat_history.png)

## Visualizations

The AI is able to produce visualizations in addition to data objects. The following visualization types are supported:
- Bar
- Line
- Area
- Scatter
- Pie

![Visualization example](/images/chat/viz_chat_example.png)

Visualizations are created using the Plotly open source library. 

## Auditing the AI output

After providing your prompt, the user is able to see the AI's thoughts in real-time. This helps the User understand the thought process the AI went through to reach its conclusion and helps the User audit the result. 

![Showing the AI thoughts](/images/chat/ai_thoughts.png)

The AI thoughts are not permanently saved however and when the page is reloaded won't be available. You can also see the SQL query used to generate the output by clicking 'See SQL'. 

Finally, the AI will provide a data object in response to your prompt if the prompt requires it to use a datasource.

![A dataset returned by the AI](/images/chat/chat_dataset.png)

Using the data spreadsheet view, you can download or save the data. If you decide to save the data by selecting the star icon, you will see a modal window pop-up with a title and description auto-populated by the AI. The title and description can be edited before saving. Saved data will appear in the data page that can be selected in the sidebar.

![Saving the data](/images/chat/save_data_view.png)

There are also 2 options at the bottom of the window. The user can share the data object with their team or save the results to a Collection.

### Verified Results

Users can mark a result as 'verified'. When Users mark a result as verified, it will add a checkmark to the result. 

![Verified result example](/images/chat/verified_result.png)

For more detail about verification, please refer to the data governance page: 

[!ref](/basejump_cloud/data-governance.md)

## Double-Texting

The AI has the ability to answer questions simultaneously. Before the AI completes its response, you can ask it another question and it will start answering both questions in parallel. 

## Result Output

While chatting with the AI, you will generate results for your queries. These results have limitations however. You cannot generate a result over 100 MB. Results over 1 week old in your chat history are not saved. 

## Stopping a Chat

While the AI is thinking through a problem, you have the option to stop the chat. In order to stop the chat, select the blue square icon that shows above the up-pointing chevron in the chat toolbar. This will stop all running requests within the chat.

![Stopping the chat](/images/chat/stop_chat.png)

## Providing Feedback through Thumbs Up/Down Reactions

When the AI responds, a User can provide feedback using a thumbs up/down reaction. 

![Thumbs up example](/images/chat/thumbs_up.png)

If a thumbs up is given, this information is cached and verified for other users using the Basejump verification engine. This will improve accuracy of results going forward and help train the AI to improve its responses going forward. 

If a thumbs down is given, a feedback modal is opened where the user can explain why this result was incorrect. This also helps the AI to improve the accuracy of the results by adding this feedback to the message history.

![Thumbs down modal](/images/chat/thumbs_down_issue_report.png)