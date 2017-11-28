---
title: Aan de slag met Azure Notification Hubs voor Windows Universal Platform-apps | Microsoft Docs
description: In deze zelfstudie leert u hoe u Azure Notification Hubs gebruikt om meldingen naar een Windows Universal Platform-toepassing te pushen.
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 9b50f1cca81348b69f7ff2d702c6c72871afe0a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a><span data-ttu-id="b371d-103">Aan de slag met Notification Hubs voor Windows Universal Platform-apps</span><span class="sxs-lookup"><span data-stu-id="b371d-103">Getting started with Notification Hubs for Windows Universal Platform Apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="b371d-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b371d-104">Overview</span></span>
<span data-ttu-id="b371d-105">In deze zelfstudie leert u hoe u Azure Notification Hubs gebruikt om pushmeldingen te verzenden naar een Universal Windows Platform-app (UWP-app).</span><span class="sxs-lookup"><span data-stu-id="b371d-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Universal Windows Platform (UWP) app.</span></span>

<span data-ttu-id="b371d-106">In deze zelfstudie maakt u een lege Windows Store-app die pushmeldingen ontvangt via Windows Push Notification Service (WNS).</span><span class="sxs-lookup"><span data-stu-id="b371d-106">In this tutorial, you create a blank Windows Store app that receives push notifications by using the Windows Push Notification Service (WNS).</span></span> <span data-ttu-id="b371d-107">Als u klaar bent, kunt u de Notification Hub gebruiken om pushmeldingen uit te zenden naar alle apparaten waarop uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b371d-107">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b371d-108">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="b371d-108">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="b371d-109">De volledige code voor deze zelfstudie vindt u [hier](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal) op GitHub.</span><span class="sxs-lookup"><span data-stu-id="b371d-109">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b371d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b371d-110">Prerequisites</span></span>
<span data-ttu-id="b371d-111">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="b371d-111">This tutorial requires the following:</span></span>

