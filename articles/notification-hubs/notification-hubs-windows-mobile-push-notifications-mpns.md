---
title: aaaSending pushmeldingen verzenden met Azure Notification Hubs op Windows Phone | Microsoft Docs
description: In deze zelfstudie leert u hoe toouse Azure Notification Hubs toopush meldingen tooa Windows Phone 8 of Windows Phone 8.1 Silverlight-toepassing.
services: notification-hubs
documentationcenter: windows
keywords: pushmelding,pushmelding,windows phone-push
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 1a0ad238fe7788ae2e4f47f02d113391af03dd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a><span data-ttu-id="a6249-104">Pushmeldingen verzenden met Azure Notification Hubs op Windows Phone</span><span class="sxs-lookup"><span data-stu-id="a6249-104">Sending push notifications with Azure Notification Hubs on Windows Phone</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="a6249-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="a6249-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="a6249-106">toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="a6249-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="a6249-107">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="a6249-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a6249-108">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a6249-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="a6249-109">Deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooa Windows Phone 8 of Windows Phone 8.1 Silverlight-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a6249-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Windows Phone 8 or Windows Phone 8.1 Silverlight application.</span></span> <span data-ttu-id="a6249-110">Als u ontwikkelt voor Windows Phone 8.1 (zonder Silverlight), raadpleegt u toohello [universele Windows-](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) versie.</span><span class="sxs-lookup"><span data-stu-id="a6249-110">If you are targeting Windows Phone 8.1 (non-Silverlight), then refer toohello [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version.</span></span>
<span data-ttu-id="a6249-111">In deze zelfstudie maakt u een lege Windows Phone 8-app die pushmeldingen ontvangt via Hallo Microsoft Push Notification Service (MPNS).</span><span class="sxs-lookup"><span data-stu-id="a6249-111">In this tutorial, you create a blank Windows Phone 8 app that receives push notifications by using hello Microsoft Push Notification Service (MPNS).</span></span> <span data-ttu-id="a6249-112">Wanneer u klaar bent, moet u kunnen toouse push uw notification hub toobroadcast meldingen tooall Hallo apparaten waarop uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a6249-112">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

> [!NOTE]
> <span data-ttu-id="a6249-113">Hallo Notification Hubs Windows Phone SDK biedt geen ondersteuning voor het gebruik van Hallo Windows Push Notification Service (WNS) met Windows Phone 8.1 Silverlight-apps.</span><span class="sxs-lookup"><span data-stu-id="a6249-113">hello Notification Hubs Windows Phone SDK does not support using hello Windows Push Notification Service (WNS) with Windows Phone 8.1 Silverlight apps.</span></span> <span data-ttu-id="a6249-114">toouse WNS (in plaats van MPNS) met Windows Phone 8.1 Silverlight-apps, volgt u Hallo [Notification Hubs - Windows Phone Silverlight-zelfstudie], waarin REST API's.</span><span class="sxs-lookup"><span data-stu-id="a6249-114">toouse WNS (instead of MPNS) with Windows Phone 8.1 Silverlight apps, follow hello [Notification Hubs - Windows Phone Silverlight tutorial], which uses REST APIs.</span></span>
> 
> 

<span data-ttu-id="a6249-115">Hallo zelfstudie wordt Hallo eenvoudige scenario uitzenden met Notification hubs beschreven.</span><span class="sxs-lookup"><span data-stu-id="a6249-115">hello tutorial demonstrates hello simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6249-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a6249-116">Prerequisites</span></span>
<span data-ttu-id="a6249-117">Deze zelfstudie vereist de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="a6249-117">This tutorial requires hello following:</span></span>

* <span data-ttu-id="a6249-118">[Visual Studio 2012 Express voor Windows Phone] of een hogere versie.</span><span class="sxs-lookup"><span data-stu-id="a6249-118">[Visual Studio 2012 Express for Windows Phone], or a later version.</span></span>

