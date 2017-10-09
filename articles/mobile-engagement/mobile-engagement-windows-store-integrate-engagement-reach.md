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
# <a name="windows-universal-apps-reach-sdk-integration"></a>Universele Windows-Apps bereiken SDK-integratie
U moet volgen Hallo integratie procedure wordt beschreven in Hallo [Windows universele Engagement SDK-integratie](mobile-engagement-windows-store-integrate-engagement.md) voordat u deze handleiding.

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a>Hallo Engagement bereiken SDK in uw universele Windows-project insluiten
U hebt geen iets tooadd. `EngagementReach`verwijzingen en bronnen bevinden zich al in uw project.

> [!TIP]
> U kunt afbeeldingen uit Hallo `Resources` map van uw project, met name Hallo merk-pictogram (die standaard toohello Engagement pictogram). Op universele Apps kunt u ook Hallo verplaatsen `Resources` map op de inhoud ervan tussen apps, maar u hebt gedeeld project-tooshare tookeep hello `Resources\EngagementConfiguration.xml` bestand op de standaardlocatie, omdat deze afhankelijk platform.
> 
> 

## <a name="enable-hello-windows-notification-service"></a>Hallo Windows Notification Service inschakelen
### <a name="windows-8x-and-windows-phone-81-only"></a>Windows 8.x en Windows Phone 8.1 alleen
In de volgorde toouse hello **Windows Notification Service** (WNS genoemd) in uw `Package.appxmanifest` -bestand in de `Application UI` klikt u op `All Image Assets` in Hallo links bot vak. Op Hallo van Hallo vak in `Notifications`, wijzigen `toast capable` van `(not set)` te`(Yes)`.