* <span data-ttu-id="b371d-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) of later</span><span class="sxs-lookup"><span data-stu-id="b371d-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) or later</span></span>
* [<span data-ttu-id="b371d-113">Universal Windows App Development Tools geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="b371d-113">Universal Windows App Development Tools installed</span></span>](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* <span data-ttu-id="b371d-114">Een actief Azure-account</span><span class="sxs-lookup"><span data-stu-id="b371d-114">An active Azure account</span></span> <br/><span data-ttu-id="b371d-115">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="b371d-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b371d-116">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b371d-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span></span>
* <span data-ttu-id="b371d-117">Een actief Windows Store-account</span><span class="sxs-lookup"><span data-stu-id="b371d-117">An active Windows Store account</span></span>

<span data-ttu-id="b371d-118">Het voltooien van deze zelfstudie is een vereiste voor alle andere Notification Hubs-zelfstudies voor Windows Universal Platform-apps.</span><span class="sxs-lookup"><span data-stu-id="b371d-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Universal Platform apps.</span></span>

## <a name="register-your-app-for-the-windows-store"></a><span data-ttu-id="b371d-119">Uw app registreren voor Windows Store</span><span class="sxs-lookup"><span data-stu-id="b371d-119">Register your app for the Windows Store</span></span>
<span data-ttu-id="b371d-120">Als u pushmeldingen naar UWP-apps wilt verzenden, moet u uw app aan de Windows Store koppelen.</span><span class="sxs-lookup"><span data-stu-id="b371d-120">To send push notifications to UWP apps, you must associate your app to the Windows Store.</span></span> <span data-ttu-id="b371d-121">Vervolgens moet u de Notification Hub configureren voor integratie met WNS.</span><span class="sxs-lookup"><span data-stu-id="b371d-121">You must then configure your notification hub to integrate with WNS.</span></span>

1. <span data-ttu-id="b371d-122">Als u uw app nog niet hebt geregistreerd, gaat u naar het [Windows-ontwikkelaarscentrum](https://dev.windows.com/overview), meldt u zich aan met uw Microsoft-account en klikt u vervolgens op **Een nieuwe app maken**.</span><span class="sxs-lookup"><span data-stu-id="b371d-122">If you have not already registered your app, navigate to the [Windows Dev Center](https://dev.windows.com/overview), sign in with your Microsoft account, and then click **Create a new app**.</span></span>

2. <span data-ttu-id="b371d-123">Typ een naam voor uw app en klik op **App-naam reserveren**.</span><span class="sxs-lookup"><span data-stu-id="b371d-123">Type a name for your app and click **Reserve app name**.</span></span> <span data-ttu-id="b371d-124">Hiermee maakt u een nieuwe Windows Store-registratie voor uw app.</span><span class="sxs-lookup"><span data-stu-id="b371d-124">This creates a new Windows Store registration for your app.</span></span>

3. <span data-ttu-id="b371d-125">Maak in Visual Studio een nieuw project voor Visual C# Store-apps met de universele sjabloon **Lege app** van Windows en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b371d-125">In Visual Studio, create a new Visual C# Store Apps project by using the Windows Universal **Blank App** template and click **OK**.</span></span>

4. <span data-ttu-id="b371d-126">Accepteer de standaardwaarden voor het doel en de minimale platformversies.</span><span class="sxs-lookup"><span data-stu-id="b371d-126">Accept the defaults for the target and minimum platform versions.</span></span>

5. <span data-ttu-id="b371d-127">Klik in Solution Explorer met de rechtermuisknop op het Windows Store-app-project, klik op **Store** en klik vervolgens op **App aan de Store koppelen**.</span><span class="sxs-lookup"><span data-stu-id="b371d-127">In Solution Explorer, right-click the Windows Store app project, click **Store**, and then click **Associate App with the Store...**.</span></span> <span data-ttu-id="b371d-128">Hierop wordt de wizard **Uw app koppelen aan Windows Store** weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b371d-128">The **Associate Your App with the Windows Store** wizard appears.</span></span>

6. <span data-ttu-id="b371d-129">Meld u in de wizard aan met uw Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="b371d-129">In the wizard, sign in with your Microsoft account.</span></span>

7. <span data-ttu-id="b371d-130">Klik op de app die u in stap 2 hebt geregistreerd, klik op **Volgende** en klik vervolgens op **Koppelen**.</span><span class="sxs-lookup"><span data-stu-id="b371d-130">Click the app that you registered in step 2, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="b371d-131">Hierdoor worden de vereiste registratiegegevens voor Windows Store toegevoegd aan het toepassingsmanifest.</span><span class="sxs-lookup"><span data-stu-id="b371d-131">This adds the required Windows Store registration information to the application manifest.</span></span>

8. <span data-ttu-id="b371d-132">Klik als u weer terug bent op de pagina [Windows-ontwikkelaarscentrum](http://dev.windows.com/overview) voor uw nieuwe app op **Services**, klik op **Pushmeldingen** en klik vervolgens op **WNS/MPNS**.</span><span class="sxs-lookup"><span data-stu-id="b371d-132">Back on the [Windows Dev Center](http://dev.windows.com/overview) page for your new app, click **Services**, click **Push notifications**, and then click **WNS/MPNS**.</span></span>

9. <span data-ttu-id="b371d-133">Klik op **Nieuwe melding**.</span><span class="sxs-lookup"><span data-stu-id="b371d-133">Click **New Notification**.</span></span>

10. <span data-ttu-id="b371d-134">Klik op de sjabloon **Leeg (pop-up)** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b371d-134">Click **Blank (Toast)** template and then click **OK**.</span></span>

11. <span data-ttu-id="b371d-135">Voer een **Naam** voor de melding en een visueel **Context**bericht in.</span><span class="sxs-lookup"><span data-stu-id="b371d-135">Enter a notification **Name** and Visual **Context** message.</span></span> <span data-ttu-id="b371d-136">Klik vervolgens op **Opslaan als concept**.</span><span class="sxs-lookup"><span data-stu-id="b371d-136">Then click **Save as draft**.</span></span>

12. <span data-ttu-id="b371d-137">Navigeer naar de [portal voor app-registratie](http://apps.dev.microsoft.com) en meld u aan.</span><span class="sxs-lookup"><span data-stu-id="b371d-137">Navigate to the [Application Registration Portal](http://apps.dev.microsoft.com) and log in.</span></span>

13. <span data-ttu-id="b371d-138">Klik op de naam van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="b371d-138">Click on your application name.</span></span> <span data-ttu-id="b371d-139">Noteer het wachtwoord voor het **Toepassingsgeheim** en de **Beveiligings-id (SID) pakket** die zich in de platforminstellingen van de **Windows Store** bevindt.</span><span class="sxs-lookup"><span data-stu-id="b371d-139">Make a note of the **Application Secret** password and the **Package security identifier (SID)** located in the **Windows Store** platform settings.</span></span>

     > [AZURE.WARNING]
    <span data-ttu-id="b371d-140">Het toepassingsgeheim en de pakket-SID zijn belangrijke beveiligingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="b371d-140">The application secret and package SID are important security credentials.</span></span> <span data-ttu-id="b371d-141">Deel deze waarden met niemand en distribueer ze niet met uw app.</span><span class="sxs-lookup"><span data-stu-id="b371d-141">Do not share these values with anyone or distribute them with your app.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="b371d-142">Uw Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="b371d-142">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="b371d-143">Selecteer de optie <b>Meldingsservices</b> en de optie <b>Windows (WNS)</b>.</span><span class="sxs-lookup"><span data-stu-id="b371d-143">Select the <b>Notification Services</b> option and the <b>Windows (WNS)</b> option.</span></span> <span data-ttu-id="b371d-144">Voer vervolgens het wachtwoord voor het <b>Toepassingsgeheim</b> in het veld <b>Beveiligingssleutel</b> in.</span><span class="sxs-lookup"><span data-stu-id="b371d-144">Then enter the <b>Application secret</b> password in the <b>Security Key</b> field.</span></span> <span data-ttu-id="b371d-145">Voer de waarde voor uw <b>Pakket-SID</b> in die u in het vorige gedeelte van WNS hebt gekregen en klik op <b>Opslaan</b>.</span><span class="sxs-lookup"><span data-stu-id="b371d-145">Enter your <b>Package SID</b> value that you obtained from WNS in the previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

<span data-ttu-id="b371d-146">De Notification Hub is nu geconfigureerd om te werken met WNS en u hebt de verbindingsreeksen om uw app te registreren en meldingen te verzenden.</span><span class="sxs-lookup"><span data-stu-id="b371d-146">Your notification hub is now configured to work with WNS, and you have the connection strings to register your app and send notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="b371d-147">Uw app verbinden met de Notification Hub</span><span class="sxs-lookup"><span data-stu-id="b371d-147">Connect your app to the notification hub</span></span>
1. <span data-ttu-id="b371d-148">Klik met de rechtermuisknop op de oplossing in Visual Studio en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="b371d-148">In Visual Studio, right-click the solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="b371d-149">Hierop wordt het dialoogvenster **NuGet-pakketten beheren** weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b371d-149">This displays the **Manage NuGet Packages** dialog box.</span></span>
2. <span data-ttu-id="b371d-150">Zoek `WindowsAzure.Messaging.Managed` en klik op **Installeren**. Accepteer vervolgens de gebruiksvoorwaarden.</span><span class="sxs-lookup"><span data-stu-id="b371d-150">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and accept the terms of use.</span></span>
   
    ![][20]
   
    <span data-ttu-id="b371d-151">Hiermee wordt een verwijzing gedownload, geïnstalleerd en toegevoegd aan de Azure Messaging-bibliotheek voor Windows met het <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet-pakket</a>.</span><span class="sxs-lookup"><span data-stu-id="b371d-151">This downloads, installs, and adds a reference to the Azure Messaging library for Windows by using the <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
3. <span data-ttu-id="b371d-152">Open het projectbestand App.xaml.cs en voeg de volgende `using`-instructies toe.</span><span class="sxs-lookup"><span data-stu-id="b371d-152">Open the App.xaml.cs project file and add the following `using` statements.</span></span> 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. <span data-ttu-id="b371d-153">Voeg in App.xaml.cs ook de volgende **InitNotificationsAsync**-methodedefinitie toe aan de klasse **App**:</span><span class="sxs-lookup"><span data-stu-id="b371d-153">Also in App.xaml.cs, add the following **InitNotificationsAsync** method definition to the **App** class:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    <span data-ttu-id="b371d-154">Met deze code wordt de kanaal-URI voor de app opgehaald uit WNS en wordt vervolgens die kanaal-URI voor uw Notification Hub geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="b371d-154">This code retrieves the channel URI for the app from WNS, and then registers that channel URI with your notification hub.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b371d-155">Vervang de tijdelijke aanduiding voor uw hubnaam door de naam van de Notification Hub die wordt weergegeven in Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b371d-155">Make sure to replace the "your hub name" placeholder with the name of the notification hub that appears in the Azure Portal.</span></span> <span data-ttu-id="b371d-156">Vervang ook de tijdelijke plaatsaanduiding voor de verbindingstekenreeks door de **DefaultListenSharedAccessSignature**-verbindingstekenreeks die u in een eerder gedeelte hebt gekregen op de pagina **Toegangsbeleid** van uw Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="b371d-156">Also replace the connection string placeholder with the **DefaultListenSharedAccessSignature** connection string that you obtained from the **Access Polices** page of your Notification Hub in a previous section.</span></span>
   > 
   > 
5. <span data-ttu-id="b371d-157">Aan de bovenkant van de gebeurtenis-handler **OnLaunched** in App.xaml.cs voegt u de volgende aanroep toe aan de nieuwe **InitNotificationsAsync**-methode:</span><span class="sxs-lookup"><span data-stu-id="b371d-157">At the top of the **OnLaunched** event handler in App.xaml.cs, add the following call to the new **InitNotificationsAsync** method:</span></span>
   
        InitNotificationsAsync();
   
    <span data-ttu-id="b371d-158">Hiermee wordt gegarandeerd dat de kanaal-URI in uw Notification Hub wordt geregistreerd telkens wanneer de toepassing wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="b371d-158">This guarantees that the channel URI is registered in your notification hub each time the application is launched.</span></span>
6. <span data-ttu-id="b371d-159">Druk op de toets **F5** om de app uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="b371d-159">Press the **F5** key to run the app.</span></span> <span data-ttu-id="b371d-160">Er wordt een pop-upvenster met de registratiesleutel weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b371d-160">A pop-up dialog that contains the registration key is displayed.</span></span>

<span data-ttu-id="b371d-161">Uw app is nu gereed om pop-upmeldingen te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="b371d-161">Your app is now ready to receive toast notifications.</span></span>

## <a name="send-notifications"></a><span data-ttu-id="b371d-162">Meldingen verzenden</span><span class="sxs-lookup"><span data-stu-id="b371d-162">Send notifications</span></span>
<span data-ttu-id="b371d-163">U kunt de ontvangst van meldingen in uw app snel testen door in [Azure Portal](https://portal.azure.com/) meldingen te verzenden met behulp van de knop **Test Send** (Verzenden testen) op de Notification Hub, zoals in het volgende scherm wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b371d-163">You can quickly test receiving notifications in your app by sending notifications in the [Azure Portal](https://portal.azure.com/) using the **Test Send** button on the notification hub, as shown in the screen below.</span></span>

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

<span data-ttu-id="b371d-164">Pushmeldingen worden gewoonlijk in een back-endservice zoals Mobile Services of ASP.NET verzonden met een compatibele bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="b371d-164">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="b371d-165">U kunt de REST API ook direct gebruiken om meldingsberichten te verzenden als er geen bibliotheek beschikbaar is voor uw back-end.</span><span class="sxs-lookup"><span data-stu-id="b371d-165">You can also use the REST API directly to send notification messages if a library is not available for your back-end.</span></span> 

<span data-ttu-id="b371d-166">In deze zelfstudie houden we het eenvoudig en wordt alleen gedemonstreerd hoe u uw clientapp test door meldingen te verzenden met de .NET SDK voor Notification Hubs in een consoletoepassing in plaats van een back-endservice.</span><span class="sxs-lookup"><span data-stu-id="b371d-166">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="b371d-167">U kunt het beste de zelfstudie [Notification Hubs gebruiken om pushmeldingen naar gebruikers te verzenden] doornemen voor informatie over het verzenden van meldingen vanuit een ASP.NET-back-end.</span><span class="sxs-lookup"><span data-stu-id="b371d-167">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="b371d-168">Voor het verzenden van meldingen kunt u echter de volgende methoden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b371d-168">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="b371d-169">**REST-interface**: u kunt meldingen op elk back-endplatform ondersteunen met de [REST-interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="b371d-169">**REST Interface**:  You can support notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="b371d-170">**Microsoft Azure Notification Hubs .NET SDK**: in NuGet Package Manager voor Visual Studio voert u [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) uit.</span><span class="sxs-lookup"><span data-stu-id="b371d-170">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="b371d-171">**Node.js**: [Notification Hubs gebruiken vanuit Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="b371d-171">**Node.js** : [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="b371d-172">**Azure Mobile Apps**: zie [Pushmeldingen toevoegen voor mobiele apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) voor een voorbeeld van hoe u meldingen verzendt vanuit een Azure Mobile App die is geïntegreerd met Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="b371d-172">**Azure Mobile Apps**: For an example of how to send notifications from an Azure Mobile App that's integrated with Notification Hubs, see [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="b371d-173">**Java/PHP**: zie 'Notification Hubs gebruiken vanuit Java/PHP' voor een voorbeeld van hoe u meldingen verzendt met de REST API's ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="b371d-173">**Java / PHP**: For an example of how to send notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-console-app"></a><span data-ttu-id="b371d-174">(Optioneel) Meldingen verzenden vanuit een console-app</span><span class="sxs-lookup"><span data-stu-id="b371d-174">(Optional) Send notifications from a console app</span></span>
<span data-ttu-id="b371d-175">Als u meldingen wilt verzenden met een .NET-consoletoepassing, voert u de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="b371d-175">To send notifications by using a .NET console application follow these steps.</span></span> 

1. <span data-ttu-id="b371d-176">Klik met de rechtermuisknop op de oplossing, selecteer **Toevoegen** en **Nieuw project**. Klik vervolgens onder **Visual C#** op **Windows** en **Consoletoepassing** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b371d-176">Right-click the solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
    <span data-ttu-id="b371d-177">Hiermee voegt u een nieuwe Visual C#-consoletoepassing toe aan de oplossing.</span><span class="sxs-lookup"><span data-stu-id="b371d-177">This adds a new Visual C# console application to the solution.</span></span> <span data-ttu-id="b371d-178">U kunt dit ook in een afzonderlijke oplossing doen.</span><span class="sxs-lookup"><span data-stu-id="b371d-178">You can also do this in a separate solution.</span></span>

2. <span data-ttu-id="b371d-179">Klik in Visual Studio achtereenvolgens op **Extra**, **NuGet Package Manager** en **Package Manager-console**.</span><span class="sxs-lookup"><span data-stu-id="b371d-179">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="b371d-180">Hiermee wordt de Package Manager-console in Visual Studio weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b371d-180">This displays the Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="b371d-181">Stel in het venster Package Manager-console het **standaardproject** in op uw nieuwe consoletoepassingsproject en voer vervolgens in het consolevenster de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="b371d-181">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="b371d-182">Hiermee wordt een verwijzing toegevoegd aan de Azure Notification Hubs SDK met het <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet-pakket</a>.</span><span class="sxs-lookup"><span data-stu-id="b371d-182">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="b371d-183">Open het bestand Program.cs en voeg de volgende `using`-instructie toe:</span><span class="sxs-lookup"><span data-stu-id="b371d-183">Open the Program.cs file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="b371d-184">Voeg in de klasse **Program** de volgende methode toe:</span><span class="sxs-lookup"><span data-stu-id="b371d-184">In the **Program** class, add the following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure to replace the "hub name" placeholder with the name of the notification hub that as it appears in the Azure Portal. Also, replace the connection string placeholder with the **DefaultFullSharedAccessSignature** connection string that you obtained from the **Access Policies** page of your Notification Hub in the section called "Configure your notification hub."
   
   > [!NOTE]
   > <span data-ttu-id="b371d-185">Zorg ervoor dat u de verbindingsreeks met het toegangsrecht **Full** (Volledig) gebruikt, dus niet **Listen** (Luisteren).</span><span class="sxs-lookup"><span data-stu-id="b371d-185">Make sure that you use the connection string that has **Full** access, not **Listen** access.</span></span> <span data-ttu-id="b371d-186">Met een verbindingsreeks met het toegangsrecht Luisteren kunnen geen meldingen worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="b371d-186">The listen-access string does not have permissions to send notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="b371d-187">Voeg de volgende regels in de **Main**-methode toe:</span><span class="sxs-lookup"><span data-stu-id="b371d-187">Add the following lines in the **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="b371d-188">Klik met de rechtermuisknop op het consoletoepassingsproject in Visual Studio en klik op **Instellen als opstartproject** om het project als opstartproject in te stellen.</span><span class="sxs-lookup"><span data-stu-id="b371d-188">Right-click the console application project in Visual Studio, and click **Set as StartUp Project** to set it as the startup project.</span></span> <span data-ttu-id="b371d-189">Druk vervolgens op de toets **F5** om de toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="b371d-189">Then press the **F5** key to run the application.</span></span>
   
    <span data-ttu-id="b371d-190">U ontvangt een pop-upmelding op alle geregistreerde apparaten.</span><span class="sxs-lookup"><span data-stu-id="b371d-190">You will receive a toast notification on all registered devices.</span></span> <span data-ttu-id="b371d-191">Als u op de banner van de pop-up klikt of tikt, wordt de app geladen.</span><span class="sxs-lookup"><span data-stu-id="b371d-191">Clicking or tapping the toast banner loads the app.</span></span>

<span data-ttu-id="b371d-192">U vindt alle ondersteunde nettoladingen in de onderwerpen [pop-upcatalogus], [tegelcatalogus] en [badge-overzicht] op MSDN.</span><span class="sxs-lookup"><span data-stu-id="b371d-192">You can find all the supported payloads in the [toast catalog], [tile catalog], and [badge overview] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b371d-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b371d-193">Next steps</span></span>
<span data-ttu-id="b371d-194">In dit eenvoudige voorbeeld hebt u meldingen uitgezonden naar al uw Windows-apparaten via de portal of een console-app.</span><span class="sxs-lookup"><span data-stu-id="b371d-194">In this simple example, you sent broadcast notifications to all your Windows devices using the portal or a console app.</span></span> <span data-ttu-id="b371d-195">U kunt het beste de zelfstudie [Notification Hubs gebruiken om pushmeldingen naar gebruikers te verzenden] doornemen.</span><span class="sxs-lookup"><span data-stu-id="b371d-195">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span></span> <span data-ttu-id="b371d-196">Hierin ziet u hoe u meldingen van een ASP.NET-back-end verzendt met tags voor specifieke gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b371d-196">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span></span>

<span data-ttu-id="b371d-197">Zie [Notification Hubs gebruiken om belangrijk nieuws te verzenden] als u gebruikers wilt indelen op belangengroepen.</span><span class="sxs-lookup"><span data-stu-id="b371d-197">If you want to segment your users by interest groups, see [Use Notification Hubs to send breaking news].</span></span> 

<span data-ttu-id="b371d-198">Zie [Notification Hubs Guidance](notification-hubs-push-notification-overview.md) (Richtlijnen voor Notification Hubs) voor meer algemene informatie over Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="b371d-198">To learn more general information about Notification Hubs, see [Notification Hubs Guidance](notification-hubs-push-notification-overview.md).</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

<span data-ttu-id="b371d-199">[Notification Hubs gebruiken om pushmeldingen naar gebruikers te verzenden]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="b371d-199">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
<span data-ttu-id="b371d-200">[Notification Hubs gebruiken om belangrijk nieuws te verzenden]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="b371d-200">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>

<span data-ttu-id="b371d-201">[pop-upcatalogus]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx</span><span class="sxs-lookup"><span data-stu-id="b371d-201">[toast catalog]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx</span></span>
<span data-ttu-id="b371d-202">[tegelcatalogus]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx</span><span class="sxs-lookup"><span data-stu-id="b371d-202">[tile catalog]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx</span></span>
<span data-ttu-id="b371d-203">[badge-overzicht]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx</span><span class="sxs-lookup"><span data-stu-id="b371d-203">[badge overview]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx</span></span>
