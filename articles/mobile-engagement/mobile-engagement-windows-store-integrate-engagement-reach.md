---
title: aaaWindows universele Apps bereiken SDK-integratie
description: Hoe tooIntegrate Azure Mobile Engagement bereiken met universele Windows-Apps
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a31ca1d6-856f-4aec-898a-07969ae5f7ec
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af311c65940014083333853875a00173b8d6783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a><span data-ttu-id="e129e-103">Universele Windows-Apps bereiken SDK-integratie</span><span class="sxs-lookup"><span data-stu-id="e129e-103">Windows Universal Apps Reach SDK Integration</span></span>
<span data-ttu-id="e129e-104">U moet volgen Hallo integratie procedure wordt beschreven in Hallo [Windows universele Engagement SDK-integratie](mobile-engagement-windows-store-integrate-engagement.md) voordat u deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="e129e-104">You must follow hello integration procedure described in hello [Windows Universal Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a><span data-ttu-id="e129e-105">Hallo Engagement bereiken SDK in uw universele Windows-project insluiten</span><span class="sxs-lookup"><span data-stu-id="e129e-105">Embed hello Engagement Reach SDK into your Windows Universal project</span></span>
<span data-ttu-id="e129e-106">U hebt geen iets tooadd.</span><span class="sxs-lookup"><span data-stu-id="e129e-106">You do not have anything tooadd.</span></span> <span data-ttu-id="e129e-107">`EngagementReach`verwijzingen en bronnen bevinden zich al in uw project.</span><span class="sxs-lookup"><span data-stu-id="e129e-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="e129e-108">U kunt afbeeldingen uit Hallo `Resources` map van uw project, met name Hallo merk-pictogram (die standaard toohello Engagement pictogram).</span><span class="sxs-lookup"><span data-stu-id="e129e-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span> <span data-ttu-id="e129e-109">Op universele Apps kunt u ook Hallo verplaatsen `Resources` map op de inhoud ervan tussen apps, maar u hebt gedeeld project-tooshare tookeep hello `Resources\EngagementConfiguration.xml` bestand op de standaardlocatie, omdat deze afhankelijk platform.</span><span class="sxs-lookup"><span data-stu-id="e129e-109">On Universal Apps you can also move hello `Resources` folder on your shared project tooshare its content between apps, but you will have tookeep hello `Resources\EngagementConfiguration.xml` file on its default location as it is platform dependent.</span></span>
> 
> 

## <a name="enable-hello-windows-notification-service"></a><span data-ttu-id="e129e-110">Hallo Windows Notification Service inschakelen</span><span class="sxs-lookup"><span data-stu-id="e129e-110">Enable hello Windows Notification Service</span></span>
### <a name="windows-8x-and-windows-phone-81-only"></a><span data-ttu-id="e129e-111">Windows 8.x en Windows Phone 8.1 alleen</span><span class="sxs-lookup"><span data-stu-id="e129e-111">Windows 8.x and Windows Phone 8.1 only</span></span>
<span data-ttu-id="e129e-112">In de volgorde toouse hello **Windows Notification Service** (WNS genoemd) in uw `Package.appxmanifest` -bestand in de `Application UI` klikt u op `All Image Assets` in Hallo links bot vak.</span><span class="sxs-lookup"><span data-stu-id="e129e-112">In order toouse hello **Windows Notification Service** (referred as WNS) in your `Package.appxmanifest` file on `Application UI` click on `All Image Assets` in hello left bot box.</span></span> <span data-ttu-id="e129e-113">Op Hallo van Hallo vak in `Notifications`, wijzigen `toast capable` van `(not set)` te`(Yes)`.</span><span class="sxs-lookup"><span data-stu-id="e129e-113">At hello right of hello box in `Notifications`, change `toast capable` from `(not set)` too`(Yes)`.</span></span>

### <a name="all-platforms"></a><span data-ttu-id="e129e-114">Alle platforms</span><span class="sxs-lookup"><span data-stu-id="e129e-114">All platforms</span></span>
<span data-ttu-id="e129e-115">U moet uw app tooyour Microsoft-account en toohello engagement-platform toosynchronize.</span><span class="sxs-lookup"><span data-stu-id="e129e-115">You need toosynchronize your app tooyour Microsoft account and toohello engagement platform.</span></span> <span data-ttu-id="e129e-116">Voor deze toocreate een account of u aanmelden [windows-ontwikkelaarscentrum](https://dev.windows.com).</span><span class="sxs-lookup"><span data-stu-id="e129e-116">For this you need toocreate an account or log on [windows dev center](https://dev.windows.com).</span></span> <span data-ttu-id="e129e-117">Nadat een nieuwe toepassing maken en vinden Hallo SID en de geheime sleutel.</span><span class="sxs-lookup"><span data-stu-id="e129e-117">After that create a new application and find hello SID and secret key.</span></span> <span data-ttu-id="e129e-118">Ga op uw app-instelling in op Hallo engagement front-end `native push` en plak uw referenties.</span><span class="sxs-lookup"><span data-stu-id="e129e-118">On hello engagement frontend, go on your app setting in `native push` and paste your credentials.</span></span> <span data-ttu-id="e129e-119">Hierna, klik met de rechtermuisknop op uw project, selecteer `store` en `Associate App with hello Store...`.</span><span class="sxs-lookup"><span data-stu-id="e129e-119">After that, right click on your project, select `store` and `Associate App with hello Store...`.</span></span> <span data-ttu-id="e129e-120">U hoeft alleen maar tooselect Hallo toepassing u hebt dit hebt gemaakt voordat toosynchronize.</span><span class="sxs-lookup"><span data-stu-id="e129e-120">You just need tooselect hello application you have create before toosynchronize it.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="e129e-121">Hallo Engagement bereiken SDK initialiseren</span><span class="sxs-lookup"><span data-stu-id="e129e-121">Initialize hello Engagement Reach SDK</span></span>
<span data-ttu-id="e129e-122">Hallo wijzigen `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="e129e-122">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="e129e-123">Invoegen `EngagementReach.Instance.Init` vlak na `EngagementAgent.Instance.Init` in uw `InitEngagement` methode:</span><span class="sxs-lookup"><span data-stu-id="e129e-123">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in your `InitEngagement` method:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  <span data-ttu-id="e129e-124">Hallo `EngagementReach.Instance.Init` in een specifieke thread wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e129e-124">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="e129e-125">U hebt geen toodo deze zelf.</span><span class="sxs-lookup"><span data-stu-id="e129e-125">You do not have toodo it yourself.</span></span>

> [!NOTE]
> <span data-ttu-id="e129e-126">Als u pushmeldingen elders in uw toepassing is er te[delen van het kanaal push](#push-channel-sharing) met Engagement bereiken.</span><span class="sxs-lookup"><span data-stu-id="e129e-126">If you are using push notifications elsewhere in your application then you have too[share your push channel](#push-channel-sharing) with Engagement Reach.</span></span>
> 
> 

## <a name="integration"></a><span data-ttu-id="e129e-127">Integratie</span><span class="sxs-lookup"><span data-stu-id="e129e-127">Integration</span></span>
<span data-ttu-id="e129e-128">Engagement biedt twee manieren tooadd Hallo Reach in-app-banner en verspreide weergaven voor aankondigingen en polls in uw toepassing: Hallo overlay-integratie en handmatige integratie met weergaven Hallo het web.</span><span class="sxs-lookup"><span data-stu-id="e129e-128">Engagement provides two ways tooadd hello Reach in-app banners and interstitial views for announcements and polls in your application: hello overlay integration and hello web views manual integration.</span></span> <span data-ttu-id="e129e-129">U moet beide benadering op Hallo niet combineren dezelfde pagina.</span><span class="sxs-lookup"><span data-stu-id="e129e-129">You should not combine both approach on hello same page.</span></span>

<span data-ttu-id="e129e-130">Hallo keuze tussen de twee integratie Hallo kan op deze manier worden samengevat:</span><span class="sxs-lookup"><span data-stu-id="e129e-130">hello choice between hello two integration could be summarized this way:</span></span>

* <span data-ttu-id="e129e-131">U kunt ervoor kiezen Hallo overlay-integratie als uw pagina's al overneemt van Hallo Agent `EngagementPage`, het is alleen een kwestie van het vervangen van `EngagementPage` door `EngagementPageOverlay` en `xmlns:engagement="using:Microsoft.Azure.Engagement"` door `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in uw pagina's.</span><span class="sxs-lookup"><span data-stu-id="e129e-131">You may choose hello overlay integration if your pages already inherits from hello Agent `EngagementPage`, it's just a matter of replacing `EngagementPage` by `EngagementPageOverlay` and `xmlns:engagement="using:Microsoft.Azure.Engagement"` by `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in your pages.</span></span>
* <span data-ttu-id="e129e-132">U kunt handmatig integratie met het Hallo web weergaven als u wilt dat tooprecisely plaats Hallo UI bereiken in de pagina's of als u niet dat tooadd wilt een andere overname niveau tooyour pagina's.</span><span class="sxs-lookup"><span data-stu-id="e129e-132">You may choose hello web views manual integration if you want tooprecisely place hello Reach UI within your pages or if you don't want tooadd another inheritance level tooyour pages.</span></span> 

### <a name="overlay-integration"></a><span data-ttu-id="e129e-133">Overlay-integratie</span><span class="sxs-lookup"><span data-stu-id="e129e-133">Overlay integration</span></span>
<span data-ttu-id="e129e-134">Hallo Engagement overlay worden dynamisch toegevoegd Hallo UI-elementen toodisplay Reach-campagnes gebruikt in uw pagina.</span><span class="sxs-lookup"><span data-stu-id="e129e-134">hello Engagement overlay dynamically adds hello UI elements used toodisplay Reach campaigns in your page.</span></span> <span data-ttu-id="e129e-135">Als het Hallo-overlay niet aan de behoeften van uw lay-out moet u Hallo webweergaven handmatige integratie in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="e129e-135">If hello overlay doesn't suit your layout you should consider hello web views manual integration instead.</span></span>

<span data-ttu-id="e129e-136">In het .xaml-bestandswijziging `EngagementPage` te verwijzen`EngagementPageOverlay`</span><span class="sxs-lookup"><span data-stu-id="e129e-136">In your .xaml file change `EngagementPage` reference too`EngagementPageOverlay`</span></span>

* <span data-ttu-id="e129e-137">Tooyour naamruimtedeclaraties toevoegen:</span><span class="sxs-lookup"><span data-stu-id="e129e-137">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* <span data-ttu-id="e129e-138">Vervang `engagement:EngagementPage` met `engagement:EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="e129e-138">Replace `engagement:EngagementPage` with `engagement:EngagementPageOverlay`:</span></span>

<span data-ttu-id="e129e-139">**Met EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="e129e-139">**With EngagementPage:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

<span data-ttu-id="e129e-140">**Met EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="e129e-140">**With EngagementPageOverlay:**</span></span>

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

<span data-ttu-id="e129e-141">Klik in het bestand .cs tag uw pagina in `EngagementPageOverlay` in plaats van `EngagementPage` en importeer `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="e129e-141">Then in your .cs file tag your page in `EngagementPageOverlay` instead of `EngagementPage` and import `Microsoft.Azure.Engagement.Overlay`.</span></span>

            using Microsoft.Azure.Engagement.Overlay;

* <span data-ttu-id="e129e-142">Vervang `EngagementPage` met `EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="e129e-142">Replace `EngagementPage` with `EngagementPageOverlay`:</span></span>

<span data-ttu-id="e129e-143">**Met EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="e129e-143">**With EngagementPage:**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

<span data-ttu-id="e129e-144">**Met EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="e129e-144">**With EngagementPageOverlay:**</span></span>

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


<span data-ttu-id="e129e-145">Hallo Engagement overlay voegt een `Grid` element boven op de pagina bestaat uit de indeling en Hallo twee `WebView` elementen één voor Hallo banner en andere één voor verspreide weergave Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="e129e-145">hello Engagement overlay adds a `Grid` element on top of your page composed of your layout and hello two `WebView` elements one for hello banner and hello other one for hello interstitial view.</span></span>

<span data-ttu-id="e129e-146">U kunt aanpassen Hallo overlay elementen rechtstreeks in Hallo `EngagementPageOverlay.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="e129e-146">You can customize hello overlay elements directly in hello `EngagementPageOverlay.cs` file.</span></span>

### <a name="web-views-manual-integration"></a><span data-ttu-id="e129e-147">Handmatige integratie met het web weergaven</span><span class="sxs-lookup"><span data-stu-id="e129e-147">Web views manual integration</span></span>
<span data-ttu-id="e129e-148">Reach zoeken op de pagina's voor Hallo twee naar `WebView` elementen die verantwoordelijk is voor het weergeven van Hallo banner en Hallo verspreide weergeven.</span><span class="sxs-lookup"><span data-stu-id="e129e-148">Reach will be searching your pages for hello two `WebView` elements responsible for displaying hello banner and hello interstitial view.</span></span> <span data-ttu-id="e129e-149">Hallo alleen dat u hoeft toodo tooadd is deze twee `WebView` elementen ergens in de pagina's, Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e129e-149">hello only thing you have toodo is tooadd those two `WebView` elements somewhere in your pages, here is an example:</span></span>

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


<span data-ttu-id="e129e-150">In dit voorbeeld Hallo `WebView` elementen zijn gespreide toofit hun container die automatisch opnieuw groottes in geval van een scherm worden gedraaid of venster grootte wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e129e-150">In this example hello `WebView` elements are stretched toofit their container which automatically re-sizes them in case of screen rotation or window size change.</span></span>

> [!WARNING]
> <span data-ttu-id="e129e-151">Het is belangrijk tookeep Hallo dezelfde naming `engagement_notification_content` en `engagement_announcement_content` voor Hallo `WebView` elementen.</span><span class="sxs-lookup"><span data-stu-id="e129e-151">It is important tookeep hello same naming `engagement_notification_content` and `engagement_announcement_content` for hello `WebView` elements.</span></span> <span data-ttu-id="e129e-152">Reach is identificeren met hun naam.</span><span class="sxs-lookup"><span data-stu-id="e129e-152">Reach is identifying them by their name.</span></span> 
> 
> 

## <a name="handle-datapush-optional"></a><span data-ttu-id="e129e-153">Ingang datapush (optioneel)</span><span class="sxs-lookup"><span data-stu-id="e129e-153">Handle datapush (optional)</span></span>
<span data-ttu-id="e129e-154">Als u wilt dat uw toepassing toobe kunnen tooreceive Reach gegevens-pushes, hebt u twee gebeurtenissen tooimplement Hallo EngagementReach klasse:</span><span class="sxs-lookup"><span data-stu-id="e129e-154">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

<span data-ttu-id="e129e-155">Voeg in App.xaml.cs in Hallo App() constructor toe:</span><span class="sxs-lookup"><span data-stu-id="e129e-155">In App.xaml.cs in hello App() constructor add:</span></span>

            EngagementReach.Instance.DataPushStringReceived += (body) =>
            {
              Debug.WriteLine("String data push message received: " + body);
              return true;
            };

            EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
            {
              Debug.WriteLine("Base64 data push message received: " + encodedBody);
              // Do something useful with decodedBody like updating an image view
              return true;
            };

<span data-ttu-id="e129e-156">U ziet dat Hallo retouraanroep van elke methode retourneert een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="e129e-156">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="e129e-157">Engagement verzendt een feedback tooits back-end na het verzenden van gegevens-push Hallo.</span><span class="sxs-lookup"><span data-stu-id="e129e-157">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="e129e-158">Als het Hallo-callback false retourneert, Hallo `exit` feedback verzenden zijn.</span><span class="sxs-lookup"><span data-stu-id="e129e-158">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="e129e-159">Anders moeten `action`.</span><span class="sxs-lookup"><span data-stu-id="e129e-159">Otherwise, it will be `action`.</span></span> <span data-ttu-id="e129e-160">Als geen retouraanroep is ingesteld op Hallo gebeurtenissen, Hallo `drop` feedback tooEngagement worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="e129e-160">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="e129e-161">Engagement is niet kunnen tooreceive veelvouden feedback voor een gegevens-push.</span><span class="sxs-lookup"><span data-stu-id="e129e-161">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="e129e-162">Als u van plan tooset verschillende handlers een gebeurtenis bent, houd er rekening mee dat Hallo feedback toohello het laatst werd verzonden overeenkomen worden.</span><span class="sxs-lookup"><span data-stu-id="e129e-162">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="e129e-163">In dit geval wordt aangeraden tooalways retourneert dezelfde waarde tooavoid verwarrend feedback over voor front-Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="e129e-163">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="e129e-164">Aanpassen van de gebruikersinterface (optioneel)</span><span class="sxs-lookup"><span data-stu-id="e129e-164">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="e129e-165">Eerste stap</span><span class="sxs-lookup"><span data-stu-id="e129e-165">First step</span></span>
<span data-ttu-id="e129e-166">We laten toocustomize Hallo reach gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="e129e-166">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="e129e-167">toodo geval is, hebt u toocreate een subklasse van Hallo `EngagementReachHandler` klasse.</span><span class="sxs-lookup"><span data-stu-id="e129e-167">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="e129e-168">**Voorbeeld van Code:**</span><span class="sxs-lookup"><span data-stu-id="e129e-168">**Sample Code :**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

<span data-ttu-id="e129e-169">Vervolgens stelt u inhoud Hallo Hallo `EngagementReach.Instance.Handler` veld met het aangepaste object in uw `App.xaml.cs` klasse binnen de Hallo `App()` methode.</span><span class="sxs-lookup"><span data-stu-id="e129e-169">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `App()` method.</span></span>

<span data-ttu-id="e129e-170">**Voorbeeld van Code:**</span><span class="sxs-lookup"><span data-stu-id="e129e-170">**Sample Code :**</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> <span data-ttu-id="e129e-171">Engagement maakt standaard gebruik van een eigen implementatie van `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="e129e-171">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span>
> <span data-ttu-id="e129e-172">U hebt geen toocreate zelf, en als u doet dit, hebt u niet toooverride elke methode.</span><span class="sxs-lookup"><span data-stu-id="e129e-172">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="e129e-173">Hallo standaardgedrag is tooselect Hallo Engagement basisobject.</span><span class="sxs-lookup"><span data-stu-id="e129e-173">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="web-view"></a><span data-ttu-id="e129e-174">Webweergave</span><span class="sxs-lookup"><span data-stu-id="e129e-174">Web View</span></span>
<span data-ttu-id="e129e-175">Standaard Reach Hallo ingesloten resources van Hallo DLL toodisplay Hallo meldingen en pagina's gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e129e-175">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="e129e-176">een volledige tooprovide mogelijkheden voor aanpassing we alleen webweergave gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e129e-176">tooprovide a full customization possibilities we only use web view.</span></span> <span data-ttu-id="e129e-177">Als u toocustomize indelingen wilt, overschrijven rechtstreeks Hallo resources bestanden `EngagementAnnouncement.html` en `EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="e129e-177">If you want toocustomize layouts, override directly hello resources files `EngagementAnnouncement.html` and `EngagementNotification.html`.</span></span> <span data-ttu-id="e129e-178">Engagement moet alle code in `<body></body>` toorun correct.</span><span class="sxs-lookup"><span data-stu-id="e129e-178">Engagement needs all code in `<body></body>` toorun correctly.</span></span> <span data-ttu-id="e129e-179">Maar u kunt de buitenste tag toevoegen `engagement_webview_area`.</span><span class="sxs-lookup"><span data-stu-id="e129e-179">But you can add tag outer `engagement_webview_area`.</span></span>

<span data-ttu-id="e129e-180">Echter, kunt u beslissen toouse uw eigen resources.</span><span class="sxs-lookup"><span data-stu-id="e129e-180">However, you can decide toouse your own resources.</span></span>

<span data-ttu-id="e129e-181">U kunt onderdrukken `EngagementReachHandler` methoden in uw subklasse tootell Engagement toouse uw indelingen, maar maken gebruik van voorzichtig tooembedded Hallo engagement mechanisme:</span><span class="sxs-lookup"><span data-stu-id="e129e-181">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts, but take care tooembedded hello engagement mechanism:</span></span>

<span data-ttu-id="e129e-182">**Voorbeeld van Code:**</span><span class="sxs-lookup"><span data-stu-id="e129e-182">**Sample Code :**</span></span>

            // In your subclass of EngagementReachHandler

            public override string GetAnnouncementHTML()
            {
              return base.GetAnnouncementHTML();
            }
            public override string GetAnnouncementName()
            {
              return base.GetAnnouncementName();
            }
            public override string GetNotfificationHTML()
            {
              return base.GetNotfificationHTML();
            }
            public override string GetNotfificationName()
            {
              return base.GetNotfificationName();
            }


<span data-ttu-id="e129e-183">AnnouncementHTML is standaard `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span><span class="sxs-lookup"><span data-stu-id="e129e-183">By default, AnnouncementHTML is `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span></span> <span data-ttu-id="e129e-184">Hiermee geeft u de Hallo HTML-bestand dat ontwerpen Hallo inhoud van een pushbericht (tekst aankondiging, Web anoucement en Poll aankondiging).</span><span class="sxs-lookup"><span data-stu-id="e129e-184">It represents hello html file that design hello content of a push message (Text announcement, Web anoucement and Poll announcement).</span></span> <span data-ttu-id="e129e-185">AnnouncementName is `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="e129e-185">AnnouncementName is `engagement_announcement_content`.</span></span> <span data-ttu-id="e129e-186">Dit is de naam Hallo van Hallo webweergave ontwerp in uw xaml-pagina.</span><span class="sxs-lookup"><span data-stu-id="e129e-186">It is hello name of hello webview design in your xaml page.</span></span>

<span data-ttu-id="e129e-187">NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="e129e-187">NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`.</span></span> <span data-ttu-id="e129e-188">Hiermee geeft u de Hallo HTML-bestand dat ontwerpen Hallo melding van een pushbericht.</span><span class="sxs-lookup"><span data-stu-id="e129e-188">It represents hello html file that design hello notification of a push message.</span></span> <span data-ttu-id="e129e-189">NotfificationName is `engagement_notification_content`.</span><span class="sxs-lookup"><span data-stu-id="e129e-189">NotfificationName is `engagement_notification_content`.</span></span> <span data-ttu-id="e129e-190">Dit is de naam Hallo van Hallo webweergave ontwerp in uw xaml-pagina.</span><span class="sxs-lookup"><span data-stu-id="e129e-190">It is hello name of hello webview design in your xaml page.</span></span>

### <a name="customization"></a><span data-ttu-id="e129e-191">Aanpassing</span><span class="sxs-lookup"><span data-stu-id="e129e-191">Customization</span></span>
<span data-ttu-id="e129e-192">U kunt de melding en aankondiging webweergave is dat u wilt dat als u Engagement object behouden aanpassen.</span><span class="sxs-lookup"><span data-stu-id="e129e-192">You can customize notification and announcement web view has you want if you preserve Engagement object.</span></span> <span data-ttu-id="e129e-193">Wees voorzichtig webweergave-object is beschreven driemaal - hello eerst in de xaml tweede tijdstip in uw bestand .cs in Hallo 'setwebview()' methode en het derde periode in Hallo HTML-bestand.</span><span class="sxs-lookup"><span data-stu-id="e129e-193">Take care that webview object is described three times - hello first time in your xaml, second time in your .cs file in hello "setwebview()" method, and third time in hello html file.</span></span>

* <span data-ttu-id="e129e-194">In de xaml beschrijft u Hallo huidige grafische indeling webweergave onderdeel.</span><span class="sxs-lookup"><span data-stu-id="e129e-194">In your xaml you describe hello current graphical layout webview component.</span></span>
* <span data-ttu-id="e129e-195">U kunt in uw bestand .cs 'setwebview()' waarin u Hallo dimensie van de twee webweergave hello (melding, aankondiging) instellen definiëren.</span><span class="sxs-lookup"><span data-stu-id="e129e-195">In your .cs file you can define "setwebview()" in which you set hello dimension of hello two webview (notification, announcement).</span></span> <span data-ttu-id="e129e-196">Het is zeer effectief zijn wanneer het formaat van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="e129e-196">It is very effective when hello application is resizing.</span></span>
* <span data-ttu-id="e129e-197">In Hallo Engagement HTML-bestand we beschrijven Hallo webweergave inhoud, ontwerpen en Hallo elementen posities tussen elkaar.</span><span class="sxs-lookup"><span data-stu-id="e129e-197">In hello Engagement html file we describe hello webview content, design and hello elements positions between each other.</span></span>

### <a name="launch-message"></a><span data-ttu-id="e129e-198">Bericht starten</span><span class="sxs-lookup"><span data-stu-id="e129e-198">Launch message</span></span>
<span data-ttu-id="e129e-199">Wanneer een gebruiker klikt op een Systeemmelding (een pop-up), Engagement Hallo toepassing wordt gestart, load Hallo inhoud Hallo push berichten en Hallo-pagina voor de bijbehorende campagne Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e129e-199">When a user clicks on a system notification (a toast), Engagement launches hello application, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="e129e-200">Er is een vertraging tussen Hallo starten van de toepassing en Hallo beeldscherm Hallo van Hallo pagina (afhankelijk van de Hallo snelheid van uw netwerk).</span><span class="sxs-lookup"><span data-stu-id="e129e-200">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="e129e-201">gebruiker toohello tooindicate dat er iets wordt geladen, moet u een visuele gegevens, zoals een voortgangsbalk zien of een voortgangsindicator opgeven.</span><span class="sxs-lookup"><span data-stu-id="e129e-201">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="e129e-202">Engagement kan niet worden verwerkt, maar enkele handlers voor u biedt.</span><span class="sxs-lookup"><span data-stu-id="e129e-202">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="e129e-203">tooimplement hello retouraanroep in App.xaml.cs in "Openbare App() {}" toevoegen:</span><span class="sxs-lookup"><span data-stu-id="e129e-203">tooimplement hello callback, in App.xaml.cs in "Public App(){}" add:</span></span>

            /* hello application has launched and hello content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* hello application has finished loading hello content and hello page
             * is about toobe displayed.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* hello content has been loaded, but an error has occurred.
             * You can provide an information toohello user.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="e129e-204">U kunt Hallo callback instellen in de methode 'Openbare App() {}' van uw `App.xaml.cs` -bestand, bij voorkeur voor Hallo `EngagementReach.Instance.Init()` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="e129e-204">You can set hello callback in your "Public App(){}" method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="e129e-205">Elke handler wordt aangeroepen door Hallo UI Thread.</span><span class="sxs-lookup"><span data-stu-id="e129e-205">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="e129e-206">U hoeft geen tooworry wanneer u een MessageBox of iets UI-gerelateerde.</span><span class="sxs-lookup"><span data-stu-id="e129e-206">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

## <span data-ttu-id="e129e-207"><a id="push-channel-sharing"></a>Push-kanaal voor delen</span><span class="sxs-lookup"><span data-stu-id="e129e-207"><a id="push-channel-sharing"></a> Push channel sharing</span></span>
<span data-ttu-id="e129e-208">Als u pushmeldingen voor een ander doel in uw toepassing hebt u toouse Hallo push kanaal functie Hallo Engagement SDK voor het delen.</span><span class="sxs-lookup"><span data-stu-id="e129e-208">If you are using push notifications for another purpose in your application then you have toouse hello push channel sharing feature of hello Engagement SDK.</span></span> <span data-ttu-id="e129e-209">Dit is tooavoid gemist push.</span><span class="sxs-lookup"><span data-stu-id="e129e-209">This is tooavoid missed push.</span></span>

* <span data-ttu-id="e129e-210">U kunt uw eigen push toohello Engagement bereiken initialisatie van een kanaal op te geven.</span><span class="sxs-lookup"><span data-stu-id="e129e-210">You can provide your own push channel toohello Engagement Reach initialization.</span></span> <span data-ttu-id="e129e-211">Hallo SDK wordt gebruikt in plaats van een nieuwe aanvragen.</span><span class="sxs-lookup"><span data-stu-id="e129e-211">hello SDK will use it instead of requesting a new one.</span></span>

<span data-ttu-id="e129e-212">Hallo Engagement bereiken initialisatie bijwerken met het kanaal push in Hallo `InitEngagement` methode van Hallo `App.xaml.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="e129e-212">Update hello Engagement Reach initialization with your push channel in hello `InitEngagement` method from hello `App.xaml.cs` file:</span></span>

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* <span data-ttu-id="e129e-213">U kunt ook als u alleen wilt tooconsume Hallo push-kanaal na de initialisatie van de Reach Hallo en vervolgens kunt u een retouraanroep instellen op Engagement bereiken tooget Hallo push kanaal eenmaal is gemaakt door Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="e129e-213">Alternatively, if you just want tooconsume hello push channel after hello Reach initialization then you can set a callback on Engagement Reach tooget hello push channel once it is created by hello SDK.</span></span>

<span data-ttu-id="e129e-214">De retouraanroep ingesteld op een willekeurige plaats **nadat** Reach-initialisatie Hallo:</span><span class="sxs-lookup"><span data-stu-id="e129e-214">Set your callback at any place **after** hello Reach initialization :</span></span>

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a><span data-ttu-id="e129e-215">Aangepaste schema tip</span><span class="sxs-lookup"><span data-stu-id="e129e-215">Custom scheme tip</span></span>
<span data-ttu-id="e129e-216">We bieden gebruik van aangepaste schema.</span><span class="sxs-lookup"><span data-stu-id="e129e-216">We provide custom scheme use.</span></span> <span data-ttu-id="e129e-217">U kunt verschillende type URI verzenden van engagement frontend toobe gebruikt in de engagement-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e129e-217">You can send different type of URI from engagement frontend toobe used in your engagement application.</span></span> <span data-ttu-id="e129e-218">Standaardschema zoals `http, ftp, ...` zijn beheren in Windows, met een venster wordt gevraagd als ze geen standaardtoepassing op apparaat geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e129e-218">Default scheme like `http, ftp, ...` are manage by Windows, a window will prompt if they are no default application installed on device.</span></span> <span data-ttu-id="e129e-219">U kunt ook uw eigen aangepaste schema maken voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="e129e-219">You can also create your own custom scheme for your application.</span></span>

<span data-ttu-id="e129e-220">Hallo op eenvoudige wijze tooset een aangepast schema in uw toepassing is tooopen uw `Package.appxmanifest` Ga in `Declarations` Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="e129e-220">hello simple way tooset a custom scheme in your application is tooopen your `Package.appxmanifest` go in `Declarations` panel.</span></span> <span data-ttu-id="e129e-221">Selecteer `Protocol` in Hallo beschikbaar declaraties Schuif vak en toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="e129e-221">Select `Protocol` in hello Available Declarations scroll box and add it.</span></span> <span data-ttu-id="e129e-222">Hallo bewerken `Name` veld met uw nieuwe protocol de gewenste naam.</span><span class="sxs-lookup"><span data-stu-id="e129e-222">Edit hello `Name` field with your new protocol desired name.</span></span>

<span data-ttu-id="e129e-223">Nu toouse dit protocol bewerken uw `App.xaml.cs` Hello `OnActivated` methode en vergeet niet tooinitialize engagement hier ook:</span><span class="sxs-lookup"><span data-stu-id="e129e-223">Now toouse this protocol, edit your `App.xaml.cs` with hello `OnActivated` method, and don't forget tooinitialize engagement here also:</span></span>

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action toodo when app is launch

              #region Custom scheme use
              if (args.Kind == ActivationKind.Protocol)
              {
                ProtocolActivatedEventArgs myProtocol = (ProtocolActivatedEventArgs)args;

                if (myProtocol.Uri.Scheme.Equals("protocolName"))
                {
                  string path = myProtocol.Uri.AbsolutePath;
                }
              }
              #endregion

