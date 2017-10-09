---
title: aaaWindows universele Apps SDK Upgrade Procedures
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
ms.openlocfilehash: 95aba5d55cd65d4190aad35737f872414b5ed443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="abc69-103">Upgradeprocedures van Windows universele Apps SDK</span><span class="sxs-lookup"><span data-stu-id="abc69-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="abc69-104">Als u hebt al een oudere versie van Engagement geïntegreerd in uw toepassing, hebt u tooconsider Hallo volgende punten bij het upgraden van Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="abc69-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="abc69-105">Mogelijk hebt u toofollow verschillende procedures als u verschillende versies van Hallo SDK gemist.</span><span class="sxs-lookup"><span data-stu-id="abc69-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="abc69-106">Bijvoorbeeld als u migreert vanaf 0.10.1 too0.11.0 hebt toofirst Volg Hallo ' van 0.9.0 too0.10.1 ' procedure vervolgens Hallo ' van 0.10.1 too0.11.0 ' procedure.</span><span class="sxs-lookup"><span data-stu-id="abc69-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-330-too340"></a><span data-ttu-id="abc69-107">Van 3.3.0 too3.4.0</span><span class="sxs-lookup"><span data-stu-id="abc69-107">From 3.3.0 too3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="abc69-108">Test-Logboeken</span><span class="sxs-lookup"><span data-stu-id="abc69-108">Test logs</span></span>
<span data-ttu-id="abc69-109">De logboeken van de console die wordt geproduceerd door Hallo SDK kunnen worden ingeschakeld/uitgeschakeld/gefilterd.</span><span class="sxs-lookup"><span data-stu-id="abc69-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="abc69-110">toocustomize deze, update Hallo eigenschap `EngagementAgent.Instance.TestLogEnabled` tooone van Hallo waarde in Hallo `EngagementTestLogLevel` opsomming, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="abc69-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="abc69-111">Resources</span><span class="sxs-lookup"><span data-stu-id="abc69-111">Resources</span></span>
<span data-ttu-id="abc69-112">Hallo Reach-overlay is verbeterd.</span><span class="sxs-lookup"><span data-stu-id="abc69-112">hello Reach overlay has been improved.</span></span> <span data-ttu-id="abc69-113">Het uitmaakt deel van Hallo SDK NuGet-pakket resources.</span><span class="sxs-lookup"><span data-stu-id="abc69-113">It is part of hello SDK NuGet package resources.</span></span>

<span data-ttu-id="abc69-114">Tijdens het upgraden van de nieuwe versie toohello Hallo SDK kunt u kiezen dat of u tookeep wilt de bestaande bestanden uit Hallo map van uw resources overlay of niet:</span><span class="sxs-lookup"><span data-stu-id="abc69-114">While upgrading toohello new version of hello SDK you can choose whether you want tookeep your existing files from hello overlay folder of your resources or not:</span></span>

