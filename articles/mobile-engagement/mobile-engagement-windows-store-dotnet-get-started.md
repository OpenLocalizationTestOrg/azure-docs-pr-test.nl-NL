---
title: aaaGet gestart met Windows universele Apps in Azure Mobile Engagement
description: Meer informatie over hoe toouse Azure Mobile Engagement met analyses en pushmeldingen voor universele Windows-Apps.
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a><span data-ttu-id="a740a-103">Aan de slag met Azure Mobile Engagement voor universele Windows-apps</span><span class="sxs-lookup"><span data-stu-id="a740a-103">Get started with Azure Mobile Engagement for Windows Universal Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="a740a-104">Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand uw app-gebruik en verzenden push notifications toosegmented gebruikers van een universele Windows-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a740a-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Universal application.</span></span>
<span data-ttu-id="a740a-105">Deze zelfstudie laat zien Hallo eenvoudig broadcast-scenario met Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a740a-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="a740a-106">In deze zelfstudie maakt u een lege universele Windows-app die basisgegevens verzamelt en pushmeldingen ontvangt via Windows Notification Service (WNS).</span><span class="sxs-lookup"><span data-stu-id="a740a-106">You create a blank Windows Universal App that collects basic app usage data and receives push notifications using Windows Notification Service (WNS).</span></span>

> [!NOTE]
> <span data-ttu-id="a740a-107">Hallo Azure Mobile Engagement service buiten gebruik gesteld maart 2018 en is momenteel alleen beschikbaar tooexisting klanten.</span><span class="sxs-lookup"><span data-stu-id="a740a-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="a740a-108">Zie [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a740a-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a740a-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a740a-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a><span data-ttu-id="a740a-110">Mobile Engagement instellen voor uw universele Windows-app</span><span class="sxs-lookup"><span data-stu-id="a740a-110">Set up Mobile Engagement for your Windows Universal app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="a740a-111"><a id="connecting-app"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end</span><span class="sxs-lookup"><span data-stu-id="a740a-111"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="a740a-112">Deze zelfstudie toont een 'basisintegratie', die wordt Hallo minimale vereiste toocollect gegevens instellen en een pushmelding verzenden.</span><span class="sxs-lookup"><span data-stu-id="a740a-112">This tutorial presents a "basic integration," which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="a740a-113">de volledige integratiedocumentatie Hallo vindt u in Hallo [Mobile Engagement universele Windows SDK-integratie](mobile-engagement-windows-store-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a740a-113">hello complete integration documentation can be found in hello [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md).</span></span>

<span data-ttu-id="a740a-114">U kunt een eenvoudige app maken met Visual Studio toodemonstrate Hallo-integratie.</span><span class="sxs-lookup"><span data-stu-id="a740a-114">You create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-windows-universal-app-project"></a><span data-ttu-id="a740a-115">Een nieuw project voor een universele Windows-app maken</span><span class="sxs-lookup"><span data-stu-id="a740a-115">Create a Windows Universal App project</span></span>
<span data-ttu-id="a740a-116">Hallo volgende stappen wordt ervan uitgegaan Hallo gebruik van Visual Studio 2015 al Hallo stappen vergelijkbaar in eerdere versies van Visual Studio zijn.</span><span class="sxs-lookup"><span data-stu-id="a740a-116">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span>

1. <span data-ttu-id="a740a-117">Start Visual Studio en in Hallo **Start** Schakel in het scherm **nieuw Project**.</span><span class="sxs-lookup"><span data-stu-id="a740a-117">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="a740a-118">Selecteer in het pop-upvenster Hallo **Windows** -> **Universal** -> **lege App (universeel Windows)**.</span><span class="sxs-lookup"><span data-stu-id="a740a-118">In hello pop-up, select **Windows** -> **Universal** -> **Blank App (Universal Windows)**.</span></span> <span data-ttu-id="a740a-119">Vul Hallo app **naam** en **oplossingsnaam**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a740a-119">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>

    ![][1]

