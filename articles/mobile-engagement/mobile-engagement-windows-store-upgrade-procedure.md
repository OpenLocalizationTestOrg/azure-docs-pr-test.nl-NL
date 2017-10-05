---
title: Upgradeprocedures van Windows universele Apps SDK
description: Upgradeprocedures van Windows universele Apps SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 4c898175-2cd6-43db-b350-bb408332f24d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: fe85a99a92fb39082cafe7422b356de1f20f14bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="69e1b-103">Upgradeprocedures van Windows universele Apps SDK</span><span class="sxs-lookup"><span data-stu-id="69e1b-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="69e1b-104">Als u hebt al een oudere versie van Engagement geïntegreerd in uw toepassing, hebt u de volgende punten overwegen bij het upgraden van de SDK.</span><span class="sxs-lookup"><span data-stu-id="69e1b-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="69e1b-105">U moet verschillende procedures volgen als u verschillende versies van de SDK hebt gemist.</span><span class="sxs-lookup"><span data-stu-id="69e1b-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="69e1b-106">Bijvoorbeeld als u migreert van 0.10.1 naar u moet eerst Volg de procedure 'van 0.9.0 naar 0.10.1' 0.11.0 vervolgens de procedure 'van 0.10.1 naar 0.11.0'.</span><span class="sxs-lookup"><span data-stu-id="69e1b-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-330-to-340"></a><span data-ttu-id="69e1b-107">Van 3.3.0 naar 3.4.0</span><span class="sxs-lookup"><span data-stu-id="69e1b-107">From 3.3.0 to 3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="69e1b-108">Test-Logboeken</span><span class="sxs-lookup"><span data-stu-id="69e1b-108">Test logs</span></span>
<span data-ttu-id="69e1b-109">De logboeken van de console die wordt geproduceerd door de SDK kunnen worden ingeschakeld/uitgeschakeld/gefilterd.</span><span class="sxs-lookup"><span data-stu-id="69e1b-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="69e1b-110">Werk de eigenschap voor het aanpassen van dit `EngagementAgent.Instance.TestLogEnabled` op een van de waarde in de `EngagementTestLogLevel` opsomming, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="69e1b-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="69e1b-111">Resources</span><span class="sxs-lookup"><span data-stu-id="69e1b-111">Resources</span></span>
<span data-ttu-id="69e1b-112">De Reach-overlay is verbeterd.</span><span class="sxs-lookup"><span data-stu-id="69e1b-112">The Reach overlay has been improved.</span></span> <span data-ttu-id="69e1b-113">Het uitmaakt deel van de resources SDK NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="69e1b-113">It is part of the SDK NuGet package resources.</span></span>

<span data-ttu-id="69e1b-114">Tijdens een upgrade uitvoeren naar de nieuwe versie van de SDK u kiezen kunt of u behouden van de bestaande bestanden uit de overlay-map van uw resources wilt of niet:</span><span class="sxs-lookup"><span data-stu-id="69e1b-114">While upgrading to the new version of the SDK you can choose whether you want to keep your existing files from the overlay folder of your resources or not:</span></span>