### <a name="all-platforms"></a>Alle platforms
U moet uw app tooyour Microsoft-account en toohello engagement-platform toosynchronize. Voor deze toocreate een account of u aanmelden [windows-ontwikkelaarscentrum](https://dev.windows.com). Nadat een nieuwe toepassing maken en vinden Hallo SID en de geheime sleutel. Ga op uw app-instelling in op Hallo engagement front-end `native push` en plak uw referenties. Hierna, klik met de rechtermuisknop op uw project, selecteer `store` en `Associate App with hello Store...`. U hoeft alleen maar tooselect Hallo toepassing u hebt dit hebt gemaakt voordat toosynchronize.

## <a name="initialize-hello-engagement-reach-sdk"></a>Hallo Engagement bereiken SDK initialiseren
Hallo wijzigen `App.xaml.cs`:

* Invoegen `EngagementReach.Instance.Init` vlak na `EngagementAgent.Instance.Init` in uw `InitEngagement` methode:
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  Hallo `EngagementReach.Instance.Init` in een specifieke thread wordt uitgevoerd. U hebt geen toodo deze zelf.

> [!NOTE]
> Als u pushmeldingen elders in uw toepassing is er te[delen van het kanaal push](#push-channel-sharing) met Engagement bereiken.
> 
> 

## <a name="integration"></a>Integratie
Engagement biedt twee manieren tooadd Hallo Reach in-app-banner en verspreide weergaven voor aankondigingen en polls in uw toepassing: Hallo overlay-integratie en handmatige integratie met weergaven Hallo het web. U moet beide benadering op Hallo niet combineren dezelfde pagina.

Hallo keuze tussen de twee integratie Hallo kan op deze manier worden samengevat:

* U kunt ervoor kiezen Hallo overlay-integratie als uw pagina's al overneemt van Hallo Agent `EngagementPage`, het is alleen een kwestie van het vervangen van `EngagementPage` door `EngagementPageOverlay` en `xmlns:engagement="using:Microsoft.Azure.Engagement"` door `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in uw pagina's.
* U kunt handmatig integratie met het Hallo web weergaven als u wilt dat tooprecisely plaats Hallo UI bereiken in de pagina's of als u niet dat tooadd wilt een andere overname niveau tooyour pagina's. 

### <a name="overlay-integration"></a>Overlay-integratie
Hallo Engagement overlay worden dynamisch toegevoegd Hallo UI-elementen toodisplay Reach-campagnes gebruikt in uw pagina. Als het Hallo-overlay niet aan de behoeften van uw lay-out moet u Hallo webweergaven handmatige integratie in plaats daarvan.

In het .xaml-bestandswijziging `EngagementPage` te verwijzen`EngagementPageOverlay`

* Tooyour naamruimtedeclaraties toevoegen:
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* Vervang `engagement:EngagementPage` met `engagement:EngagementPageOverlay`:

**Met EngagementPage:**

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

**Met EngagementPageOverlay:**

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

Klik in het bestand .cs tag uw pagina in `EngagementPageOverlay` in plaats van `EngagementPage` en importeer `Microsoft.Azure.Engagement.Overlay`.

            using Microsoft.Azure.Engagement.Overlay;

* Vervang `EngagementPage` met `EngagementPageOverlay`:

**Met EngagementPage:**

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

**Met EngagementPageOverlay:**

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


Hallo Engagement overlay voegt een `Grid` element boven op de pagina bestaat uit de indeling en Hallo twee `WebView` elementen één voor Hallo banner en andere één voor verspreide weergave Hallo Hallo.

U kunt aanpassen Hallo overlay elementen rechtstreeks in Hallo `EngagementPageOverlay.cs` bestand.

### <a name="web-views-manual-integration"></a>Handmatige integratie met het web weergaven
Reach zoeken op de pagina's voor Hallo twee naar `WebView` elementen die verantwoordelijk is voor het weergeven van Hallo banner en Hallo verspreide weergeven. Hallo alleen dat u hoeft toodo tooadd is deze twee `WebView` elementen ergens in de pagina's, Hier volgt een voorbeeld:

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


In dit voorbeeld Hallo `WebView` elementen zijn gespreide toofit hun container die automatisch opnieuw groottes in geval van een scherm worden gedraaid of venster grootte wijzigen.

> [!WARNING]
> Het is belangrijk tookeep Hallo dezelfde naming `engagement_notification_content` en `engagement_announcement_content` voor Hallo `WebView` elementen. Reach is identificeren met hun naam. 
> 
> 

## <a name="handle-datapush-optional"></a>Ingang datapush (optioneel)
Als u wilt dat uw toepassing toobe kunnen tooreceive Reach gegevens-pushes, hebt u twee gebeurtenissen tooimplement Hallo EngagementReach klasse:

Voeg in App.xaml.cs in Hallo App() constructor toe:

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

U ziet dat Hallo retouraanroep van elke methode retourneert een Booleaanse waarde. Engagement verzendt een feedback tooits back-end na het verzenden van gegevens-push Hallo. Als het Hallo-callback false retourneert, Hallo `exit` feedback verzenden zijn. Anders moeten `action`. Als geen retouraanroep is ingesteld op Hallo gebeurtenissen, Hallo `drop` feedback tooEngagement worden geretourneerd.

> [!WARNING]
> Engagement is niet kunnen tooreceive veelvouden feedback voor een gegevens-push. Als u van plan tooset verschillende handlers een gebeurtenis bent, houd er rekening mee dat Hallo feedback toohello het laatst werd verzonden overeenkomen worden. In dit geval wordt aangeraden tooalways retourneert dezelfde waarde tooavoid verwarrend feedback over voor front-Hallo Hallo.
> 
> 

## <a name="customize-ui-optional"></a>Aanpassen van de gebruikersinterface (optioneel)
### <a name="first-step"></a>Eerste stap
We laten toocustomize Hallo reach gebruikersinterface.

toodo geval is, hebt u toocreate een subklasse van Hallo `EngagementReachHandler` klasse.

**Voorbeeld van Code:**

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

Vervolgens stelt u inhoud Hallo Hallo `EngagementReach.Instance.Handler` veld met het aangepaste object in uw `App.xaml.cs` klasse binnen de Hallo `App()` methode.

**Voorbeeld van Code:**

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> Engagement maakt standaard gebruik van een eigen implementatie van `EngagementReachHandler`.
> U hebt geen toocreate zelf, en als u doet dit, hebt u niet toooverride elke methode. Hallo standaardgedrag is tooselect Hallo Engagement basisobject.
> 
> 

### <a name="web-view"></a>Webweergave
Standaard Reach Hallo ingesloten resources van Hallo DLL toodisplay Hallo meldingen en pagina's gebruikt.

een volledige tooprovide mogelijkheden voor aanpassing we alleen webweergave gebruiken. Als u toocustomize indelingen wilt, overschrijven rechtstreeks Hallo resources bestanden `EngagementAnnouncement.html` en `EngagementNotification.html`. Engagement moet alle code in `<body></body>` toorun correct. Maar u kunt de buitenste tag toevoegen `engagement_webview_area`.

Echter, kunt u beslissen toouse uw eigen resources.

U kunt onderdrukken `EngagementReachHandler` methoden in uw subklasse tootell Engagement toouse uw indelingen, maar maken gebruik van voorzichtig tooembedded Hallo engagement mechanisme:

**Voorbeeld van Code:**

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


AnnouncementHTML is standaard `ms-appx-web:///Resources/EngagementAnnouncement.html`. Hiermee geeft u de Hallo HTML-bestand dat ontwerpen Hallo inhoud van een pushbericht (tekst aankondiging, Web anoucement en Poll aankondiging). AnnouncementName is `engagement_announcement_content`. Dit is de naam Hallo van Hallo webweergave ontwerp in uw xaml-pagina.

NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`. Hiermee geeft u de Hallo HTML-bestand dat ontwerpen Hallo melding van een pushbericht. NotfificationName is `engagement_notification_content`. Dit is de naam Hallo van Hallo webweergave ontwerp in uw xaml-pagina.

### <a name="customization"></a>Aanpassing
U kunt de melding en aankondiging webweergave is dat u wilt dat als u Engagement object behouden aanpassen. Wees voorzichtig webweergave-object is beschreven driemaal - hello eerst in de xaml tweede tijdstip in uw bestand .cs in Hallo 'setwebview()' methode en het derde periode in Hallo HTML-bestand.

* In de xaml beschrijft u Hallo huidige grafische indeling webweergave onderdeel.
* U kunt in uw bestand .cs 'setwebview()' waarin u Hallo dimensie van de twee webweergave hello (melding, aankondiging) instellen definiëren. Het is zeer effectief zijn wanneer het formaat van de toepassing hello.
* In Hallo Engagement HTML-bestand we beschrijven Hallo webweergave inhoud, ontwerpen en Hallo elementen posities tussen elkaar.

### <a name="launch-message"></a>Bericht starten
Wanneer een gebruiker klikt op een Systeemmelding (een pop-up), Engagement Hallo toepassing wordt gestart, load Hallo inhoud Hallo push berichten en Hallo-pagina voor de bijbehorende campagne Hallo weergegeven.

Er is een vertraging tussen Hallo starten van de toepassing en Hallo beeldscherm Hallo van Hallo pagina (afhankelijk van de Hallo snelheid van uw netwerk).

gebruiker toohello tooindicate dat er iets wordt geladen, moet u een visuele gegevens, zoals een voortgangsbalk zien of een voortgangsindicator opgeven. Engagement kan niet worden verwerkt, maar enkele handlers voor u biedt.

tooimplement hello retouraanroep in App.xaml.cs in "Openbare App() {}" toevoegen:

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

U kunt Hallo callback instellen in de methode 'Openbare App() {}' van uw `App.xaml.cs` -bestand, bij voorkeur voor Hallo `EngagementReach.Instance.Init()` aanroepen.

> [!TIP]
> Elke handler wordt aangeroepen door Hallo UI Thread. U hoeft geen tooworry wanneer u een MessageBox of iets UI-gerelateerde.
> 
> 

## <a id="push-channel-sharing"></a>Push-kanaal voor delen
Als u pushmeldingen voor een ander doel in uw toepassing hebt u toouse Hallo push kanaal functie Hallo Engagement SDK voor het delen. Dit is tooavoid gemist push.

* U kunt uw eigen push toohello Engagement bereiken initialisatie van een kanaal op te geven. Hallo SDK wordt gebruikt in plaats van een nieuwe aanvragen.

Hallo Engagement bereiken initialisatie bijwerken met het kanaal push in Hallo `InitEngagement` methode van Hallo `App.xaml.cs` bestand:

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* U kunt ook als u alleen wilt tooconsume Hallo push-kanaal na de initialisatie van de Reach Hallo en vervolgens kunt u een retouraanroep instellen op Engagement bereiken tooget Hallo push kanaal eenmaal is gemaakt door Hallo SDK.

De retouraanroep ingesteld op een willekeurige plaats **nadat** Reach-initialisatie Hallo:

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a>Aangepaste schema tip
We bieden gebruik van aangepaste schema. U kunt verschillende type URI verzenden van engagement frontend toobe gebruikt in de engagement-toepassing. Standaardschema zoals `http, ftp, ...` zijn beheren in Windows, met een venster wordt gevraagd als ze geen standaardtoepassing op apparaat geïnstalleerd. U kunt ook uw eigen aangepaste schema maken voor uw toepassing.

Hallo op eenvoudige wijze tooset een aangepast schema in uw toepassing is tooopen uw `Package.appxmanifest` Ga in `Declarations` Configuratiescherm. Selecteer `Protocol` in Hallo beschikbaar declaraties Schuif vak en toe te voegen. Hallo bewerken `Name` veld met uw nieuwe protocol de gewenste naam.

Nu toouse dit protocol bewerken uw `App.xaml.cs` Hello `OnActivated` methode en vergeet niet tooinitialize engagement hier ook:

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