<span data-ttu-id="a740a-120">U hebt nu een universele Windows-App-project waarin u naast hello Azure Mobile Engagement SDK integreren gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a740a-120">You have now created a Windows Universal App project into which you next integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="a740a-121">Verbinding maken met uw app tooMobile Engagement back-end</span><span class="sxs-lookup"><span data-stu-id="a740a-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="a740a-122">Hallo installeren [MicrosoftAzure.MobileEngagement] Nuget-pakket in uw project.</span><span class="sxs-lookup"><span data-stu-id="a740a-122">Install hello [MicrosoftAzure.MobileEngagement] Nuget package in your project.</span></span> <span data-ttu-id="a740a-123">Als u voor zowel Windows als Windows Phone ontwikkelt, moet u toodo dit voor beide projecten.</span><span class="sxs-lookup"><span data-stu-id="a740a-123">If you are targeting both Windows and Windows Phone platforms, you need toodo this for both projects.</span></span> <span data-ttu-id="a740a-124">Voor Windows 8.x en Windows Phone 8.1, Hallo hetzelfde Nuget-pakket plaatsen Hallo juiste platform-specifieke binaire bestanden in elk project.</span><span class="sxs-lookup"><span data-stu-id="a740a-124">For Windows 8.x and Windows Phone 8.1, hello same Nuget package places hello correct platform-specific binaries in each project.</span></span>
2. <span data-ttu-id="a740a-125">Open **Package.appxmanifest** en zorg ervoor dat Hallo volgende mogelijkheid is toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="a740a-125">Open **Package.appxmanifest** and make sure that hello following capability is added there:</span></span>

        Internet (Client)

    ![][2]
3. <span data-ttu-id="a740a-126">Nu Hallo verbindingsreeks die u eerder hebt gekopieerd voor uw Mobile Engagement-App kopiëren en plakken in Hallo `Resources\EngagementConfiguration.xml` bestand tussen Hallo `<connectionString>` en `</connectionString>` tags:</span><span class="sxs-lookup"><span data-stu-id="a740a-126">Now copy hello connection string that you copied earlier for your Mobile Engagement App and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>

    ![][3]

    > [!TIP]
    > <span data-ttu-id="a740a-127">Als u een app maakt voor zowel Windows als Windows Phone, moet u nog steeds twee Mobile Engagement-toepassingen maken, een voor elk ondersteund platform.</span><span class="sxs-lookup"><span data-stu-id="a740a-127">If your App targets both Windows and Windows Phone platforms, you should still create two Mobile Engagement Applications - one for each supported platform.</span></span> <span data-ttu-id="a740a-128">Met twee apps zorgt ervoor dat u juist segmentering van Hallo doelgroep maken kunt en op de juiste wijze gerichte meldingen voor elk platform kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="a740a-128">Having two apps ensures that you can create correct segmentation of hello audience and can send appropriately targeted notifications for each platform.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a740a-129">NuGet kopiëren hello SDK-bronnen in uw Windows 10 UWP-toepassing niet automatisch.</span><span class="sxs-lookup"><span data-stu-id="a740a-129">NuGet does not automatically copy hello SDK resources in your Windows 10 UWP application.</span></span> <span data-ttu-id="a740a-130">U hebt toodo het Hallo-stappen die worden weergegeven wanneer u Hallo Nuget-pakket is geïnstalleerd (Leesmij) handmatig te volgen.</span><span class="sxs-lookup"><span data-stu-id="a740a-130">You have toodo it manually following hello steps which show up (readme.txt) when hello Nuget package is installed.</span></span>  

