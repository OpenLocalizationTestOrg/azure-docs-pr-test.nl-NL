---
title: aaaGet de slag met Azure Notification Hubs voor universele Windows-Platform-Apps | Microsoft Docs
description: In deze zelfstudie leert u hoe toouse Azure Notification Hubs toopush meldingen tooa universele Windows-Platform-toepassing.
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
ms.openlocfilehash: 11056842d205522ed493dc61c76ecf78ebb5a363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a><span data-ttu-id="6d887-103">Aan de slag met Notification Hubs voor Windows Universal Platform-apps</span><span class="sxs-lookup"><span data-stu-id="6d887-103">Getting started with Notification Hubs for Windows Universal Platform Apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="6d887-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="6d887-104">Overview</span></span>
<span data-ttu-id="6d887-105">Deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooa Universal Windows Platform (UWP)-app.</span><span class="sxs-lookup"><span data-stu-id="6d887-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Universal Windows Platform (UWP) app.</span></span>

<span data-ttu-id="6d887-106">In deze zelfstudie maakt u een lege Windows Store-app die pushmeldingen ontvangt via Hallo Windows Push Notification Service (WNS).</span><span class="sxs-lookup"><span data-stu-id="6d887-106">In this tutorial, you create a blank Windows Store app that receives push notifications by using hello Windows Push Notification Service (WNS).</span></span> <span data-ttu-id="6d887-107">Wanneer u klaar bent, moet u kunnen toouse push uw notification hub toobroadcast meldingen tooall Hallo apparaten waarop uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6d887-107">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6d887-108">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="6d887-108">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="6d887-109">Hallo voltooid code voor deze zelfstudie kunt u vinden op GitHub [hier](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span><span class="sxs-lookup"><span data-stu-id="6d887-109">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d887-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6d887-110">Prerequisites</span></span>
<span data-ttu-id="6d887-111">Deze zelfstudie vereist de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="6d887-111">This tutorial requires hello following:</span></span>

* <span data-ttu-id="6d887-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) of later</span><span class="sxs-lookup"><span data-stu-id="6d887-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) or later</span></span>
* [<span data-ttu-id="6d887-113">Universal Windows App Development Tools geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="6d887-113">Universal Windows App Development Tools installed</span></span>](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* <span data-ttu-id="6d887-114">Een actief Azure-account</span><span class="sxs-lookup"><span data-stu-id="6d887-114">An active Azure account</span></span> <br/><span data-ttu-id="6d887-115">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="6d887-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6d887-116">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6d887-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span></span>
* <span data-ttu-id="6d887-117">Een actief Windows Store-account</span><span class="sxs-lookup"><span data-stu-id="6d887-117">An active Windows Store account</span></span>

<span data-ttu-id="6d887-118">Het voltooien van deze zelfstudie is een vereiste voor alle andere Notification Hubs-zelfstudies voor Windows Universal Platform-apps.</span><span class="sxs-lookup"><span data-stu-id="6d887-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Universal Platform apps.</span></span>

## <a name="register-your-app-for-hello-windows-store"></a><span data-ttu-id="6d887-119">Uw app registreren voor Hallo Windows Store</span><span class="sxs-lookup"><span data-stu-id="6d887-119">Register your app for hello Windows Store</span></span>
<span data-ttu-id="6d887-120">toosend push notifications tooUWP apps, moet u uw app toohello Windows Store koppelen.</span><span class="sxs-lookup"><span data-stu-id="6d887-120">toosend push notifications tooUWP apps, you must associate your app toohello Windows Store.</span></span> <span data-ttu-id="6d887-121">Vervolgens moet u uw notification hub toointegrate configureren met WNS.</span><span class="sxs-lookup"><span data-stu-id="6d887-121">You must then configure your notification hub toointegrate with WNS.</span></span>

1. <span data-ttu-id="6d887-122">Als u uw app nog niet hebt geregistreerd, gaat u toohello [Windows-ontwikkelaarscentrum](https://dev.windows.com/overview), meld u aan met uw Microsoft-account en klik vervolgens op **maakt een nieuwe app**.</span><span class="sxs-lookup"><span data-stu-id="6d887-122">If you have not already registered your app, navigate toohello [Windows Dev Center](https://dev.windows.com/overview), sign in with your Microsoft account, and then click **Create a new app**.</span></span>

2. <span data-ttu-id="6d887-123">Typ een naam voor uw app en klik op **App-naam reserveren**.</span><span class="sxs-lookup"><span data-stu-id="6d887-123">Type a name for your app and click **Reserve app name**.</span></span> <span data-ttu-id="6d887-124">Hiermee maakt u een nieuwe Windows Store-registratie voor uw app.</span><span class="sxs-lookup"><span data-stu-id="6d887-124">This creates a new Windows Store registration for your app.</span></span>

3. <span data-ttu-id="6d887-125">In Visual Studio kunt u een nieuw Visual C# Store-Apps-project maken met behulp van Universal Windows hello **lege App** sjabloon en klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6d887-125">In Visual Studio, create a new Visual C# Store Apps project by using hello Windows Universal **Blank App** template and click **OK**.</span></span>

4. <span data-ttu-id="6d887-126">Accepteer de standaardinstellingen Hallo voor Hallo doel en minimale platformversies.</span><span class="sxs-lookup"><span data-stu-id="6d887-126">Accept hello defaults for hello target and minimum platform versions.</span></span>

5. <span data-ttu-id="6d887-127">Klik in Solution Explorer met de rechtermuisknop op Hallo Windows Store-app-project, klikt u op **Store**, en klik vervolgens op **App aan Hallo Store koppelen...** . Hallo **uw App koppelen aan Windows Store Hallo** wizard wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6d887-127">In Solution Explorer, right-click hello Windows Store app project, click **Store**, and then click **Associate App with hello Store...**. hello **Associate Your App with hello Windows Store** wizard appears.</span></span>

6. <span data-ttu-id="6d887-128">Klik in de wizard Hallo zich aanmelden met je Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="6d887-128">In hello wizard, sign in with your Microsoft account.</span></span>

7. <span data-ttu-id="6d887-129">Klik op Hallo-app die u in stap 2 hebt geregistreerd, klikt u op **volgende**, en klik vervolgens op **koppelen**.</span><span class="sxs-lookup"><span data-stu-id="6d887-129">Click hello app that you registered in step 2, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="6d887-130">Hallo vereist Windows Store-registratie informatie toohello toepassingsmanifest wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="6d887-130">This adds hello required Windows Store registration information toohello application manifest.</span></span>

8. <span data-ttu-id="6d887-131">Terug op Hallo [Windows-ontwikkelaarscentrum](http://dev.windows.com/overview) voor uw nieuwe app pagina, klikt u op **Services**, klikt u op **Pushmeldingen**, en klik vervolgens op **WNS/MPNS**.</span><span class="sxs-lookup"><span data-stu-id="6d887-131">Back on hello [Windows Dev Center](http://dev.windows.com/overview) page for your new app, click **Services**, click **Push notifications**, and then click **WNS/MPNS**.</span></span>

9. <span data-ttu-id="6d887-132">Klik op **Nieuwe melding**.</span><span class="sxs-lookup"><span data-stu-id="6d887-132">Click **New Notification**.</span></span>

10. <span data-ttu-id="6d887-133">Klik op de sjabloon **Leeg (pop-up)** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6d887-133">Click **Blank (Toast)** template and then click **OK**.</span></span>

11. <span data-ttu-id="6d887-134">Voer een **Naam** voor de melding en een visueel **Context**bericht in.</span><span class="sxs-lookup"><span data-stu-id="6d887-134">Enter a notification **Name** and Visual **Context** message.</span></span> <span data-ttu-id="6d887-135">Klik vervolgens op **Opslaan als concept**.</span><span class="sxs-lookup"><span data-stu-id="6d887-135">Then click **Save as draft**.</span></span>

12. <span data-ttu-id="6d887-136">Navigeer toohello [Registratieportal toepassing](http://apps.dev.microsoft.com) en zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="6d887-136">Navigate toohello [Application Registration Portal](http://apps.dev.microsoft.com) and log in.</span></span>

13. <span data-ttu-id="6d887-137">Klik op de naam van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="6d887-137">Click on your application name.</span></span> <span data-ttu-id="6d887-138">Noteer Hallo **Toepassingsgeheim** wachtwoord en Hallo **pakket beveiligings-id (SID)** zich in Hallo **Windows Store** platform-instellingen.</span><span class="sxs-lookup"><span data-stu-id="6d887-138">Make a note of hello **Application Secret** password and hello **Package security identifier (SID)** located in hello **Windows Store** platform settings.</span></span>

     > [AZURE.WARNING]
    <span data-ttu-id="6d887-139">Hallo toepassingsgeheim en pakket-SID zijn belangrijke beveiligingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="6d887-139">hello application secret and package SID are important security credentials.</span></span> <span data-ttu-id="6d887-140">Deel deze waarden met niemand en distribueer ze niet met uw app.</span><span class="sxs-lookup"><span data-stu-id="6d887-140">Do not share these values with anyone or distribute them with your app.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="6d887-141">Uw Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="6d887-141">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="6d887-142">Selecteer Hallo <b>Notification Services</b> optie en Hallo <b>Windows (WNS)</b> optie.</span><span class="sxs-lookup"><span data-stu-id="6d887-142">Select hello <b>Notification Services</b> option and hello <b>Windows (WNS)</b> option.</span></span> <span data-ttu-id="6d887-143">Voer vervolgens Hallo <b>toepassingsgeheim</b> wachtwoord in Hallo <b>beveiligingssleutel</b> veld.</span><span class="sxs-lookup"><span data-stu-id="6d887-143">Then enter hello <b>Application secret</b> password in hello <b>Security Key</b> field.</span></span> <span data-ttu-id="6d887-144">Voer uw <b>pakket-SID</b> waarde die u hebt verkregen van WNS in de vorige sectie Hallo en klik vervolgens op <b>opslaan</b>.</span><span class="sxs-lookup"><span data-stu-id="6d887-144">Enter your <b>Package SID</b> value that you obtained from WNS in hello previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

<span data-ttu-id="6d887-145">Uw notification hub is nu geconfigureerd toowork met WNS en u uw app Hallo verbinding tekenreeksen tooregister hebt en meldingen te verzenden.</span><span class="sxs-lookup"><span data-stu-id="6d887-145">Your notification hub is now configured toowork with WNS, and you have hello connection strings tooregister your app and send notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="6d887-146">Verbinding maken met uw app toohello notification hub</span><span class="sxs-lookup"><span data-stu-id="6d887-146">Connect your app toohello notification hub</span></span>
1. <span data-ttu-id="6d887-147">Met de rechtermuisknop op het Hallo-oplossing in Visual Studio en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="6d887-147">In Visual Studio, right-click hello solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="6d887-148">U ziet nu Hallo **NuGet-pakketten beheren** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d887-148">This displays hello **Manage NuGet Packages** dialog box.</span></span>
2. <span data-ttu-id="6d887-149">Zoeken naar `WindowsAzure.Messaging.Managed` en klik op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="6d887-149">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and accept hello terms of use.</span></span>
   
    ![][20]
   
    <span data-ttu-id="6d887-150">Hiermee downloadt, installeert en wordt een verwijzing toohello Azure Messaging-bibliotheek voor Windows hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet-pakket</a>.</span><span class="sxs-lookup"><span data-stu-id="6d887-150">This downloads, installs, and adds a reference toohello Azure Messaging library for Windows by using hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
3. <span data-ttu-id="6d887-151">Open Hallo projectbestand App.XAML.cs en voeg de volgende Hallo `using` instructies.</span><span class="sxs-lookup"><span data-stu-id="6d887-151">Open hello App.xaml.cs project file and add hello following `using` statements.</span></span> 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. <span data-ttu-id="6d887-152">Voeg ook in App.xaml.cs Hallo volgende **InitNotificationsAsync** methode definitie toohello **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="6d887-152">Also in App.xaml.cs, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    <span data-ttu-id="6d887-153">Deze code Hallo kanaal-URI voor Hallo app opgehaald uit WNS en vervolgens die kanaal-URI voor uw notification hub geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="6d887-153">This code retrieves hello channel URI for hello app from WNS, and then registers that channel URI with your notification hub.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6d887-154">Zorg ervoor dat tooreplace 'uw hubnaam'-tijdelijke aanduiding met de naam van Hallo notification hub die wordt weergegeven in Azure Portal Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="6d887-154">Make sure tooreplace hello "your hub name" placeholder with hello name of hello notification hub that appears in hello Azure Portal.</span></span> <span data-ttu-id="6d887-155">Hallo verbinding de tijdelijke aanduiding voor ook vervangen door Hallo **DefaultListenSharedAccessSignature** verbindingsreeks die u hebt verkregen via Hallo **toegangsbeleid** pagina van de Notification Hub in een vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="6d887-155">Also replace hello connection string placeholder with hello **DefaultListenSharedAccessSignature** connection string that you obtained from hello **Access Polices** page of your Notification Hub in a previous section.</span></span>
   > 
   > 
5. <span data-ttu-id="6d887-156">Hallo boven aan het Hallo **OnLaunched** gebeurtenis-handler in App.xaml.cs toevoegen na de aanroep toohello nieuwe Hallo **InitNotificationsAsync** methode:</span><span class="sxs-lookup"><span data-stu-id="6d887-156">At hello top of hello **OnLaunched** event handler in App.xaml.cs, add hello following call toohello new **InitNotificationsAsync** method:</span></span>
   
        InitNotificationsAsync();
   
    <span data-ttu-id="6d887-157">Dit zorgt ervoor dat Hallo kanaal-URI is geregistreerd in uw notification hub die elke keer Hallo-toepassing wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="6d887-157">This guarantees that hello channel URI is registered in your notification hub each time hello application is launched.</span></span>
6. <span data-ttu-id="6d887-158">Druk op Hallo **F5** key toorun Hallo app.</span><span class="sxs-lookup"><span data-stu-id="6d887-158">Press hello **F5** key toorun hello app.</span></span> <span data-ttu-id="6d887-159">Een pop-upvenster met de registratiesleutel hello wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6d887-159">A pop-up dialog that contains hello registration key is displayed.</span></span>

<span data-ttu-id="6d887-160">Uw app is nu gereed tooreceive pop-upmeldingen.</span><span class="sxs-lookup"><span data-stu-id="6d887-160">Your app is now ready tooreceive toast notifications.</span></span>

## <a name="send-notifications"></a><span data-ttu-id="6d887-161">Meldingen verzenden</span><span class="sxs-lookup"><span data-stu-id="6d887-161">Send notifications</span></span>
<span data-ttu-id="6d887-162">U kunt snel testen ontvangst van meldingen in uw app door meldingen te verzenden in Hallo [Azure Portal](https://portal.azure.com/) Hallo met **Test verzenden** knop op Hallo notification hub, zoals wordt weergegeven in onderstaande welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="6d887-162">You can quickly test receiving notifications in your app by sending notifications in hello [Azure Portal](https://portal.azure.com/) using hello **Test Send** button on hello notification hub, as shown in hello screen below.</span></span>

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

<span data-ttu-id="6d887-163">Pushmeldingen worden gewoonlijk in een back-endservice zoals Mobile Services of ASP.NET verzonden met een compatibele bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="6d887-163">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="6d887-164">U kunt ook Hallo REST-API gebruiken direct toosend worden meldingsberichten als een bibliotheek niet beschikbaar voor uw back-end is.</span><span class="sxs-lookup"><span data-stu-id="6d887-164">You can also use hello REST API directly toosend notification messages if a library is not available for your back-end.</span></span> 

<span data-ttu-id="6d887-165">In deze zelfstudie wordt Houd het eenvoudig en alleen gedemonstreerd hoe u uw clientapp test door meldingen met behulp van Hallo .NET SDK voor notification hubs in een consoletoepassing in plaats van een back-endservice te verzenden.</span><span class="sxs-lookup"><span data-stu-id="6d887-165">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="6d887-166">We raden aan Hallo [Notification Hubs gebruiken toopush meldingen toousers] Hallo volgende stap voor het verzenden van meldingen vanuit een ASP.NET-back-end zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6d887-166">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="6d887-167">Hallo volgende methoden kan echter worden gebruikt voor het verzenden van meldingen:</span><span class="sxs-lookup"><span data-stu-id="6d887-167">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="6d887-168">**REST-Interface**: U kunt meldingen ondersteunen op elk back-end-platform Hallo met [REST-interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d887-168">**REST Interface**:  You can support notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="6d887-169">**Microsoft Azure Notification Hubs .NET SDK**: In Hallo Nuget Package Manager voor Visual Studio, voert u [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="6d887-169">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="6d887-170">**Node.js** : [hoe toouse Notification Hubs met Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="6d887-170">**Node.js** : [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="6d887-171">**Azure Mobile Apps**: voor een voorbeeld van hoe u meldingen vanuit een mobiele App van Azure die geïntegreerd met Notification Hubs toosend Zie [pushmeldingen toevoegen voor mobiele Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="6d887-171">**Azure Mobile Apps**: For an example of how toosend notifications from an Azure Mobile App that's integrated with Notification Hubs, see [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="6d887-172">**Java / PHP**: Zie voor een voorbeeld van hoe toosend meldingen met REST-API's Hallo ' hoe toouse Notification Hubs vanuit Java/PHP ' ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="6d887-172">**Java / PHP**: For an example of how toosend notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-console-app"></a><span data-ttu-id="6d887-173">(Optioneel) Meldingen verzenden vanuit een console-app</span><span class="sxs-lookup"><span data-stu-id="6d887-173">(Optional) Send notifications from a console app</span></span>
<span data-ttu-id="6d887-174">toosend meldingen met een .NET-consoletoepassing Volg deze stappen.</span><span class="sxs-lookup"><span data-stu-id="6d887-174">toosend notifications by using a .NET console application follow these steps.</span></span> 

1. <span data-ttu-id="6d887-175">Klik met de rechtermuisknop Hallo-oplossing, selecteer **toevoegen** en **nieuw Project...** , en klik vervolgens onder **Visual C#**, klikt u op **Windows** en **consoletoepassing**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6d887-175">Right-click hello solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
    <span data-ttu-id="6d887-176">Hiermee wordt een nieuwe Visual C# console toepassing toohello oplossing toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="6d887-176">This adds a new Visual C# console application toohello solution.</span></span> <span data-ttu-id="6d887-177">U kunt dit ook in een afzonderlijke oplossing doen.</span><span class="sxs-lookup"><span data-stu-id="6d887-177">You can also do this in a separate solution.</span></span>

2. <span data-ttu-id="6d887-178">Klik in Visual Studio achtereenvolgens op **Extra**, **NuGet Package Manager** en **Package Manager-console**.</span><span class="sxs-lookup"><span data-stu-id="6d887-178">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="6d887-179">Hiermee geeft Hallo Package Manager-Console in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6d887-179">This displays hello Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="6d887-180">In Hallo venster Package Manager-Console, stelt u Hallo **standaardproject** tooyour nieuwe console toepassingsproject en vervolgens in het consolevenster hello, Hallo volgende opdracht wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="6d887-180">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="6d887-181">Hiermee voegt u een verwijzing toohello Azure Notification Hubs SDK met de Hallo <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet-pakket</a>.</span><span class="sxs-lookup"><span data-stu-id="6d887-181">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="6d887-182">Open het bestand Program.cs hello en voeg de volgende Hallo `using` instructie:</span><span class="sxs-lookup"><span data-stu-id="6d887-182">Open hello Program.cs file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="6d887-183">In Hallo **programma** klasse, Hallo volgende methode toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="6d887-183">In hello **Program** class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > <span data-ttu-id="6d887-184">Zorg ervoor dat u het Hallo-verbindingsreeks die is **volledige** toegang niet **luisteren** toegang.</span><span class="sxs-lookup"><span data-stu-id="6d887-184">Make sure that you use hello connection string that has **Full** access, not **Listen** access.</span></span> <span data-ttu-id="6d887-185">Hallo toegangsrecht luisteren tekenreeks heeft geen machtigingen toosend meldingen.</span><span class="sxs-lookup"><span data-stu-id="6d887-185">hello listen-access string does not have permissions toosend notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="6d887-186">Toevoegen van de volgende regels in Hallo Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="6d887-186">Add hello following lines in hello **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="6d887-187">Met de rechtermuisknop op het Hallo-consoletoepassingsproject in Visual Studio en klik op **instellen als opstartproject** tooset als opstartproject Hallo.</span><span class="sxs-lookup"><span data-stu-id="6d887-187">Right-click hello console application project in Visual Studio, and click **Set as StartUp Project** tooset it as hello startup project.</span></span> <span data-ttu-id="6d887-188">Druk op Hallo **F5** sleutel toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6d887-188">Then press hello **F5** key toorun hello application.</span></span>
   
    <span data-ttu-id="6d887-189">U ontvangt een pop-upmelding op alle geregistreerde apparaten.</span><span class="sxs-lookup"><span data-stu-id="6d887-189">You will receive a toast notification on all registered devices.</span></span> <span data-ttu-id="6d887-190">Hallo-app, klikt of tikt Hallo toast banner wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="6d887-190">Clicking or tapping hello toast banner loads hello app.</span></span>

<span data-ttu-id="6d887-191">U vindt alle Hallo ondersteunde nettoladingen in Hallo [pop-upcatalogus], [tegelcatalogus], en [badge-overzicht] onderwerpen op MSDN.</span><span class="sxs-lookup"><span data-stu-id="6d887-191">You can find all hello supported payloads in hello [toast catalog], [tile catalog], and [badge overview] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d887-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6d887-192">Next steps</span></span>
<span data-ttu-id="6d887-193">In dit eenvoudige voorbeeld verzonden u broadcast meldingen tooall uw Windows-apparaten via Hallo portal of een console-app.</span><span class="sxs-lookup"><span data-stu-id="6d887-193">In this simple example, you sent broadcast notifications tooall your Windows devices using hello portal or a console app.</span></span> <span data-ttu-id="6d887-194">Hallo wordt aangeraden [Notification Hubs gebruiken toopush meldingen toousers] zelfstudie Hallo volgende stap.</span><span class="sxs-lookup"><span data-stu-id="6d887-194">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="6d887-195">Hierin ziet u hoe toosend meldingen vanuit een ASP.NET-back-end met tags voor specifieke gebruikers tootarget.</span><span class="sxs-lookup"><span data-stu-id="6d887-195">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="6d887-196">Als u wilt dat toosegment gebruikers op belangengroepen, raadpleegt u [Notification Hubs gebruiken toosend belangrijk nieuws].</span><span class="sxs-lookup"><span data-stu-id="6d887-196">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span> 

<span data-ttu-id="6d887-197">toolearn Zie voor meer algemene informatie over Notification Hubs [richtlijnen voor Notification Hubs](notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6d887-197">toolearn more general information about Notification Hubs, see [Notification Hubs Guidance](notification-hubs-push-notification-overview.md).</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[Notification Hubs gebruiken toopush meldingen toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Notification Hubs gebruiken toosend belangrijk nieuws]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[pop-upcatalogus]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[tegelcatalogus]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[badge-overzicht]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx
