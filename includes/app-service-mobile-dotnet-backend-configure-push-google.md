Gebruik Hallo procedure die overeenkomt met uw back-end projecttype&mdash;beide [.NET back-end](#dotnet) of [Node.js-back-end](#nodejs).

### <a name="dotnet"></a>.NET-back-end-project
1. In Visual Studio met de rechtermuisknop op het serverproject Hallo en klikt u op **NuGet-pakketten beheren**. Zoeken naar `Microsoft.Azure.NotificationHubs`, en klik vervolgens op **installeren**. Hiermee installeert u Hallo Notification Hubs-clientbibliotheek.
2. Open TodoItemController.cs in map Hallo-Controllers, en voeg de volgende Hallo `using` instructies:

        using Microsoft.Azure.Mobile.Server.Config;
        using Microsoft.Azure.NotificationHubs;
3. Vervang Hallo `PostTodoItem` methode Hello code te volgen:  

        public async Task<IHttpActionResult> PostTodoItem(TodoItem item)
        {
            TodoItem current = await InsertAsync(item);
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

            // Android payload
            var androidNotificationPayload = "{ \"data\" : {\"message\":\"" + item.Text + "\"}}";

            try
            {
                // Send hello push notification and log hello results.
                var result = await hub.SendGcmNativeNotificationAsync(androidNotificationPayload);

                // Write hello success result toohello logs.
                config.Services.GetTraceWriter().Info(result.State.ToString());
            }
            catch (System.Exception ex)
            {
                // Write hello failure result toohello logs.
                config.Services.GetTraceWriter()
                    .Error(ex.Message, null, "Push.SendAsync Error");
            }
            return CreatedAtRoute("Tables", new { id = current.Id }, current);
        }

4. Hallo serverproject publiceren.

### <a name="nodejs"></a>Node.js-back-end-project
1. Als u dit nog niet hebt gedaan, [Hallo Quick Start-project downloaden](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), of gebruik anders Hallo [online-editor in Azure-portal Hallo](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).
2. Vervang bestaande code in Hallo todoitem.js bestand Hallo door Hallo volgende:

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello GCM payload.
        var payload = {
            "data": {
                "message": context.item.text
            }
        };   

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a GCM native notification.
                    context.push.gcm.send(null, payload, function (error) {
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

    Deze stuurt een GCM-melding waarin Hallo item.text wanneer een nieuwe takenlijstitem wordt ingevoerd.
3. Wanneer u bewerkt Hallo-bestand in uw lokale computer, opnieuw publiceren Hallo serverproject.
