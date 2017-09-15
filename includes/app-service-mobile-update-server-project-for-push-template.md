<span data-ttu-id="1a85f-101">In deze sectie kunt u code bijwerken in uw bestaande Mobile Apps back-end-project voor het verzenden van een push-melding telkens wanneer een nieuw item wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1a85f-101">In this section, you update code in your existing Mobile Apps back-end project to send a push notification every time a new item is added.</span></span> <span data-ttu-id="1a85f-102">Dit wordt mogelijk gemaakt door de [sjabloon](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) functie van Azure Notification Hubs, platformoverschrijdende pushes inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1a85f-102">This is powered by the [template](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs, enabling cross-platform pushes.</span></span> <span data-ttu-id="1a85f-103">De verschillende clients worden geregistreerd voor pushmeldingen met behulp van sjablonen en een enkele universal push toegang krijgen tot alle clientplatforms.</span><span class="sxs-lookup"><span data-stu-id="1a85f-103">The various clients are registered for push notifications using templates, and a single universal push can get to all client platforms.</span></span>

<span data-ttu-id="1a85f-104">Kies een van de volgende procedures die overeenkomt met uw back-end projecttype&mdash;beide [.NET back-end](#dotnet) of [Node.js-back-end](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="1a85f-104">Choose one of the following procedures that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="1a85f-105"><a name="dotnet"></a>.NET-back-end-project</span><span class="sxs-lookup"><span data-stu-id="1a85f-105"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="1a85f-106">In Visual Studio met de rechtermuisknop op het serverproject en klik op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="1a85f-106">In Visual Studio, right-click the server project and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="1a85f-107">Zoeken naar `Microsoft.Azure.NotificationHubs`, en klik vervolgens op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="1a85f-107">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="1a85f-108">Hiermee installeert u de Notification Hubs-bibliotheek voor het verzenden van meldingen vanuit uw back-end.</span><span class="sxs-lookup"><span data-stu-id="1a85f-108">This installs the Notification Hubs library for sending notifications from your back end.</span></span>
2. <span data-ttu-id="1a85f-109">Open in het serverproject **domeincontrollers** > **TodoItemController.cs**, en voeg de volgende using-instructies:</span><span class="sxs-lookup"><span data-stu-id="1a85f-109">In the server project, open **Controllers** > **TodoItemController.cs**, and add the following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="1a85f-110">In de **PostTodoItem** methode, voeg de volgende code na het aanroepen van **InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="1a85f-110">In the **PostTodoItem** method, add the following code after the call to **InsertAsync**:</span></span>  

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
        .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Sending the message so that all template registrations that contain "messageParam"
        // will receive the notifications. This includes APNS, GCM, WNS, and MPNS template registrations.
        Dictionary<string,string> templateParams = new Dictionary<string,string>();
        templateParams["messageParam"] = item.Text + " was added to the list.";

        try
        {
            // Send the push notification and log the results.
            var result = await hub.SendTemplateNotificationAsync(templateParams);

            // Write the success result to the logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write the failure result to the logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="1a85f-111">Dit stuurt de melding van een sjabloon die het item bevat. Tekst als er een nieuw item wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1a85f-111">This sends a template notification that contains the item.Text when a new item is inserted.</span></span>
4. <span data-ttu-id="1a85f-112">Het serverproject publiceren.</span><span class="sxs-lookup"><span data-stu-id="1a85f-112">Republish the server project.</span></span>

### <span data-ttu-id="1a85f-113"><a name="nodejs"></a>Node.js-back-end-project</span><span class="sxs-lookup"><span data-stu-id="1a85f-113"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="1a85f-114">Als u dit nog niet hebt gedaan, [downloaden van het snelstartproject dat back-end](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), of gebruik anders de [online-editor in Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="1a85f-114">If you haven't already done so, [download the quickstart back-end project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use the [online editor in the Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="1a85f-115">Vervang de bestaande code in todoitem.js door het volgende:</span><span class="sxs-lookup"><span data-stu-id="1a85f-115">Replace the existing code in todoitem.js with the following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about the Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define the template payload.
        var payload = '{"messageParam": "' + context.item.text + '" }';  

        // Execute the insert.  The insert returns the results as a Promise,
        // Do the push as a post-execute action within the promise flow.
        return context.execute()
            .then(function (results) {
                // Only do the push if configured
                if (context.push) {
                    // Send a template notification.
                    context.push.send(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget to return the results from the context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;  

    <span data-ttu-id="1a85f-116">Dit stuurt de melding van een sjabloon waarin de item.text wanneer een nieuw item wordt ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="1a85f-116">This sends a template notification that contains the item.text when a new item is inserted.</span></span>
3. <span data-ttu-id="1a85f-117">Bij het bewerken van het bestand op uw lokale computer opnieuw publiceren het serverproject.</span><span class="sxs-lookup"><span data-stu-id="1a85f-117">When editing the file on your local computer, republish the server project.</span></span>
