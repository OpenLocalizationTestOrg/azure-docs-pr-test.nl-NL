



<span data-ttu-id="9330b-101">Bij het verzenden van Sjabloonmeldingen u alleen hoeft te bieden van een set eigenschappen in ons geval ontvangt van ons de set eigenschappen die de gelokaliseerde versie van het huidige nieuws voor exemplaar:</span><span class="sxs-lookup"><span data-stu-id="9330b-101">When you send template notifications you only need to provide a set of properties, in our case we will send the set of properties containing the localized version of the current news, for instance:</span></span>

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


<span data-ttu-id="9330b-102">Deze sectie wordt beschreven hoe u meldingen met een console-app verzenden</span><span class="sxs-lookup"><span data-stu-id="9330b-102">This section shows how to send notifications using a console app</span></span>

<span data-ttu-id="9330b-103">De opgenomen code zendt voor Windows Store en iOS-apparaten, omdat de back-end naar een van de ondersteunde apparaten verzenden kunt.</span><span class="sxs-lookup"><span data-stu-id="9330b-103">The included code broadcasts to both Windows Store and iOS devices, since the backend can broadcast to any of the supported devices.</span></span>

### <a name="to-send-notifications-using-a-c-console-app"></a><span data-ttu-id="9330b-104">Voor het verzenden van meldingen via een C#-consoletoepassing</span><span class="sxs-lookup"><span data-stu-id="9330b-104">To send notifications using a C# console app</span></span>
<span data-ttu-id="9330b-105">Wijzig de `SendTemplateNotificationAsync` methode in de console-app die u eerder hebt gemaakt met de volgende code.</span><span class="sxs-lookup"><span data-stu-id="9330b-105">Modify the `SendTemplateNotificationAsync` method in the console app you previously created with the following code.</span></span> <span data-ttu-id="9330b-106">U ziet hoe in dit geval hoeft niet meerdere meldingen voor verschillende talen en platforms wilt verzenden.</span><span class="sxs-lookup"><span data-stu-id="9330b-106">Notice how in this case there is no need to send multiple notifications for different locales and platforms.</span></span>

        private static async void SendTemplateNotificationAsync()
        {
            // Define the notification hub.
            NotificationHubClient hub = 
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");

            // Sending the notification as a template notification. All template registrations that contain 
            // "messageParam" or "News_<local selected>" and the proper tags will receive the notifications. 
            // This includes APNS, GCM, WNS, and MPNS template registrations.
            Dictionary<string, string> templateParams = new Dictionary<string, string>();

            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business", "Technology", "Science", "Sports"};
            var locales = new string[] { "English", "French", "Mandarin" };

            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";

                // Sending localized News for each tag too...
                foreach( var locale in locales)
                {
                    string key = "News_" + locale;

                    // Your real localized news content would go here.
                    templateParams[key] = "Breaking " + category + " News in " + locale + "!";
                }

                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
        }


<span data-ttu-id="9330b-107">Houd er rekening mee dat deze eenvoudige aanroep de gelokaliseerde stukje nieuws levert **alle** uw apparaten, ongeacht het platform, zoals uw Notification Hub bouwt en levert de juiste systeemeigen nettolading voor alle apparaten die zijn geabonneerd op een specifieke label.</span><span class="sxs-lookup"><span data-stu-id="9330b-107">Note that this simple call will deliver the localized piece of news to **all** your devices, irrespective of the platform, as your Notification Hub builds and delivers the correct native payload to all the devices subscribed to a specific tag.</span></span>

### <a name="sending-the-notification-with-mobile-services"></a><span data-ttu-id="9330b-108">Verzenden van de melding met Mobile Services</span><span class="sxs-lookup"><span data-stu-id="9330b-108">Sending the notification with Mobile Services</span></span>
<span data-ttu-id="9330b-109">In de planner van uw mobiele Service, kunt u het volgende script:</span><span class="sxs-lookup"><span data-stu-id="9330b-109">In your Mobile Service scheduler, you can use the following script:</span></span>

    var azure = require('azure');
    var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string with full access>');
    var notification = {
            "News_English": "World News in English!",
            "News_French": "World News in French!",
            "News_Mandarin", "World News in Mandarin!"
    }
    notificationHubService.send('World', notification, function(error) {
        if (!error) {
            console.warn("Notification successful");
        }
    });


