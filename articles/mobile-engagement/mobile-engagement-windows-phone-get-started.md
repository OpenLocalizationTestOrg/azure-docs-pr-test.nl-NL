---
title: Aan de slag met Azure Mobile Engagement voor Windows Phone Silverlight-apps
description: Informatie over het gebruik van Azure Mobile Engagement met analyses en pushmeldingen voor Windows Phone Silverlight-apps.
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: aa34692f-87f7-47c6-a20c-a1972750bc25
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d2334a59d83c90bdd02c4fa29261d36aad292892
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a><span data-ttu-id="526c4-103">Aan de slag met Azure Mobile Engagement voor Windows Phone Silverlight-apps</span><span class="sxs-lookup"><span data-stu-id="526c4-103">Get started with Azure Mobile Engagement for Windows Phone Silverlight apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="526c4-104">In dit onderwerp leest u hoe u Azure Mobile Engagement gebruikt om inzicht te krijgen in het gebruik van uw apps, en om pushmeldingen te verzenden aan gesegmenteerde gebruikers van een Windows Phone Silverlight-toepassing.</span><span class="sxs-lookup"><span data-stu-id="526c4-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users of a Windows Phone Silverlight application.</span></span>
<span data-ttu-id="526c4-105">Deze zelfstudie laat een eenvoudig broadcast-scenario met Mobile Engagement zien.</span><span class="sxs-lookup"><span data-stu-id="526c4-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="526c4-106">In deze zelfstudie maakt u een lege Windows Phone Silverlight-app die basisgegevens verzamelt en pushmeldingen ontvangt via Microsoft Push Notification Service (MPNS).</span><span class="sxs-lookup"><span data-stu-id="526c4-106">In it, you create a blank Windows Phone Silverlight app that collects basic data and receives push notifications using Microsoft Push Notification Service (MPNS).</span></span>

> [!NOTE]
> <span data-ttu-id="526c4-107">De Azure Mobile Engagement-service wordt in maart 2018 beëindigd en is momenteel alleen beschikbaar voor bestaande klanten.</span><span class="sxs-lookup"><span data-stu-id="526c4-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="526c4-108">Zie [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="526c4-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