* <span data-ttu-id="abc69-115">Als vorige overlay Hallo u werkt of u Hallo integreert `WebView` elementen handmatig en u uw bestaande bestanden tookeep kunt, er nog steeds werken.</span><span class="sxs-lookup"><span data-stu-id="abc69-115">If hello previous overlay is working for you or you are integrating hello `WebView` elements manually then you can decide tookeep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="abc69-116">Als u wilt dat tooupdate toohello nieuwe overlay alleen vervangen Hallo hele `overlay` map van uw resources Hello nieuwe van Hallo SDK-pakket (UWP-apps: na de upgrade hello, kunt u Hallo nieuwe overlay map ophalen van % USERPROFILE %\\. nuget\ packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span><span class="sxs-lookup"><span data-stu-id="abc69-116">If you want tooupdate toohello new overlay, just replace hello whole `overlay` folder from your resources with hello new one from hello SDK package (UWP apps: after hello upgrade, you can get hello new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="abc69-117">Met behulp van de nieuwe overlay Hallo overschrijft aanpassingen op Hallo vorige versie.</span><span class="sxs-lookup"><span data-stu-id="abc69-117">Using hello new overlay will overwrite any customizations made on hello previous version.</span></span>
> 
> 

## <a name="from-320-too330"></a><span data-ttu-id="abc69-118">Van 3.2.0 too3.3.0</span><span class="sxs-lookup"><span data-stu-id="abc69-118">From 3.2.0 too3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="abc69-119">Resources</span><span class="sxs-lookup"><span data-stu-id="abc69-119">Resources</span></span>
<span data-ttu-id="abc69-120">Deze stap betreft alleen de aangepaste resources.</span><span class="sxs-lookup"><span data-stu-id="abc69-120">This step concerns customized resources only.</span></span> <span data-ttu-id="abc69-121">Als u Hallo resources die worden geleverd door Hallo SDK (html, afbeeldingen, overlay), hebt u toobackup hebt aangepast ze voordat u gaat upgraden en opnieuw toepassen op aanpassing bijgewerkt resources.</span><span class="sxs-lookup"><span data-stu-id="abc69-121">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-too320"></a><span data-ttu-id="abc69-122">Van 3.1.0 too3.2.0</span><span class="sxs-lookup"><span data-stu-id="abc69-122">From 3.1.0 too3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="abc69-123">Resources</span><span class="sxs-lookup"><span data-stu-id="abc69-123">Resources</span></span>
<span data-ttu-id="abc69-124">Deze stap betreft alleen de aangepaste resources.</span><span class="sxs-lookup"><span data-stu-id="abc69-124">This step concerns customized resources only.</span></span> <span data-ttu-id="abc69-125">Als u Hallo resources die worden geleverd door Hallo SDK (html, afbeeldingen, overlay), hebt u toobackup hebt aangepast ze voordat u gaat upgraden en opnieuw toepassen op aanpassing bijgewerkt resources.</span><span class="sxs-lookup"><span data-stu-id="abc69-125">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="abc69-126">Webweergave-integratie</span><span class="sxs-lookup"><span data-stu-id="abc69-126">Webview integration</span></span>
<span data-ttu-id="abc69-127">Een aantal verbeteringen toomatch ander apparaat vormen verkrijgbaar zijn geïntroduceerd in deze versie.</span><span class="sxs-lookup"><span data-stu-id="abc69-127">Some improvements toomatch different device form factors were introduced in this version.</span></span> <span data-ttu-id="abc69-128">Zorg ervoor dat de integratie van Hallo webweergave overeenkomt met Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="abc69-128">Make sure that your integration of hello webview match hello following:</span></span>

<span data-ttu-id="abc69-129">In uw pagina-(XAML):</span><span class="sxs-lookup"><span data-stu-id="abc69-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="abc69-130">En in uw bestand gekoppeld .cs:</span><span class="sxs-lookup"><span data-stu-id="abc69-130">And in your associated .cs file:</span></span>

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated toowithin a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

              #region tooimplement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update hello webview when hello app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update hello webview when hello app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure toodetach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are hello current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements toohello correct size.
              /// </summary>
              /// <param name="width">hello width of your current display.</param>
              /// <param name="height">hello height of your current display.</param>
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
              /// Handler that takes hello Windows.Current.SizeChanged and indicates that webviews have toobe resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes hello ApplicationView.VisibleBoundsChanged and indicates that webviews have toobe resized
              /// </summary>
              /// <param name="sender">hello related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-too300"></a><span data-ttu-id="abc69-131">Van 2.0.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="abc69-131">From 2.0.0 too3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="abc69-132">Resources</span><span class="sxs-lookup"><span data-stu-id="abc69-132">Resources</span></span>
<span data-ttu-id="abc69-133">Deze stap betreft alleen de aangepaste resources.</span><span class="sxs-lookup"><span data-stu-id="abc69-133">This step concerns customized resources only.</span></span> <span data-ttu-id="abc69-134">Als u Hallo resources die worden geleverd door Hallo SDK (html, afbeeldingen, overlay), hebt u toobackup hebt aangepast ze voordat u gaat upgraden en opnieuw toepassen op aanpassing bijgewerkt resources.</span><span class="sxs-lookup"><span data-stu-id="abc69-134">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-too200"></a><span data-ttu-id="abc69-135">Van 1.1.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="abc69-135">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="abc69-136">Hallo hieronder wordt beschreven hoe toomigrate een SDK-integratie van Hallo Capptain service aangeboden door Capptain SAS in een app die is aangedreven door Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="abc69-136">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="abc69-137">Capptain en Mobile Engagement dezelfde services niet zijn Hallo en Hallo onderstaande procedure alleen illustreert hoe toomigrate Hallo client-app.</span><span class="sxs-lookup"><span data-stu-id="abc69-137">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="abc69-138">Uw gegevens worden niet van Hallo Capptain servers toohello Mobile Engagement servers migreren Hallo SDK in Hallo-app gemigreerd</span><span class="sxs-lookup"><span data-stu-id="abc69-138">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="abc69-139">Als u vanaf een eerdere versie migreert, verwijder Hallo Capptain website toomigrate too1.1.1 eerst overleggen en toepassing hello procedure te volgen</span><span class="sxs-lookup"><span data-stu-id="abc69-139">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="abc69-140">Nuget-pakket</span><span class="sxs-lookup"><span data-stu-id="abc69-140">Nuget package</span></span>
<span data-ttu-id="abc69-141">Vervang **Capptain.WindowsPhone** door **MicrosoftAzure.MobileEngagement** Nuget-pakket.</span><span class="sxs-lookup"><span data-stu-id="abc69-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="abc69-142">Mobile Engagement toepassen</span><span class="sxs-lookup"><span data-stu-id="abc69-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="abc69-143">Hallo SDK gebruikt Hallo term `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="abc69-143">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="abc69-144">U moet tooupdate uw project toomatch deze wijziging.</span><span class="sxs-lookup"><span data-stu-id="abc69-144">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="abc69-145">U moet toouninstall uw huidige Capptain nuget-pakket.</span><span class="sxs-lookup"><span data-stu-id="abc69-145">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="abc69-146">Houd rekening met dat uw wijzigingen in de map Capptain bronnen worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="abc69-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="abc69-147">Als u deze bestanden tookeep wilt maken van een kopie van deze.</span><span class="sxs-lookup"><span data-stu-id="abc69-147">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="abc69-148">Daarna Hallo nieuwe Microsoft Azure Engagement nuget-pakket te installeren op uw project.</span><span class="sxs-lookup"><span data-stu-id="abc69-148">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="abc69-149">U vindt deze rechtstreeks op [nuget website].</span><span class="sxs-lookup"><span data-stu-id="abc69-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="abc69-150">of hier index.</span><span class="sxs-lookup"><span data-stu-id="abc69-150">or here index.</span></span> <span data-ttu-id="abc69-151">Deze actie vervangt alle bestanden van de resources gebruikt door Engagement en voegt het nieuwe Engagement DLL tooyour Hallo project verwijzingen.</span><span class="sxs-lookup"><span data-stu-id="abc69-151">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="abc69-152">U hebt uw projectverwijzingen tooclean door Capptain DLL verwijzingen te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="abc69-152">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="abc69-153">Als u dit niet doet, Hallo-versie van Capptain conflict veroorzaken en fouten gebeurt.</span><span class="sxs-lookup"><span data-stu-id="abc69-153">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="abc69-154">Als u Capptain resources hebt aangepast, wordt de inhoud van uw oude bestanden kopiëren en plak deze in Hallo nieuwe Engagement bestanden.</span><span class="sxs-lookup"><span data-stu-id="abc69-154">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="abc69-155">Houd er rekening mee dat zowel xaml en cs-bestanden bijgewerkt toobe hebben.</span><span class="sxs-lookup"><span data-stu-id="abc69-155">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="abc69-156">Wanneer deze stappen zijn voltooid. hoeft u alleen tooreplace oude Capptain verwijzingen door Hallo nieuwe Engagement verwijzingen.</span><span class="sxs-lookup"><span data-stu-id="abc69-156">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="abc69-157">Alle Capptain naamruimten hebben toobe bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="abc69-157">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="abc69-158">Vóór de migratie:</span><span class="sxs-lookup"><span data-stu-id="abc69-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="abc69-159">Na de migratie:</span><span class="sxs-lookup"><span data-stu-id="abc69-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="abc69-160">Alle Capptain klassen met 'Capptain' moeten 'Engagement' bevatten.</span><span class="sxs-lookup"><span data-stu-id="abc69-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="abc69-161">Vóór de migratie:</span><span class="sxs-lookup"><span data-stu-id="abc69-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="abc69-162">Na de migratie:</span><span class="sxs-lookup"><span data-stu-id="abc69-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="abc69-163">Voor xaml-bestanden wijzigen Capptain naamruimte en kenmerken ook.</span><span class="sxs-lookup"><span data-stu-id="abc69-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="abc69-164">Vóór de migratie:</span><span class="sxs-lookup"><span data-stu-id="abc69-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="abc69-165">Na de migratie:</span><span class="sxs-lookup"><span data-stu-id="abc69-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="abc69-166">Overlay pagina wijzigingen</span><span class="sxs-lookup"><span data-stu-id="abc69-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="abc69-167">Overlay ook gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="abc69-167">Overlay also changes.</span></span> <span data-ttu-id="abc69-168">De nieuwe naamruimte is `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="abc69-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="abc69-169">Heeft toobe in xaml- en cs-bestanden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="abc69-169">It has toobe used in both xaml and cs files.</span></span> <span data-ttu-id="abc69-170">Bovendien `CapptainGrid` heet toobe `EngagementGrid`, `capptain_notification_content` en `capptain_announcement_content` zijn benoemde `engagement_notification_content` en `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="abc69-170">Moreover `CapptainGrid` is toobe named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="abc69-171">Voor de overlay:</span><span class="sxs-lookup"><span data-stu-id="abc69-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="abc69-172">Wordt deze:</span><span class="sxs-lookup"><span data-stu-id="abc69-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="abc69-173">Voor Hallo andere bronnen zoals Capptain foto's en HTML-bestanden, houd er rekening mee dat ze ook zijn gewijzigd toouse 'Engagement'.</span><span class="sxs-lookup"><span data-stu-id="abc69-173">For hello other resources like Capptain pictures and HTML files, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="abc69-174">Project-declaratie</span><span class="sxs-lookup"><span data-stu-id="abc69-174">Project declaration</span></span>
<span data-ttu-id="abc69-175">Op Package.appxmanifest `File Type Associations` is bijgewerkt op basis van:</span><span class="sxs-lookup"><span data-stu-id="abc69-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="abc69-176">capptain\_bereiken\_inhoud tooengagement\_bereiken\_inhoud</span><span class="sxs-lookup"><span data-stu-id="abc69-176">capptain\_reach\_content tooengagement\_reach\_content</span></span>
* <span data-ttu-id="abc69-177">capptain\_logboek\_bestand tooengagement\_logboek\_bestand</span><span class="sxs-lookup"><span data-stu-id="abc69-177">capptain\_log\_file tooengagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="abc69-178">Toepassings-ID / SDK-sleutel</span><span class="sxs-lookup"><span data-stu-id="abc69-178">Application ID / SDK Key</span></span>
<span data-ttu-id="abc69-179">Engagement maakt gebruik van een verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="abc69-179">Engagement uses a connection string.</span></span> <span data-ttu-id="abc69-180">U hebt geen toospecify een toepassings-ID en een met Mobile Engagement SDK-sleutel, u hoeft alleen toospecify een verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="abc69-180">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="abc69-181">U kunt deze functie instellen op uw EngagementConfiguration-bestand.</span><span class="sxs-lookup"><span data-stu-id="abc69-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="abc69-182">Hallo Engagement configuratie kan worden ingesteld in uw `Resources\EngagementConfiguration.xml` -bestand van uw project.</span><span class="sxs-lookup"><span data-stu-id="abc69-182">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="abc69-183">Dit bestand toospecify bewerken:</span><span class="sxs-lookup"><span data-stu-id="abc69-183">Edit this file toospecify:</span></span>

* <span data-ttu-id="abc69-184">De verbindingsreeks voor de toepassing tussen de tags `<connectionString>` en `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="abc69-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="abc69-185">Als u wilt dat deze tijdens runtime in plaats daarvan kunt u bellen Hallo volgende toospecify methode voordat de initialisatie van de agent Hallo Engagement:</span><span class="sxs-lookup"><span data-stu-id="abc69-185">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="abc69-186">Hallo-verbindingsreeks voor uw toepassing wordt weergegeven op Hallo klassieke Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="abc69-186">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="abc69-187">Wijziging van items</span><span class="sxs-lookup"><span data-stu-id="abc69-187">Items name change</span></span>
<span data-ttu-id="abc69-188">Alle items met de naam *capptain* naam hebt gegeven *engagement*.</span><span class="sxs-lookup"><span data-stu-id="abc69-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="abc69-189">Op dezelfde manier voor *Capptain* te*Engagement*.</span><span class="sxs-lookup"><span data-stu-id="abc69-189">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="abc69-190">Voorbeelden van veelgebruikte Capptain items:</span><span class="sxs-lookup"><span data-stu-id="abc69-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="abc69-191">CapptainConfiguration EngagementConfiguration nu met de naam</span><span class="sxs-lookup"><span data-stu-id="abc69-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="abc69-192">CapptainAgent EngagementAgent nu met de naam</span><span class="sxs-lookup"><span data-stu-id="abc69-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="abc69-193">CapptainReach EngagementReach nu met de naam</span><span class="sxs-lookup"><span data-stu-id="abc69-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="abc69-194">CapptainHttpConfig EngagementHttpConfig nu met de naam</span><span class="sxs-lookup"><span data-stu-id="abc69-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="abc69-195">GetCapptainPageName GetEngagementPageName nu met de naam</span><span class="sxs-lookup"><span data-stu-id="abc69-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="abc69-196">Houd er rekening mee dat rename ook van invloed op overschreven methoden.</span><span class="sxs-lookup"><span data-stu-id="abc69-196">Note that rename also affects overridden methods.</span></span>