<span data-ttu-id="a6249-119">Het voltooien van deze zelfstudie is een vereiste voor alle andere Notification Hubs-zelfstudies voor Windows Phone 8-apps.</span><span class="sxs-lookup"><span data-stu-id="a6249-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Phone 8 apps.</span></span>

## <a name="create-your-notification-hub"></a><span data-ttu-id="a6249-120">Een Notification Hub maken</span><span class="sxs-lookup"><span data-stu-id="a6249-120">Create your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="a6249-121">Klik op Hallo <b>Notification Services</b> sectie (binnen <i>instellingen</i>), klikt u op <b>Windows Phone (MPNS)</b> en klik vervolgens op Hallo <b>niet-geverifieerde pushmeldingen inschakelen </b> selectievakje.</span><span class="sxs-lookup"><span data-stu-id="a6249-121">Click hello <b>Notification Services</b> section (within <i>Settings</i>), click on <b>Windows Phone (MPNS)</b> and then click hello <b>Enable unauthenticated push</b> check box.</span></span></p>
</li>
</ol>

&emsp;&emsp;![Azure Portal - Niet-geverifieerde pushmeldingen inschakelen](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

<span data-ttu-id="a6249-123">De hub is nu gemaakt en geconfigureerd toosend niet-geverifieerde meldingen voor Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="a6249-123">Your hub is now created and configured toosend unauthenticated notification for Windows Phone.</span></span>

> [!NOTE]
> <span data-ttu-id="a6249-124">In deze zelfstudie wordt MPNS in niet-geverifieerde modus gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a6249-124">This tutorial uses MPNS in unauthenticated mode.</span></span> <span data-ttu-id="a6249-125">Niet-geverifieerde MPNS-modus gelden beperkingen voor meldingen dat u tooeach kanaal kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="a6249-125">MPNS unauthenticated mode comes with restrictions on notifications that you can send tooeach channel.</span></span> <span data-ttu-id="a6249-126">Notification Hubs ondersteunt [geverifieerde MPNS-modus](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) doordat u tooupload uw certificaat.</span><span class="sxs-lookup"><span data-stu-id="a6249-126">Notification Hubs supports [MPNS authenticated mode](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) by allowing you tooupload your certificate.</span></span>
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a><span data-ttu-id="a6249-127">Verbinding maken met uw app toohello notification hub</span><span class="sxs-lookup"><span data-stu-id="a6249-127">Connecting your app toohello notification hub</span></span>
1. <span data-ttu-id="a6249-128">Maak een nieuwe Windows Phone 8-toepassing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a6249-128">In Visual Studio, create a new Windows Phone 8 application.</span></span>
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    <span data-ttu-id="a6249-129">In Visual Studio 2013 Update 2 of hoger maakt u daarentegen een Windows Phone Silverlight-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a6249-129">In Visual Studio 2013 Update 2 or later, you instead create a Windows Phone Silverlight application.</span></span>
   
    ![Visual Studio - Nieuw project - Lege app - Windows Phone Silverlight][11]
2. <span data-ttu-id="a6249-131">Met de rechtermuisknop op het Hallo-oplossing in Visual Studio en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="a6249-131">In Visual Studio, right-click hello solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="a6249-132">U ziet nu Hallo **NuGet-pakketten beheren** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a6249-132">This displays hello **Manage NuGet Packages** dialog box.</span></span>
3. <span data-ttu-id="a6249-133">Zoeken naar `WindowsAzure.Messaging.Managed` en klik op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="a6249-133">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and then accept hello terms of use.</span></span>
   
    ![Visual Studio - NuGet Package Manager][20]
   
    <span data-ttu-id="a6249-135">Hiermee downloadt, installeert en wordt een verwijzing toohello Azure Messaging-bibliotheek voor Windows hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet-pakket</a>.</span><span class="sxs-lookup"><span data-stu-id="a6249-135">This downloads, installs, and adds a reference toohello Azure Messaging library for Windows by using hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
4. <span data-ttu-id="a6249-136">Open Hallo bestand App.xaml.cs en voeg de volgende Hallo `using` instructies:</span><span class="sxs-lookup"><span data-stu-id="a6249-136">Open hello file App.xaml.cs and add hello following `using` statements:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. <span data-ttu-id="a6249-137">Hallo code Hallo boven aan het volgende toevoegen **Application_Launching** methode in App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="a6249-137">Add hello following code at hello top of **Application_Launching** method in App.xaml.cs:</span></span>
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > <span data-ttu-id="a6249-138">Hallo waarde **MyPushChannel** is een index die is gebruikt toolookup een bestaand kanaal in Hallo [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) verzameling.</span><span class="sxs-lookup"><span data-stu-id="a6249-138">hello value **MyPushChannel** is an index that is used toolookup an existing channel in hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) collection.</span></span> <span data-ttu-id="a6249-139">Als het kanaal niet wordt gevonden, maakt u een nieuwe vermelding met die naam.</span><span class="sxs-lookup"><span data-stu-id="a6249-139">If there isn't one there, create a new entry with that name.</span></span>
   > 
   > 
   
    <span data-ttu-id="a6249-140">Zorg ervoor dat tooinsert Hallo-naam van uw hub en Hallo-verbindingsreeks aangeroepen **DefaultListenSharedAccessSignature** die u hebt verkregen in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="a6249-140">Make sure tooinsert hello name of your hub and hello connection string called **DefaultListenSharedAccessSignature** that you obtained in hello previous section.</span></span>
    <span data-ttu-id="a6249-141">Deze code Hallo kanaal-URI voor Hallo app opgehaald uit MPNS en vervolgens die kanaal-URI voor uw notification hub geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="a6249-141">This code retrieves hello channel URI for hello app from MPNS, and then registers that channel URI with your notification hub.</span></span> <span data-ttu-id="a6249-142">Ook wordt hiermee gegarandeerd dat Hallo kanaal-URI is geregistreerd in uw notification hub die elke keer Hallo-toepassing wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="a6249-142">It also guarantees that hello channel URI is registered in your notification hub each time hello application is launched.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a6249-143">Deze zelfstudie wordt een toast-melding toohello apparaat verzonden.</span><span class="sxs-lookup"><span data-stu-id="a6249-143">This tutorial sends a toast notification toohello device.</span></span> <span data-ttu-id="a6249-144">Wanneer u een tegelmelding verzendt, moet u in plaats daarvan Hallo aanroepen **BindToShellTile** methode op het Hallo-kanaal.</span><span class="sxs-lookup"><span data-stu-id="a6249-144">When you send a tile notification, you must instead call hello **BindToShellTile** method on hello channel.</span></span> <span data-ttu-id="a6249-145">toosupport toast en de tegel meldingen, roept **BindToShellTile** en **BindToShellToast**.</span><span class="sxs-lookup"><span data-stu-id="a6249-145">toosupport both toast and tile notifications, call both **BindToShellTile** and  **BindToShellToast**.</span></span>
   > 
   > 
