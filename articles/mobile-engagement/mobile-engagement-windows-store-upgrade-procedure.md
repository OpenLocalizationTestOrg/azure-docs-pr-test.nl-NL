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
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a>Upgradeprocedures van Windows universele Apps SDK
Als u hebt al een oudere versie van Engagement geïntegreerd in uw toepassing, hebt u tooconsider Hallo volgende punten bij het upgraden van Hallo SDK.

Mogelijk hebt u toofollow verschillende procedures als u verschillende versies van Hallo SDK gemist. Bijvoorbeeld als u migreert vanaf 0.10.1 too0.11.0 hebt toofirst Volg Hallo ' van 0.9.0 too0.10.1 ' procedure vervolgens Hallo ' van 0.10.1 too0.11.0 ' procedure.

## <a name="from-330-too340"></a>Van 3.3.0 too3.4.0
### <a name="test-logs"></a>Test-Logboeken
De logboeken van de console die wordt geproduceerd door Hallo SDK kunnen worden ingeschakeld/uitgeschakeld/gefilterd. toocustomize deze, update Hallo eigenschap `EngagementAgent.Instance.TestLogEnabled` tooone van Hallo waarde in Hallo `EngagementTestLogLevel` opsomming, bijvoorbeeld:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a>Resources
Hallo Reach-overlay is verbeterd. Het uitmaakt deel van Hallo SDK NuGet-pakket resources.

Tijdens het upgraden van de nieuwe versie toohello Hallo SDK kunt u kiezen dat of u tookeep wilt de bestaande bestanden uit Hallo map van uw resources overlay of niet:

* Als vorige overlay Hallo u werkt of u Hallo integreert `WebView` elementen handmatig en u uw bestaande bestanden tookeep kunt, er nog steeds werken. 
* Als u wilt dat tooupdate toohello nieuwe overlay alleen vervangen Hallo hele `overlay` map van uw resources Hello nieuwe van Hallo SDK-pakket (UWP-apps: na de upgrade hello, kunt u Hallo nieuwe overlay map ophalen van % USERPROFILE %\\. nuget\ packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).

> [!WARNING]
> Met behulp van de nieuwe overlay Hallo overschrijft aanpassingen op Hallo vorige versie.
> 
> 

## <a name="from-320-too330"></a>Van 3.2.0 too3.3.0
### <a name="resources"></a>Resources
Deze stap betreft alleen de aangepaste resources. Als u Hallo resources die worden geleverd door Hallo SDK (html, afbeeldingen, overlay), hebt u toobackup hebt aangepast ze voordat u gaat upgraden en opnieuw toepassen op aanpassing bijgewerkt resources.

## <a name="from-310-too320"></a>Van 3.1.0 too3.2.0
### <a name="resources"></a>Resources
Deze stap betreft alleen de aangepaste resources. Als u Hallo resources die worden geleverd door Hallo SDK (html, afbeeldingen, overlay), hebt u toobackup hebt aangepast ze voordat u gaat upgraden en opnieuw toepassen op aanpassing bijgewerkt resources.

### <a name="webview-integration"></a>Webweergave-integratie
Een aantal verbeteringen toomatch ander apparaat vormen verkrijgbaar zijn geïntroduceerd in deze versie. Zorg ervoor dat de integratie van Hallo webweergave overeenkomt met Hallo volgende:

In uw pagina-(XAML):

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

En in uw bestand gekoppeld .cs:

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

## <a name="from-200-too300"></a>Van 2.0.0 too3.0.0
### <a name="resources"></a>Resources
Deze stap betreft alleen de aangepaste resources. Als u Hallo resources die worden geleverd door Hallo SDK (html, afbeeldingen, overlay), hebt u toobackup hebt aangepast ze voordat u gaat upgraden en opnieuw toepassen op aanpassing bijgewerkt resources.

## <a name="from-111-too200"></a>Van 1.1.1 too2.0.0
Hallo hieronder wordt beschreven hoe toomigrate een SDK-integratie van Hallo Capptain service aangeboden door Capptain SAS in een app die is aangedreven door Azure Mobile Engagement. 

> [!IMPORTANT]
> Capptain en Mobile Engagement dezelfde services niet zijn Hallo en Hallo onderstaande procedure alleen illustreert hoe toomigrate Hallo client-app. Uw gegevens worden niet van Hallo Capptain servers toohello Mobile Engagement servers migreren Hallo SDK in Hallo-app gemigreerd
> 
> 

Als u vanaf een eerdere versie migreert, verwijder Hallo Capptain website toomigrate too1.1.1 eerst overleggen en toepassing hello procedure te volgen

