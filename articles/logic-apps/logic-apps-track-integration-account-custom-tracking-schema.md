---
title: bijhouden van schema's voor B2B aaaCustom monitoring - Azure Logic Apps | Microsoft Docs
description: Bijhouden van aangepaste schema's toomonitor B2B-berichten van transacties in uw Azure-integratie-Account maken.
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a>Uw volledige werkstroom, end-to-end voor bijhouden toomonitor inschakelen
Er is ingebouwde bijhouden dat u voor de verschillende onderdelen van uw business-to-business-werkstroom, zoals bijhouden AS2 of X12 berichten inschakelen kunt. Wanneer u werkstromen met een logische app, BizTalk Server, SQL Server of een andere laag maakt, kunt u aangepaste bijhouden die legt gebeurtenissen van Hallo begin toohello einde van uw werkstroom vast. 

Dit onderwerp bevat aangepaste code die u in Hallo lagen buiten uw logische app gebruiken kunt. 

## <a name="custom-tracking-schema"></a>Bijhouden van aangepaste schema
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| Eigenschap | Type | Beschrijving |
| --- | --- | --- |
| SourceType |   | Type bron Hallo uitvoeren. Toegestane waarden zijn **Microsoft.Logic/workflows** en **aangepaste**. (Verplicht) |
| Bron |   | Als het brontype Hallo **Microsoft.Logic/workflows**, Hallo broninformatie moet toofollow dit schema. Als het brontype Hallo **aangepaste**, Hallo-schema is een JToken. (Verplicht) |
| systeem-id | Tekenreeks | Logic app systeem-ID. (Verplicht) |
| runId | Tekenreeks | Logische app uitgevoerd ID. (Verplicht) |
| operationName | Tekenreeks | Naam van bewerking hello (bijvoorbeeld actie of trigger). (Verplicht) |
| repeatItemScopeName | Tekenreeks | Herhaal itemnaam als Hallo actie binnen een `foreach` / `until` lus. (Verplicht) |
| repeatItemIndex | Geheel getal | Of Hallo actie is binnen een `foreach` / `until` lus. Hiermee wordt aangegeven Hallo herhaalde itemindex. (Verplicht) |
| trackingId | Tekenreeks | Tracerings-ID, toocorrelate Hallo-berichten. (Optioneel) |
| correlationId | Tekenreeks | Correlatie-ID, toocorrelate Hallo-berichten. (Optioneel) |
| clientRequestId | Tekenreeks | Client kan het vullen toocorrelate berichten. (Optioneel) |
| eventLevel |   | Niveau van het Hallo-gebeurtenis. (Verplicht) |
| eventTime |   | Tijd van de Hallo gebeurtenis, in UTC-notatie jjjj-MM-DDTHH:MM:SS.00000Z. (Verplicht) |
| recordType |   | Type Hallo bijhouden record. De waarde is toegestaan **aangepaste**. (Verplicht) |
| Record |   | Aangepaste recordtype. Toegestane indeling is JToken. (Verplicht) |

## <a name="b2b-protocol-tracking-schemas"></a>Schema's voor bijhouden van B2B-protocol
Zie voor informatie over B2B-protocol voor het bijhouden van schema's:
* [Volgschema’s voor AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [Volgschema’s voor X12](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [B2B-berichten controleren](logic-apps-monitor-b2b-message.md).   
* Meer informatie over [B2B-berichten in de Operations Management Suite-portal Hallo traceren](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
* Meer informatie over Hallo [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).
