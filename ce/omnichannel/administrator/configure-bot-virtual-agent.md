---
title: "Integrate a bot | MicrosoftDocs"
description: "Instructions to integrate a bot in Omnichannel for Customer Service."
author: platkat
ms.author: ktaylor
manager: shujoshi
ms.date: 10/12/2020
ms.service: dynamics-365-customerservice
ms.topic: article
---

# Integrate a Power Virtual Agents bot

[!INCLUDE[cc-use-with-omnichannel](../../includes/cc-use-with-omnichannel.md)]

Microsoft Power Virtual Agents allows organizations to automate routine conversations, letting agents focus on high-value interactions. When a conversation is escalated from a bot to a human agent, agents can see the full transcript of bot conversations and have complete context while engaging with customers.

After you have created your bot and connected it to an Omnichannel for Customer Service environment, you can go to the Omnichannel Administration app in order to add your bot to queues and configure context variables to route chat sessions to queues. 

When you integrate a Power Virtual Agents bot with Omnichannel for Customer Service, you get the following capabilities for bot conversations:

- Seamlessly integrate your bot with all channels without needing to add channel-specific code in the bot.
- Transfer bot conversations to human agents, and include the full context of the conversation.
- Analyze the bot transcript that's available in Common Data Service after the chat is completed.
- Configure routing rules to selectively route incoming requests to bots based on context, such as issue type or customer type. For example, you can route low-complexity issues to bots, or route the conversation to a sales or support bot based on the webpage browsing history of the customer.
- Monitor the bot conversations in real time by using the supervisor dashboard, which includes details such as customer sentiment.
- Use the historical dashboards to get insights into the effectiveness of the bots through metrics, such as resolution rate, escalation rate, resolution time, escalation time, and average sentiment.

## Prerequisites

