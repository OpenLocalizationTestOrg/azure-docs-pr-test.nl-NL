---
title: Universele geavanceerde Reporting met MobileApps Engagement aaaWindows
description: Hoe tooIntegrate Azure Mobile Engagement met universele Windows-Apps
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a>Geavanceerde rapportage Hello Windows universele Apps Engagement SDK
> [!div class="op_single_selector"]
> * [Universeel Windows](mobile-engagement-windows-store-advanced-reporting.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

Dit onderwerp beschrijft aanvullende scenario's voor rapportage in uw universele Windows-toepassing. Deze scenario's omvatten opties die u tooapply toohello app gemaakt in Hallo kunt [aan de slag](mobile-engagement-windows-store-dotnet-get-started.md) zelfstudie.

## <a name="prerequisites"></a>Vereisten
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

Voordat u deze zelfstudie begint, moet u eerst Hallo voltooien [aan de slag](mobile-engagement-windows-store-dotnet-get-started.md) zelfstudie, namelijk opzettelijk direct en eenvoudig. Deze zelfstudie bevat informatie over aanvullende opties die u kunt kiezen uit.

## <a name="specifying-engagement-configuration-at-runtime"></a>Configuratie van de engagement tijdens runtime opgeven
Hallo Engagement configuratie op Hallo is gecentraliseerd `Resources\EngagementConfiguration.xml` -bestand van uw project, namelijk waarin deze is opgegeven in Hallo [aan de slag](mobile-engagement-windows-store-dotnet-get-started.md) onderwerp.

Maar u kunt dit ook opgeven tijdens runtime: u kunt de volgende methode voordat de initialisatie van de agent Engagement Hallo Hallo aanroepen:

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a>Aanbevolen methode: overbelasting uw `Page` klassen
alle tooactivate Hallo rapportage van alle Hallo logboeken vereist voor Engagement toocompute gebruikers, sessies, activiteiten, Crashes en technische statistieken maken uw `Page` onderliggende klassen overnemen van Hallo `EngagementPage` klassen.

Hier volgt een voorbeeld van een pagina van uw toepassing. U kunt doen Hallo hetzelfde geldt voor alle pagina's van uw toepassing.

### <a name="c-source-file"></a>C#-bronbestand
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

### <a name="xaml-file"></a>XAML-bestand
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

### <a name="override-hello-default-behaviour"></a>Hallo standaardwerking overschrijven
Standaard is als Hallo activiteitsnaam, zonder extra Hallo klassenaam van Hallo pagina gerapporteerd. Als Hallo klasse Hallo 'Pagina' achtervoegsel gebruikt, Engagement, wordt deze verwijderd.

toooverride hello standaardgedrag voor de naam van de hello, voeg deze code:

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

tooreport extra informatie aan de activiteit, voeg deze code:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

Deze methoden worden aangeroepen vanuit Hallo `OnNavigatedTo` methode van uw pagina.

### <a name="alternate-method-call-startactivity-manually"></a>Alternatieve methode: call `StartActivity()` handmatig
Als u niet kunt of toooverload niet wilt dat uw `Page` klassen, in plaats daarvan kunt u uw activiteiten starten door het aanroepen van `EngagementAgent` rechtstreeks methoden.

We raden aan aanroepen `StartActivity` binnen uw `OnNavigatedTo` methode van uw pagina.

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> Zorg ervoor dat u uw sessie correct beëindigen.
> 
> Hallo universele Windows SDK roept automatisch Hallo `EndActivity` methode wanneer de toepassing hello wordt gesloten. Het is dus **maximaal** toocall Hallo aanbevolen `StartActivity` methode wanneer Hallo activiteit van Hallo gebruiker wijzigt, en te**nooit** aanroep Hallo `EndActivity` methode. Deze methode waarschuwt Hallo Engagement server dat Hallo huidige gebruiker heeft verlaten Hallo toepassing; dit is van invloed op alle toepassingslogboeken.
> 
> 

## <a name="advanced-reporting"></a>Geavanceerde rapportage
Desgewenst kunt u tooreport toepassingsspecifieke gebeurtenissen, fouten en taken, toodo dus, gebruik andere methoden gevonden in Hallo Hallo `EngagementAgent` klasse. Hallo Engagement API staat het gebruik van geavanceerde mogelijkheden voor alle Engagement.

Zie voor meer informatie [hoe toouse Hallo Mobile Engagement API in uw universele Windows-app-tagging geavanceerde](mobile-engagement-windows-store-use-engagement-api.md).

