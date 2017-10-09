



<span data-ttu-id="80059-101">Bij het verzenden van Sjabloonmeldingen hoeft u alleen een set eigenschappen tooprovide in ons geval ontvangt van ons Hallo set eigenschappen met Hallo gelokaliseerde versie van de huidige nieuws hello, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="80059-101">When you send template notifications you only need tooprovide a set of properties, in our case we will send hello set of properties containing hello localized version of hello current news, for instance:</span></span>

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


<span data-ttu-id="80059-102">Deze sectie wordt beschreven hoe toosend meldingen met een console-app</span><span class="sxs-lookup"><span data-stu-id="80059-102">This section shows how toosend notifications using a console app</span></span>

<span data-ttu-id="80059-103">Hallo opgenomen code broadcasts tooboth Windows Store en iOS-apparaten omdat Hallo back-end tooany Hallo ondersteunde apparaten uitzenden kunt.</span><span class="sxs-lookup"><span data-stu-id="80059-103">hello included code broadcasts tooboth Windows Store and iOS devices, since hello backend can broadcast tooany of hello supported devices.</span></span>

### <a name="toosend-notifications-using-a-c-console-app"></a><span data-ttu-id="80059-104">toosend meldingen met een C#-consoletoepassing</span><span class="sxs-lookup"><span data-stu-id="80059-104">toosend notifications using a C# console app</span></span>
<span data-ttu-id="80059-105">Hallo wijzigen `SendTemplateNotificationAsync` methode in Hallo-consoletoepassing die u eerder hebt gemaakt met de volgende code Hallo.</span><span class="sxs-lookup"><span data-stu-id="80059-105">Modify hello `SendTemplateNotificationAsync` method in hello console app you previously created with hello following code.</span></span> <span data-ttu-id="80059-106">U ziet hoe in dit geval er is geen toosend moeten meerdere meldingen voor verschillende talen en platforms.</span><span class="sxs-lookup"><span data-stu-id="80059-106">Notice how in this case there is no need toosend multiple notifications for different locales and platforms.</span></span>

        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub = 
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");

            // Sending hello notification as a template notification. All template registrations that contain 
            // "messageParam" or "News_<local selected>" and hello proper tags will receive hello notifications. 
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


<span data-ttu-id="80059-107">Houd er rekening mee dat deze eenvoudige aanroep gelokaliseerde stukje nieuws hello te levert**alle** uw apparaten, ongeacht het platform hello, zoals uw Notification Hub bouwt en levert Hallo juist systeemeigen nettolading tooall Hallo apparaten geabonneerd specifieke tag tooa.</span><span class="sxs-lookup"><span data-stu-id="80059-107">Note that this simple call will deliver hello localized piece of news too**all** your devices, irrespective of hello platform, as your Notification Hub builds and delivers hello correct native payload tooall hello devices subscribed tooa specific tag.</span></span>

### <a name="sending-hello-notification-with-mobile-services"></a><span data-ttu-id="80059-108">Verzenden van de melding Hallo met Mobile Services</span><span class="sxs-lookup"><span data-stu-id="80059-108">Sending hello notification with Mobile Services</span></span>
<span data-ttu-id="80059-109">In de planner van uw mobiele Service, kunt u Hallo script volgen:</span><span class="sxs-lookup"><span data-stu-id="80059-109">In your Mobile Service scheduler, you can use hello following script:</span></span>

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


