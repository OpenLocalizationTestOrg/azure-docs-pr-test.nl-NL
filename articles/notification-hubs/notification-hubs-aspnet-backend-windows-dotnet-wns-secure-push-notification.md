---
title: Notification Hubs Secure Push aaaAzure
description: Meer informatie over hoe toosend beveiligde pushmeldingen in Azure. Codevoorbeelden geschreven in C# met Hallo .NET API.
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: b6fe16c96d28d75ff698278409fb012472ba6396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="71a8a-104">Azure Notification Hubs beveiligde Push</span><span class="sxs-lookup"><span data-stu-id="71a8a-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="71a8a-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="71a8a-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="71a8a-106">iOS</span><span class="sxs-lookup"><span data-stu-id="71a8a-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="71a8a-107">Android</span><span class="sxs-lookup"><span data-stu-id="71a8a-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="71a8a-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="71a8a-108">Overview</span></span>
<span data-ttu-id="71a8a-109">Push notification-ondersteuning in Microsoft Azure kunt u tooaccess een eenvoudig te gebruiken, meerdere platforms, uitgebreid pushinfrastructuur, die sterk vereenvoudigd Hallo-implementatie van pushmeldingen voor consumenten- en enterprise-toepassingen voor mobiele telefoons -platforms.</span><span class="sxs-lookup"><span data-stu-id="71a8a-109">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="71a8a-110">Vanwege beperkingen voor tooregulatory of beveiliging kunt soms een toepassing tooinclude iets in Hallo-bericht dat via Hallo standaard push notification-infrastructuur kan niet worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="71a8a-110">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="71a8a-111">Deze zelfstudie wordt beschreven hoe tooachieve dezelfde ervaring Hallo door te sturen van gevoelige gegevens via een veilige en geverifieerde verbinding tussen clientapparaat Hallo en back-end Hallo app.</span><span class="sxs-lookup"><span data-stu-id="71a8a-111">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client device and hello app backend.</span></span>

<span data-ttu-id="71a8a-112">Op een hoog niveau is Hallo-stroom als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="71a8a-112">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="71a8a-113">Hallo back-end van app:</span><span class="sxs-lookup"><span data-stu-id="71a8a-113">hello app back-end:</span></span>
   * <span data-ttu-id="71a8a-114">Winkels beveiligde nettolading in back-enddatabase.</span><span class="sxs-lookup"><span data-stu-id="71a8a-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="71a8a-115">Hallo-ID van deze melding toohello apparaat (geen beveiligde gegevens verzonden) verzendt.</span><span class="sxs-lookup"><span data-stu-id="71a8a-115">Sends hello ID of this notification toohello device (no secure information is sent).</span></span>
