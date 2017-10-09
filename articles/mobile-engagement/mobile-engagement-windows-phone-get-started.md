---
title: aaaGet de slag met Azure Mobile Engagement voor Windows Phone Silverlight-apps
description: Meer informatie over hoe toouse Azure Mobile Engagement met analyses en pushmeldingen voor Windows Phone Silverlight-apps.
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
ms.openlocfilehash: b39a838ab03217b2dc845cbf59d7bf8b094dac1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a><span data-ttu-id="2658b-103">Aan de slag met Azure Mobile Engagement voor Windows Phone Silverlight-apps</span><span class="sxs-lookup"><span data-stu-id="2658b-103">Get started with Azure Mobile Engagement for Windows Phone Silverlight apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="2658b-104">Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand uw app-gebruik en verzenden push notifications toosegmented gebruikers van een Windows Phone Silverlight-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2658b-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Phone Silverlight application.</span></span>
<span data-ttu-id="2658b-105">Deze zelfstudie laat zien Hallo eenvoudig broadcast-scenario met Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="2658b-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="2658b-106">In deze zelfstudie maakt u een lege Windows Phone Silverlight-app die basisgegevens verzamelt en pushmeldingen ontvangt via Microsoft Push Notification Service (MPNS).</span><span class="sxs-lookup"><span data-stu-id="2658b-106">In it, you create a blank Windows Phone Silverlight app that collects basic data and receives push notifications using Microsoft Push Notification Service (MPNS).</span></span>

> [!NOTE]
> <span data-ttu-id="2658b-107">Hallo Azure Mobile Engagement service buiten gebruik gesteld maart 2018 en is momenteel alleen beschikbaar tooexisting klanten.</span><span class="sxs-lookup"><span data-stu-id="2658b-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="2658b-108">Zie [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2658b-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

