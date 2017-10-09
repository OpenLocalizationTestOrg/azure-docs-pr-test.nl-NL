---
title: aaaWindows universele Apps Engagement SDK-integratie
description: Hoe tooIntegrate Azure Mobile Engagement met universele Windows-Apps
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 18543798099c233dbe55cc387ba0216e369c8596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a><span data-ttu-id="d7319-103">Windows universele Apps Engagement SDK-integratie</span><span class="sxs-lookup"><span data-stu-id="d7319-103">Windows Universal Apps Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d7319-104">Universeel Windows</span><span class="sxs-lookup"><span data-stu-id="d7319-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="d7319-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="d7319-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="d7319-106">iOS</span><span class="sxs-lookup"><span data-stu-id="d7319-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="d7319-107">Android</span><span class="sxs-lookup"><span data-stu-id="d7319-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="d7319-108">Deze procedure wordt beschreven Hallo eenvoudigste manier tooactivate Engagement Analytics en bewaking van functies in uw universele Windows-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d7319-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your Windows Universal application.</span></span>

<span data-ttu-id="d7319-109">Hallo stappen te volgen zijn dat onvoldoende tooactivate Hallo rapport van Logboeken nodig toocompute alle statistische gegevens over gebruikers, sessies, activiteiten, Crashes en Technicals.</span><span class="sxs-lookup"><span data-stu-id="d7319-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="d7319-110">rapport van Logboeken Hallo nodig toocompute andere statistieken zoals gebeurtenissen, fouten en taken moeten worden uitgevoerd handmatig met Hallo Engagement API (Zie [hoe toouse Hallo Mobile Engagement API in uw universele Windows-app-tagging geavanceerde](mobile-engagement-windows-store-use-engagement-api.md) sinds Deze statistieken zijn afhankelijk van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d7319-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="d7319-111">Ondersteunde versies</span><span class="sxs-lookup"><span data-stu-id="d7319-111">Supported versions</span></span>
<span data-ttu-id="d7319-112">Hallo Mobile Engagement SDK voor Windows universele Apps kan alleen worden geïntegreerd in Windows Runtime en universele Windows-Platform-toepassingen die gericht is op:</span><span class="sxs-lookup"><span data-stu-id="d7319-112">hello Mobile Engagement SDK for Windows Universal Apps can only be integrated into Windows Runtime and Universal Windows Platform applications targeting :</span></span>

* <span data-ttu-id="d7319-113">Windows 8</span><span class="sxs-lookup"><span data-stu-id="d7319-113">Windows 8</span></span>
* <span data-ttu-id="d7319-114">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="d7319-114">Windows 8.1</span></span>
* <span data-ttu-id="d7319-115">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="d7319-115">Windows Phone 8.1</span></span>
* <span data-ttu-id="d7319-116">Windows 10 (desktop en mobiel families)</span><span class="sxs-lookup"><span data-stu-id="d7319-116">Windows 10 (desktop and mobile families)</span></span>