2. <span data-ttu-id="71a8a-116">Hallo-app op Hallo apparaat tijdens het Hallo-bericht ontvangen:</span><span class="sxs-lookup"><span data-stu-id="71a8a-116">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="71a8a-117">Hallo-apparaat neemt contact Hallo back-end aanvragende Hallo beveiligde nettolading.</span><span class="sxs-lookup"><span data-stu-id="71a8a-117">hello device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="71a8a-118">Hallo-app kunt Hallo nettolading weergeven als een melding op Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="71a8a-118">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="71a8a-119">Het is belangrijk dat in de voorgaande stroom Hallo (en in deze zelfstudie), gaan we ervan uit dat apparaat Hallo toonote slaat geen verificatietoken in lokale opslag nadat Hallo gebruiker zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="71a8a-119">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="71a8a-120">Dit garandeert een volledig naadloze ervaring als apparaat Hallo Hallo melding van beveiligde nettolading met dit token kan ophalen.</span><span class="sxs-lookup"><span data-stu-id="71a8a-120">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="71a8a-121">Als uw toepassing slaat geen verificatietokens op Hallo-apparaat, of als deze tokens kunnen verlopen, hello apparaattoepassing bij Hallo melding moet worden weergegeven een algemene melding Hallo gebruiker toolaunch Hallo app te vragen.</span><span class="sxs-lookup"><span data-stu-id="71a8a-121">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="71a8a-122">Hallo-app vervolgens verifieert de gebruiker Hallo en toont de nettolading van de Hallo-meldingen.</span><span class="sxs-lookup"><span data-stu-id="71a8a-122">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="71a8a-123">Deze Secure Push-zelfstudie laat zien hoe een push-melding toosend veilig.</span><span class="sxs-lookup"><span data-stu-id="71a8a-123">This Secure Push tutorial shows how toosend a push notification securely.</span></span> <span data-ttu-id="71a8a-124">Hallo-zelfstudie bouwt voort op Hallo [gebruikers waarschuwen](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) zelfstudie, dus u moet eerst de voltooit Hallo stappen in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="71a8a-124">hello tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete hello steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="71a8a-125">Deze zelfstudie wordt ervan uitgegaan dat u hebt gemaakt en uw notification hub geconfigureerd zoals beschreven in [aan de slag met Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="71a8a-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span></span>
> <span data-ttu-id="71a8a-126">Ook, houd er rekening mee dat Windows Phone 8.1 (geen Windows Phone) voor Windows-referenties vereist en achtergrondtaken werken niet op Windows Phone 8.0 of Silverlight 8.1.</span><span class="sxs-lookup"><span data-stu-id="71a8a-126">Also, note that Windows Phone 8.1 requires Windows (not Windows Phone) credentials, and that background tasks do not work on Windows Phone 8.0 or Silverlight 8.1.</span></span> <span data-ttu-id="71a8a-127">Voor Windows Store-toepassingen, kunt u meldingen via een achtergrondtaak ontvangen alleen als Hallo app vergrendelingsscherm ingeschakeld (Klik op Hallo checkbox in Hallo Appmanifest).</span><span class="sxs-lookup"><span data-stu-id="71a8a-127">For Windows Store applications, you can receive notifications via a background task only if hello app is lock-screen enabled (click hello checkbox in hello Appmanifest).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-windows-phone-project"></a><span data-ttu-id="71a8a-128">Hallo Windows Phone-Project wijzigen</span><span class="sxs-lookup"><span data-stu-id="71a8a-128">Modify hello Windows Phone Project</span></span>
1. <span data-ttu-id="71a8a-129">In Hallo **NotifyUserWindowsPhone** project, het toevoegen van Hallo code tooApp.xaml.cs tooregister Hallo push achtergrondtaak te volgen.</span><span class="sxs-lookup"><span data-stu-id="71a8a-129">In hello **NotifyUserWindowsPhone** project, add hello following code tooApp.xaml.cs tooregister hello push background task.</span></span> <span data-ttu-id="71a8a-130">Toevoegen van de volgende regel code achter Hallo HALLO hallo `OnLaunched()` methode:</span><span class="sxs-lookup"><span data-stu-id="71a8a-130">Add hello following line of code at hello end of hello `OnLaunched()` method:</span></span>
   
        RegisterBackgroundTask();
2. <span data-ttu-id="71a8a-131">Voeg nog steeds in App.xaml.cs Hallo volgende code direct na Hallo `OnLaunched()` methode:</span><span class="sxs-lookup"><span data-stu-id="71a8a-131">Still in App.xaml.cs, add hello following code immediately after hello `OnLaunched()` method:</span></span>
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. <span data-ttu-id="71a8a-132">Voeg de volgende Hallo `using` instructies Hallo boven aan het bestand Hallo-App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="71a8a-132">Add hello following `using` statements at hello top of hello App.xaml.cs file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. <span data-ttu-id="71a8a-133">Van Hallo **bestand** menu in Visual Studio, klikt u op **Alles opslaan**.</span><span class="sxs-lookup"><span data-stu-id="71a8a-133">From hello **File** menu in Visual Studio, click **Save All**.</span></span>

## <a name="create-hello-push-background-component"></a><span data-ttu-id="71a8a-134">Hallo Push achtergrond onderdeel maken</span><span class="sxs-lookup"><span data-stu-id="71a8a-134">Create hello Push Background Component</span></span>
<span data-ttu-id="71a8a-135">de volgende stap Hallo is toocreate Hallo push achtergrond onderdeel.</span><span class="sxs-lookup"><span data-stu-id="71a8a-135">hello next step is toocreate hello push background component.</span></span>

1. <span data-ttu-id="71a8a-136">In Solution Explorer met de rechtermuisknop op het hoogste niveau knooppunt Hallo Hallo-oplossing (**oplossing SecurePush** in dit geval), klikt u vervolgens op **toevoegen**, klikt u vervolgens op **nieuw Project**.</span><span class="sxs-lookup"><span data-stu-id="71a8a-136">In Solution Explorer, right-click hello top-level node of hello solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span></span>
2. <span data-ttu-id="71a8a-137">Vouw **Store-Apps**, klikt u vervolgens op **Windows Phone-Apps**, klikt u vervolgens op **Windows Runtime-onderdeel (Windows Phone)**.</span><span class="sxs-lookup"><span data-stu-id="71a8a-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span></span> <span data-ttu-id="71a8a-138">Naam Hallo project **PushBackgroundComponent**, en klik vervolgens op **OK** toocreate Hallo project.</span><span class="sxs-lookup"><span data-stu-id="71a8a-138">Name hello project **PushBackgroundComponent**, and then click **OK** toocreate hello project.</span></span>
   
    ![][12]
3. <span data-ttu-id="71a8a-139">Klik in Solution Explorer met de rechtermuisknop op Hallo **PushBackgroundComponent (Windows Phone 8.1)** project en klik vervolgens op **toevoegen**, klikt u vervolgens op **klasse**.</span><span class="sxs-lookup"><span data-stu-id="71a8a-139">In Solution Explorer, right-click hello **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span></span> <span data-ttu-id="71a8a-140">Naam nieuwe klasse Hallo **PushBackgroundTask.cs**.</span><span class="sxs-lookup"><span data-stu-id="71a8a-140">Name hello new class **PushBackgroundTask.cs**.</span></span> <span data-ttu-id="71a8a-141">Klik op **toevoegen** toogenerate Hallo-klasse.</span><span class="sxs-lookup"><span data-stu-id="71a8a-141">Click **Add** toogenerate hello class.</span></span>
4. <span data-ttu-id="71a8a-142">Vervang de volledige inhoud Hallo Hallo **PushBackgroundComponent** naamruimtedefinitie Hello code de volgende, waarbij Hallo tijdelijke aanduiding vervangt `{back-end endpoint}` met Hallo backend-eindpunt is verkregen tijdens de implementatie van uw back-end:</span><span class="sxs-lookup"><span data-stu-id="71a8a-142">Replace hello entire contents of hello **PushBackgroundComponent** namespace definition with hello following code, substituting hello placeholder `{back-end endpoint}` with hello back-end endpoint obtained while deploying your back-end:</span></span>
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store hello content received from hello notification so it can be retrieved from hello UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. <span data-ttu-id="71a8a-143">Klik in Solution Explorer met de rechtermuisknop op Hallo **PushBackgroundComponent (Windows Phone 8.1)** project en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="71a8a-143">In Solution Explorer, right-click hello **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="71a8a-144">Aan de linkerkant Hallo en klikt u op **Online**.</span><span class="sxs-lookup"><span data-stu-id="71a8a-144">On hello left-hand side, click **Online**.</span></span>
7. <span data-ttu-id="71a8a-145">In Hallo **Search** in het vak **HTTP-Client**.</span><span class="sxs-lookup"><span data-stu-id="71a8a-145">In hello **Search** box, type **Http Client**.</span></span>
8. <span data-ttu-id="71a8a-146">Klik in de lijst met resultaten Hallo op **Microsoft HTTP-clientbibliotheken**, en klik vervolgens op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="71a8a-146">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="71a8a-147">Hallo-installatie voltooien.</span><span class="sxs-lookup"><span data-stu-id="71a8a-147">Complete hello installation.</span></span>
9. <span data-ttu-id="71a8a-148">Terug in Hallo NuGet **Search** in het vak **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="71a8a-148">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="71a8a-149">Hallo installeren **Json.NET** pakket en klik op sluiten Hallo NuGet Package Manager-venster.</span><span class="sxs-lookup"><span data-stu-id="71a8a-149">Install hello **Json.NET** package, then close hello NuGet Package Manager window.</span></span>
10. <span data-ttu-id="71a8a-150">Voeg de volgende Hallo `using` instructies boven Hallo Hallo **PushBackgroundTask.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="71a8a-150">Add hello following `using` statements at hello top of hello **PushBackgroundTask.cs** file:</span></span>
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. <span data-ttu-id="71a8a-151">Klik in Solution Explorer in Hallo **NotifyUserWindowsPhone (Windows Phone 8.1)** project, met de rechtermuisknop op **verwijzingen**, klikt u vervolgens op **verwijzing toevoegen...** . In het dialoogvenster Reference Manager Hallo Hallo het selectievakje naast te**PushBackgroundComponent**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="71a8a-151">In Solution Explorer, in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**. In hello Reference Manager dialog, check hello box next too**PushBackgroundComponent**, and then click **OK**.</span></span>
12. <span data-ttu-id="71a8a-152">Dubbelklik in Solution Explorer op **Package.appxmanifest** in Hallo **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span><span class="sxs-lookup"><span data-stu-id="71a8a-152">In Solution Explorer, double-click **Package.appxmanifest** in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span></span> <span data-ttu-id="71a8a-153">Onder **meldingen**stelt **Toast geschikt** te**Ja**.</span><span class="sxs-lookup"><span data-stu-id="71a8a-153">Under **Notifications**, set **Toast Capable** too**Yes**.</span></span>
    
    ![][3]
13. <span data-ttu-id="71a8a-154">Nog steeds in **Package.appxmanifest**, klikt u op Hallo **declaraties** menu aan de bovenkant Hallo.</span><span class="sxs-lookup"><span data-stu-id="71a8a-154">Still in **Package.appxmanifest**, click hello **Declarations** menu near hello top.</span></span> <span data-ttu-id="71a8a-155">In Hallo **beschikbaar declaraties** dropdown, klikt u op **achtergrondtaken**, en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="71a8a-155">In hello **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span></span>
14. <span data-ttu-id="71a8a-156">In **Package.appxmanifest**onder **eigenschappen**, Controleer **Push-melding**.</span><span class="sxs-lookup"><span data-stu-id="71a8a-156">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span></span>
15. <span data-ttu-id="71a8a-157">In **Package.appxmanifest**onder **Appinstellingen**, type **PushBackgroundComponent.PushBackgroundTask** in Hallo **toegangspunt** veld.</span><span class="sxs-lookup"><span data-stu-id="71a8a-157">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in hello **Entry Point** field.</span></span>
    
    ![][13]
16. <span data-ttu-id="71a8a-158">Van Hallo **bestand** menu, klikt u op **Alles opslaan**.</span><span class="sxs-lookup"><span data-stu-id="71a8a-158">From hello **File** menu, click **Save All**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="71a8a-159">Hallo toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="71a8a-159">Run hello Application</span></span>
<span data-ttu-id="71a8a-160">toorun toepassing hello, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="71a8a-160">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="71a8a-161">In Visual Studio, voert u Hallo **AppBackend** Web API-toepassing.</span><span class="sxs-lookup"><span data-stu-id="71a8a-161">In Visual Studio, run hello **AppBackend** Web API application.</span></span> <span data-ttu-id="71a8a-162">Een ASP.NET-webpagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="71a8a-162">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="71a8a-163">In Visual Studio, voert u Hallo **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone-app.</span><span class="sxs-lookup"><span data-stu-id="71a8a-163">In Visual Studio, run hello **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span></span> <span data-ttu-id="71a8a-164">Hallo Windows Phone-emulator wordt uitgevoerd en Hallo app automatisch wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="71a8a-164">hello Windows Phone emulator runs and loads hello app automatically.</span></span>
3. <span data-ttu-id="71a8a-165">In Hallo **NotifyUserWindowsPhone** app-gebruikersinterface een gebruikersnaam en wachtwoord invoeren.</span><span class="sxs-lookup"><span data-stu-id="71a8a-165">In hello **NotifyUserWindowsPhone** app UI, enter a username and password.</span></span> <span data-ttu-id="71a8a-166">Deze kunnen zich een willekeurige tekenreeks, maar ze moet dezelfde waarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="71a8a-166">These can be any string, but they must be hello same value.</span></span>
4. <span data-ttu-id="71a8a-167">In Hallo **NotifyUserWindowsPhone** app-gebruikersinterface Klik **aanmelden en registreren**.</span><span class="sxs-lookup"><span data-stu-id="71a8a-167">In hello **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span></span> <span data-ttu-id="71a8a-168">Klik vervolgens op **push verzenden**.</span><span class="sxs-lookup"><span data-stu-id="71a8a-168">Then click **Send push**.</span></span>

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
