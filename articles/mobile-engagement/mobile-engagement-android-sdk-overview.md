---
title: aaaAndroid voor Azure Mobile Engagement SDK-integratie
description: Hierin wordt beschreven hoe toointegrate Azure Mobile Engagement SDK in de Android-apps
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a91ed04f-f3ce-4692-a6dd-b56a28d7dee8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo;ricksal
ms.openlocfilehash: 0c63bfaf673abbda7ea498390f8282c43e2fb8df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a>Android SDK-integratie voor Azure Mobile Engagement
> [!div class="op_single_selector"]
> * [Universeel Windows](mobile-engagement-windows-store-sdk-overview.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-sdk-overview.md)
> * [iOS](mobile-engagement-ios-sdk-overview.md)
> * [Android](mobile-engagement-android-sdk-overview.md)
> 
> 

Dit document beschrijft alle Hallo-integratie en configuratieopties beschikbaar voor Azure Mobile Engagement Android SDK.

## <a name="prerequisites"></a>Vereisten
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a>Geavanceerde functies
### <a name="reporting-features"></a>Rapportagefuncties
U kunt deze functies kunt toevoegen:

1. [Geavanceerde opties voor rapportage](mobile-engagement-android-advanced-reporting.md)
2. [Locatie rapportage-opties](mobile-engagement-android-location-reporting.md)
3. [Geavanceerde configuratieopties](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a>Meldingen:
[Hoe toointegrate Reach (meldingen) in uw Android-app](mobile-engagement-android-integrate-engagement-reach.md)

1. Google Cloud Messaging (GCM): [hoe tooIntegrate GCM met Mobile Engagement](mobile-engagement-android-gcm-integrate.md)
2. Amazon Device Messaging (ADM): [hoe tooIntegrate ADM met Mobile Engagement](mobile-engagement-android-adm-integrate.md)

### <a name="tag-plan-implementation"></a>Tag plan implementatie:
[Hoe toouse Hallo Geavanceerd Mobile Engagement tags API in uw Android-app](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a>Releaseopmerkingen

### <a name="431-07172017"></a>4.3.1 (07/17/2017)
* Herstel van een crash die zelden optreden kan bij het aanroepen van `EngagementAgentUtils.isInDedicatedEngagementProcess`, die ook wordt gebruikt door Hallo `EngagementApplication` klasse.

### <a name="430-06272017"></a>4.3.0 (06/27/2017)
* Android 8-ondersteuning (vorige versies van Hallo SDK niet in Android 8 werken).
* Er is geen meer afhankelijkheid van ondersteuningsbibliotheek.
* Verwijder `EngagementFragmentActivity` klasse.
* Vervaldatum te[achtergrond uitvoering limieten](https://developer.android.com/preview/features/background.html) op Android 8 logboeken op de achtergrond kunnen worden uitgesteld totdat Hallo gebruiker werkt met Hallo-apparaat, wordt dit een invloed hebben op campagne Push **geleverd** en **Systeemmelding weergegeven** statistieken als Hallo-apparaat is in de slaapstand wordt uitgesteld (Hallo melding nog wel weergegeven, wordt ring en Trillen in realtime zonder problemen).
* Vervaldatum te[achtergrond locatie limieten](https://developer.android.com/preview/features/background-location-limits.html), Hallo realtime locatie op de achtergrond wordt niet vaak op Android 8 worden bijgewerkt.

Zie voor alle versies Hallo [voltooien releaseopmerkingen](mobile-engagement-android-release-notes.md).

## <a name="upgrade-procedures"></a>Upgradeprocedures
Als u hebt al een oudere versie van onze SDK geïntegreerd in uw toepassing, raadpleegt u [Procedures Upgrade](mobile-engagement-android-upgrade-procedure.md).

