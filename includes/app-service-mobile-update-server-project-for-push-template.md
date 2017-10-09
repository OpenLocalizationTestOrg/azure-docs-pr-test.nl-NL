In deze sectie maakt bijwerken u code in uw bestaande Mobile Apps back-end-project toosend een push-melding telkens wanneer een nieuw item wordt toegevoegd. Dit wordt mogelijk gemaakt door Hallo [sjabloon](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) functie van Azure Notification Hubs, platformoverschrijdende pushes inschakelen. Hallo zijn verschillende clients geregistreerd voor pushmeldingen met behulp van sjablonen en een enkele universal push tooall kan ophalen-clientplatforms.

Kies een van de Hallo procedures te volgen die overeenkomt met uw back-end projecttype&mdash;beide [.NET back-end](#dotnet) of [Node.js-back-end](#nodejs).

### <a name="dotnet"></a>.NET-back-end-project
1. In Visual Studio met de rechtermuisknop op het serverproject Hallo en klikt u op **NuGet-pakketten beheren**. Zoeken naar `Microsoft.Azure.NotificationHubs`, en klik vervolgens op **installeren**. Hiermee installeert u Hallo Notification Hubs-bibliotheek voor het verzenden van meldingen vanuit uw back-end.
2. Open in Hallo serverproject **domeincontrollers** > **TodoItemController.cs**, en voeg de volgende Hallo using-instructies:

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. In Hallo **PostTodoItem** methode toevoegen Hallo code te volgen na de aanroep Hallo**InsertAsync**:  

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

    Dit stuurt de melding van een sjabloon die Hallo-item bevat. Tekst als er een nieuw item wordt toegevoegd.
4. Hallo serverproject publiceren.

### <a name="nodejs"></a>Node.js-back-end-project
1. Als u dit nog niet hebt gedaan, [Hallo Quick Start back-end-project downloaden](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), of gebruik anders Hallo [online-editor in Azure-portal Hallo](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).
2. Hallo bestaande code in todoitem.js vervangen door de volgende Hallo:

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

    Dit stuurt de melding van een sjabloon met Hallo item.text wanneer een nieuw item wordt ingevoerd.
3. Wanneer u bewerkt Hallo-bestand op uw lokale computer, opnieuw publiceren Hallo serverproject.
