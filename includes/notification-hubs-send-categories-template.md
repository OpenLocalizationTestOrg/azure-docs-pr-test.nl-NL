
Deze sectie wordt beschreven hoe toosend belangrijk nieuws als Sjabloonmeldingen vanuit een .NET-consoletoepassing gelabeld.

Als u werkt met Mobile Apps raadpleegt u toohello [pushmeldingen toevoegen voor mobiele Apps] zelfstudie en selecteert u uw platform Hallo bovenaan.

Als u toouse Java wilt of PHP te verwijzen[hoe toouse Notification Hubs vanuit Java/PHP]. U kunt meldingen verzenden vanuit een back-end met de [Notification Hubs REST-interface].

Overslaan stappen 1-3 als u Hallo console-app voor meldingen te verzenden wanneer u voltooid gemaakt [aan de slag met Notification Hubs].

1. Maak een nieuwe Visual C#-consoletoepassing in Visual Studio:
   
       ![][13]
2. Klik in het hoofdmenu afkomstig is Hallo Visual Studio, op **hulpprogramma's**, **Library Package Manager**, en **Package Manager Console**, klikt u vervolgens in het consolevenster Hallo typt u het volgende en druk op **Voer**:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Hiermee voegt u een verwijzing toohello Azure Notification Hubs SDK met de Hallo [Microsoft.Azure.Notification Hubs NuGet-pakket].
3. Open Hallo bestand Program.cs en voeg de volgende Hallo `using` instructie:
   
        using Microsoft.Azure.NotificationHubs;
4. In Hallo `Program` klasse, Hallo na methode toevoegen of vervangen als deze al bestaat:
   
        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub =
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");
   
            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business",
                                            "Technology", "Science", "Sports"};
   
            // Sending hello notification as a template notification. All template registrations that contain
            // "messageParam" and hello proper tags will receive hello notifications.
            // This includes APNS, GCM, WNS, and MPNS template registrations.
   
            Dictionary<string, string> templateParams = new Dictionary<string, string>();
   
            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";
                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
         }
   
    Deze code verzendt de melding van een sjabloon voor elk van de zes labels in de tekenreeksmatrix Hallo Hallo. Hallo-gebruik van labels zorgt ervoor dat apparaten meldingen alleen voor categorieën Hallo geregistreerd ontvangen.
5. Vervang in Hallo bovenstaande code Hallo `<hub name>` en `<connection string with full access>` tijdelijke aanduidingen door uw notification hub naam en het Hallo verbindingsreeks voor *DefaultFullSharedAccessSignature* vanuit Hallo dashboard van uw notification hub .
6. Toevoegen van de volgende regels in Hallo Hallo **Main** methode:
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. Hallo-consoletoepassing bouwen.

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[aan de slag met Notification Hubs]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[Notification Hubs REST-interface]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[pushmeldingen toevoegen voor mobiele Apps]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[hoe toouse Notification Hubs vanuit Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[Microsoft.Azure.Notification Hubs NuGet-pakket]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