1. <span data-ttu-id="a740a-131">In Hallo `App.xaml.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="a740a-131">In hello `App.xaml.cs` file:</span></span>

    <span data-ttu-id="a740a-132">a.</span><span class="sxs-lookup"><span data-stu-id="a740a-132">a.</span></span> <span data-ttu-id="a740a-133">Hallo toevoegen `using` instructie:</span><span class="sxs-lookup"><span data-stu-id="a740a-133">Add hello `using` statement:</span></span>

            using Microsoft.Azure.Engagement;

    <span data-ttu-id="a740a-134">b.</span><span class="sxs-lookup"><span data-stu-id="a740a-134">b.</span></span> <span data-ttu-id="a740a-135">Toevoegen van een methode die wordt geïnitialiseerd Hallo Engagement:</span><span class="sxs-lookup"><span data-stu-id="a740a-135">Add a method that initializes hello Engagement:</span></span>

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    <span data-ttu-id="a740a-136">c.</span><span class="sxs-lookup"><span data-stu-id="a740a-136">c.</span></span> <span data-ttu-id="a740a-137">Hallo SDK in Hallo initialiseren **OnLaunched** methode:</span><span class="sxs-lookup"><span data-stu-id="a740a-137">Initialize hello SDK in hello **OnLaunched** method:</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    <span data-ttu-id="a740a-138">c.</span><span class="sxs-lookup"><span data-stu-id="a740a-138">c.</span></span> <span data-ttu-id="a740a-139">Hallo volgende invoegen in Hallo **OnActivated** methode en het Hallo-methode toevoegen als deze nog niet aanwezig is:</span><span class="sxs-lookup"><span data-stu-id="a740a-139">Insert hello following in hello **OnActivated** method and add hello method if it is not already present:</span></span>

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <span data-ttu-id="a740a-140"><a id="monitor"></a>Realtime-bewaking inschakelen</span><span class="sxs-lookup"><span data-stu-id="a740a-140"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="a740a-141">toostart verzenden van gegevens en ervoor te zorgen dat Hallo gebruikers actief zijn, moet u ten minste één scherm (activiteit) toohello Mobile Engagement back-end verzenden.</span><span class="sxs-lookup"><span data-stu-id="a740a-141">toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="a740a-142">In Hallo **MainPage.xaml.cs**, voeg de volgende Hallo `using` instructie:</span><span class="sxs-lookup"><span data-stu-id="a740a-142">In hello **MainPage.xaml.cs**, add hello following `using` statement:</span></span>

    <span data-ttu-id="a740a-143">met behulp van Microsoft.Azure.Engagement.Overlay;</span><span class="sxs-lookup"><span data-stu-id="a740a-143">using Microsoft.Azure.Engagement.Overlay;</span></span>
2. <span data-ttu-id="a740a-144">Wijzigen van de basisklasse Hallo van **MainPage** van **pagina** te**EngagementPageOverlay**:</span><span class="sxs-lookup"><span data-stu-id="a740a-144">Change hello base class of **MainPage** from **Page** too**EngagementPageOverlay**:</span></span>

        class MainPage : EngagementPageOverlay
3. <span data-ttu-id="a740a-145">In Hallo `MainPage.xaml` bestand:</span><span class="sxs-lookup"><span data-stu-id="a740a-145">In hello `MainPage.xaml` file:</span></span>

    <span data-ttu-id="a740a-146">a.</span><span class="sxs-lookup"><span data-stu-id="a740a-146">a.</span></span> <span data-ttu-id="a740a-147">Tooyour naamruimtedeclaraties toevoegen:</span><span class="sxs-lookup"><span data-stu-id="a740a-147">Add tooyour namespaces declarations:</span></span>

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    <span data-ttu-id="a740a-148">b.</span><span class="sxs-lookup"><span data-stu-id="a740a-148">b.</span></span> <span data-ttu-id="a740a-149">Vervang Hallo **pagina** in Hallo XML-tagnaam met **engagement: EngagementPageOverlay**</span><span class="sxs-lookup"><span data-stu-id="a740a-149">Replace hello **Page** in hello XML tag name with **engagement:EngagementPageOverlay**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a740a-150">Als uw pagina Hallo overschrijft `OnNavigatedTo` methode ervoor toocall worden `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="a740a-150">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="a740a-151">Hallo-activiteit is anders niet gerapporteerd `EngagementPage` aanroepen `StartActivity` binnen de `OnNavigatedTo` methode).</span><span class="sxs-lookup"><span data-stu-id="a740a-151">Otherwise, hello activity is not reported `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span> <span data-ttu-id="a740a-152">Dit is vooral belangrijk in een Windows Phone-project waarbij de standaardsjabloon Hallo heeft een `OnNavigatedTo` methode.</span><span class="sxs-lookup"><span data-stu-id="a740a-152">This is especially important in a Windows Phone project where hello default template has an `OnNavigatedTo` method.</span></span>
>
> <span data-ttu-id="a740a-153">Voor **Windows 10 Universal-apps**, gebruik Hallo methode aanbevolen in Hallo ' aanbevolen methode: uw pagina klassen van de overbelasting ' sectie van [geavanceerde Reporting Hello Windows universele Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md) , in plaats van Hallo een hierboven vermeld.</span><span class="sxs-lookup"><span data-stu-id="a740a-153">For **Windows 10 Universal apps**, use hello method recommended in hello "Recommended method: overload your Page classes" section of [Advanced Reporting with hello Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md), rather than hello one mentioned above.</span></span>

## <span data-ttu-id="a740a-154"><a id="monitor"></a>App verbinden met realtime-bewaking</span><span class="sxs-lookup"><span data-stu-id="a740a-154"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="a740a-155"><a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen</span><span class="sxs-lookup"><span data-stu-id="a740a-155"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="a740a-156">Mobile Engagement kunt u toointeract en uw gebruikers met pushmeldingen en in-app-berichten in de context van campagnes Hallo bereiken.</span><span class="sxs-lookup"><span data-stu-id="a740a-156">Mobile Engagement allows you toointeract and reach your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="a740a-157">Deze module heet REACH in Hallo Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="a740a-157">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="a740a-158">Hallo volgende secties stelt u uw app tooreceive ze.</span><span class="sxs-lookup"><span data-stu-id="a740a-158">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a><span data-ttu-id="a740a-159">Uw app tooreceive WNS-Pushmeldingen inschakelen</span><span class="sxs-lookup"><span data-stu-id="a740a-159">Enable your app tooreceive WNS Push Notifications</span></span>
1. <span data-ttu-id="a740a-160">In Hallo `Package.appxmanifest` bestand in Hallo **toepassing** tabblad onder **meldingen**stelt **Toast capable:** te**Ja**</span><span class="sxs-lookup"><span data-stu-id="a740a-160">In hello `Package.appxmanifest` file, in hello **Application** tab, under **Notifications**, set **Toast capable:** too**Yes**</span></span>

    ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="a740a-161">Hallo bereiken SDK initialiseren</span><span class="sxs-lookup"><span data-stu-id="a740a-161">Initialize hello REACH SDK</span></span>
<span data-ttu-id="a740a-162">In `App.xaml.cs`, roepen **EngagementReach.Instance.Init(e);** in Hallo **InitEngagement** functie meteen na de initialisatie van de agent Hallo:</span><span class="sxs-lookup"><span data-stu-id="a740a-162">In `App.xaml.cs`, call **EngagementReach.Instance.Init(e);** in hello **InitEngagement** function right after hello agent initialization:</span></span>

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

<span data-ttu-id="a740a-163">U bent klaar toosend een toast-melding.</span><span class="sxs-lookup"><span data-stu-id="a740a-163">You're ready toosend a toast.</span></span> <span data-ttu-id="a740a-164">Vervolgens controleren we of u deze basisintegratie juist hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a740a-164">Next we verify that you have correctly carried out this basic integration.</span></span>

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a><span data-ttu-id="a740a-165">Verleen toegang tooMobile Engagement toosend meldingen</span><span class="sxs-lookup"><span data-stu-id="a740a-165">Grant access tooMobile Engagement toosend notifications</span></span>
1. <span data-ttu-id="a740a-166">Open het [ontwikkelaarscentrum voor Windows Store] in uw webbrowser, meld u aan, en maak indien nodig een account.</span><span class="sxs-lookup"><span data-stu-id="a740a-166">Open [Windows Store Dev Center] in your web browser, login, and create an account if necessary.</span></span>
2. <span data-ttu-id="a740a-167">Klik op **Dashboard** op Hallo rechterbovenhoek hoek en klik vervolgens op **maakt een nieuwe app** Hallo linker deelvenster menu.</span><span class="sxs-lookup"><span data-stu-id="a740a-167">Click **Dashboard** at hello top right corner and then click **Create a new app** from hello left panel menu.</span></span>

    ![][9]
3. <span data-ttu-id="a740a-168">Maak uw app door de naam ervan te reserveren.</span><span class="sxs-lookup"><span data-stu-id="a740a-168">Create your app by reserving its name.</span></span>

    ![][10]
4. <span data-ttu-id="a740a-169">Zodra het Hallo-app is gemaakt, te navigeren**Services -> Push notifications** in het linkermenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="a740a-169">Once hello app has been created, navigate too**Services -> Push notifications** from hello left menu.</span></span>

    ![][11]
5. <span data-ttu-id="a740a-170">Push sectie meldingen in hello, klikt u op Hallo **Live Services site** koppeling.</span><span class="sxs-lookup"><span data-stu-id="a740a-170">In hello Push notifications section, click hello **Live Services site** link.</span></span>

    ![][12]
6. <span data-ttu-id="a740a-171">U navigeren gedeelte toohello Push credentials.</span><span class="sxs-lookup"><span data-stu-id="a740a-171">You navigate toohello Push credentials section.</span></span> <span data-ttu-id="a740a-172">Zorg ervoor dat u in Hallo **Appinstellingen** sectie en kopieer uw **pakket-SID** en **clientgeheim**</span><span class="sxs-lookup"><span data-stu-id="a740a-172">Make sure you are in hello **App Settings** section and then copy your **Package SID** and **Client secret**</span></span>

    ![][13]
7. <span data-ttu-id="a740a-173">Navigeer toohello **instellingen** van uw Mobile Engagement-portal en klikt u op Hallo **Native Pushbericht** sectie aan de linkerkant Hallo.</span><span class="sxs-lookup"><span data-stu-id="a740a-173">Navigate toohello **Settings** of your Mobile Engagement portal, and click hello **Native Push** section on hello left.</span></span> <span data-ttu-id="a740a-174">Klik vervolgens op Hallo **bewerken** knop tooenter uw **pakket beveiligings-id (SID)** en uw **geheime sleutel** zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="a740a-174">Then, click hello **Edit** button tooenter your **Package security identifier (SID)** and your **Secret Key** as shown:</span></span>

    ![][6]
8. <span data-ttu-id="a740a-175">Controleer ten slotte dat u uw app in Visual Studio hebt gekoppeld aan deze app gemaakt in Hallo appstore.</span><span class="sxs-lookup"><span data-stu-id="a740a-175">Finally make sure that you have associated your Visual Studio app with this created app in hello App store.</span></span> <span data-ttu-id="a740a-176">Klik in Visual Studio op **Associate App with Store** (App koppelen aan Store).</span><span class="sxs-lookup"><span data-stu-id="a740a-176">Click **Associate App with Store** in Visual Studio.</span></span>

    ![][7]

## <span data-ttu-id="a740a-177"><a id="send"></a>Een melding tooyour app verzenden</span><span class="sxs-lookup"><span data-stu-id="a740a-177"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="a740a-178">Als het Hallo-app wordt uitgevoerd, ziet u een melding in de app.</span><span class="sxs-lookup"><span data-stu-id="a740a-178">If hello app is running, you see an in-app notification.</span></span> <span data-ttu-id="a740a-179">anders als Hallo app is gesloten, ziet u een pop-upmelding.</span><span class="sxs-lookup"><span data-stu-id="a740a-179">otherwise if hello app is closed, you see a toast notification.</span></span>
<span data-ttu-id="a740a-180">Als u een melding in de app, maar geen toast-melding ziet en u Hallo app in de foutopsporingsmodus in Visual Studio uitvoert, probeer **Lifecycle events -> Suspend** in Hallo werkbalk tooensure die Hallo-app is onderbroken.</span><span class="sxs-lookup"><span data-stu-id="a740a-180">If you see an in-app notification but not a toast notification, and you are running hello app in debug mode in Visual Studio, then try **Lifecycle events -> Suspend** in hello toolbar tooensure that hello app is suspended.</span></span> <span data-ttu-id="a740a-181">Als u de knop Start Hallo tijdens het opsporen van Hallo-toepassing in Visual Studio hebt geklikt, klikt u vervolgens het niet altijd onderbroken en terwijl u Hallo melding als in de app ziet, deze niet wordt weergegeven als een toast-melding.</span><span class="sxs-lookup"><span data-stu-id="a740a-181">If you clicked hello Home button while debugging hello application in Visual Studio, then it doesn't always get suspended and while you see hello notification as in-app, it doesn't show up as a toast notification.</span></span>  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[ontwikkelaarscentrum voor Windows Store]: https://dev.windows.com
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
