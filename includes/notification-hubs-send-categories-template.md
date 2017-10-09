
<span data-ttu-id="4d23a-101">Deze sectie wordt beschreven hoe toosend belangrijk nieuws als Sjabloonmeldingen vanuit een .NET-consoletoepassing gelabeld.</span><span class="sxs-lookup"><span data-stu-id="4d23a-101">This section shows how toosend breaking news as tagged template notifications from a .NET console app.</span></span>

<span data-ttu-id="4d23a-102">Als u werkt met Mobile Apps raadpleegt u toohello [pushmeldingen toevoegen voor mobiele Apps] zelfstudie en selecteert u uw platform Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="4d23a-102">If you are using Mobile Apps please refer toohello [Add push notifications for Mobile Apps] tutorial and select your platform at hello top.</span></span>

<span data-ttu-id="4d23a-103">Als u toouse Java wilt of PHP te verwijzen[hoe toouse Notification Hubs vanuit Java/PHP].</span><span class="sxs-lookup"><span data-stu-id="4d23a-103">If you want toouse Java or PHP refer too[How toouse Notification Hubs from Java/PHP].</span></span> <span data-ttu-id="4d23a-104">U kunt meldingen verzenden vanuit een back-end met de [Notification Hubs REST-interface].</span><span class="sxs-lookup"><span data-stu-id="4d23a-104">You can send notifications from any backend using the [Notification Hubs REST interface].</span></span>

<span data-ttu-id="4d23a-105">Overslaan stappen 1-3 als u Hallo console-app voor meldingen te verzenden wanneer u voltooid gemaakt [aan de slag met Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="4d23a-105">Skip steps 1-3 if you created hello console app for sending notifications when you completed [Get started with Notification Hubs].</span></span>

1. <span data-ttu-id="4d23a-106">Maak een nieuwe Visual C#-consoletoepassing in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="4d23a-106">In Visual Studio create a new Visual C# console application:</span></span>
   
       ![][13]
2. <span data-ttu-id="4d23a-107">Klik in het hoofdmenu afkomstig is Hallo Visual Studio, op **hulpprogramma's**, **Library Package Manager**, en **Package Manager Console**, klikt u vervolgens in het consolevenster Hallo typt u het volgende en druk op **Voer**:</span><span class="sxs-lookup"><span data-stu-id="4d23a-107">In hello Visual Studio main menu, click **Tools**, **Library Package Manager**, and **Package Manager Console**, then in hello console window type the  following and press **Enter**:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="4d23a-108">Hiermee voegt u een verwijzing toohello Azure Notification Hubs SDK met de Hallo [Microsoft.Azure.Notification Hubs NuGet-pakket].</span><span class="sxs-lookup"><span data-stu-id="4d23a-108">This adds a reference toohello Azure Notification Hubs SDK using hello [Microsoft.Azure.Notification Hubs NuGet package].</span></span>
3. <span data-ttu-id="4d23a-109">Open Hallo bestand Program.cs en voeg de volgende Hallo `using` instructie:</span><span class="sxs-lookup"><span data-stu-id="4d23a-109">Open hello file Program.cs and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="4d23a-110">In Hallo `Program` klasse, Hallo na methode toevoegen of vervangen als deze al bestaat:</span><span class="sxs-lookup"><span data-stu-id="4d23a-110">In hello `Program` class, add hello following method, or replace it if it already exists:</span></span>
   
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
   
    <span data-ttu-id="4d23a-111">Deze code verzendt de melding van een sjabloon voor elk van de zes labels in de tekenreeksmatrix Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d23a-111">This code sends a template notification for each of hello six tags in hello string array.</span></span> <span data-ttu-id="4d23a-112">Hallo-gebruik van labels zorgt ervoor dat apparaten meldingen alleen voor categorieën Hallo geregistreerd ontvangen.</span><span class="sxs-lookup"><span data-stu-id="4d23a-112">hello use of tags makes sure that devices receive notifications only for hello registered categories.</span></span>
5. <span data-ttu-id="4d23a-113">Vervang in Hallo bovenstaande code Hallo `<hub name>` en `<connection string with full access>` tijdelijke aanduidingen door uw notification hub naam en het Hallo verbindingsreeks voor *DefaultFullSharedAccessSignature* vanuit Hallo dashboard van uw notification hub .</span><span class="sxs-lookup"><span data-stu-id="4d23a-113">In hello above code, replace hello `<hub name>` and `<connection string with full access>` placeholders with your notification hub name and hello connection  string for *DefaultFullSharedAccessSignature* from hello dashboard of your notification hub.</span></span>
6. <span data-ttu-id="4d23a-114">Toevoegen van de volgende regels in Hallo Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="4d23a-114">Add hello following lines in hello **Main** method:</span></span>
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="4d23a-115">Hallo-consoletoepassing bouwen.</span><span class="sxs-lookup"><span data-stu-id="4d23a-115">Build hello console app.</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[aan de slag met Notification Hubs]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[Notification Hubs REST-interface]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[pushmeldingen toevoegen voor mobiele Apps]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[hoe toouse Notification Hubs vanuit Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[Microsoft.Azure.Notification Hubs NuGet-pakket]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