6. <span data-ttu-id="a6249-146">Vouw in Solution Explorer **eigenschappen**Open Hallo `WMAppManifest.xml` bestand, klikt u op Hallo **mogelijkheden** tabblad en zorg ervoor dat Hallo **ID_CAP_PUSH_NOTIFICATION** is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a6249-146">In Solution Explorer, expand **Properties**, open hello `WMAppManifest.xml` file, click hello **Capabilities** tab, and make sure that hello **ID_CAP_PUSH_NOTIFICATION** capability is checked.</span></span>
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. <span data-ttu-id="a6249-147">Druk op Hallo `F5` key toorun Hallo app.</span><span class="sxs-lookup"><span data-stu-id="a6249-147">Press hello `F5` key toorun hello app.</span></span>
   
    <span data-ttu-id="a6249-148">Een registratiebericht wordt weergegeven in het Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="a6249-148">A registration message is displayed in hello app.</span></span>
8. <span data-ttu-id="a6249-149">Sluit Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="a6249-149">Close hello app.</span></span>  
   
   > [!NOTE]
   > <span data-ttu-id="a6249-150">een pop-upmelding tooreceive, Hallo toepassing moet niet worden uitgevoerd op de voorgrond Hallo.</span><span class="sxs-lookup"><span data-stu-id="a6249-150">tooreceive a toast push notification, hello application must not be running in hello foreground.</span></span>
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a><span data-ttu-id="a6249-151">Pushmeldingen verzenden vanuit uw back-end</span><span class="sxs-lookup"><span data-stu-id="a6249-151">Send push notifications from your backend</span></span>
<span data-ttu-id="a6249-152">U kunt pushmeldingen verzenden via Notification Hubs vanuit elke back-end via openbare Hallo <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST-interface</a>.</span><span class="sxs-lookup"><span data-stu-id="a6249-152">You can send push notifications by using Notification Hubs from any backend via hello public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="a6249-153">In deze zelfstudie verzendt u pushmeldingen met een .NET-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="a6249-153">In this tutorial, you send push notifications using a .NET console application.</span></span> 