### <a name="nuget-package"></a>Nuget-pakket
Vervang **Capptain.WindowsPhone** door **MicrosoftAzure.MobileEngagement** Nuget-pakket.

### <a name="applying-mobile-engagement"></a>Mobile Engagement toepassen
Hallo SDK gebruikt Hallo term `Engagement`. U moet tooupdate uw project toomatch deze wijziging.

U moet toouninstall uw huidige Capptain nuget-pakket. Houd rekening met dat uw wijzigingen in de map Capptain bronnen worden verwijderd. Als u deze bestanden tookeep wilt maken van een kopie van deze.

Daarna Hallo nieuwe Microsoft Azure Engagement nuget-pakket te installeren op uw project. U vindt deze rechtstreeks op [nuget website]. of hier index. Deze actie vervangt alle bestanden van de resources gebruikt door Engagement en voegt het nieuwe Engagement DLL tooyour Hallo project verwijzingen.

U hebt uw projectverwijzingen tooclean door Capptain DLL verwijzingen te verwijderen. Als u dit niet doet, Hallo-versie van Capptain conflict veroorzaken en fouten gebeurt.

Als u Capptain resources hebt aangepast, wordt de inhoud van uw oude bestanden kopiëren en plak deze in Hallo nieuwe Engagement bestanden. Houd er rekening mee dat zowel xaml en cs-bestanden bijgewerkt toobe hebben.

Wanneer deze stappen zijn voltooid. hoeft u alleen tooreplace oude Capptain verwijzingen door Hallo nieuwe Engagement verwijzingen.

1. Alle Capptain naamruimten hebben toobe bijgewerkt.
   
    Vóór de migratie:
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    Na de migratie:
   
        using Microsoft.Azure.Engagement;
2. Alle Capptain klassen met 'Capptain' moeten 'Engagement' bevatten.
   
    Vóór de migratie:
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    Na de migratie:
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. Voor xaml-bestanden wijzigen Capptain naamruimte en kenmerken ook.
   
    Vóór de migratie:
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    Na de migratie:
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. Overlay pagina wijzigingen
   
   > [!IMPORTANT]
   > Overlay ook gewijzigd. De nieuwe naamruimte is `Microsoft.Azure.Engagement.Overlay`. Heeft toobe in xaml- en cs-bestanden gebruikt. Bovendien `CapptainGrid` heet toobe `EngagementGrid`, `capptain_notification_content` en `capptain_announcement_content` zijn benoemde `engagement_notification_content` en `engagement_announcement_content`.
   > 
   > 
   
    Voor de overlay:
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    Wordt deze:
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. Voor Hallo andere bronnen zoals Capptain foto's en HTML-bestanden, houd er rekening mee dat ze ook zijn gewijzigd toouse 'Engagement'.

### <a name="project-declaration"></a>Project-declaratie
Op Package.appxmanifest `File Type Associations` is bijgewerkt op basis van:

* capptain\_bereiken\_inhoud tooengagement\_bereiken\_inhoud
* capptain\_logboek\_bestand tooengagement\_logboek\_bestand

### <a name="application-id--sdk-key"></a>Toepassings-ID / SDK-sleutel
Engagement maakt gebruik van een verbindingsreeks. U hebt geen toospecify een toepassings-ID en een met Mobile Engagement SDK-sleutel, u hoeft alleen toospecify een verbindingsreeks. U kunt deze functie instellen op uw EngagementConfiguration-bestand.

Hallo Engagement configuratie kan worden ingesteld in uw `Resources\EngagementConfiguration.xml` -bestand van uw project.

Dit bestand toospecify bewerken:

* De verbindingsreeks voor de toepassing tussen de tags `<connectionString>` en `<\connectionString>`.

Als u wilt dat deze tijdens runtime in plaats daarvan kunt u bellen Hallo volgende toospecify methode voordat de initialisatie van de agent Hallo Engagement:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

Hallo-verbindingsreeks voor uw toepassing wordt weergegeven op Hallo klassieke Azure-Portal.

### <a name="items-name-change"></a>Wijziging van items
Alle items met de naam *capptain* naam hebt gegeven *engagement*. Op dezelfde manier voor *Capptain* te*Engagement*.

Voorbeelden van veelgebruikte Capptain items:

* CapptainConfiguration EngagementConfiguration nu met de naam
* CapptainAgent EngagementAgent nu met de naam
* CapptainReach EngagementReach nu met de naam
* CapptainHttpConfig EngagementHttpConfig nu met de naam
* GetCapptainPageName GetEngagementPageName nu met de naam

Houd er rekening mee dat rename ook van invloed op overschreven methoden.