> [!NOTE]
> <span data-ttu-id="2658b-109">Projecten met Windows Phone 8.1 en een eerdere versie worden niet ondersteund in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2658b-109">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="2658b-110">Zie [Geschikte platforms voor Visual Studio 2017 en compatibiliteit](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2658b-110">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="2658b-111">Als u ontwikkelt voor Windows Phone 8.1 (zonder Silverlight), raadpleegt u toohello [universele Windows-zelfstudie](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2658b-111">If you are targeting Windows Phone 8.1 (non-Silverlight), refer toohello [Windows Universal tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>
> 
> 

<span data-ttu-id="2658b-112">Deze zelfstudie vereist de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="2658b-112">This tutorial requires hello following:</span></span>

* <span data-ttu-id="2658b-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="2658b-113">Visual Studio 2013</span></span>
* <span data-ttu-id="2658b-114">NuGet-pakket van [MicrosoftAzure.MobileEngagement]</span><span class="sxs-lookup"><span data-stu-id="2658b-114">[MicrosoftAzure.MobileEngagement] Nuget package</span></span>

> [!NOTE]
> <span data-ttu-id="2658b-115">toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="2658b-115">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="2658b-116">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="2658b-116">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2658b-117">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2658b-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span></span>
> 
> 

## <span data-ttu-id="2658b-118"><a id="setup-azme"></a>Mobile Engagement instellen voor uw Windows Phone-app</span><span class="sxs-lookup"><span data-stu-id="2658b-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Windows Phone app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="2658b-119"><a id="connecting-app"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end</span><span class="sxs-lookup"><span data-stu-id="2658b-119"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="2658b-120">Deze zelfstudie toont een 'basisintegratie', die wordt Hallo minimale vereiste toocollect gegevens instellen en een pushmelding verzenden.</span><span class="sxs-lookup"><span data-stu-id="2658b-120">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="2658b-121">de volledige integratiedocumentatie Hallo vindt u in Hallo [Mobile Engagement Windows Phone SDK-integratie](mobile-engagement-windows-phone-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2658b-121">hello complete integration documentation can be found in hello [Mobile Engagement Windows Phone SDK integration](mobile-engagement-windows-phone-sdk-overview.md)</span></span>

<span data-ttu-id="2658b-122">We gaan een eenvoudige app maken met Visual Studio toodemonstrate Hallo-integratie.</span><span class="sxs-lookup"><span data-stu-id="2658b-122">We will create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-windows-phone-silverlight-project"></a><span data-ttu-id="2658b-123">Een nieuw Windows Phone Silverlight-project maken</span><span class="sxs-lookup"><span data-stu-id="2658b-123">Create a new Windows Phone Silverlight project</span></span>
<span data-ttu-id="2658b-124">Hallo volgende stappen wordt ervan uitgegaan Hallo gebruik van Visual Studio 2015 al Hallo stappen vergelijkbaar in eerdere versies van Visual Studio zijn.</span><span class="sxs-lookup"><span data-stu-id="2658b-124">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="2658b-125">Start Visual Studio en in Hallo **Start** Schakel in het scherm **nieuw Project**.</span><span class="sxs-lookup"><span data-stu-id="2658b-125">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="2658b-126">Selecteer in het pop-upvenster Hallo **Windows 8** -> **Windows Phone** -> **lege App (Windows Phone Silverlight)**.</span><span class="sxs-lookup"><span data-stu-id="2658b-126">In hello pop-up, select **Windows 8** -> **Windows Phone** -> **Blank App (Windows Phone Silverlight)**.</span></span> <span data-ttu-id="2658b-127">Vul Hallo app **naam** en **oplossingsnaam**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2658b-127">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>
   
    ![][1]
3. <span data-ttu-id="2658b-128">U kunt tootarget ofwel **Windows Phone 8.0** of **Windows Phone 8.1**.</span><span class="sxs-lookup"><span data-stu-id="2658b-128">You can choose tootarget either **Windows Phone 8.0** or **Windows Phone 8.1**.</span></span>

<span data-ttu-id="2658b-129">U hebt nu een nieuwe Windows Phone Silverlight-app waarin we hello Azure Mobile Engagement SDK wordt integreren gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2658b-129">You have now created a new Windows Phone Silverlight app into which we will integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="2658b-130">Verbinding maken met uw app toohello Mobile Engagement-back-end</span><span class="sxs-lookup"><span data-stu-id="2658b-130">Connect your app toohello Mobile Engagement backend</span></span>
1. <span data-ttu-id="2658b-131">Hallo installeren [MicrosoftAzure.MobileEngagement] nuget-pakket in uw project.</span><span class="sxs-lookup"><span data-stu-id="2658b-131">Install hello [MicrosoftAzure.MobileEngagement] nuget package in your project.</span></span>
2. <span data-ttu-id="2658b-132">Open `WMAppManifest.xml` (onder de map Hallo-eigenschappen) en zorg ervoor dat de volgende Hallo is gedeclareerd (Voeg ze als ze niet zijn) in Hallo `<Capabilities />` tag:</span><span class="sxs-lookup"><span data-stu-id="2658b-132">Open `WMAppManifest.xml` (under hello Properties folder) and make sure hello following are declared (add them if they are not) in hello `<Capabilities />` tag:</span></span>
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. <span data-ttu-id="2658b-133">Nu Hallo verbindingsreeks die u eerder hebt gekopieerd voor uw Mobile Engagement-app te plakken en plak deze in Hallo `Resources\EngagementConfiguration.xml` bestand tussen Hallo `<connectionString>` en `</connectionString>` tags:</span><span class="sxs-lookup"><span data-stu-id="2658b-133">Now paste hello connection string that you copied earlier for your Mobile Engagement app and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>
   
    ![][3]
4. <span data-ttu-id="2658b-134">In Hallo `App.xaml.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="2658b-134">In hello `App.xaml.cs` file:</span></span>
   
    <span data-ttu-id="2658b-135">a.</span><span class="sxs-lookup"><span data-stu-id="2658b-135">a.</span></span> <span data-ttu-id="2658b-136">Hallo toevoegen `using` instructie:</span><span class="sxs-lookup"><span data-stu-id="2658b-136">Add hello `using` statement:</span></span>
   
            using Microsoft.Azure.Engagement;
   
    <span data-ttu-id="2658b-137">b.</span><span class="sxs-lookup"><span data-stu-id="2658b-137">b.</span></span> <span data-ttu-id="2658b-138">Hallo SDK in Hallo initialiseren `Application_Launching` methode:</span><span class="sxs-lookup"><span data-stu-id="2658b-138">Initialize hello SDK in hello `Application_Launching` method:</span></span>
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    <span data-ttu-id="2658b-139">c.</span><span class="sxs-lookup"><span data-stu-id="2658b-139">c.</span></span> <span data-ttu-id="2658b-140">Hallo volgende invoegen in Hallo `Application_Activated`:</span><span class="sxs-lookup"><span data-stu-id="2658b-140">Insert hello following in hello `Application_Activated`:</span></span>
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <span data-ttu-id="2658b-141"><a id="monitor"></a>Realtime-bewaking inschakelen</span><span class="sxs-lookup"><span data-stu-id="2658b-141"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="2658b-142">U moet ten minste één scherm (activiteit) toohello Mobile Engagement back-end verzenden in volgorde toostart verzenden van gegevens en ervoor te zorgen dat Hallo gebruikers actief zijn.</span><span class="sxs-lookup"><span data-stu-id="2658b-142">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="2658b-143">Voeg in MainPage.xaml.cs hello, Hallo `using` instructie:</span><span class="sxs-lookup"><span data-stu-id="2658b-143">In hello MainPage.xaml.cs, add hello `using` statement:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="2658b-144">Vervang de basisklasse Hallo van **MainPage**, die zich voor **PhoneApplicationPage**, met **EngagementPage**.</span><span class="sxs-lookup"><span data-stu-id="2658b-144">Replace hello base class of **MainPage**, which is before **PhoneApplicationPage**, with **EngagementPage**.</span></span>
   
        class MainPage : EngagementPage 
3. <span data-ttu-id="2658b-145">In uw bestand `MainPage.xml`:</span><span class="sxs-lookup"><span data-stu-id="2658b-145">In your `MainPage.xml` file:</span></span>
   
    <span data-ttu-id="2658b-146">a.</span><span class="sxs-lookup"><span data-stu-id="2658b-146">a.</span></span> <span data-ttu-id="2658b-147">Tooyour naamruimtedeclaraties toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2658b-147">Add tooyour namespaces declarations:</span></span>
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    <span data-ttu-id="2658b-148">b.</span><span class="sxs-lookup"><span data-stu-id="2658b-148">b.</span></span> <span data-ttu-id="2658b-149">Vervang `phone:PhoneApplicationPage` in Hallo XML-tagnaam met `engagement:EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="2658b-149">Replace `phone:PhoneApplicationPage` in hello XML tag name with `engagement:EngagementPage`.</span></span>

## <span data-ttu-id="2658b-150"><a id="monitor"></a>App verbinden met realtime-bewaking</span><span class="sxs-lookup"><span data-stu-id="2658b-150"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="2658b-151"><a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen</span><span class="sxs-lookup"><span data-stu-id="2658b-151"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="2658b-152">Mobile Engagement kunt u toointeract en uw gebruikers via Pushmeldingen en in-app-berichten in de context van campagnes Hallo bereiken.</span><span class="sxs-lookup"><span data-stu-id="2658b-152">Mobile Engagement allows you toointeract and reach your users with Push Notifications and in-app Messaging in hello context of campaigns.</span></span> <span data-ttu-id="2658b-153">Deze module heet REACH in Hallo Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="2658b-153">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="2658b-154">Hallo volgende secties stelt u uw app tooreceive ze.</span><span class="sxs-lookup"><span data-stu-id="2658b-154">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-mpns-push-notifications"></a><span data-ttu-id="2658b-155">Uw app tooreceive MPNS-Pushmeldingen inschakelen</span><span class="sxs-lookup"><span data-stu-id="2658b-155">Enable your app tooreceive MPNS Push Notifications</span></span>
<span data-ttu-id="2658b-156">Toevoegen van nieuwe mogelijkheden tooyour `WMAppManifest.xml` bestand:</span><span class="sxs-lookup"><span data-stu-id="2658b-156">Add new Capabilities tooyour `WMAppManifest.xml` file:</span></span>

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="2658b-157">Hallo bereiken SDK initialiseren</span><span class="sxs-lookup"><span data-stu-id="2658b-157">Initialize hello REACH SDK</span></span>
1. <span data-ttu-id="2658b-158">In `App.xaml.cs`, roepen `EngagementReach.Instance.Init();` in Hallo **Application_Launching** functie, meteen na de initialisatie van de agent Hallo:</span><span class="sxs-lookup"><span data-stu-id="2658b-158">In `App.xaml.cs`, call `EngagementReach.Instance.Init();` in hello **Application_Launching** function, right after hello agent initialization:</span></span>
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. <span data-ttu-id="2658b-159">In `App.xaml.cs`, roepen `EngagementReach.Instance.OnActivated(e);` in Hallo **Application_Activated** functie, meteen na de initialisatie van de agent Hallo:</span><span class="sxs-lookup"><span data-stu-id="2658b-159">In `App.xaml.cs`, call `EngagementReach.Instance.OnActivated(e);` in hello **Application_Activated** function, right after hello agent initialization:</span></span>
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

<span data-ttu-id="2658b-160">U bent nu klaar.</span><span class="sxs-lookup"><span data-stu-id="2658b-160">You're all set.</span></span> <span data-ttu-id="2658b-161">Nu controleren we of u hebt deze basisintegratie juist hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2658b-161">Now we will verify that you have correctly cried out this basic integration.</span></span>

## <span data-ttu-id="2658b-162"><a id="send"></a>Een melding tooyour app verzenden</span><span class="sxs-lookup"><span data-stu-id="2658b-162"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="2658b-163">U ziet nu een melding op uw apparaat worden weergegeven als een in-app-melding indien Hallo app geopend of anders als een toast-melding zoals Hallo volgende is:</span><span class="sxs-lookup"><span data-stu-id="2658b-163">You should now see a notification on your device which will show up as an in-app notification if hello app is open otherwise as a toast notification like hello following:</span></span> 

![][6]

<!-- URLs. -->
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
