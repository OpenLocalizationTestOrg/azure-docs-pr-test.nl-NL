
Deze sectie wordt beschreven hoe belangrijk nieuws als gelabeld Sjabloonmeldingen verzendt vanuit een .NET-consoletoepassing.

Als u werkt met Mobile Apps raadpleegt u de [pushmeldingen toevoegen voor mobiele Apps] zelfstudie en selecteert u uw platform aan het begin.

Als u wilt gebruiken, Java of PHP verwijzen naar [hoe Notification Hubs gebruiken vanuit Java/PHP]. U kunt meldingen verzenden vanuit een back-end met de [Notification Hubs REST-interface].

Overslaan stappen 1-3 als u de console-app voor meldingen te verzenden wanneer u voltooid gemaakt [aan de slag met Notification Hubs].

1. Maak een nieuwe Visual C#-consoletoepassing in Visual Studio:
   
       ![][13]
2. Klik in het hoofdmenu van Visual Studio op **extra**, **Library Package Manager**, en **Package Manager Console**, in het consolevenster typt u het volgende en druk op  **Voer**:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Hiermee wordt een verwijzing toegevoegd aan de Azure Notification Hubs SDK met het [Microsoft.Azure.Notification Hubs NuGet-pakket].
3. Open het bestand Program.cs en voeg de volgende `using` instructie:
   
        using Microsoft.Azure.NotificationHubs;
4. In de `Program` klasse, voeg de volgende methode toe of vervangen als deze al bestaat:
   
        private static async void SendTemplateNotificationAsync()
        {
            // Define the notification hub.
            NotificationHubClient hub =
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");
   
            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business",
                                            "Technology", "Science", "Sports"};
   
            // Sending the notification as a template notification. All template registrations that contain
            // "messageParam" and the proper tags will receive the notifications.
            // This includes APNS, GCM, WNS, and MPNS template registrations.
   
            Dictionary<string, string> templateParams = new Dictionary<string, string>();
   
            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";
                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
         }
   
    Deze code verzendt de melding van een sjabloon voor elk van de zes labels in de tekenreeksmatrix. Het gebruik van labels zorgt ervoor dat apparaten meldingen alleen voor de geregistreerde categorieën ontvangen.
5. Vervang in de bovenstaande code de `<hub name>` en `<connection string with full access>` tijdelijke aanduidingen door de naam van uw notification hub en de verbindingsreeks voor *DefaultFullSharedAccessSignature* vanuit het dashboard van uw notification hub.
6. Voeg de volgende regels in de **Main**-methode toe:
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. De console-app bouwen.

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[aan de slag met Notification Hubs]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[Notification Hubs REST-interface]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[pushmeldingen toevoegen voor mobiele Apps]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[hoe Notification Hubs gebruiken vanuit Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[Microsoft.Azure.Notification Hubs NuGet-pakket]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
