



Bij het verzenden van Sjabloonmeldingen hoeft u alleen een set eigenschappen tooprovide in ons geval ontvangt van ons Hallo set eigenschappen met Hallo gelokaliseerde versie van de huidige nieuws hello, bijvoorbeeld:

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


Deze sectie wordt beschreven hoe toosend meldingen met een console-app

Hallo opgenomen code broadcasts tooboth Windows Store en iOS-apparaten omdat Hallo back-end tooany Hallo ondersteunde apparaten uitzenden kunt.

### <a name="toosend-notifications-using-a-c-console-app"></a>toosend meldingen met een C#-consoletoepassing
Hallo wijzigen `SendTemplateNotificationAsync` methode in Hallo-consoletoepassing die u eerder hebt gemaakt met de volgende code Hallo. U ziet hoe in dit geval er is geen toosend moeten meerdere meldingen voor verschillende talen en platforms.

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


Houd er rekening mee dat deze eenvoudige aanroep gelokaliseerde stukje nieuws hello te levert**alle** uw apparaten, ongeacht het platform hello, zoals uw Notification Hub bouwt en levert Hallo juist systeemeigen nettolading tooall Hallo apparaten geabonneerd specifieke tag tooa.

### <a name="sending-hello-notification-with-mobile-services"></a>Verzenden van de melding Hallo met Mobile Services
In de planner van uw mobiele Service, kunt u Hallo script volgen:

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


