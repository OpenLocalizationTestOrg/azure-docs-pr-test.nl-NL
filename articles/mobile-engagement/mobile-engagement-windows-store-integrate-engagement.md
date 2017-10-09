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
# <a name="windows-universal-apps-engagement-sdk-integration"></a>Windows universele Apps Engagement SDK-integratie
> [!div class="op_single_selector"]
> * [Universeel Windows](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

Deze procedure wordt beschreven Hallo eenvoudigste manier tooactivate Engagement Analytics en bewaking van functies in uw universele Windows-toepassing.

Hallo stappen te volgen zijn dat onvoldoende tooactivate Hallo rapport van Logboeken nodig toocompute alle statistische gegevens over gebruikers, sessies, activiteiten, Crashes en Technicals. rapport van Logboeken Hallo nodig toocompute andere statistieken zoals gebeurtenissen, fouten en taken moeten worden uitgevoerd handmatig met Hallo Engagement API (Zie [hoe toouse Hallo Mobile Engagement API in uw universele Windows-app-tagging geavanceerde](mobile-engagement-windows-store-use-engagement-api.md) sinds Deze statistieken zijn afhankelijk van de toepassing.

## <a name="supported-versions"></a>Ondersteunde versies
Hallo Mobile Engagement SDK voor Windows universele Apps kan alleen worden geïntegreerd in Windows Runtime en universele Windows-Platform-toepassingen die gericht is op:

* Windows 8
* Windows 8.1
* Windows Phone 8.1
* Windows 10 (desktop en mobiel families)

> [!NOTE]
> Als u ontwikkelt voor Windows Phone Silverlight verwijzen toohello [Windows Phone Silverlight-integratie procedure](mobile-engagement-windows-phone-integrate-engagement.md).
> 
> 

## <a name="install-hello-mobile-engagement-universal-apps-sdk"></a>Hallo Mobile Engagement universele Apps SDK installeren
### <a name="all-platforms"></a>Alle platforms
Hallo Mobile Engagement SDK voor universele Windows-App is beschikbaar als een Nuget-pakket aangeroepen *MicrosoftAzure.MobileEngagement*. U kunt deze installeren via Hallo Nuget Package Manager voor Visual Studio.

### <a name="windows-8x-and-windows-phone-81"></a>Windows 8.x en Windows Phone 8.1
NuGet automatisch wordt geïmplementeerd Hallo SDK bronnen in Hallo `Resources` map in de hoofdmap Hallo van uw toepassingsproject.

### <a name="windows-10-universal-windows-platform-applications"></a>Windows 10 Universal Windows Platform-toepassingen
NuGet distribueert Hallo SDK resources in uw UWP-toepassing nog niet automatisch. Hebt u het programma handmatig tot implementatie van resources wordt teruggeplaatst in NuGet toodo:

1. Open de Verkenner.
2. Navigeer toohello volgende op locatie (**x.x.x** Hallo-versie van Engagement u installeert): *% USERPROFILE %\\.nuget\packages\MicrosoftAzure.MobileEngagement\\*  *x.x.x**\\content\win81*
3. Slepen en neerzetten Hallo **Resources** map uit Hallo bestand explorer toohello hoofdmap van uw project in Visual Studio.
4. Selecteer uw project in Visual Studio en activeren Hallo **weergeven van alle bestanden** pictogram boven op Hallo **Solution Explorer**.
5. Sommige bestanden zijn niet opgenomen in het Hallo-project. ze in één keer Klik met de rechtermuisknop op Hallo tooimport **Resources** map **uitsluiten van project** en vervolgens een andere Klik met de rechtermuisknop op Hallo **Resources** map **opnemen in het project** toore-Hallo hele map bevatten. Alle bestanden uit Hallo **Resources** map nu zijn opgenomen in uw project.

## <a name="add-hello-capabilities"></a>Hallo mogelijkheden toevoegen
Hallo Engagement SDK moet enkele mogelijkheden van Hallo Windows SDK in de volgorde toowork goed.

Open uw `Package.appxmanifest` -bestand en zorg ervoor dat die Hallo volgende mogelijkheden worden gedefinieerd:

* `Internet (Client)`

## <a name="initialize-hello-engagement-sdk"></a>Hallo Engagement SDK initialiseren
### <a name="engagement-configuration"></a>Engagement configuratie
Hallo Engagement configuratie op Hallo is gecentraliseerd `Resources\EngagementConfiguration.xml` -bestand van uw project.

Dit bestand toospecify bewerken:

* De verbindingsreeks voor de toepassing tussen de tags `<connectionString>` en `<\connectionString>`.

Als u wilt dat deze tijdens runtime in plaats daarvan kunt u bellen Hallo volgende toospecify methode voordat de initialisatie van de agent Hallo Engagement:

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

Hallo-verbindingsreeks voor uw toepassing wordt weergegeven op Hallo klassieke Azure-Portal.

### <a name="engagement-initialization"></a>De initialisatie van de engagement
Wanneer u een nieuw project maakt een `App.xaml.cs` -bestand is gegenereerd. Deze klasse neemt over van `Application` en bevat veel belangrijke methoden. Dit wordt ook worden de gebruikte tooinitialize Hallo Engagement SDK.

Hallo wijzigen `App.xaml.cs`:

* Toevoegen van tooyour `using` instructies:
  
      using Microsoft.Azure.Engagement;
* Een methode tooshare Hallo Engagement initialisatie voor alle aanroepen eenmaal definiëren:
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* Roep `InitEngagement` in Hallo `OnLaunched` methode:
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* Wanneer uw toepassing wordt gestart met behulp van een aangepast schema, een andere toepassing of Hallo opdrachtregel vervolgens Hallo `OnActivated` methode wordt aangeroepen. U moet ook tooinitiate Hallo Engagement SDK wanneer uw app wordt geactiveerd. toodo dus overschrijven `OnActivated` methode:
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> We afraden raden u tooadd Hallo Engagement-initialisatie in een andere locatie van uw toepassing.
> 
> 

## <a name="basic-reporting"></a>Basic-rapportage
### <a name="recommended-method-overload-your-page-classes"></a>Aanbevolen methode: overbelasting uw `Page` klassen
In volgorde tooactivate Hallo rapport van alle Hallo Logboeken door Engagement toocompute gebruikers, sessies, activiteiten, Crashes en technische statistieken vereist, kunt u gewoon zodat alle uw `Page` onderliggende klassen overnemen van Hallo `EngagementPage` klassen.

Hier volgt een voorbeeld van hoe toodo dit voor een pagina van uw toepassing. U kunt doen Hallo hetzelfde geldt voor alle pagina's van uw toepassing.

#### <a name="c-source-file"></a>C#-bronbestand
Wijzigen van uw pagina `.xaml.cs` bestand:

* Toevoegen van tooyour `using` instructies:
  
      using Microsoft.Azure.Engagement;
* Vervang `Page` met `EngagementPage`:

**Zonder Engagement:**

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

**Met Engagement:**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> Als uw pagina Hallo overschrijft `OnNavigatedTo` methode ervoor toocall worden `base.OnNavigatedTo(e)`. Anders Hallo activiteit wordt niet gerapporteerd (Hallo `EngagementPage` aanroepen `StartActivity` binnen de `OnNavigatedTo` methode).
> 
> 

#### <a name="xaml-file"></a>XAML-bestand
Wijzigen van uw pagina `.xaml` bestand:

* Tooyour naamruimtedeclaraties toevoegen:
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* Vervang `Page` met `engagement:EngagementPage`:

**Zonder Engagement:**

        <Page>
            <!-- layout -->
            ...
        </Page>

**Met Engagement:**

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-hello-default-behaviour"></a>Hallo standaardwerking overschrijven
Standaard is als Hallo activiteitsnaam, zonder extra Hallo klassenaam van Hallo pagina gerapporteerd. Als Hallo klasse Hallo 'Pagina' achtervoegsel gebruikt, Engagement wordt het ook verwijderd.

Als u toooverride Hallo standaard gedrag voor de naam van de hello wilt, programmacode toe te voegen deze tooyour:

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

Als u een aantal extra informatie over tooreport met uw activiteiten wilt, kunt u deze code tooyour toevoegen:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

Deze methoden worden aangeroepen vanuit Hallo `OnNavigatedTo` methode van uw pagina.

### <a name="alternate-method-call-startactivity-manually"></a>Alternatieve methode: call `StartActivity()` handmatig
Als u niet kunt of toooverload niet wilt dat uw `Page` klassen, in plaats daarvan kunt u uw activiteiten starten door het aanroepen van `EngagementAgent` rechtstreeks methoden.

We raden aan toocall `StartActivity` binnen uw `OnNavigatedTo` methode van uw pagina.

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> Zorg ervoor dat u uw sessie correct beëindigen.
> 
> Hallo universele Windows SDK roept automatisch Hallo `EndActivity` methode wanneer de toepassing hello wordt gesloten. Het is dus **maximaal** toocall Hallo aanbevolen `StartActivity` methode wanneer Hallo activiteit van Hallo gebruiker wijzigt, en te**nooit** aanroep Hallo `EndActivity` methode deze methode verzendt tooEngagement Server dat de huidige gebruiker heeft verlaten Hallo toepassing, deze van invloed is op alle toepassingslogboeken.
> 
> 

## <a name="advanced-reporting"></a>Geavanceerde rapportage
Desgewenst kunt u tooreport toepassing specifieke gebeurtenissen, fouten en taken, toodo dus, gebruik andere methoden gevonden in Hallo Hallo `EngagementAgent` klasse. Hallo Engagement API kunt toouse alle Engagement geavanceerde mogelijkheden.

Zie voor meer informatie [hoe toouse Hallo Mobile Engagement API in uw universele Windows-app-tagging geavanceerde](mobile-engagement-windows-store-use-engagement-api.md).

## <a name="advanced-configuration"></a>Geavanceerde configuratie
### <a name="disable-automatic-crash-reporting"></a>Automatische crashrapporten uitschakelen
U kunt automatische Hallo-crash rapportagefunctie van Engagement uitschakelen. Vervolgens, als er wordt een niet-verwerkte uitzondering optreedt, Engagement is geen alles.

> [!WARNING]
> Als u van plan toodisable deze functie bent, houd er rekening mee dat wanneer het vastlopen van een niet-verwerkte in uw app optreden zal, Engagement geen Hallo crashes verzenden worden **en** Hallo-sessie en taken niet gesloten.
> 
> 

toodisable automatische crash rapportage, alleen uw configuratie, afhankelijk van Hallo manier waarop u het gedeclareerd aanpassen:

#### <a name="from-engagementconfigurationxml-file"></a>Van `EngagementConfiguration.xml` bestand
Rapport vastlopen te ingesteld`false` tussen `<reportCrash>` en `</reportCrash>` labels.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>Van `EngagementConfiguration` object tijdens runtime
Rapport crash toofalse met behulp van het object EngagementConfiguration ingesteld.

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>Burst-modus
Standaard Hallo Engagement servicerapporten Logboeken in realtime. Als uw toepassing Logboeken heel vaak rapporteert, is het beter toobuffer Hallo logboeken en tooreport ze allemaal tegelijk op een vaste tijd base (dit wordt Hallo 'burst modus' genoemd).

toodo worden dus Hallo-methode aanroept:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

Hallo-argument is een waarde in **milliseconden**. Op elk gewenst moment als u tooreactivate Hallo realtime logboekregistratie wilt, roept Hallo methode geen parameters of met de Hallo 0-waarde.

Hallo burst-modus iets langer Hallo accu levensduur maar heeft een invloed op Hallo Engagement-Monitor: alle sessies en taken duur zijn afgerond toohello burst drempelwaarde (dus sessies en korter zijn dan Hallo burst drempelwaarde is mogelijk niet zichtbaar taken). Het is aanbevolen toouse een ' burst ' drempelwaarde niet langer dan 30000 (30s). U hebt toobe Houd er rekening mee dat opgeslagen logboeken zijn beperkt too300-items. U kunt sommige logboeken verliezen als verzenden te lang is.

> [!WARNING]
> Hallo burst drempelwaarde kan niet worden geconfigureerd als tooa periode minder dan 1s. Als u dus toodo probeert, opnieuw Hallo SDK wordt een tracering met Hallo fout weergeven en automatisch toohello standaardwaarde, dat wil zeggen, 0s. Dit activeert Hallo SDK tooreport Hallo Logboeken in realtime.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

