---
title: aaaTroubleshoot BizTalk Services met behulp van bewerkingslogboeken | Microsoft Docs
description: Problemen oplossen met bewerkingslogboeken BizTalk-Services. MABS, WABS
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 1081a9c6-58cc-4a76-8ac8-11e5e7a6ea27
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 102779ed6e29784f190c28e4102a7d9670614914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-troubleshoot-using-operation-logs"></a>BizTalk Services: Problemen oplossen met bewerkingslogboeken

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="what-are-hello-operation-logs"></a>Wat zijn de Bewerkingslogboeken Hallo
Bewerkingslogboeken is een beschikbaar in de klassieke Azure-portal kunt u historische logboeken van de bewerkingen die worden uitgevoerd op uw Azure-services, met inbegrip van BizTalk Services tooview Hallo Management Services-functie. Hiermee kunt u historische gegevens tooview gerelateerde toomanagement bewerkingen voor uw BizTalk Service-abonnement tot 180 dagen.

> [!NOTE]
> Deze functie bevat alleen de logboeken voor beheerbewerkingen op BizTalk Services, zoals wanneer Hallo-service is gestart, een back-up, enzovoort gemaakt. Deze bewerkingen worden bijgehouden ongeacht of ze worden uitgevoerd vanuit Hallo klassieke Azure-portal of met behulp van Hallo [BizTalk Service REST-API's](http://msdn.microsoft.com/library/azure/dn232347.aspx). Zie voor een volledige lijst van bewerkingen die worden bijgehouden met beheerservices [bewerkingen bijgehouden met behulp van Azure Management Services](#bizops).<br/><br/>
> Dit wordt niet vastgelegd Hallo-logboeken voor activiteiten, gerelateerde tooBizTalk Service runtime (zoals bericht verwerkt door bruggen, enzovoort.). tooview deze zich aanmeldt, gebruik Hallo bijhouden weergave van Hallo BizTalk Services-portal. Zie voor meer informatie [berichten bijhouden](http://msdn.microsoft.com/library/azure/hh949805.aspx).
> 
> 

## <a name="view-biztalk-services-operation-logs"></a>BizTalk Services Bewerkingslogboeken weergeven
1. Selecteer in de klassieke Azure-portal hello, **beheerservices**, en selecteer vervolgens Hallo **Bewerkingslogboeken** tabblad.
2. U kunt filteren Hallo logboeken op basis van verschillende parameters zoals abonnement, datumbereik, servicetype (bijvoorbeeld BizTalk Services), servicenaam of status van Hallo-bewerking (geslaagd, mislukt).
3. Selecteer Hallo vinkje tooview Hallo gefilterde lijst. Hallo volgende afbeelding toont activiteiten, gerelateerde tootestbiztalkservice: ![bewerkingslogboeken weergeven][ViewLogs] 
4. tooview meer informatie over een specifieke bewerking Hallo rij selecteren en op **Details** in de taakbalk Hallo Hallo onderaan.

## <a name="bizops"></a>Bewerkingen bijgehouden met Azure Management-Services
Hallo bevat volgende tabel Hallo-bewerkingen die worden bijgehouden met hello Azure Management Services:

| De naam van bewerking | Taak |
| --- | --- |
| CreateBizTalkService |Bewerking toocreate een nieuwe BizTalk Service |
| DeleteBizTalkService |Bewerking toodelete een BizTalk Service |
| RestartBizTalkService |Bewerking toorestart een BizTalk Service |
| StartBizTalkService |Bewerking toostart een BizTalk Service |
| StopBizTalkService |Bewerking toostop een BizTalk Service |
| DisableBizTalkService |Bewerking toodisable een BizTalk Service |
| EnableBizTalkService |Bewerking tooenable een BizTalk Service |
| BackupBizTalkService |Bewerking tooback van een BizTalk Service |
| RestoreBizTalkService |Bewerking toorestore een BizTalk Service van de opgegeven back-up |
| SuspendBizTalkService |Bewerking toosuspend een BizTalk Service |
| ResumeBizTalkService |Bewerking tooresume een BizTalk Service |
| ScaleBizTalkService |Bewerking tooscale een BizTalk Service omhoog of omlaag |
| ConfigUpdateBizTalkService |Bewerking tooupdate Hallo configuratie van een BizTalk Service |
| ServiceUpdateBizTalkService |Bewerking tooupgrade of een downgrade van een andere versie van BizTalk Service tooa |
| PurgeBackupBizTalkService |Bewerking toopurge back-ups van Hallo BizTalk Service buiten de bewaarperiode Hallo |

## <a name="see-also"></a>Zie ook
* [Back-up van BizTalk-Service](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [BizTalk Service back-up terugzetten](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [BizTalk Services: Developer, Basic, Standard en Premium-edities grafiek](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [BizTalk Services: Inrichten met behulp van Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [BizTalk Services: statusgrafiek voor de inrichting](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [BizTalk Services: de tabbladen Dashboard, Bewaken en Schalen](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [BizTalk Services: beperking](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [BizTalk Services: naam en sleutel van verlener](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [Hoe gaan gebruiken Azure BizTalk Services SDK Hallo](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[ViewLogs]: ./media/biztalk-troubleshoot-using-ops-logs/Operation-Logs.png