* <span data-ttu-id="69e1b-115">Als de vorige overlay u werkt of u integreert de `WebView` elementen handmatig vervolgens u bepalen kunt om uw bestaande bestanden te houden, er nog steeds werken.</span><span class="sxs-lookup"><span data-stu-id="69e1b-115">If the previous overlay is working for you or you are integrating the `WebView` elements manually then you can decide to keep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="69e1b-116">Als u bijwerken naar de nieuwe overlay wilt, vervangt het gehele `overlay` map van uw resources met de nieuwe versie van de SDK-pakket (UWP-apps: na de upgrade kunt u de nieuwe map in de overlay ophalen van % USERPROFILE %\\.nuget\packages\ MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span><span class="sxs-lookup"><span data-stu-id="69e1b-116">If you want to update to the new overlay, just replace the whole `overlay` folder from your resources with the new one from the SDK package (UWP apps: after the upgrade, you can get the new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="69e1b-117">Met behulp van de nieuwe overlay overschrijft aanpassingen op de vorige versie.</span><span class="sxs-lookup"><span data-stu-id="69e1b-117">Using the new overlay will overwrite any customizations made on the previous version.</span></span>
> 
> 

## <a name="from-320-to-330"></a><span data-ttu-id="69e1b-118">Van 3.2.0 naar 3.3.0</span><span class="sxs-lookup"><span data-stu-id="69e1b-118">From 3.2.0 to 3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="69e1b-119">Resources</span><span class="sxs-lookup"><span data-stu-id="69e1b-119">Resources</span></span>
<span data-ttu-id="69e1b-120">Deze stap betreft alleen de aangepaste resources.</span><span class="sxs-lookup"><span data-stu-id="69e1b-120">This step concerns customized resources only.</span></span> <span data-ttu-id="69e1b-121">Als u de resources die worden geleverd door de SDK (html, afbeeldingen, overlay) hebt aangepast hebt u deze back-up voordat u de upgrade en pas uw aanpassingen op bijgewerkte bronnen.</span><span class="sxs-lookup"><span data-stu-id="69e1b-121">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-to-320"></a><span data-ttu-id="69e1b-122">Van 3.1.0 naar 3.2.0</span><span class="sxs-lookup"><span data-stu-id="69e1b-122">From 3.1.0 to 3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="69e1b-123">Resources</span><span class="sxs-lookup"><span data-stu-id="69e1b-123">Resources</span></span>
<span data-ttu-id="69e1b-124">Deze stap betreft alleen de aangepaste resources.</span><span class="sxs-lookup"><span data-stu-id="69e1b-124">This step concerns customized resources only.</span></span> <span data-ttu-id="69e1b-125">Als u de resources die worden geleverd door de SDK (html, afbeeldingen, overlay) hebt aangepast hebt u deze back-up voordat u de upgrade en pas uw aanpassingen op bijgewerkte bronnen.</span><span class="sxs-lookup"><span data-stu-id="69e1b-125">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="69e1b-126">Webweergave-integratie</span><span class="sxs-lookup"><span data-stu-id="69e1b-126">Webview integration</span></span>
<span data-ttu-id="69e1b-127">Enkele verbeteringen aan verschillende apparaten vormfactoren zijn geïntroduceerd in deze versie.</span><span class="sxs-lookup"><span data-stu-id="69e1b-127">Some improvements to match different device form factors were introduced in this version.</span></span> <span data-ttu-id="69e1b-128">Zorg ervoor dat de integratie van de webweergave overeenkomen met het volgende:</span><span class="sxs-lookup"><span data-stu-id="69e1b-128">Make sure that your integration of the webview match the following:</span></span>

<span data-ttu-id="69e1b-129">In uw pagina-(XAML):</span><span class="sxs-lookup"><span data-stu-id="69e1b-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="69e1b-130">En in uw bestand gekoppeld .cs:</span><span class="sxs-lookup"><span data-stu-id="69e1b-130">And in your associated .cs file:</span></span>

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated to within a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

              #region to implement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update the webview when the app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update the webview when the app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure to detach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are the current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements to the correct size.
              /// </summary>
              /// <param name="width">The width of your current display.</param>
              /// <param name="height">The height of your current display.</param>
              private void SetWebView(double width, double height)
              {
                #pragma warning disable 4014
                CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
                        () =>
                        {
                          this.engagement_notification_content.Width = width;
                          this.engagement_announcement_content.Width = width;
                          this.engagement_announcement_content.Height = height;
                        });
              }

              /// <summary>
              /// Handler that takes the Windows.Current.SizeChanged and indicates that webviews have to be resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes the ApplicationView.VisibleBoundsChanged and indicates that webviews have to be resized
              /// </summary>
              /// <param name="sender">The related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-to-300"></a><span data-ttu-id="69e1b-131">Van 2.0.0 naar 3.0.0</span><span class="sxs-lookup"><span data-stu-id="69e1b-131">From 2.0.0 to 3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="69e1b-132">Resources</span><span class="sxs-lookup"><span data-stu-id="69e1b-132">Resources</span></span>
<span data-ttu-id="69e1b-133">Deze stap betreft alleen de aangepaste resources.</span><span class="sxs-lookup"><span data-stu-id="69e1b-133">This step concerns customized resources only.</span></span> <span data-ttu-id="69e1b-134">Als u de resources die worden geleverd door de SDK (html, afbeeldingen, overlay) hebt aangepast hebt u deze back-up voordat u de upgrade en pas uw aanpassingen op bijgewerkte bronnen.</span><span class="sxs-lookup"><span data-stu-id="69e1b-134">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-to-200"></a><span data-ttu-id="69e1b-135">Van 1.1.1 naar 2.0.0</span><span class="sxs-lookup"><span data-stu-id="69e1b-135">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="69e1b-136">De volgende beschrijft het migreren van een SDK-integratie van de service van Capptain SAS Capptain in een app die is aangedreven door Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="69e1b-136">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="69e1b-137">Capptain en Mobile Engagement zijn niet dezelfde services en de procedure die hieronder wordt alleen uitgelegd hoe u voor het migreren van de client-app.</span><span class="sxs-lookup"><span data-stu-id="69e1b-137">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="69e1b-138">Migreren van de SDK in de app wordt niet uw gegevens migreren van de servers Capptain naar de Mobile Engagement-servers</span><span class="sxs-lookup"><span data-stu-id="69e1b-138">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="69e1b-139">Als u vanaf een eerdere versie migreert, raadpleegt u de Capptain-website om te migreren naar 1.1.1 eerst en vervolgens de volgende procedure toepassen</span><span class="sxs-lookup"><span data-stu-id="69e1b-139">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="69e1b-140">Nuget-pakket</span><span class="sxs-lookup"><span data-stu-id="69e1b-140">Nuget package</span></span>
<span data-ttu-id="69e1b-141">Vervang **Capptain.WindowsPhone** door **MicrosoftAzure.MobileEngagement** Nuget-pakket.</span><span class="sxs-lookup"><span data-stu-id="69e1b-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="69e1b-142">Mobile Engagement toepassen</span><span class="sxs-lookup"><span data-stu-id="69e1b-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="69e1b-143">De SDK gebruikt de term `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="69e1b-143">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="69e1b-144">U moet uw project zodat deze overeenkomt met deze wijziging bijwerken.</span><span class="sxs-lookup"><span data-stu-id="69e1b-144">You need to update your project to match this change.</span></span>

<span data-ttu-id="69e1b-145">U moet uw huidige Capptain nuget-pakket te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="69e1b-145">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="69e1b-146">Houd rekening met dat uw wijzigingen in de map Capptain bronnen worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="69e1b-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="69e1b-147">Als u wilt behouden die bestanden vervolgens een kopie maken van deze.</span><span class="sxs-lookup"><span data-stu-id="69e1b-147">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="69e1b-148">Daarna het nieuwe Microsoft Azure Engagement nuget-pakket te installeren op uw project.</span><span class="sxs-lookup"><span data-stu-id="69e1b-148">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="69e1b-149">U vindt deze rechtstreeks op [nuget website].</span><span class="sxs-lookup"><span data-stu-id="69e1b-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="69e1b-150">of hier index.</span><span class="sxs-lookup"><span data-stu-id="69e1b-150">or here index.</span></span> <span data-ttu-id="69e1b-151">Deze bewerking vervangt alle resources bestanden die worden gebruikt door Engagement en voegt u het nieuwe Engagement dll-bestand toe aan de projectverwijzingen.</span><span class="sxs-lookup"><span data-stu-id="69e1b-151">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="69e1b-152">U moet uw projectverwijzingen door Capptain DLL verwijzingen te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="69e1b-152">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="69e1b-153">Als u dit niet doet, wordt de versie van Capptain conflict veroorzaken en fouten gebeurt.</span><span class="sxs-lookup"><span data-stu-id="69e1b-153">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="69e1b-154">Als u Capptain resources hebt aangepast, uw oude bestanden inhoud kopiëren en plak deze in de nieuwe Engagement-bestanden.</span><span class="sxs-lookup"><span data-stu-id="69e1b-154">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="69e1b-155">Houd er rekening mee dat zowel xaml en cs-bestanden moeten worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="69e1b-155">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="69e1b-156">Wanneer deze stappen zijn voltooid. hoeft u alleen oude Capptain verwijzingen door de nieuwe Engagement verwijzingen moeten worden vervangen.</span><span class="sxs-lookup"><span data-stu-id="69e1b-156">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="69e1b-157">Alle Capptain naamruimten moeten worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="69e1b-157">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="69e1b-158">Vóór de migratie:</span><span class="sxs-lookup"><span data-stu-id="69e1b-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="69e1b-159">Na de migratie:</span><span class="sxs-lookup"><span data-stu-id="69e1b-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="69e1b-160">Alle Capptain klassen met 'Capptain' moeten 'Engagement' bevatten.</span><span class="sxs-lookup"><span data-stu-id="69e1b-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="69e1b-161">Vóór de migratie:</span><span class="sxs-lookup"><span data-stu-id="69e1b-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="69e1b-162">Na de migratie:</span><span class="sxs-lookup"><span data-stu-id="69e1b-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="69e1b-163">Voor xaml-bestanden wijzigen Capptain naamruimte en kenmerken ook.</span><span class="sxs-lookup"><span data-stu-id="69e1b-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="69e1b-164">Vóór de migratie:</span><span class="sxs-lookup"><span data-stu-id="69e1b-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="69e1b-165">Na de migratie:</span><span class="sxs-lookup"><span data-stu-id="69e1b-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="69e1b-166">Overlay pagina wijzigingen</span><span class="sxs-lookup"><span data-stu-id="69e1b-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="69e1b-167">Overlay ook gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="69e1b-167">Overlay also changes.</span></span> <span data-ttu-id="69e1b-168">De nieuwe naamruimte is `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="69e1b-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="69e1b-169">Er moet worden gebruikt in xaml- en cs-bestanden.</span><span class="sxs-lookup"><span data-stu-id="69e1b-169">It has to be used in both xaml and cs files.</span></span> <span data-ttu-id="69e1b-170">Bovendien `CapptainGrid` is naam `EngagementGrid`, `capptain_notification_content` en `capptain_announcement_content` zijn benoemde `engagement_notification_content` en `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="69e1b-170">Moreover `CapptainGrid` is to be named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="69e1b-171">Voor de overlay:</span><span class="sxs-lookup"><span data-stu-id="69e1b-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="69e1b-172">Wordt deze:</span><span class="sxs-lookup"><span data-stu-id="69e1b-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="69e1b-173">Voor de andere resources zoals Capptain afbeeldingen en HTML-bestanden, houd er rekening mee dat ze ook zijn gewijzigd voor het gebruik van 'Engagement'.</span><span class="sxs-lookup"><span data-stu-id="69e1b-173">For the other resources like Capptain pictures and HTML files, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="69e1b-174">Project-declaratie</span><span class="sxs-lookup"><span data-stu-id="69e1b-174">Project declaration</span></span>
<span data-ttu-id="69e1b-175">Op Package.appxmanifest `File Type Associations` is bijgewerkt op basis van:</span><span class="sxs-lookup"><span data-stu-id="69e1b-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="69e1b-176">capptain\_bereiken\_inhoud engagement\_bereiken\_inhoud</span><span class="sxs-lookup"><span data-stu-id="69e1b-176">capptain\_reach\_content to engagement\_reach\_content</span></span>
* <span data-ttu-id="69e1b-177">capptain\_logboek\_bestand engagement\_logboek\_bestand</span><span class="sxs-lookup"><span data-stu-id="69e1b-177">capptain\_log\_file to engagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="69e1b-178">Toepassings-ID / SDK-sleutel</span><span class="sxs-lookup"><span data-stu-id="69e1b-178">Application ID / SDK Key</span></span>
<span data-ttu-id="69e1b-179">Engagement maakt gebruik van een verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="69e1b-179">Engagement uses a connection string.</span></span> <span data-ttu-id="69e1b-180">U hoeft niet te geven van een toepassings-ID en een SDK-sleutel met Mobile Engagement, hoeft u een verbindingsreeks opgeven.</span><span class="sxs-lookup"><span data-stu-id="69e1b-180">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="69e1b-181">U kunt deze functie instellen op uw EngagementConfiguration-bestand.</span><span class="sxs-lookup"><span data-stu-id="69e1b-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="69e1b-182">De configuratie van de Engagement kan worden ingesteld in uw `Resources\EngagementConfiguration.xml` -bestand van uw project.</span><span class="sxs-lookup"><span data-stu-id="69e1b-182">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="69e1b-183">Dit bestand op te geven bewerken:</span><span class="sxs-lookup"><span data-stu-id="69e1b-183">Edit this file to specify:</span></span>

* <span data-ttu-id="69e1b-184">De verbindingsreeks voor de toepassing tussen de tags `<connectionString>` en `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="69e1b-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="69e1b-185">Als u in plaats daarvan tijdens runtime opgeven wilt, kunt u de volgende methode voordat de initialisatie van de Engagement-agent kunt aanroepen:</span><span class="sxs-lookup"><span data-stu-id="69e1b-185">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="69e1b-186">De verbindingsreeks voor uw toepassing wordt weergegeven in de klassieke Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="69e1b-186">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="69e1b-187">Wijziging van items</span><span class="sxs-lookup"><span data-stu-id="69e1b-187">Items name change</span></span>
<span data-ttu-id="69e1b-188">Alle items met de naam *capptain* naam hebt gegeven *engagement*.</span><span class="sxs-lookup"><span data-stu-id="69e1b-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="69e1b-189">Op dezelfde manier voor *Capptain* naar *Engagement*.</span><span class="sxs-lookup"><span data-stu-id="69e1b-189">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="69e1b-190">Voorbeelden van veelgebruikte Capptain items:</span><span class="sxs-lookup"><span data-stu-id="69e1b-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="69e1b-191">CapptainConfiguration EngagementConfiguration nu met de naam</span><span class="sxs-lookup"><span data-stu-id="69e1b-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="69e1b-192">CapptainAgent EngagementAgent nu met de naam</span><span class="sxs-lookup"><span data-stu-id="69e1b-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="69e1b-193">CapptainReach EngagementReach nu met de naam</span><span class="sxs-lookup"><span data-stu-id="69e1b-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="69e1b-194">CapptainHttpConfig EngagementHttpConfig nu met de naam</span><span class="sxs-lookup"><span data-stu-id="69e1b-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="69e1b-195">GetCapptainPageName GetEngagementPageName nu met de naam</span><span class="sxs-lookup"><span data-stu-id="69e1b-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="69e1b-196">Houd er rekening mee dat rename ook van invloed op overschreven methoden.</span><span class="sxs-lookup"><span data-stu-id="69e1b-196">Note that rename also affects overridden methods.</span></span>

