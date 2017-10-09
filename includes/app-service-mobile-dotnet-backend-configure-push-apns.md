
* **.NET-back-end (C#)**:      
  
  1. In Visual Studio met de rechtermuisknop op het serverproject Hallo en klikt u op **NuGet-pakketten beheren**, zoeken naar `Microsoft.Azure.NotificationHubs`, klikt u vervolgens op **installeren**. Hiermee installeert u Hallo Notification Hubs-bibliotheek voor het verzenden van meldingen vanuit uw back-end.
  2. Open in Visual Studio-project Hallo-end, **domeincontrollers** > **TodoItemController.cs**. Bovenaan Hallo Hallo-bestand, voeg Hallo volgende `using` instructie:
     
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

                // iOS payload
                var appleNotificationPayload = "{\"aps\":{\"alert\":\"" + item.Text + "\"}}";

                try
                {
                    // Send hello push notification and log hello results.
                    var result = await hub.SendAppleNativeNotificationAsync(appleNotificationPayload);

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

* **Back-end voor node.js** : 
  
  1. Als u dit nog niet hebt gedaan, [Hallo Quick Start-project downloaden](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) of gebruik anders Hallo [online-editor in Azure-portal Hallo](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).    
  2. Hallo todoitem.js tabel script vervangen door Hallo code te volgen:

            var azureMobileApps = require('azure-mobile-apps'),
                promises = require('azure-mobile-apps/src/utilities/promises'),
                logger = require('azure-mobile-apps/src/logger');

            var table = azureMobileApps.table();

            // When adding record, send a push notification via APNS
            table.insert(function (context) {
                // For details of hello Notification Hubs JavaScript SDK, 
                // see http://aka.ms/nodejshubs
                logger.info('Running TodoItem.insert');

                // Create a payload that contains hello new item Text.
                var payload = "{\"aps\":{\"alert\":\"" + context.item.text + "\"}}";

                // Execute hello insert; Push as a post-execute action when results are returned as a Promise.
                return context.execute()
                    .then(function (results) {
                        // Only do hello push if configured
                        if (context.push) {
                            context.push.apns.send(null, payload, function (error) {
                                if (error) {
                                    logger.error('Error while sending push notification: ', error);
                                } else {
                                    logger.info('Push notification sent successfully!');
                                }
                            });
                        }
                        return results;
                    })
                    .catch(function (error) {
                        logger.error('Error while running context.execute: ', error);
                    });
            });

            module.exports = table;

    2. Wanneer u bewerkt Hallo-bestand op uw lokale computer, opnieuw publiceren Hallo serverproject.