> [!NOTE]
> <span data-ttu-id="526c4-109">Projecten met Windows Phone 8.1 en een eerdere versie worden niet ondersteund in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="526c4-109">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="526c4-110">Zie [Geschikte platforms voor Visual Studio 2017 en compatibiliteit](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="526c4-110">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="526c4-111">Als u ontwikkelt voor Windows Phone 8.1 (zonder Silverlight), raadpleegt u de [universele Windows-zelfstudie](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="526c4-111">If you are targeting Windows Phone 8.1 (non-Silverlight), refer to the [Windows Universal tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>
> 
> 

<span data-ttu-id="526c4-112">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="526c4-112">This tutorial requires the following:</span></span>

* <span data-ttu-id="526c4-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="526c4-113">Visual Studio 2013</span></span>
* <span data-ttu-id="526c4-114">NuGet-pakket van [MicrosoftAzure.MobileEngagement]</span><span class="sxs-lookup"><span data-stu-id="526c4-114">[MicrosoftAzure.MobileEngagement] Nuget package</span></span>

> [!NOTE]
> <span data-ttu-id="526c4-115">U hebt een actief Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="526c4-115">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="526c4-116">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="526c4-116">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="526c4-117">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="526c4-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span></span>
> 
> 

## <span data-ttu-id="526c4-118"><a id="setup-azme"></a>Mobile Engagement instellen voor uw Windows Phone-app</span><span class="sxs-lookup"><span data-stu-id="526c4-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Windows Phone app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="526c4-119"><a id="connecting-app"></a>Uw app verbinden met de back-end van Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="526c4-119"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="526c4-120">Deze zelfstudie toont een ‘basisintegratie’, de minimale set die vereist is voor het verzamelen van gegevens en verzenden van een pushmelding.</span><span class="sxs-lookup"><span data-stu-id="526c4-120">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="526c4-121">De volledige integratiedocumentatie is te vinden in de [Mobile Engagement Windows Phone SDK-integratie](mobile-engagement-windows-phone-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="526c4-121">The complete integration documentation can be found in the [Mobile Engagement Windows Phone SDK integration](mobile-engagement-windows-phone-sdk-overview.md)</span></span>

<span data-ttu-id="526c4-122">We gaan een eenvoudige app maken met Visual Studio ter illustratie van de integratie.</span><span class="sxs-lookup"><span data-stu-id="526c4-122">We will create a basic app with Visual Studio to demonstrate the integration.</span></span>

### <a name="create-a-new-windows-phone-silverlight-project"></a><span data-ttu-id="526c4-123">Een nieuw Windows Phone Silverlight-project maken</span><span class="sxs-lookup"><span data-stu-id="526c4-123">Create a new Windows Phone Silverlight project</span></span>
<span data-ttu-id="526c4-124">In de volgende stappen wordt ervan uitgegaan dat u Visual Studio 2015 gebruikt, hoewel de stappen hetzelfde zijn in eerdere versies van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="526c4-124">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="526c4-125">Start Visual Studio en selecteer **New Project** in het scherm **Home**.</span><span class="sxs-lookup"><span data-stu-id="526c4-125">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="526c4-126">Selecteer in het pop-upvenster **Windows 8** -> **Windows Phone** -> **Blank App (Windows Phone Silverlight)**.</span><span class="sxs-lookup"><span data-stu-id="526c4-126">In the pop-up, select **Windows 8** -> **Windows Phone** -> **Blank App (Windows Phone Silverlight)**.</span></span> <span data-ttu-id="526c4-127">Vul de velden **Name** en **Solution name** in voor de app en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="526c4-127">Fill in the app **Name** and **Solution name**, and then click **OK**.</span></span>
   
    ![][1]
3. <span data-ttu-id="526c4-128">U kunt **Windows Phone 8.0** of **Windows Phone 8.1** als doel kiezen.</span><span class="sxs-lookup"><span data-stu-id="526c4-128">You can choose to target either **Windows Phone 8.0** or **Windows Phone 8.1**.</span></span>

<span data-ttu-id="526c4-129">U hebt nu een nieuwe Windows Phone Silverlight-app gemaakt waarin de Azure Mobile Engagement SDK is geïntegreerd.</span><span class="sxs-lookup"><span data-stu-id="526c4-129">You have now created a new Windows Phone Silverlight app into which we will integrate the Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="526c4-130">Uw app verbinden met de back-end van Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="526c4-130">Connect your app to the Mobile Engagement backend</span></span>
1. <span data-ttu-id="526c4-131">Installeer het NuGet-pakket van [MicrosoftAzure.MobileEngagement] in het project.</span><span class="sxs-lookup"><span data-stu-id="526c4-131">Install the [MicrosoftAzure.MobileEngagement] nuget package in your project.</span></span>
2. <span data-ttu-id="526c4-132">Open `WMAppManifest.xml` (onder de map Eigenschappen) en zorg ervoor dat het volgende is gedeclareerd (voeg items toe als dat niet het geval is) in de tag `<Capabilities />`:</span><span class="sxs-lookup"><span data-stu-id="526c4-132">Open `WMAppManifest.xml` (under the Properties folder) and make sure the following are declared (add them if they are not) in the `<Capabilities />` tag:</span></span>
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. <span data-ttu-id="526c4-133">Plak nu de verbindingsreeks die u eerder hebt gekopieerd voor uw Mobile Engagement-app in het bestand `Resources\EngagementConfiguration.xml`, tussen de tags `<connectionString>` en `</connectionString>`:</span><span class="sxs-lookup"><span data-stu-id="526c4-133">Now paste the connection string that you copied earlier for your Mobile Engagement app and paste it in the `Resources\EngagementConfiguration.xml` file, between the `<connectionString>` and `</connectionString>` tags:</span></span>
   
    ![][3]
4. <span data-ttu-id="526c4-134">In het bestand `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="526c4-134">In the `App.xaml.cs` file:</span></span>
   
    <span data-ttu-id="526c4-135">a.</span><span class="sxs-lookup"><span data-stu-id="526c4-135">a.</span></span> <span data-ttu-id="526c4-136">Voeg de instructie `using` toe:</span><span class="sxs-lookup"><span data-stu-id="526c4-136">Add the `using` statement:</span></span>
   
            using Microsoft.Azure.Engagement;
   
    <span data-ttu-id="526c4-137">b.</span><span class="sxs-lookup"><span data-stu-id="526c4-137">b.</span></span> <span data-ttu-id="526c4-138">Initialiseer de SDK in de methode `Application_Launching`:</span><span class="sxs-lookup"><span data-stu-id="526c4-138">Initialize the SDK in the `Application_Launching` method:</span></span>
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    <span data-ttu-id="526c4-139">c.</span><span class="sxs-lookup"><span data-stu-id="526c4-139">c.</span></span> <span data-ttu-id="526c4-140">Voeg het volgende toe in de `Application_Activated`:</span><span class="sxs-lookup"><span data-stu-id="526c4-140">Insert the following in the `Application_Activated`:</span></span>
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <span data-ttu-id="526c4-141"><a id="monitor"></a>Realtime-bewaking inschakelen</span><span class="sxs-lookup"><span data-stu-id="526c4-141"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="526c4-142">U dient ten minste één scherm (activiteit) naar de back-end van Mobile Engagement te sturen om te beginnen met het verzenden van gegevens en ervoor te zorgen dat de gebruikers actief zijn.</span><span class="sxs-lookup"><span data-stu-id="526c4-142">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="526c4-143">Voeg in MainPage.xaml.cs de instructie `using` toe:</span><span class="sxs-lookup"><span data-stu-id="526c4-143">In the MainPage.xaml.cs, add the `using` statement:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="526c4-144">Vervang de basisklasse van **MainPage**, die zich voor **PhoneApplicationPage** bevindt, door **EngagementPage**.</span><span class="sxs-lookup"><span data-stu-id="526c4-144">Replace the base class of **MainPage**, which is before **PhoneApplicationPage**, with **EngagementPage**.</span></span>
   
        class MainPage : EngagementPage 
3. <span data-ttu-id="526c4-145">In uw bestand `MainPage.xml`:</span><span class="sxs-lookup"><span data-stu-id="526c4-145">In your `MainPage.xml` file:</span></span>
   
    <span data-ttu-id="526c4-146">a.</span><span class="sxs-lookup"><span data-stu-id="526c4-146">a.</span></span> <span data-ttu-id="526c4-147">Toevoegen aan de naamruimtedeclaraties:</span><span class="sxs-lookup"><span data-stu-id="526c4-147">Add to your namespaces declarations:</span></span>
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    <span data-ttu-id="526c4-148">b.</span><span class="sxs-lookup"><span data-stu-id="526c4-148">b.</span></span> <span data-ttu-id="526c4-149">Vervang `phone:PhoneApplicationPage` in de XML-tagnaam met `engagement:EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="526c4-149">Replace `phone:PhoneApplicationPage` in the XML tag name with `engagement:EngagementPage`.</span></span>

## <span data-ttu-id="526c4-150"><a id="monitor"></a>App verbinden met realtime-bewaking</span><span class="sxs-lookup"><span data-stu-id="526c4-150"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="526c4-151"><a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen</span><span class="sxs-lookup"><span data-stu-id="526c4-151"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="526c4-152">Met Mobile Engagement kunt u communiceren met uw gebruikers en ze bereiken met pushmeldingen en in-app-berichten in de context van campagnes.</span><span class="sxs-lookup"><span data-stu-id="526c4-152">Mobile Engagement allows you to interact and reach your users with Push Notifications and in-app Messaging in the context of campaigns.</span></span> <span data-ttu-id="526c4-153">Deze module heet REACH in de Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="526c4-153">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="526c4-154">In de volgende secties stelt u de app in om die te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="526c4-154">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-mpns-push-notifications"></a><span data-ttu-id="526c4-155">Ontvangen van MPNS-pushmeldingen inschakelen voor de app</span><span class="sxs-lookup"><span data-stu-id="526c4-155">Enable your app to receive MPNS Push Notifications</span></span>
<span data-ttu-id="526c4-156">Nieuwe mogelijkheden toevoegen aan uw bestand `WMAppManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="526c4-156">Add new Capabilities to your `WMAppManifest.xml` file:</span></span>

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-the-reach-sdk"></a><span data-ttu-id="526c4-157">Initialiseer de REACH-SDK.</span><span class="sxs-lookup"><span data-stu-id="526c4-157">Initialize the REACH SDK</span></span>
1. <span data-ttu-id="526c4-158">Roep in `App.xaml.cs` `EngagementReach.Instance.Init();` aan in de functie **Application_Launching**, meteen na de initialisatie van de agent:</span><span class="sxs-lookup"><span data-stu-id="526c4-158">In `App.xaml.cs`, call `EngagementReach.Instance.Init();` in the **Application_Launching** function, right after the agent initialization:</span></span>
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. <span data-ttu-id="526c4-159">Roep in `App.xaml.cs` `EngagementReach.Instance.OnActivated(e);` aan in de functie **Application_Activated**, meteen na de initialisatie van de agent:</span><span class="sxs-lookup"><span data-stu-id="526c4-159">In `App.xaml.cs`, call `EngagementReach.Instance.OnActivated(e);` in the **Application_Activated** function, right after the agent initialization:</span></span>
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

<span data-ttu-id="526c4-160">U bent nu klaar.</span><span class="sxs-lookup"><span data-stu-id="526c4-160">You're all set.</span></span> <span data-ttu-id="526c4-161">Nu controleren we of u hebt deze basisintegratie juist hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="526c4-161">Now we will verify that you have correctly cried out this basic integration.</span></span>

## <span data-ttu-id="526c4-162"><a id="send"></a>Een melding verzenden naar uw app</span><span class="sxs-lookup"><span data-stu-id="526c4-162"><a id="send"></a>Send a notification to your app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="526c4-163">Er moet nu een melding op uw apparaat worden weergegeven, als een in-app-melding indien de app is geopend, of anders als een toast-melding zoals in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="526c4-163">You should now see a notification on your device which will show up as an in-app notification if the app is open otherwise as a toast notification like the following:</span></span> 

![][6]

<!-- URLs. -->
<span data-ttu-id="526c4-164">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664</span><span class="sxs-lookup"><span data-stu-id="526c4-164">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664</span></span>
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