- Product licenses - You need a product license for Power Virtual Agents ([start a trial](https://go.microsoft.com/fwlink/p/?LinkId=2092080&clcid=0x409)) and Omnichannel for Customer service ([learn more](https://docs.microsoft.com/dynamics365/customer-engagement/omnichannel/try-chat-for-dynamics365)).
- Role - In order to successfully complete these steps, the signed-in user must be an Omnichannel Administrator. [Learn more about managing and assigning user roles in Omnichannel](add-users-assign-roles.md).
- Azure Application ID - You will need an application registered in Azure prior to connecting to Omnichannel for Customer Service. [Learn more](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#create-an-azure-active-directory-application)
- Bot - You must have a preconfigured bot that can integrate with Omnichannel for Customer Service. For more information, see [Configure seamless and contextual hand-off to Omnichannel for Customer Service](https://docs.microsoft.com/dynamics365/ai/customer-service-virtual-agent/configuration-hand-off-omnichannel).
- Chat widget - You must have a preconfigured chat widget to enable the bot to communicate with end users. For more information, see [Add a chat widget](add-chat-widget.md).

## Configure your Power Virtual Agents bot

Once the Power Virtual Agents bot is created and configured to work with Omnichannel for Customer Service, you can configure it to hand off conversations to queues in the Omnichannel Administration app. To receive incoming messages, you must add the bot to at least one queue. The bot will use the routing rules that were created at setup. You can change them in the **Work Streams** section of Omnichannel.

**Set up your Power Virtual Agents bot**

1. Connect the bot to Omnichannel for Customer Service and go to the Omnichannel Administration app. For more information, see [Configure seamless and contextual hand-off to Omnichannel for Customer Service](https://docs.microsoft.com/dynamics365/ai/customer-service-virtual-agent/configuration-hand-off-omnichannel).

    ![Virtual Agent bot settings](../media/virtual-agent-bot-settings.png)
    
    The bot will appear in Omnichannel for Customer Service.

2. Assign the bot to an existing queue.
    
    ![Virtual Agent bot select queue](../media/virtual-agent-bot-select-queues.png)

3. Click **Done**. Now you're on the bot profile page and you can see that your bot is connected.
    
    ![Virtual Agent bot profile page](../media/virtual-agent-bot-profile.png)
    
    Your bot is ready to accept and respond to customer-initiated conversations.
    
 4. Set escalation rules so the bot can route the queries to the appropriate agent. You can set up escalation rules in one of the following ways:
 
    - **Add the bot to an existing human agent queue:**	If you add the bot to an existing human agent queue, you don’t need to change your existing routing rule. Existing routing rules will send incoming messages to the Power Virtual Agents. When a handoff is triggered, customers will be transferred from the Power Virtual Agents to the human agent according to the escalation routing rules.
    
    - **Create a bot queue and a human agent queue:** If you create two queues, you must create work streams that contain context variables and appropriate routing rules to route the customer queries.

For information about working with queues, see [Work with queues in Omnichannel for Customer Service](queues-omnichannel.md).

### Create a bot queue and a human agent queue

1. Select or create a work stream. For more information about work streams, see [Understand and create work streams](work-streams-introduction.md).

![Virtual Agent work streams](../media/virtual-agent-work-streams.png)

2. Create context variables.

You must use the context variables that were created during setup for the bot to handle the customer queries appropriately. The context variable is used in routing the incoming customer queries to the appropriate bots and agents. For information about context variables, see [Contextual variables available upon hand-off](https://docs.microsoft.com/dynamics365/ai/customer-service-virtual-agent/how-to-handoff#contextual-variables-available-upon-hand-off).

   > [!div class=mx-imgBorder]
   > ![Virtual Agent work stream context variable](../media/virtual-agent-work-stream-context-variables.png "Virtual Agent work stream context variable")

3. Create a routing rule for the human agent and add it to the work stream.

    > [!div class=mx-imgBorder]
    > ![Virtual Agent work stream routing rules](../media/virtual-agent-work-stream-routing-rule.png "Virtual Agent work stream routing rules")

4.  Create a routing rule for the virtual agent and add it to the work stream.

    > [!div class=mx-imgBorder]
    > ![Virtual Agent work stream bot routing rules](../media/virtual-agent-work-stream-routing-rule-bot.png "Virtual Agent work stream bot routing rules")

Routing rules route the incoming customer queries to their respective queues. Each routing rule has a condition and a destination queue. If the condition is evaluated as true, the customer query is routed to the destination queue. For bots, the condition is built by using the context variable.

Bots are developed to receive customer queries first, gain information of the query, and then pass the query to a human agent, if required. To achieve this behavior, you must add a bot user to the queue and configure routing rules in a way that the incoming customer queries are routed to the queue with bot user.

Ensure to map the routing rules to the correct queues so that the queries are routed appropriately. For information about routing rules, see [Create and manage routing rules](routing-rules.md).

> [!NOTE]
> When you run a report on Power Virtual Agent activity, the number of bot sessions may differ from the number of sessions in Omnichannel for Customer Service.

## Configure context variables for a bot

When customers initiate a conversation, the relevant context related to the customer, the issue they are facing, and recent activities performed by them can be made available for the bot to intelligently provide contextual responses to resolve customer issues in a quick and efficient manner. For example, the bot can use the logged in user information to look up recent case information or the order history of the customer and provide a response. Similarly, the pre-conversation information, custom context, or recent pages browsed on a website by the customer can be passed to the bot by configuring context variables for the bot in Power Virtual Agents. For information on context variables that can be configured, see [Context variables](context-variables-for-bot.md).

In Power Virtual Agents, do the following:

1. On the **Topics** page, select **New topic**.
2. On the **Setup** tab, enter a name and description, and save the topic.
3. Select **Go to authoring canvas**.
4. Select **Add node**, choose an appropriate action, such as **Ask a question**.
5. Edit **Save response as**, and update the value for **Name** with the required context variable. Make sure **Bot (any topic can access)** and **External sources can set values** are selected.
    > ![Configure context variable in a topic](../media/Configure-bot-context-variable.png "Configure context variable in a topic")

6. Save and publish the changes.

At run time, the required information is captured in the context variable that can then be used for further actions based on the workflow you configure. For more information, see [Context variables for a bot](context-variables-for-bot.md).

## Known limitations
 
| Description     | Limitation     |
|-----------------|----------------|
| **Adaptive cards:** An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.|	Power Virtual Agents supports adaptive cards for CSAT surveys and they will display text only. For more information, see the [Channel experience reference table](https://docs.microsoft.com/power-virtual-agents/publication-fundamentals-publish-channels#channel-experience-reference-table). <br>You can build an adaptive card by adding a skill through Power Virtual Agents. For more information, see [Use Microsoft Bot Framework Skills in Power Virtual Agents](https://docs.microsoft.com/power-virtual-agents/advanced-use-skills). <br>Adaptive card styling is not supported. |
| **Single sign-on (SSO):** Chatbots can sign the user in if they're in to the page where the bot is deployed. | SSO is not supported. |
| **Typing:** A bot receives a typing activity to indicate that the user is typing a response. A bot may send a typing activity to indicate to the user that it is working to fulfill a request or compile a response. | Typing indicators will not appear. |
| **Suggested actions:** Suggested actions enable your bot to present buttons that the user can tap to provide input. Suggested actions appear close to the composer and enhance user experience. They enable the user to answer a question or make a selection with a simple tap of a button, rather than having to type a response with a keyboard. |	Suggested actions cannot display vertically. |
| **Format bot messages:** You can set the optional TextFormat property to control how your message's text content is rendered. | Power Virtual Agents does not support markdown with images and text. <br>When Power Virtual Agents sends markdown text, there is extra space between lines. <br>Carousel layout is not supported. |
| **File attachments:** Once file attachments are enabled in Omnichannel, customers can send file attachments. | Power Virtual Agents cannot operate on Omnichannel file attachments. |
|||

## Privacy notice

You understand that your data may be transmitted and shared with external systems and that your data may flow outside of your organization's compliance boundary (even if your organization is in a Government Cloud environment). For example, your messages will be shared with the bot which could be interacting with a third-party system based on the integration done by you. For more information on how we process your data, please refer to the [Microsoft Privacy Statement](https://privacy.microsoft.com/privacystatement).

## Videos

[Power Virtual Agents integration with Omnichannel for Customer Service](https://go.microsoft.com/fwlink/p/?linkid=2114716)

To view more videos on Omnichannel for Customer Service, see [Videos](../videos.md).

### See also

[Understand and create work streams](work-streams-introduction.md)

[Work with queues in Omnichannel for Customer Service](queues-omnichannel.md)

[Create and manage routing rules](routing-rules.md)

[Add a chat widget](add-chat-widget.md)

[Enable a bot to escalate and end conversation](../developer/bot-escalate-end-conversation.md)