<span data-ttu-id="a6249-154">Zie voor een voorbeeld van hoe toosend pushmeldingen vanuit een back-end voor een ASP.NET WebAPI die geïntegreerd met Notification Hubs [Azure Notification Hubs gebruikers waarschuwen met .NET back-end](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span><span class="sxs-lookup"><span data-stu-id="a6249-154">For an example of how toosend push notifications from an ASP.NET WebAPI backend that's integrated with Notification Hubs, see [Azure Notification Hubs Notify Users with .NET backend](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span></span>  

<span data-ttu-id="a6249-155">Voor een voorbeeld van hoe toosend pushmeldingen met Hallo [REST-API's](https://msdn.microsoft.com/library/azure/dn223264.aspx), Bekijk [hoe toouse Notification Hubs vanuit Java](notification-hubs-java-push-notification-tutorial.md) en [hoe toouse Notification Hubs vanuit PHP](notification-hubs-php-push-notification-tutorial.md) .</span><span class="sxs-lookup"><span data-stu-id="a6249-155">For an example of how toosend push notifications by using hello [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx), check out [How toouse Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) and [How toouse Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

1. <span data-ttu-id="a6249-156">Klik met de rechtermuisknop Hallo-oplossing, selecteer **toevoegen** en **nieuw Project...** , en klik vervolgens onder **Visual C#**, klikt u op **Windows** en **consoletoepassing**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a6249-156">Right-click hello solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
       ![Visual Studio - New Project - Console Application][6]
   
    <span data-ttu-id="a6249-157">Hiermee wordt een nieuwe Visual C# console toepassing toohello oplossing toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="a6249-157">This adds a new Visual C# console application toohello solution.</span></span> <span data-ttu-id="a6249-158">U kunt dit ook in een afzonderlijke oplossing doen.</span><span class="sxs-lookup"><span data-stu-id="a6249-158">You can also do this in a separate solution.</span></span>
2. <span data-ttu-id="a6249-159">Klik achtereenvolgens op **Extra**, **Library Package Manager** en **Package Manager-console**.</span><span class="sxs-lookup"><span data-stu-id="a6249-159">Click **Tools**, click **Library Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="a6249-160">Hallo Package Manager-Console worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a6249-160">This displays hello Package Manager Console.</span></span>
3. <span data-ttu-id="a6249-161">In Hallo **Package Manager Console** venster, set Hallo **standaardproject** tooyour nieuwe console toepassingsproject en vervolgens in het consolevenster hello, Hallo volgende opdracht wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="a6249-161">In hello **Package Manager Console** window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   <span data-ttu-id="a6249-162">Hiermee voegt u een verwijzing toohello Azure Notification Hubs SDK met de Hallo <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet-pakket</a>.</span><span class="sxs-lookup"><span data-stu-id="a6249-162">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="a6249-163">Open Hallo `Program.cs` -bestand en voeg de volgende Hallo `using` instructie:</span><span class="sxs-lookup"><span data-stu-id="a6249-163">Open hello `Program.cs` file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="a6249-164">In Hallo `Program` klasse, Hallo volgende methode toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="a6249-164">In hello `Program` class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    <span data-ttu-id="a6249-165">Zorg ervoor dat tooreplace hello `<hub name>` tijdelijke aanduiding met de naam van Hallo notification hub die wordt weergegeven in de portal Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="a6249-165">Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello portal.</span></span> <span data-ttu-id="a6249-166">Vervang ook Hallo connection string tijdelijke aanduiding door Hallo verbindingsreeks genaamd **DefaultFullSharedAccessSignature** die u hebt verkregen in de sectie Hallo 'Uw notification hub configureren'.</span><span class="sxs-lookup"><span data-stu-id="a6249-166">Also, replace hello connection string placeholder with hello connection string called **DefaultFullSharedAccessSignature** that you obtained in hello section "Configure your notification hub."</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a6249-167">Zorg ervoor dat u de verbindingsreeks Hallo met **volledige** toegang niet **luisteren** toegang.</span><span class="sxs-lookup"><span data-stu-id="a6249-167">Make sure that you use hello connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="a6249-168">Hallo toegangsrecht luisteren tekenreeks heeft geen machtigingen toosend pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="a6249-168">hello listen-access string does not have permissions toosend push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="a6249-169">Toevoegen van Hallo volgende regel in uw `Main` methode:</span><span class="sxs-lookup"><span data-stu-id="a6249-169">Add hello following line in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="a6249-170">Met uw Windows Phone-emulator wordt uitgevoerd en uw app gesloten, stel Hallo consoletoepassingsproject als Hallo standaard opstartproject en druk vervolgens op Hallo `F5` key toorun Hallo app.</span><span class="sxs-lookup"><span data-stu-id="a6249-170">With your Windows Phone emulator running and your app closed, set hello console application project as hello default startup project, and then press hello `F5` key toorun hello app.</span></span>
   
    <span data-ttu-id="a6249-171">U ontvangt een pop-uppushmelding.</span><span class="sxs-lookup"><span data-stu-id="a6249-171">You will receive a toast push notification.</span></span> <span data-ttu-id="a6249-172">Hallo-app te tikken op Hallo toast banner worden geladen.</span><span class="sxs-lookup"><span data-stu-id="a6249-172">Tapping hello toast banner loads hello app.</span></span>

<span data-ttu-id="a6249-173">U vindt alle mogelijke nettoladingen van Hallo in Hallo [pop-upcatalogus] en [tegelcatalogus] onderwerpen op MSDN.</span><span class="sxs-lookup"><span data-stu-id="a6249-173">You can find all hello possible payloads in hello [toast catalog] and [tile catalog] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6249-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a6249-174">Next steps</span></span>
<span data-ttu-id="a6249-175">In dit eenvoudige voorbeeld hebt u uitgezonden push notifications tooall uw Windows Phone 8-apparaten.</span><span class="sxs-lookup"><span data-stu-id="a6249-175">In this simple example, you broadcasted push notifications tooall your Windows Phone 8 devices.</span></span> 

<span data-ttu-id="a6249-176">In de volgorde tootarget specifieke gebruikers, raadpleeg dan toohello [Notification Hubs gebruiken toopush meldingen toousers] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a6249-176">In order tootarget specific users, refer toohello [Use Notification Hubs toopush notifications toousers] tutorial.</span></span> 

<span data-ttu-id="a6249-177">Als u wilt dat toosegment gebruikers op belangengroepen, kunt u lezen [Notification Hubs gebruiken toosend belangrijk nieuws].</span><span class="sxs-lookup"><span data-stu-id="a6249-177">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> 

<span data-ttu-id="a6249-178">Meer informatie over het toouse Notification Hubs in [richtlijnen voor Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="a6249-178">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance].</span></span>

<!-- Images. -->
[6]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: ./media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: ./media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: ./media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
[Visual Studio 2012 Express voor Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374
[richtlijnen voor Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[Notification Hubs gebruiken toopush meldingen toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Notification Hubs gebruiken toosend belangrijk nieuws]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[pop-upcatalogus]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[tegelcatalogus]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[Notification Hubs - Windows Phone Silverlight-zelfstudie]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp

