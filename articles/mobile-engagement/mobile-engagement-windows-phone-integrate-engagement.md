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
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a>Windows Phone Silverlight Engagement SDK-integratie
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

Deze procedure wordt beschreven Hallo eenvoudigste manier tooactivate Azure Mobile Engagement Analytics en bewaking van functies in uw Windows Phone Silverlight-toepassing.

Hallo stappen te volgen zijn dat onvoldoende tooactivate Hallo rapport van Logboeken nodig toocompute alle statistische gegevens over gebruikers, sessies, activiteiten, Crashes en Technicals. rapport van Logboeken Hallo nodig toocompute andere statistieken zoals gebeurtenissen, fouten en taken moeten worden uitgevoerd handmatig met Hallo Engagement API (Zie [hoe toouse Hallo Mobile Engagement API in uw Windows Phone Silverlight-app-tagging geavanceerde](mobile-engagement-windows-phone-use-engagement-api.md) Zie hieronder) omdat deze statistieken afhankelijk zijn van toepassing zijn.

## <a name="supported-versions"></a>Ondersteunde versies
Hallo Mobile Engagement SDK voor Windows Silverlight kan alleen worden geïntegreerd in toepassingen die gericht is op:

* Windows Phone 8.0
* Windows Phone 8.1 Silverlight

> [!NOTE]
> Als u ontwikkelt voor Windows Phone 8.1 (zonder Silverlight) verwijzen toohello [universele Windows-integratie procedure](mobile-engagement-windows-store-integrate-engagement.md).
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a>Hallo Mobile Engagement Silverlight-SDK installeren
Hallo Mobile Engagement SDK voor Windows Silverlight is beschikbaar als een Nuget-pakket aangeroepen *MicrosoftAzure.MobileEngagement*. U kunt deze installeren via Hallo Nuget Package Manager voor Visual Studio. 

## <a name="add-hello-capabilities"></a>Hallo mogelijkheden toevoegen
Hallo Engagement SDK moet enkele mogelijkheden van Windows Phone Silverlight-SDK Hallo in volgorde toowork goed.

Open uw `WMAppManifest.xml` -bestand en zorg ervoor dat die Hallo na mogelijkheden zijn gedeclareerd in Hallo `Capabilities` Configuratiescherm:

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a>Hallo Engagement SDK initialiseren
### <a name="engagement-configuration"></a>Engagement configuratie
Hallo Engagement configuratie op Hallo is gecentraliseerd `Resources\EngagementConfiguration.xml` -bestand van uw project.

Dit bestand toospecify bewerken:

* De verbindingsreeks voor de toepassing tussen de tags `<connectionString>` en `<\connectionString>`.

Als u wilt dat deze tijdens runtime in plaats daarvan kunt u bellen Hallo volgende toospecify methode voordat de initialisatie van de agent Hallo Engagement:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

Hallo-verbindingsreeks voor uw toepassing wordt weergegeven op Hallo klassieke Azure-Portal.

### <a name="engagement-initialization"></a>De initialisatie van de engagement
Wanneer u een nieuw project maakt een `App.xaml.cs` -bestand is gegenereerd. Deze klasse neemt over van `Application` en bevat veel belangrijke methoden. Dit wordt ook worden de gebruikte tooinitialize Hallo Engagement SDK.

Hallo wijzigen `App.xaml.cs`:

* Toevoegen van tooyour `using` instructies:
  
      using Microsoft.Azure.Engagement;
* Invoegen `EngagementAgent.Instance.Init` in Hallo `Application_Launching` methode:
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* Invoegen `EngagementAgent.Instance.OnActivated` in Hallo `Application_Activated` methode:
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> We afraden raden u tooadd Hallo Engagement-initialisatie in een andere locatie van uw toepassing. Echter wel rekening die Hallo `EngagementAgent.Instance.Init` methode wordt uitgevoerd op een specifieke thread en niet op Hallo UI-thread.
> 
> 

## <a name="basic-reporting"></a>Basic-rapportage
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a>Aanbevolen methode: overbelasting uw `PhoneApplicationPage` klassen
In volgorde tooactivate Hallo rapport van alle Hallo Logboeken door Engagement toocompute gebruikers, sessies, activiteiten, Crashes en technische statistieken vereist, kunt u gewoon zodat alle uw `PhoneApplicationPage` onderliggende klassen overnemen van Hallo `EngagementPage` klassen.

Hier volgt een voorbeeld van hoe toodo dit voor een pagina van uw toepassing. U kunt doen Hallo hetzelfde geldt voor alle pagina's van uw toepassing.

#### <a name="c-source-file"></a>C#-bronbestand
Wijzigen van uw pagina `.xaml.cs` bestand:

* Toevoegen van tooyour `using` instructies:
  
      using Microsoft.Azure.Engagement;
* Vervang `PhoneApplicationPage` met `EngagementPage` :

**Zonder Engagement:**

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

**Met Engagement:**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> Als uw pagina van Hallo overneemt `OnNavigatedTo` -methode worden zorgvuldige toolet hello `base.OnNavigatedTo(e)` aanroepen. Anders Hallo activiteit niet gerapporteerd. Hallo immers `EngagementPage` aanroept `StartActivity` binnen Hallo `OnNavigatedTo` methode.
> 
> 

#### <a name="xaml-file"></a>XAML-bestand
Wijzigen van uw pagina `.xaml` bestand:

* Tooyour naamruimtedeclaraties toevoegen:
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* Vervang `phone:PhoneApplicationPage` met `engagement:EngagementPage` :

**Zonder Engagement:**

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

**Met Engagement:**

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a>Hallo standaardgedrag negeren
Standaard is als Hallo activiteitsnaam, zonder extra Hallo klassenaam van Hallo pagina gerapporteerd. Als Hallo klasse Hallo 'Pagina' achtervoegsel gebruikt, Engagement wordt het ook verwijderd.

Als u toooverride Hallo standaardgedrag voor de naam van de hello wilt, programmacode toe te voegen deze tooyour:

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

Als u wilt dat tooreport wat extra informatie met uw activiteiten, kunt u deze code tooyour toevoegen:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

Deze methoden worden aangeroepen vanuit Hallo `OnNavigatedTo` methode van uw pagina.

### <a name="alternate-method-call-startactivity-manually"></a>Alternatieve methode: call `StartActivity()` handmatig
Als u niet kunt of toooverload niet wilt dat uw `PhoneApplicationPage` klassen, in plaats daarvan kunt u uw activiteiten starten door het aanroepen van `EngagementAgent` rechtstreeks methoden.

We raden aan aanroepen `StartActivity` binnen uw `OnNavigatedTo` methode van uw PhoneApplicationPage.

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> Zorg ervoor dat u uw sessie correct beëindigen.
> 
> Hallo SDK roept automatisch Hallo `EndActivity` methode wanneer de toepassing hello wordt gesloten. Het is dus **maximaal** toocall Hallo aanbevolen `StartActivity` methode wanneer Hallo activiteit van Hallo gebruiker wijzigt, en te**nooit** aanroep Hallo `EndActivity` methode. Deze methode verzendt een bericht toohello Engagement server dat de huidige gebruiker Hallo Hallo toepassing is verdwenen en dit heeft gevolgen voor alle toepassingslogboeken.
> 
> 

## <a name="advanced-reporting"></a>Geavanceerde rapportage
Desgewenst kunt u tooreport toepassing specifieke gebeurtenissen, fouten en taken, toodo dus, gebruik andere methoden gevonden in Hallo Hallo `EngagementAgent` klasse. Hallo Engagement API kunt toouse alle Engagement geavanceerde mogelijkheden.

Zie voor meer informatie [hoe toouse Hallo Mobile Engagement API in uw Windows Phone Silverlight-app-tagging geavanceerde](mobile-engagement-windows-phone-use-engagement-api.md).

## <a name="advanced-configuration"></a>Geavanceerde configuratie
### <a name="disable-automatic-crash-reporting"></a>Automatische crashrapporten uitschakelen
U kunt automatische Hallo-crash rapportagefunctie van Engagement uitschakelen. Vervolgens, als er wordt een niet-verwerkte uitzondering optreedt, Engagement is geen alles.

> [!WARNING]
> Als u van plan toodisable deze functie bent, houd er rekening mee dat wanneer het vastlopen van een niet-verwerkte in uw app optreden zal, Engagement geen Hallo crashes verzenden worden **en** het Hallo-sessie en taken niet gesloten.
> 
> 

toodisable automatische crash rapportage, alleen uw configuratie, afhankelijk van Hallo manier waarop u het gedeclareerd aanpassen:

#### <a name="from-engagementconfigurationxml-file"></a>Van `EngagementConfiguration.xml` bestand
Rapport vastlopen te ingesteld`false` tussen `<reportCrash>` en `</reportCrash>` labels.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>Van `EngagementConfiguration` object tijdens runtime
Rapport crash toofalse met behulp van het object EngagementConfiguration ingesteld.

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>Burst-modus
Standaard Hallo Engagement servicerapporten Logboeken in realtime. Als uw toepassing Logboeken heel vaak rapporteert, is het beter toobuffer Hallo logboeken en tooreport ze allemaal tegelijk op een vaste tijd base (dit wordt Hallo 'burst modus' genoemd).

toodo worden dus Hallo-methode aanroept:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

Hallo-argument is een waarde in **milliseconden**. Op elk gewenst moment als u tooreactivate Hallo realtime logboekregistratie wilt, roept Hallo methode geen parameters of met de Hallo 0-waarde.

Hallo burst-modus iets langer Hallo accu levensduur maar heeft een invloed op Hallo Engagement-Monitor: alle sessies en taken duur zijn afgerond toohello burst drempelwaarde (dus sessies en korter zijn dan Hallo burst drempelwaarde is mogelijk niet zichtbaar taken). Het is aanbevolen toouse een ' burst ' drempelwaarde niet langer dan 30000 (30s). U hebt toobe Houd er rekening mee dat opgeslagen logboeken zijn beperkt too300-items. U kunt sommige logboeken verliezen als verzenden te lang is.

> [!WARNING]
> Hallo burst drempelwaarde kan niet worden geconfigureerd tooa periode minder dan één seconde. Als u dus toodo probeert, Hallo SDK wordt een tracering met Hallo fout weergeven en automatisch opnieuw instellen toohello standaardwaarde, dat wil zeggen, nul seconden. Dit activeert Hallo SDK tooreport Hallo Logboeken in realtime.
> 
> 