> [!NOTE]
> <span data-ttu-id="d7319-117">Als u ontwikkelt voor Windows Phone Silverlight verwijzen toohello [Windows Phone Silverlight-integratie procedure](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="d7319-117">If you are targeting Windows Phone Silverlight then refer toohello [Windows Phone Silverlight integration procedure](mobile-engagement-windows-phone-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-universal-apps-sdk"></a><span data-ttu-id="d7319-118">Hallo Mobile Engagement universele Apps SDK installeren</span><span class="sxs-lookup"><span data-stu-id="d7319-118">Install hello Mobile Engagement Universal Apps SDK</span></span>
### <a name="all-platforms"></a><span data-ttu-id="d7319-119">Alle platforms</span><span class="sxs-lookup"><span data-stu-id="d7319-119">All platforms</span></span>
<span data-ttu-id="d7319-120">Hallo Mobile Engagement SDK voor universele Windows-App is beschikbaar als een Nuget-pakket aangeroepen *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="d7319-120">hello Mobile Engagement SDK for Windows Universal App is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="d7319-121">U kunt deze installeren via Hallo Nuget Package Manager voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d7319-121">You can install it from hello Visual Studio Nuget Package Manager.</span></span>

### <a name="windows-8x-and-windows-phone-81"></a><span data-ttu-id="d7319-122">Windows 8.x en Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="d7319-122">Windows 8.x and Windows Phone 8.1</span></span>
<span data-ttu-id="d7319-123">NuGet automatisch wordt geïmplementeerd Hallo SDK bronnen in Hallo `Resources` map in de hoofdmap Hallo van uw toepassingsproject.</span><span class="sxs-lookup"><span data-stu-id="d7319-123">NuGet automatically deploys hello SDK resources in hello `Resources` folder at hello root of your application project.</span></span>

### <a name="windows-10-universal-windows-platform-applications"></a><span data-ttu-id="d7319-124">Windows 10 Universal Windows Platform-toepassingen</span><span class="sxs-lookup"><span data-stu-id="d7319-124">Windows 10 Universal Windows Platform applications</span></span>
<span data-ttu-id="d7319-125">NuGet distribueert Hallo SDK resources in uw UWP-toepassing nog niet automatisch.</span><span class="sxs-lookup"><span data-stu-id="d7319-125">NuGet does not automatically deploy hello SDK resources in your UWP application yet.</span></span> <span data-ttu-id="d7319-126">Hebt u het programma handmatig tot implementatie van resources wordt teruggeplaatst in NuGet toodo:</span><span class="sxs-lookup"><span data-stu-id="d7319-126">You have toodo it manually until resources deployment is reintroduced in NuGet:</span></span>

1. <span data-ttu-id="d7319-127">Open de Verkenner.</span><span class="sxs-lookup"><span data-stu-id="d7319-127">Open your File Explorer.</span></span>
2. <span data-ttu-id="d7319-128">Navigeer toohello volgende op locatie (**x.x.x** Hallo-versie van Engagement u installeert): *% USERPROFILE %\\.nuget\packages\MicrosoftAzure.MobileEngagement\\*  *x.x.x**\\content\win81*</span><span class="sxs-lookup"><span data-stu-id="d7319-128">Navigate toohello following location (**x.x.x** is hello version of Engagement you are installing): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span></span>
3. <span data-ttu-id="d7319-129">Slepen en neerzetten Hallo **Resources** map uit Hallo bestand explorer toohello hoofdmap van uw project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d7319-129">Drag and drop hello **Resources** folder from hello file explorer toohello root of your project in Visual Studio.</span></span>
4. <span data-ttu-id="d7319-130">Selecteer uw project in Visual Studio en activeren Hallo **weergeven van alle bestanden** pictogram boven op Hallo **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d7319-130">In Visual Studio select your project and activate hello **Show All files** icon on top of hello **Solution Explorer**.</span></span>
5. <span data-ttu-id="d7319-131">Sommige bestanden zijn niet opgenomen in het Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="d7319-131">Some files are not included in hello project.</span></span> <span data-ttu-id="d7319-132">ze in één keer Klik met de rechtermuisknop op Hallo tooimport **Resources** map **uitsluiten van project** en vervolgens een andere Klik met de rechtermuisknop op Hallo **Resources** map **opnemen in het project** toore-Hallo hele map bevatten.</span><span class="sxs-lookup"><span data-stu-id="d7319-132">tooimport them at once right click on hello **Resources** folder, **Exclude from project** then another right click on hello **Resources** folder, **Include in project** toore-include hello whole folder.</span></span> <span data-ttu-id="d7319-133">Alle bestanden uit Hallo **Resources** map nu zijn opgenomen in uw project.</span><span class="sxs-lookup"><span data-stu-id="d7319-133">All files from hello **Resources** folder are now included in your project.</span></span>

## <a name="add-hello-capabilities"></a><span data-ttu-id="d7319-134">Hallo mogelijkheden toevoegen</span><span class="sxs-lookup"><span data-stu-id="d7319-134">Add hello capabilities</span></span>
<span data-ttu-id="d7319-135">Hallo Engagement SDK moet enkele mogelijkheden van Hallo Windows SDK in de volgorde toowork goed.</span><span class="sxs-lookup"><span data-stu-id="d7319-135">hello Engagement SDK needs some capabilities of hello Windows SDK in order toowork properly.</span></span>

<span data-ttu-id="d7319-136">Open uw `Package.appxmanifest` -bestand en zorg ervoor dat die Hallo volgende mogelijkheden worden gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="d7319-136">Open your `Package.appxmanifest` file and be sure that hello following capabilities are declared:</span></span>

* `Internet (Client)`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="d7319-137">Hallo Engagement SDK initialiseren</span><span class="sxs-lookup"><span data-stu-id="d7319-137">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="d7319-138">Engagement configuratie</span><span class="sxs-lookup"><span data-stu-id="d7319-138">Engagement configuration</span></span>
<span data-ttu-id="d7319-139">Hallo Engagement configuratie op Hallo is gecentraliseerd `Resources\EngagementConfiguration.xml` -bestand van uw project.</span><span class="sxs-lookup"><span data-stu-id="d7319-139">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="d7319-140">Dit bestand toospecify bewerken:</span><span class="sxs-lookup"><span data-stu-id="d7319-140">Edit this file toospecify:</span></span>

* <span data-ttu-id="d7319-141">De verbindingsreeks voor de toepassing tussen de tags `<connectionString>` en `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="d7319-141">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="d7319-142">Als u wilt dat deze tijdens runtime in plaats daarvan kunt u bellen Hallo volgende toospecify methode voordat de initialisatie van de agent Hallo Engagement:</span><span class="sxs-lookup"><span data-stu-id="d7319-142">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

<span data-ttu-id="d7319-143">Hallo-verbindingsreeks voor uw toepassing wordt weergegeven op Hallo klassieke Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="d7319-143">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="d7319-144">De initialisatie van de engagement</span><span class="sxs-lookup"><span data-stu-id="d7319-144">Engagement initialization</span></span>
<span data-ttu-id="d7319-145">Wanneer u een nieuw project maakt een `App.xaml.cs` -bestand is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="d7319-145">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="d7319-146">Deze klasse neemt over van `Application` en bevat veel belangrijke methoden.</span><span class="sxs-lookup"><span data-stu-id="d7319-146">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="d7319-147">Dit wordt ook worden de gebruikte tooinitialize Hallo Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="d7319-147">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="d7319-148">Hallo wijzigen `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="d7319-148">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="d7319-149">Toevoegen van tooyour `using` instructies:</span><span class="sxs-lookup"><span data-stu-id="d7319-149">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="d7319-150">Een methode tooshare Hallo Engagement initialisatie voor alle aanroepen eenmaal definiëren:</span><span class="sxs-lookup"><span data-stu-id="d7319-150">Define a method tooshare hello Engagement initialization once for all calls:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* <span data-ttu-id="d7319-151">Roep `InitEngagement` in Hallo `OnLaunched` methode:</span><span class="sxs-lookup"><span data-stu-id="d7319-151">Call `InitEngagement` in hello `OnLaunched` method:</span></span>
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* <span data-ttu-id="d7319-152">Wanneer uw toepassing wordt gestart met behulp van een aangepast schema, een andere toepassing of Hallo opdrachtregel vervolgens Hallo `OnActivated` methode wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d7319-152">When your application is launched using a custom scheme, another application or hello command line then hello `OnActivated` method is called.</span></span> <span data-ttu-id="d7319-153">U moet ook tooinitiate Hallo Engagement SDK wanneer uw app wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="d7319-153">You also need tooinitiate hello Engagement SDK when your app is activated.</span></span> <span data-ttu-id="d7319-154">toodo dus overschrijven `OnActivated` methode:</span><span class="sxs-lookup"><span data-stu-id="d7319-154">toodo so, override `OnActivated` method:</span></span>
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> <span data-ttu-id="d7319-155">We afraden raden u tooadd Hallo Engagement-initialisatie in een andere locatie van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="d7319-155">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="d7319-156">Basic-rapportage</span><span class="sxs-lookup"><span data-stu-id="d7319-156">Basic reporting</span></span>
### <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="d7319-157">Aanbevolen methode: overbelasting uw `Page` klassen</span><span class="sxs-lookup"><span data-stu-id="d7319-157">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="d7319-158">In volgorde tooactivate Hallo rapport van alle Hallo Logboeken door Engagement toocompute gebruikers, sessies, activiteiten, Crashes en technische statistieken vereist, kunt u gewoon zodat alle uw `Page` onderliggende klassen overnemen van Hallo `EngagementPage` klassen.</span><span class="sxs-lookup"><span data-stu-id="d7319-158">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="d7319-159">Hier volgt een voorbeeld van hoe toodo dit voor een pagina van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="d7319-159">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="d7319-160">U kunt doen Hallo hetzelfde geldt voor alle pagina's van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="d7319-160">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="d7319-161">C#-bronbestand</span><span class="sxs-lookup"><span data-stu-id="d7319-161">C# Source file</span></span>
<span data-ttu-id="d7319-162">Wijzigen van uw pagina `.xaml.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="d7319-162">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="d7319-163">Toevoegen van tooyour `using` instructies:</span><span class="sxs-lookup"><span data-stu-id="d7319-163">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="d7319-164">Vervang `Page` met `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="d7319-164">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="d7319-165">**Zonder Engagement:**</span><span class="sxs-lookup"><span data-stu-id="d7319-165">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="d7319-166">**Met Engagement:**</span><span class="sxs-lookup"><span data-stu-id="d7319-166">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="d7319-167">Als uw pagina Hallo overschrijft `OnNavigatedTo` methode ervoor toocall worden `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="d7319-167">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="d7319-168">Anders Hallo activiteit wordt niet gerapporteerd (Hallo `EngagementPage` aanroepen `StartActivity` binnen de `OnNavigatedTo` methode).</span><span class="sxs-lookup"><span data-stu-id="d7319-168">Otherwise,  hello activity will not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="d7319-169">XAML-bestand</span><span class="sxs-lookup"><span data-stu-id="d7319-169">XAML file</span></span>
<span data-ttu-id="d7319-170">Wijzigen van uw pagina `.xaml` bestand:</span><span class="sxs-lookup"><span data-stu-id="d7319-170">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="d7319-171">Tooyour naamruimtedeclaraties toevoegen:</span><span class="sxs-lookup"><span data-stu-id="d7319-171">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="d7319-172">Vervang `Page` met `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="d7319-172">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="d7319-173">**Zonder Engagement:**</span><span class="sxs-lookup"><span data-stu-id="d7319-173">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="d7319-174">**Met Engagement:**</span><span class="sxs-lookup"><span data-stu-id="d7319-174">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-hello-default-behaviour"></a><span data-ttu-id="d7319-175">Hallo standaardwerking overschrijven</span><span class="sxs-lookup"><span data-stu-id="d7319-175">Override hello default behaviour</span></span>
<span data-ttu-id="d7319-176">Standaard is als Hallo activiteitsnaam, zonder extra Hallo klassenaam van Hallo pagina gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="d7319-176">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="d7319-177">Als Hallo klasse Hallo 'Pagina' achtervoegsel gebruikt, Engagement wordt het ook verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d7319-177">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="d7319-178">Als u toooverride Hallo standaard gedrag voor de naam van de hello wilt, programmacode toe te voegen deze tooyour:</span><span class="sxs-lookup"><span data-stu-id="d7319-178">If you want toooverride hello default behaviour for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="d7319-179">Als u een aantal extra informatie over tooreport met uw activiteiten wilt, kunt u deze code tooyour toevoegen:</span><span class="sxs-lookup"><span data-stu-id="d7319-179">If you want tooreport some extra informations with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="d7319-180">Deze methoden worden aangeroepen vanuit Hallo `OnNavigatedTo` methode van uw pagina.</span><span class="sxs-lookup"><span data-stu-id="d7319-180">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="d7319-181">Alternatieve methode: call `StartActivity()` handmatig</span><span class="sxs-lookup"><span data-stu-id="d7319-181">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="d7319-182">Als u niet kunt of toooverload niet wilt dat uw `Page` klassen, in plaats daarvan kunt u uw activiteiten starten door het aanroepen van `EngagementAgent` rechtstreeks methoden.</span><span class="sxs-lookup"><span data-stu-id="d7319-182">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="d7319-183">We raden aan toocall `StartActivity` binnen uw `OnNavigatedTo` methode van uw pagina.</span><span class="sxs-lookup"><span data-stu-id="d7319-183">We recommend toocall `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="d7319-184">Zorg ervoor dat u uw sessie correct beëindigen.</span><span class="sxs-lookup"><span data-stu-id="d7319-184">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="d7319-185">Hallo universele Windows SDK roept automatisch Hallo `EndActivity` methode wanneer de toepassing hello wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="d7319-185">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="d7319-186">Het is dus **maximaal** toocall Hallo aanbevolen `StartActivity` methode wanneer Hallo activiteit van Hallo gebruiker wijzigt, en te**nooit** aanroep Hallo `EndActivity` methode deze methode verzendt tooEngagement Server dat de huidige gebruiker heeft verlaten Hallo toepassing, deze van invloed is op alle toepassingslogboeken.</span><span class="sxs-lookup"><span data-stu-id="d7319-186">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method, this method sends tooEngagement server that current user has leave hello application, this will impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="d7319-187">Geavanceerde rapportage</span><span class="sxs-lookup"><span data-stu-id="d7319-187">Advanced reporting</span></span>
<span data-ttu-id="d7319-188">Desgewenst kunt u tooreport toepassing specifieke gebeurtenissen, fouten en taken, toodo dus, gebruik andere methoden gevonden in Hallo Hallo `EngagementAgent` klasse.</span><span class="sxs-lookup"><span data-stu-id="d7319-188">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="d7319-189">Hallo Engagement API kunt toouse alle Engagement geavanceerde mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="d7319-189">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="d7319-190">Zie voor meer informatie [hoe toouse Hallo Mobile Engagement API in uw universele Windows-app-tagging geavanceerde](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="d7319-190">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="d7319-191">Geavanceerde configuratie</span><span class="sxs-lookup"><span data-stu-id="d7319-191">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="d7319-192">Automatische crashrapporten uitschakelen</span><span class="sxs-lookup"><span data-stu-id="d7319-192">Disable automatic crash reporting</span></span>
<span data-ttu-id="d7319-193">U kunt automatische Hallo-crash rapportagefunctie van Engagement uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="d7319-193">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="d7319-194">Vervolgens, als er wordt een niet-verwerkte uitzondering optreedt, Engagement is geen alles.</span><span class="sxs-lookup"><span data-stu-id="d7319-194">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="d7319-195">Als u van plan toodisable deze functie bent, houd er rekening mee dat wanneer het vastlopen van een niet-verwerkte in uw app optreden zal, Engagement geen Hallo crashes verzenden worden **en** Hallo-sessie en taken niet gesloten.</span><span class="sxs-lookup"><span data-stu-id="d7319-195">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="d7319-196">toodisable automatische crash rapportage, alleen uw configuratie, afhankelijk van Hallo manier waarop u het gedeclareerd aanpassen:</span><span class="sxs-lookup"><span data-stu-id="d7319-196">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="d7319-197">Van `EngagementConfiguration.xml` bestand</span><span class="sxs-lookup"><span data-stu-id="d7319-197">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="d7319-198">Rapport vastlopen te ingesteld`false` tussen `<reportCrash>` en `</reportCrash>` labels.</span><span class="sxs-lookup"><span data-stu-id="d7319-198">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="d7319-199">Van `EngagementConfiguration` object tijdens runtime</span><span class="sxs-lookup"><span data-stu-id="d7319-199">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="d7319-200">Rapport crash toofalse met behulp van het object EngagementConfiguration ingesteld.</span><span class="sxs-lookup"><span data-stu-id="d7319-200">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="d7319-201">Burst-modus</span><span class="sxs-lookup"><span data-stu-id="d7319-201">Burst mode</span></span>
<span data-ttu-id="d7319-202">Standaard Hallo Engagement servicerapporten Logboeken in realtime.</span><span class="sxs-lookup"><span data-stu-id="d7319-202">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="d7319-203">Als uw toepassing Logboeken heel vaak rapporteert, is het beter toobuffer Hallo logboeken en tooreport ze allemaal tegelijk op een vaste tijd base (dit wordt Hallo 'burst modus' genoemd).</span><span class="sxs-lookup"><span data-stu-id="d7319-203">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="d7319-204">toodo worden dus Hallo-methode aanroept:</span><span class="sxs-lookup"><span data-stu-id="d7319-204">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="d7319-205">Hallo-argument is een waarde in **milliseconden**.</span><span class="sxs-lookup"><span data-stu-id="d7319-205">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="d7319-206">Op elk gewenst moment als u tooreactivate Hallo realtime logboekregistratie wilt, roept Hallo methode geen parameters of met de Hallo 0-waarde.</span><span class="sxs-lookup"><span data-stu-id="d7319-206">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="d7319-207">Hallo burst-modus iets langer Hallo accu levensduur maar heeft een invloed op Hallo Engagement-Monitor: alle sessies en taken duur zijn afgerond toohello burst drempelwaarde (dus sessies en korter zijn dan Hallo burst drempelwaarde is mogelijk niet zichtbaar taken).</span><span class="sxs-lookup"><span data-stu-id="d7319-207">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="d7319-208">Het is aanbevolen toouse een ' burst ' drempelwaarde niet langer dan 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="d7319-208">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="d7319-209">U hebt toobe Houd er rekening mee dat opgeslagen logboeken zijn beperkt too300-items.</span><span class="sxs-lookup"><span data-stu-id="d7319-209">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="d7319-210">U kunt sommige logboeken verliezen als verzenden te lang is.</span><span class="sxs-lookup"><span data-stu-id="d7319-210">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="d7319-211">Hallo burst drempelwaarde kan niet worden geconfigureerd als tooa periode minder dan 1s.</span><span class="sxs-lookup"><span data-stu-id="d7319-211">hello burst threshold cannot be configured tooa period lesser than 1s.</span></span> <span data-ttu-id="d7319-212">Als u dus toodo probeert, opnieuw Hallo SDK wordt een tracering met Hallo fout weergeven en automatisch toohello standaardwaarde, dat wil zeggen, 0s.</span><span class="sxs-lookup"><span data-stu-id="d7319-212">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, i.e., 0s.</span></span> <span data-ttu-id="d7319-213">Dit activeert Hallo SDK tooreport Hallo Logboeken in realtime.</span><span class="sxs-lookup"><span data-stu-id="d7319-213">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

