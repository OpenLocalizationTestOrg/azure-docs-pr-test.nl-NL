---
title: aaaWindows Phone Silverlight-SDK Upgrade Procedures
description: Windows Phone Silverlight-SDK upgradeprocedures voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d72e7b8a59ef2c0a95b22efbf1e5257271399ddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a>Windows Phone Silverlight-SDK upgradeprocedures
Als u hebt al een oudere versie van onze SDK geïntegreerd in uw toepassing, hebt u tooconsider Hallo volgende punten bij het upgraden van Hallo SDK.

Mogelijk hebt u toofollow verschillende procedures als u verschillende versies van Hallo SDK gemist. Bijvoorbeeld als u migreert vanaf 0.10.1 too0.11.0 hebt toofirst Volg Hallo ' van 0.9.0 too0.10.1 ' procedure vervolgens Hallo ' van 0.10.1 too0.11.0 ' procedure.

## <a name="from-200-too330"></a>Van 2.0.0 too3.3.0
### <a name="test-logs"></a>Test-Logboeken
De logboeken van de console die wordt geproduceerd door Hallo SDK kunnen worden ingeschakeld/uitgeschakeld/gefilterd. toocustomize deze, update Hallo eigenschap `EngagementAgent.Instance.TestLogEnabled` tooone van Hallo waarde in Hallo `EngagementTestLogLevel` opsomming, bijvoorbeeld:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

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

Daarna Hallo nieuwe Microsoft Azure Engagement nuget-pakket te installeren op uw project. U vindt deze op [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement). Deze actie vervangt alle bestanden van de resources gebruikt door Engagement en voegt het nieuwe Engagement DLL tooyour Hallo project verwijzingen.

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
4. Hallo voor andere bronnen zoals Capptain afbeeldingen, houd er rekening mee dat ze ook zijn gewijzigd toouse 'Engagement'.

### <a name="application-id--sdk-key"></a>Toepassings-ID / SDK-sleutel
Engagement maakt gebruik van een verbindingsreeks. U hebt geen toospecify een toepassings-ID en een met Mobile Engagement SDK-sleutel, u hoeft alleen toospecify een verbindingsreeks. U kunt deze functie instellen op uw EngagementConfiguration-bestand.

Hallo Engagement configuratie kan worden ingesteld in uw `Resources\EngagementConfiguration.xml` -bestand van uw project.

Dit bestand toospecify bewerken:

* De verbindingsreeks voor de toepassing tussen de tags `<connectionString>` en `<\connectionString>`.

Als u wilt dat deze tijdens runtime in plaats daarvan kunt u bellen Hallo volgende toospecify methode voordat de initialisatie van de agent Hallo Engagement:

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

Hallo-verbindingsreeks voor uw toepassing wordt weergegeven in de klassieke Azure-Portal Hallo.

### <a name="items-name-change"></a>Wijziging van items
Alle items met de naam *capptain* naam hebt gegeven *engagement*. Op dezelfde manier voor *Capptain* te*Engagement*.

Voorbeelden van veelgebruikte Capptain items:

* CapptainConfiguration EngagementConfiguration nu met de naam
* CapptainAgent EngagementAgent nu met de naam
* CapptainReach EngagementReach nu met de naam
* CapptainHttpConfig EngagementHttpConfig nu met de naam
* GetCapptainPageName GetEngagementPageName nu met de naam

Houd er rekening mee dat rename ook van invloed op overschreven methoden.

