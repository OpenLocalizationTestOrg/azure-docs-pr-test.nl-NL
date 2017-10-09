---
title: aaaEncode EDIFACT berichten - Azure Logic Apps | Microsoft Docs
description: EDI valideren en genereren van XML met EDIFACT berichtencoder in Enterprise Integration Pack Hallo voor Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: b3799dbd2492adef597022d017cf28f5ceb1085c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>EDIFACT-berichten voor Azure Logic Apps Hello Enterprise Integration Pack coderen

Met Hallo coderen EDIFACT bericht connector, kunt u valideren EDI- en partner-specifieke eigenschappen, een XML-document voor elke set transactie genereren en aanvragen van een bevestiging van technische, functionele bevestiging of beide.
toouse deze connector, moet u Hallo connector tooan bestaande trigger in uw logische app toevoegen.

## <a name="before-you-start"></a>Voordat u begint

Hier volgt Hallo items die u nodig:

* Een Azure-account; kunt u een [gratis account](https://azure.microsoft.com/free)
* Een [integratie account](logic-apps-enterprise-integration-create-integration-account.md) die al is gedefinieerd en die zijn gekoppeld aan uw Azure-abonnement. U moet een connector integratie account toouse Hallo coderen EDIFACT bericht hebben. 
* Ten minste twee [partners](logic-apps-enterprise-integration-partners.md) die al zijn gedefinieerd in uw account integratie
* Een [EDIFACT overeenkomst](logic-apps-enterprise-integration-edifact.md) die al is gedefinieerd in uw account integratie

## <a name="encode-edifact-messages"></a>EDIFACT-berichten te coderen

1. [Een logische app maken](logic-apps-create-a-logic-app.md).

2. Hallo coderen EDIFACT bericht connector geen triggers, dus moet u een trigger voor het starten van uw logische app, zoals een aanvraag-trigger toevoegen. In Hallo Logic App-ontwerper, een trigger toevoegen en voeg vervolgens een actie tooyour logische app.

3.  Voer in het zoekvak hello, 'EDIFACT' als filter. Selecteer een **coderen EDIFACT bericht met de Overeenkomstnaam** of **coderen tooEDIFACT bericht door identiteiten**.
   
    ![EDIFACT zoeken](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. Als u niet alle verbindingen eerder tooyour integratie account maakt, wordt u gevraagd toocreate nu dat connection. Naam van uw verbinding en Hallo integratie-account dat u wilt dat tooconnect selecteren.

    ![integratie-account verbinding maken](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    Eigenschappen met een sterretje zijn vereist.

    | Eigenschap | Details |
    | --- | --- |
    | Verbindingsnaam * |Voer een naam voor de verbinding. |
    | Integratie Account * |Voer een naam voor uw account integratie. Zorg ervoor dat uw account en logica app voor integratie in Hallo dezelfde Azure-locatie. |

5.  Wanneer u bent klaar, ziet uw Verbindingsdetails vergelijkbaar toothis voorbeeld. maken van uw verbinding toofinish kiezen **maken**.

    ![de accountdetails verbinding integratie](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    De verbinding wordt nu gemaakt.

    ![integratie-account verbinding is gemaakt](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a>EDIFACT-bericht met de Overeenkomstnaam coderen

Als u hebt gekozen tooencode EDIFACT berichten door de naam van de overeenkomst, open Hallo **overeenkomst met de naam van EDIFACT** lijst, typ of Selecteer de naam van de overeenkomst EDIFACT. Voer Hallo XML-bericht tooencode.

![Voer de naam van de overeenkomst EDIFACT en XML-bericht tooencode](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a>EDIFACT-bericht met identiteiten coderen

Als u tooencode EDIFACT berichten door identiteiten kiest, Voer Hallo afzender-id, kwalificatie afzender, ontvanger-id en ontvanger kwalificatie zoals geconfigureerd in uw EDIFACT-overeenkomst. Selecteer Hallo XML-bericht tooencode.

![Geef identiteiten voor een afzender en ontvanger, selecteer van XML-bericht tooencode](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a>Details EDIFACT coderen

Hallo coderen EDIFACT connector voert deze taken uit: 

* Hallo overeenkomst oplossen door het overeenkomende Hallo afzender kwalificatie & -id en ontvanger kwalificatie en id
* Hallo EDI uitwisseling van berichten XML-indeling converteren naar EDI transactie sets in een Hallo interchange serialiseert.
* Transactie set-header en trailer segmenten van toepassing is
* Genereren van een besturingselement interchange getal, een besturingselement groepsnummer en een getal voor het instellen van transactie voor elke uitgaande uitwisseling
* Vervangt scheidingstekens in Hallo-nettolading
* Valideert EDI en partner-specifieke eigenschappen
  * Schemavalidatie van Hallo transactie-set gegevenselementen volgens het schema voor Hallo-bericht.
  * EDI gevalideerd gegevenselementen transactie-set.
  * Uitgebreide validatie uitgevoerd op van de transactie-set-gegevenselementen
* Genereert een XML-document voor elke set transactie.
* Vraagt om bevestiging van de technische en/of functionele (indien geconfigureerd).
  * Een technische bevestiging duidt CONTRL het Hallo-bericht ontvangst van een knooppunt.
  * Als een functionele bevestiging CONTRL het Hallo-bericht geeft aan acceptatie- of afwijzing van Hallo ontvangen interchange, groep of -bericht, een lijst met fouten of niet-ondersteunde functies

## <a name="view-swagger-file"></a>Swagger-bestand weergeven
tooview hello Swagger voor Hallo EDIFACT connector, Zie [EDIFACT](/connectors/edifact/).

## <a name="next-steps"></a>Volgende stappen
[Meer informatie over Enterprise Integration Pack Hallo](logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack") 

