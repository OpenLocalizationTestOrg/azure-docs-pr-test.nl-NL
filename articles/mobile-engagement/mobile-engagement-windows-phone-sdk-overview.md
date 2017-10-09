---
title: Overzicht van Mobile Engagement Windows Phone Silverlight-SDK aaaAzure | Microsoft Docs
description: Overzicht van Windows Phone Silverlight-SDK voor Azure Mobile Engagement Hallo
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0e3d2420-0509-4952-8891-392e3dad9aaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: ff2febed2202127e0538373ebbabe674993ce39d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-overview-for-azure-mobile-engagement"></a>Windows Phone Silverlight-SDK overzicht voor Azure Mobile Engagement
Begin hier tooget Hallo details over het toointegrate Azure Mobile Engagement in een Windows Phone Silverlight-App. Als u toogive wilt het probeer Controleer eerst of u voltooid onze [15 minuten zelfstudie](mobile-engagement-windows-phone-get-started.md).

Klik op toosee hello [SDK-inhoud](mobile-engagement-windows-phone-sdk-content.md)

## <a name="integration-procedures"></a>Integratie procedures
1. Begin hier: [hoe toointegrate Mobile Engagement in uw Windows Phone Silverlight-app](mobile-engagement-windows-phone-integrate-engagement.md)
2. Voor meldingen: [hoe toointegrate Reach (meldingen) in uw Windows Phone Silverlight-app](mobile-engagement-windows-phone-integrate-engagement-reach.md)
3. Tag plan implementatie: [hoe toouse Hallo Geavanceerd Mobile Engagement tagging API in uw Windows Phone Silverlight-app](mobile-engagement-windows-phone-use-engagement-api.md)

## <a name="release-notes"></a>Releaseopmerkingen
###<a name="331-11032016"></a>3.3.1 (11/03/2016)
Onderdeel van Hallo *MicrosoftAzure.MobileEngagement* Nuget-pakket **v3.4.1**

* Verbeteringen in stabiliteit.

Zie voor een eerdere versie Hallo [voltooien release-opmerkingen](mobile-engagement-windows-phone-release-notes.md)

## <a name="upgrade-procedures"></a>Upgradeprocedures
Als u hebt al een oudere versie van onze SDK geïntegreerd in uw toepassing, hebt u tooconsider Hallo volgende punten bij het upgraden van Hallo SDK.

Mogelijk hebt u toofollow verschillende procedures als u verschillende versies van Hallo SDK gemist. Zie Hallo voltooid [Procedures Upgrade](mobile-engagement-windows-phone-upgrade-procedure.md). Bijvoorbeeld als u migreert vanaf 0.10.1 too0.11.0 hebt toofirst Volg Hallo ' van 0.9.0 too0.10.1 ' procedure vervolgens Hallo ' van 0.10.1 too0.11.0 ' procedure.

### <a name="from-200-too330"></a>Van 2.0.0 too3.3.0
#### <a name="test-logs"></a>Test-Logboeken
De logboeken van de console die wordt geproduceerd door Hallo SDK kunnen worden ingeschakeld/uitgeschakeld/gefilterd. toocustomize deze, update Hallo eigenschap `EngagementAgent.Instance.TestLogEnabled` tooone van Hallo waarde in Hallo `EngagementTestLogLevel` opsomming, bijvoorbeeld:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="upgrade-from-older-versions"></a>Upgraden van oudere versies
Zie [Procedures upgraden](mobile-engagement-windows-phone-upgrade-procedure.md)

