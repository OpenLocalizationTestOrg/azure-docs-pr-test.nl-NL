---
title: aaaAzure Mobile Engagement Windows universele SDK-integratie | Microsoft Docs
description: Universele integratie van Windows voor de SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ded187d-5c07-4377-a41c-ce205dd38b50
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: 2f88e58adb349a2a4eb43b0f182f99b3e8b8cfd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-sdk-integration-for-azure-mobile-engagement"></a>Windows universele SDK-integratie voor Azure Mobile Engagement
Dit document beschrijft alle Hallo-integratie en configuratieopties voor hello Azure Mobile Engagement universele Windows SDK beschikbaar.

## <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, moet u eerst voltooien onze [15 minuten zelfstudie](mobile-engagement-windows-store-dotnet-get-started.md).

## <a name="advanced-features"></a>Geavanceerde functies
### <a name="reporting-features"></a>Rapportagefuncties
U kunt deze functies kunt toevoegen:

1. [Geavanceerde opties voor rapportage](mobile-engagement-windows-store-advanced-reporting.md)
2. [Geavanceerde configuratieopties](mobile-engagement-windows-store-advanced-configuration.md)

### <a name="notifications"></a>Meldingen
[Hoe toointegrate Reach (meldingen) in uw universele Windows-app](mobile-engagement-windows-store-integrate-engagement-reach.md)

### <a name="tag-plan-implementation"></a>Tag plan implementatie:
[Hoe toouse Hallo Geavanceerd Mobile Engagement tagging API in uw universele Windows-app](mobile-engagement-windows-store-use-engagement-api.md)

## <a name="release-notes"></a>Releaseopmerkingen
### <a name="341-11032016"></a>3.4.1 (11/03/2016)

* Verbeteringen in stabiliteit.

Zie voor eerdere versies Hallo [voltooien release-opmerkingen](mobile-engagement-windows-store-release-notes.md)

## <a name="upgrade-procedures"></a>Upgradeprocedures
Als u hebt al een oudere versie van Engagement geïntegreerd in uw toepassing, hebt u tooconsider Hallo volgende punten bij het upgraden van Hallo SDK.

Als u verschillende versies van Hallo SDK gemist, hebben verschillende procedures toofollow. Zie Hallo voltooid [Procedures Upgrade](mobile-engagement-windows-store-upgrade-procedure.md). Bijvoorbeeld als u migreert vanaf 0.10.1 too0.11.0 hebt toofirst Volg Hallo ' van 0.9.0 too0.10.1 ' procedure vervolgens Hallo ' van 0.10.1 too0.11.0 ' procedure.

### <a name="from-330-too340"></a>Van 3.3.0 too3.4.0
#### <a name="test-logs"></a>Test-Logboeken
De logboeken van de console die wordt geproduceerd door Hallo SDK kunnen worden ingeschakeld/uitgeschakeld/gefilterd. toocustomize, de eigenschap Hallo update `EngagementAgent.Instance.TestLogEnabled` tooone van Hallo waarden beschikbaar is via Hallo `EngagementTestLogLevel` opsomming, bijvoorbeeld:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

#### <a name="resources"></a>Resources
Hallo Reach-overlay is verbeterd. Het uitmaakt deel van Hallo SDK NuGet-pakket resources.

Tijdens het upgraden van de nieuwe versie toohello Hallo SDK kunt u kiezen dat of u tookeep wilt de bestaande bestanden uit Hallo map van uw resources overlay of niet:

* Als vorige overlay Hallo u werkt of u Hallo integreert `WebView` elementen handmatig, klikt u vervolgens kunt u bepalen tookeep uw afgesloten bestanden, werkt nog steeds.
* tooupdate toohello nieuwe overlay vervangen Hallo hele `overlay` map van uw resources Hello nieuwe van Hallo SDK-pakket (UWP-apps: na de upgrade hello, kunt u Hallo nieuwe overlay map ophalen van % USERPROFILE %\\.nuget\packages\ MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).

> [!WARNING]
> Met behulp van de nieuwe overlay Hallo overschrijft aanpassingen op de vorige versie Hallo.
> 
> 

### <a name="upgrade-from-older-versions"></a>Upgraden van oudere versies
Zie [Procedures upgraden](mobile-engagement-windows-store-upgrade-procedure.md)

