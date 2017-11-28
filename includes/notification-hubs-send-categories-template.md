
<span data-ttu-id="07531-101">Deze sectie wordt beschreven hoe belangrijk nieuws als gelabeld Sjabloonmeldingen verzendt vanuit een .NET-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="07531-101">This section shows how to send breaking news as tagged template notifications from a .NET console app.</span></span>

<span data-ttu-id="07531-102">Als u werkt met Mobile Apps raadpleegt u de [pushmeldingen toevoegen voor mobiele Apps] zelfstudie en selecteert u uw platform aan het begin.</span><span class="sxs-lookup"><span data-stu-id="07531-102">If you are using Mobile Apps please refer to the [Add push notifications for Mobile Apps] tutorial and select your platform at the top.</span></span>

<span data-ttu-id="07531-103">Als u wilt gebruiken, Java of PHP verwijzen naar [hoe Notification Hubs gebruiken vanuit Java/PHP].</span><span class="sxs-lookup"><span data-stu-id="07531-103">If you want to use Java or PHP refer to [How to use Notification Hubs from Java/PHP].</span></span> <span data-ttu-id="07531-104">U kunt meldingen verzenden vanuit een back-end met de [Notification Hubs REST-interface].</span><span class="sxs-lookup"><span data-stu-id="07531-104">You can send notifications from any backend using the [Notification Hubs REST interface].</span></span>

<span data-ttu-id="07531-105">Overslaan stappen 1-3 als u de console-app voor meldingen te verzenden wanneer u voltooid gemaakt [aan de slag met Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="07531-105">Skip steps 1-3 if you created the console app for sending notifications when you completed [Get started with Notification Hubs].</span></span>

1. <span data-ttu-id="07531-106">Maak een nieuwe Visual C#-consoletoepassing in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="07531-106">In Visual Studio create a new Visual C# console application:</span></span>
   
       ![][13]
2. <span data-ttu-id="07531-107">Klik in het hoofdmenu van Visual Studio op **extra**, **Library Package Manager**, en **Package Manager Console**, in het consolevenster typt u het volgende en druk op  **Voer**:</span><span class="sxs-lookup"><span data-stu-id="07531-107">In the Visual Studio main menu, click **Tools**, **Library Package Manager**, and **Package Manager Console**, then in the console window type the  following and press **Enter**:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="07531-108">Hiermee wordt een verwijzing toegevoegd aan de Azure Notification Hubs SDK met het [Microsoft.Azure.Notification Hubs NuGet-pakket].</span><span class="sxs-lookup"><span data-stu-id="07531-108">This adds a reference to the Azure Notification Hubs SDK using the [Microsoft.Azure.Notification Hubs NuGet package].</span></span>
3. <span data-ttu-id="07531-109">Open het bestand Program.cs en voeg de volgende `using` instructie:</span><span class="sxs-lookup"><span data-stu-id="07531-109">Open the file Program.cs and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="07531-110">In de `Program` klasse, voeg de volgende methode toe of vervangen als deze al bestaat:</span><span class="sxs-lookup"><span data-stu-id="07531-110">In the `Program` class, add the following method, or replace it if it already exists:</span></span>
   
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
   
    <span data-ttu-id="07531-111">Deze code verzendt de melding van een sjabloon voor elk van de zes labels in de tekenreeksmatrix.</span><span class="sxs-lookup"><span data-stu-id="07531-111">This code sends a template notification for each of the six tags in the string array.</span></span> <span data-ttu-id="07531-112">Het gebruik van labels zorgt ervoor dat apparaten meldingen alleen voor de geregistreerde categorieën ontvangen.</span><span class="sxs-lookup"><span data-stu-id="07531-112">The use of tags makes sure that devices receive notifications only for the registered categories.</span></span>
5. <span data-ttu-id="07531-113">Vervang in de bovenstaande code de `<hub name>` en `<connection string with full access>` tijdelijke aanduidingen door de naam van uw notification hub en de verbindingsreeks voor *DefaultFullSharedAccessSignature* vanuit het dashboard van uw notification hub.</span><span class="sxs-lookup"><span data-stu-id="07531-113">In the above code, replace the `<hub name>` and `<connection string with full access>` placeholders with your notification hub name and the connection  string for *DefaultFullSharedAccessSignature* from the dashboard of your notification hub.</span></span>
6. <span data-ttu-id="07531-114">Voeg de volgende regels in de **Main**-methode toe:</span><span class="sxs-lookup"><span data-stu-id="07531-114">Add the following lines in the **Main** method:</span></span>
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="07531-115">De console-app bouwen.</span><span class="sxs-lookup"><span data-stu-id="07531-115">Build the console app.</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
<span data-ttu-id="07531-116">[aan de slag met Notification Hubs]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="07531-116">[Get started with Notification Hubs]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span></span>
<span data-ttu-id="07531-117">[Notification Hubs REST-interface]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx</span><span class="sxs-lookup"><span data-stu-id="07531-117">[Notification Hubs REST interface]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx</span></span>
<span data-ttu-id="07531-118">[pushmeldingen toevoegen voor mobiele Apps]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="07531-118">[Add push notifications for Mobile Apps]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md</span></span>
<span data-ttu-id="07531-119">[hoe Notification Hubs gebruiken vanuit Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md</span><span class="sxs-lookup"><span data-stu-id="07531-119">[How to use Notification Hubs from Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md</span></span>
<span data-ttu-id="07531-120">[Microsoft.Azure.Notification Hubs NuGet-pakket]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/</span><span class="sxs-lookup"><span data-stu-id="07531-120">[Microsoft.Azure.Notification Hubs NuGet package]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/</span></span>
