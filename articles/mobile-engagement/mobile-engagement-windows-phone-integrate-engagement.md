---
title: aaaWindows Phone Silverlight Engagement SDK-integratie
description: Hoe tooIntegrate Azure Mobile Engagement met Windows Phone Silverlight-Apps
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f65683a62e5256cea469a3a73d99ade4331cb6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="636c7-103">Windows Phone Silverlight Engagement SDK-integratie</span><span class="sxs-lookup"><span data-stu-id="636c7-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="636c7-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="636c7-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="636c7-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="636c7-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="636c7-106">iOS</span><span class="sxs-lookup"><span data-stu-id="636c7-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="636c7-107">Android</span><span class="sxs-lookup"><span data-stu-id="636c7-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="636c7-108">Deze procedure wordt beschreven Hallo eenvoudigste manier tooactivate Azure Mobile Engagement Analytics en bewaking van functies in uw Windows Phone Silverlight-toepassing.</span><span class="sxs-lookup"><span data-stu-id="636c7-108">This procedure describes hello simplest way tooactivate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="636c7-109">Hallo stappen te volgen zijn dat onvoldoende tooactivate Hallo rapport van Logboeken nodig toocompute alle statistische gegevens over gebruikers, sessies, activiteiten, Crashes en Technicals.</span><span class="sxs-lookup"><span data-stu-id="636c7-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="636c7-110">rapport van Logboeken Hallo nodig toocompute andere statistieken zoals gebeurtenissen, fouten en taken moeten worden uitgevoerd handmatig met Hallo Engagement API (Zie [hoe toouse Hallo Mobile Engagement API in uw Windows Phone Silverlight-app-tagging geavanceerde](mobile-engagement-windows-phone-use-engagement-api.md) Zie hieronder) omdat deze statistieken afhankelijk zijn van toepassing zijn.</span><span class="sxs-lookup"><span data-stu-id="636c7-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="636c7-111">Ondersteunde versies</span><span class="sxs-lookup"><span data-stu-id="636c7-111">Supported versions</span></span>
<span data-ttu-id="636c7-112">Hallo Mobile Engagement SDK voor Windows Silverlight kan alleen worden geïntegreerd in toepassingen die gericht is op:</span><span class="sxs-lookup"><span data-stu-id="636c7-112">hello Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="636c7-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="636c7-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="636c7-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="636c7-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> <span data-ttu-id="636c7-115">Als u ontwikkelt voor Windows Phone 8.1 (zonder Silverlight) verwijzen toohello [universele Windows-integratie procedure](mobile-engagement-windows-store-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="636c7-115">If you are targeting Windows Phone 8.1 (non-Silverlight) then refer toohello [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="636c7-116">Hallo Mobile Engagement Silverlight-SDK installeren</span><span class="sxs-lookup"><span data-stu-id="636c7-116">Install hello Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="636c7-117">Hallo Mobile Engagement SDK voor Windows Silverlight is beschikbaar als een Nuget-pakket aangeroepen *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="636c7-117">hello Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="636c7-118">U kunt deze installeren via Hallo Nuget Package Manager voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="636c7-118">You can install it from hello Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="636c7-119">Hallo mogelijkheden toevoegen</span><span class="sxs-lookup"><span data-stu-id="636c7-119">Add hello capabilities</span></span>
<span data-ttu-id="636c7-120">Hallo Engagement SDK moet enkele mogelijkheden van Windows Phone Silverlight-SDK Hallo in volgorde toowork goed.</span><span class="sxs-lookup"><span data-stu-id="636c7-120">hello Engagement SDK needs some capabilities of hello Windows Phone Silverlight SDK in order toowork properly.</span></span>

<span data-ttu-id="636c7-121">Open uw `WMAppManifest.xml` -bestand en zorg ervoor dat die Hallo na mogelijkheden zijn gedeclareerd in Hallo `Capabilities` Configuratiescherm:</span><span class="sxs-lookup"><span data-stu-id="636c7-121">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared in hello `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="636c7-122">Hallo Engagement SDK initialiseren</span><span class="sxs-lookup"><span data-stu-id="636c7-122">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="636c7-123">Engagement configuratie</span><span class="sxs-lookup"><span data-stu-id="636c7-123">Engagement configuration</span></span>
<span data-ttu-id="636c7-124">Hallo Engagement configuratie op Hallo is gecentraliseerd `Resources\EngagementConfiguration.xml` -bestand van uw project.</span><span class="sxs-lookup"><span data-stu-id="636c7-124">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="636c7-125">Dit bestand toospecify bewerken:</span><span class="sxs-lookup"><span data-stu-id="636c7-125">Edit this file toospecify :</span></span>

* <span data-ttu-id="636c7-126">De verbindingsreeks voor de toepassing tussen de tags `<connectionString>` en `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="636c7-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="636c7-127">Als u wilt dat deze tijdens runtime in plaats daarvan kunt u bellen Hallo volgende toospecify methode voordat de initialisatie van de agent Hallo Engagement:</span><span class="sxs-lookup"><span data-stu-id="636c7-127">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="636c7-128">Hallo-verbindingsreeks voor uw toepassing wordt weergegeven op Hallo klassieke Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="636c7-128">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="636c7-129">De initialisatie van de engagement</span><span class="sxs-lookup"><span data-stu-id="636c7-129">Engagement initialization</span></span>
<span data-ttu-id="636c7-130">Wanneer u een nieuw project maakt een `App.xaml.cs` -bestand is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="636c7-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="636c7-131">Deze klasse neemt over van `Application` en bevat veel belangrijke methoden.</span><span class="sxs-lookup"><span data-stu-id="636c7-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="636c7-132">Dit wordt ook worden de gebruikte tooinitialize Hallo Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="636c7-132">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="636c7-133">Hallo wijzigen `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="636c7-133">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="636c7-134">Toevoegen van tooyour `using` instructies:</span><span class="sxs-lookup"><span data-stu-id="636c7-134">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="636c7-135">Invoegen `EngagementAgent.Instance.Init` in Hallo `Application_Launching` methode:</span><span class="sxs-lookup"><span data-stu-id="636c7-135">Insert `EngagementAgent.Instance.Init` in hello `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="636c7-136">Invoegen `EngagementAgent.Instance.OnActivated` in Hallo `Application_Activated` methode:</span><span class="sxs-lookup"><span data-stu-id="636c7-136">Insert `EngagementAgent.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> <span data-ttu-id="636c7-137">We afraden raden u tooadd Hallo Engagement-initialisatie in een andere locatie van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="636c7-137">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span> <span data-ttu-id="636c7-138">Echter wel rekening die Hallo `EngagementAgent.Instance.Init` methode wordt uitgevoerd op een specifieke thread en niet op Hallo UI-thread.</span><span class="sxs-lookup"><span data-stu-id="636c7-138">However, be aware that hello `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on hello UI thread.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="636c7-139">Basic-rapportage</span><span class="sxs-lookup"><span data-stu-id="636c7-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="636c7-140">Aanbevolen methode: overbelasting uw `PhoneApplicationPage` klassen</span><span class="sxs-lookup"><span data-stu-id="636c7-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="636c7-141">In volgorde tooactivate Hallo rapport van alle Hallo Logboeken door Engagement toocompute gebruikers, sessies, activiteiten, Crashes en technische statistieken vereist, kunt u gewoon zodat alle uw `PhoneApplicationPage` onderliggende klassen overnemen van Hallo `EngagementPage` klassen.</span><span class="sxs-lookup"><span data-stu-id="636c7-141">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="636c7-142">Hier volgt een voorbeeld van hoe toodo dit voor een pagina van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="636c7-142">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="636c7-143">U kunt doen Hallo hetzelfde geldt voor alle pagina's van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="636c7-143">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="636c7-144">C#-bronbestand</span><span class="sxs-lookup"><span data-stu-id="636c7-144">C# Source file</span></span>
<span data-ttu-id="636c7-145">Wijzigen van uw pagina `.xaml.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="636c7-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="636c7-146">Toevoegen van tooyour `using` instructies:</span><span class="sxs-lookup"><span data-stu-id="636c7-146">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="636c7-147">Vervang `PhoneApplicationPage` met `EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="636c7-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="636c7-148">**Zonder Engagement:**</span><span class="sxs-lookup"><span data-stu-id="636c7-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="636c7-149">**Met Engagement:**</span><span class="sxs-lookup"><span data-stu-id="636c7-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> <span data-ttu-id="636c7-150">Als uw pagina van Hallo overneemt `OnNavigatedTo` -methode worden zorgvuldige toolet hello `base.OnNavigatedTo(e)` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="636c7-150">If your page inherits from hello `OnNavigatedTo` method, be careful toolet hello `base.OnNavigatedTo(e)` call.</span></span> <span data-ttu-id="636c7-151">Anders Hallo activiteit niet gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="636c7-151">Otherwise, hello activity will not be reported.</span></span> <span data-ttu-id="636c7-152">Hallo immers `EngagementPage` aanroept `StartActivity` binnen Hallo `OnNavigatedTo` methode.</span><span class="sxs-lookup"><span data-stu-id="636c7-152">Indeed, hello `EngagementPage` is calling `StartActivity` inside hello `OnNavigatedTo` method.</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="636c7-153">XAML-bestand</span><span class="sxs-lookup"><span data-stu-id="636c7-153">XAML file</span></span>
<span data-ttu-id="636c7-154">Wijzigen van uw pagina `.xaml` bestand:</span><span class="sxs-lookup"><span data-stu-id="636c7-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="636c7-155">Tooyour naamruimtedeclaraties toevoegen:</span><span class="sxs-lookup"><span data-stu-id="636c7-155">Add tooyour namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="636c7-156">Vervang `phone:PhoneApplicationPage` met `engagement:EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="636c7-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="636c7-157">**Zonder Engagement:**</span><span class="sxs-lookup"><span data-stu-id="636c7-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="636c7-158">**Met Engagement:**</span><span class="sxs-lookup"><span data-stu-id="636c7-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a><span data-ttu-id="636c7-159">Hallo standaardgedrag negeren</span><span class="sxs-lookup"><span data-stu-id="636c7-159">Override hello default behavior</span></span>
<span data-ttu-id="636c7-160">Standaard is als Hallo activiteitsnaam, zonder extra Hallo klassenaam van Hallo pagina gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="636c7-160">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="636c7-161">Als Hallo klasse Hallo 'Pagina' achtervoegsel gebruikt, Engagement wordt het ook verwijderd.</span><span class="sxs-lookup"><span data-stu-id="636c7-161">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="636c7-162">Als u toooverride Hallo standaardgedrag voor de naam van de hello wilt, programmacode toe te voegen deze tooyour:</span><span class="sxs-lookup"><span data-stu-id="636c7-162">If you want toooverride hello default behavior for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="636c7-163">Als u wilt dat tooreport wat extra informatie met uw activiteiten, kunt u deze code tooyour toevoegen:</span><span class="sxs-lookup"><span data-stu-id="636c7-163">If you want tooreport some extra information with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="636c7-164">Deze methoden worden aangeroepen vanuit Hallo `OnNavigatedTo` methode van uw pagina.</span><span class="sxs-lookup"><span data-stu-id="636c7-164">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="636c7-165">Alternatieve methode: call `StartActivity()` handmatig</span><span class="sxs-lookup"><span data-stu-id="636c7-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="636c7-166">Als u niet kunt of toooverload niet wilt dat uw `PhoneApplicationPage` klassen, in plaats daarvan kunt u uw activiteiten starten door het aanroepen van `EngagementAgent` rechtstreeks methoden.</span><span class="sxs-lookup"><span data-stu-id="636c7-166">If you cannot or do not want toooverload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="636c7-167">We raden aan aanroepen `StartActivity` binnen uw `OnNavigatedTo` methode van uw PhoneApplicationPage.</span><span class="sxs-lookup"><span data-stu-id="636c7-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> <span data-ttu-id="636c7-168">Zorg ervoor dat u uw sessie correct beëindigen.</span><span class="sxs-lookup"><span data-stu-id="636c7-168">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="636c7-169">Hallo SDK roept automatisch Hallo `EndActivity` methode wanneer de toepassing hello wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="636c7-169">hello SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="636c7-170">Het is dus **maximaal** toocall Hallo aanbevolen `StartActivity` methode wanneer Hallo activiteit van Hallo gebruiker wijzigt, en te**nooit** aanroep Hallo `EndActivity` methode.</span><span class="sxs-lookup"><span data-stu-id="636c7-170">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="636c7-171">Deze methode verzendt een bericht toohello Engagement server dat de huidige gebruiker Hallo Hallo toepassing is verdwenen en dit heeft gevolgen voor alle toepassingslogboeken.</span><span class="sxs-lookup"><span data-stu-id="636c7-171">This method sends a message toohello Engagement server that hello current user has left hello application and this impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="636c7-172">Geavanceerde rapportage</span><span class="sxs-lookup"><span data-stu-id="636c7-172">Advanced reporting</span></span>
<span data-ttu-id="636c7-173">Desgewenst kunt u tooreport toepassing specifieke gebeurtenissen, fouten en taken, toodo dus, gebruik andere methoden gevonden in Hallo Hallo `EngagementAgent` klasse.</span><span class="sxs-lookup"><span data-stu-id="636c7-173">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="636c7-174">Hallo Engagement API kunt toouse alle Engagement geavanceerde mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="636c7-174">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="636c7-175">Zie voor meer informatie [hoe toouse Hallo Mobile Engagement API in uw Windows Phone Silverlight-app-tagging geavanceerde](mobile-engagement-windows-phone-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="636c7-175">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="636c7-176">Geavanceerde configuratie</span><span class="sxs-lookup"><span data-stu-id="636c7-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="636c7-177">Automatische crashrapporten uitschakelen</span><span class="sxs-lookup"><span data-stu-id="636c7-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="636c7-178">U kunt automatische Hallo-crash rapportagefunctie van Engagement uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="636c7-178">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="636c7-179">Vervolgens, als er wordt een niet-verwerkte uitzondering optreedt, Engagement is geen alles.</span><span class="sxs-lookup"><span data-stu-id="636c7-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="636c7-180">Als u van plan toodisable deze functie bent, houd er rekening mee dat wanneer het vastlopen van een niet-verwerkte in uw app optreden zal, Engagement geen Hallo crashes verzenden worden **en** het Hallo-sessie en taken niet gesloten.</span><span class="sxs-lookup"><span data-stu-id="636c7-180">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** it will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="636c7-181">toodisable automatische crash rapportage, alleen uw configuratie, afhankelijk van Hallo manier waarop u het gedeclareerd aanpassen:</span><span class="sxs-lookup"><span data-stu-id="636c7-181">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="636c7-182">Van `EngagementConfiguration.xml` bestand</span><span class="sxs-lookup"><span data-stu-id="636c7-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="636c7-183">Rapport vastlopen te ingesteld`false` tussen `<reportCrash>` en `</reportCrash>` labels.</span><span class="sxs-lookup"><span data-stu-id="636c7-183">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="636c7-184">Van `EngagementConfiguration` object tijdens runtime</span><span class="sxs-lookup"><span data-stu-id="636c7-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="636c7-185">Rapport crash toofalse met behulp van het object EngagementConfiguration ingesteld.</span><span class="sxs-lookup"><span data-stu-id="636c7-185">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="636c7-186">Burst-modus</span><span class="sxs-lookup"><span data-stu-id="636c7-186">Burst mode</span></span>
<span data-ttu-id="636c7-187">Standaard Hallo Engagement servicerapporten Logboeken in realtime.</span><span class="sxs-lookup"><span data-stu-id="636c7-187">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="636c7-188">Als uw toepassing Logboeken heel vaak rapporteert, is het beter toobuffer Hallo logboeken en tooreport ze allemaal tegelijk op een vaste tijd base (dit wordt Hallo 'burst modus' genoemd).</span><span class="sxs-lookup"><span data-stu-id="636c7-188">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="636c7-189">toodo worden dus Hallo-methode aanroept:</span><span class="sxs-lookup"><span data-stu-id="636c7-189">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="636c7-190">Hallo-argument is een waarde in **milliseconden**.</span><span class="sxs-lookup"><span data-stu-id="636c7-190">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="636c7-191">Op elk gewenst moment als u tooreactivate Hallo realtime logboekregistratie wilt, roept Hallo methode geen parameters of met de Hallo 0-waarde.</span><span class="sxs-lookup"><span data-stu-id="636c7-191">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="636c7-192">Hallo burst-modus iets langer Hallo accu levensduur maar heeft een invloed op Hallo Engagement-Monitor: alle sessies en taken duur zijn afgerond toohello burst drempelwaarde (dus sessies en korter zijn dan Hallo burst drempelwaarde is mogelijk niet zichtbaar taken).</span><span class="sxs-lookup"><span data-stu-id="636c7-192">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="636c7-193">Het is aanbevolen toouse een ' burst ' drempelwaarde niet langer dan 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="636c7-193">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="636c7-194">U hebt toobe Houd er rekening mee dat opgeslagen logboeken zijn beperkt too300-items.</span><span class="sxs-lookup"><span data-stu-id="636c7-194">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="636c7-195">U kunt sommige logboeken verliezen als verzenden te lang is.</span><span class="sxs-lookup"><span data-stu-id="636c7-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="636c7-196">Hallo burst drempelwaarde kan niet worden geconfigureerd tooa periode minder dan één seconde.</span><span class="sxs-lookup"><span data-stu-id="636c7-196">hello burst threshold cannot be configured tooa period lesser than one second.</span></span> <span data-ttu-id="636c7-197">Als u dus toodo probeert, Hallo SDK wordt een tracering met Hallo fout weergeven en automatisch opnieuw instellen toohello standaardwaarde, dat wil zeggen, nul seconden.</span><span class="sxs-lookup"><span data-stu-id="636c7-197">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, that is, zero seconds.</span></span> <span data-ttu-id="636c7-198">Dit activeert Hallo SDK tooreport Hallo Logboeken in realtime.</span><span class="sxs-lookup"><span data-stu-id="636c7-198">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

