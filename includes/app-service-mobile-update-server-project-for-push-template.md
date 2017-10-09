<span data-ttu-id="cb86c-101">In deze sectie maakt bijwerken u code in uw bestaande Mobile Apps back-end-project toosend een push-melding telkens wanneer een nieuw item wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="cb86c-101">In this section, you update code in your existing Mobile Apps back-end project toosend a push notification every time a new item is added.</span></span> <span data-ttu-id="cb86c-102">Dit wordt mogelijk gemaakt door Hallo [sjabloon](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) functie van Azure Notification Hubs, platformoverschrijdende pushes inschakelen.</span><span class="sxs-lookup"><span data-stu-id="cb86c-102">This is powered by hello [template](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs, enabling cross-platform pushes.</span></span> <span data-ttu-id="cb86c-103">Hallo zijn verschillende clients geregistreerd voor pushmeldingen met behulp van sjablonen en een enkele universal push tooall kan ophalen-clientplatforms.</span><span class="sxs-lookup"><span data-stu-id="cb86c-103">hello various clients are registered for push notifications using templates, and a single universal push can get tooall client platforms.</span></span>

<span data-ttu-id="cb86c-104">Kies een van de Hallo procedures te volgen die overeenkomt met uw back-end projecttype&mdash;beide [.NET back-end](#dotnet) of [Node.js-back-end](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="cb86c-104">Choose one of hello following procedures that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="cb86c-105"><a name="dotnet"></a>.NET-back-end-project</span><span class="sxs-lookup"><span data-stu-id="cb86c-105"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="cb86c-106">In Visual Studio met de rechtermuisknop op het serverproject Hallo en klikt u op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="cb86c-106">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="cb86c-107">Zoeken naar `Microsoft.Azure.NotificationHubs`, en klik vervolgens op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="cb86c-107">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="cb86c-108">Hiermee installeert u Hallo Notification Hubs-bibliotheek voor het verzenden van meldingen vanuit uw back-end.</span><span class="sxs-lookup"><span data-stu-id="cb86c-108">This installs hello Notification Hubs library for sending notifications from your back end.</span></span>
2. <span data-ttu-id="cb86c-109">Open in Hallo serverproject **domeincontrollers** > **TodoItemController.cs**, en voeg de volgende Hallo using-instructies:</span><span class="sxs-lookup"><span data-stu-id="cb86c-109">In hello server project, open **Controllers** > **TodoItemController.cs**, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="cb86c-110">In Hallo **PostTodoItem** methode toevoegen Hallo code te volgen na de aanroep Hallo**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="cb86c-110">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>  

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
        .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Sending hello message so that all template registrations that contain "messageParam"
        // will receive hello notifications. This includes APNS, GCM, WNS, and MPNS template registrations.
        Dictionary<string,string> templateParams = new Dictionary<string,string>();
        templateParams["messageParam"] = item.Text + " was added toohello list.";

        try
        {
            // Send hello push notification and log hello results.
            var result = await hub.SendTemplateNotificationAsync(templateParams);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="cb86c-111">Dit stuurt de melding van een sjabloon die Hallo-item bevat. Tekst als er een nieuw item wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="cb86c-111">This sends a template notification that contains hello item.Text when a new item is inserted.</span></span>
4. <span data-ttu-id="cb86c-112">Hallo serverproject publiceren.</span><span class="sxs-lookup"><span data-stu-id="cb86c-112">Republish hello server project.</span></span>

### <span data-ttu-id="cb86c-113"><a name="nodejs"></a>Node.js-back-end-project</span><span class="sxs-lookup"><span data-stu-id="cb86c-113"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="cb86c-114">Als u dit nog niet hebt gedaan, [Hallo Quick Start back-end-project downloaden](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), of gebruik anders Hallo [online-editor in Azure-portal Hallo](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="cb86c-114">If you haven't already done so, [download hello quickstart back-end project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="cb86c-115">Hallo bestaande code in todoitem.js vervangen door de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="cb86c-115">Replace hello existing code in todoitem.js with hello following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello template payload.
        var payload = '{"messageParam": "' + context.item.text + '" }';  

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
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
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;  

    <span data-ttu-id="cb86c-116">Dit stuurt de melding van een sjabloon met Hallo item.text wanneer een nieuw item wordt ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="cb86c-116">This sends a template notification that contains hello item.text when a new item is inserted.</span></span>
3. <span data-ttu-id="cb86c-117">Wanneer u bewerkt Hallo-bestand op uw lokale computer, opnieuw publiceren Hallo serverproject.</span><span class="sxs-lookup"><span data-stu-id="cb86c-117">When editing hello file on your local computer, republish hello server project.</span></span>
