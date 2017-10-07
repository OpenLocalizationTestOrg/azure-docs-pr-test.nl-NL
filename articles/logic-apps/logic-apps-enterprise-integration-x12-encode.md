---
title: aaaEncode X12 berichten - Azure Logic Apps | Microsoft Docs
description: EDI valideren en converteren XML-codering berichten met X12 bericht encoder in Enterprise Integration Pack Hallo voor Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 785dbd2c7c82463154732921e07e3586d2307840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Codeer X12 berichten voor Azure Logic Apps Hello Enterprise Integration Pack

Met Hallo coderen X12 bericht connector kunt u valideren EDI- en partner-specifieke eigenschappen, XML-codering berichten converteren naar EDI transactie sets in een Hallo interchange en aanvragen van een bevestiging van technische, functionele bevestiging of beide.
toouse deze connector, moet u Hallo connector tooan bestaande trigger in uw logische app toevoegen.

## <a name="before-you-start"></a>Voordat u begint

Hier volgt Hallo items die u nodig:

* Een Azure-account; kunt u een [gratis account](https://azure.microsoft.com/free)
* Een [integratie account](logic-apps-enterprise-integration-create-integration-account.md) die al is gedefinieerd en die zijn gekoppeld aan uw Azure-abonnement. U moet een connector integratie account toouse Hallo coderen X12 bericht hebben.
* Ten minste twee [partners](logic-apps-enterprise-integration-partners.md) die al zijn gedefinieerd in uw account integratie
* Een [X12 overeenkomst](logic-apps-enterprise-integration-x12.md) die al is gedefinieerd in uw account integratie

## <a name="encode-x12-messages"></a>Codeer X12 berichten

1. [Een logische app maken](logic-apps-create-a-logic-app.md).

2. Hallo coderen X12 bericht connector geen triggers, dus moet u een trigger voor het starten van uw logische app, zoals een aanvraag-trigger toevoegen. In Hallo Logic App-ontwerper, een trigger toevoegen en voeg vervolgens een actie tooyour logische app.

3.  Voer in het zoekvak hello, 'x12' voor uw filter. Selecteer een **X12-tooX12 bericht coderen door de naam van de overeenkomst** of **X12-tooX12 bericht coderen met identiteiten**.
   
    ![Zoek naar 'x12'](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. Als u niet alle verbindingen eerder tooyour integratie account maakt, wordt u gevraagd toocreate nu dat connection. Naam van uw verbinding en Hallo integratie-account dat u wilt dat tooconnect selecteren. 
   
    ![integratie-account verbinding](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    Eigenschappen met een sterretje zijn vereist.

    | Eigenschap | Details |
    | --- | --- |
    | Verbindingsnaam * |Voer een naam voor de verbinding. |
    | Integratie Account * |Voer een naam voor uw account integratie. Zorg ervoor dat uw account en logica app voor integratie in Hallo dezelfde Azure-locatie. |

5.  Wanneer u bent klaar, ziet uw Verbindingsdetails vergelijkbaar toothis voorbeeld. maken van uw verbinding toofinish kiezen **maken**.

    ![integratie-account verbinding is gemaakt](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    De verbinding wordt nu gemaakt.

    ![de accountdetails verbinding integratie](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a>Codeer X12 berichten door de naam van de overeenkomst

Als u hebt gekozen tooencode X12 berichten door de naam van de overeenkomst, open Hallo **naam van X12 overeenkomst** lijst Typ of Selecteer uw bestaande X12 overeenkomst. Voer Hallo XML-bericht tooencode.

![Voer X12 overeenkomst naam en het XML-bericht tooencode](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a>Codeer X12 berichten door identiteiten

Als u tooencode X12 berichten door identiteiten kiest, Hallo afzender-id, kwalificatie afzender, ontvanger-id en ontvanger kwalificatie invoeren zoals geconfigureerd in uw x12-overeenkomst(en) overeenkomst. Selecteer Hallo XML-bericht tooencode.
   
![Geef identiteiten voor een afzender en ontvanger, selecteer van XML-bericht tooencode](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a>X12 details coderen

Hallo X12 coderen connector voert deze taken uit:

* De resolutie van de overeenkomst door overeenkomende zender en ontvanger context-eigenschappen.
* Hallo EDI uitwisseling van berichten XML-indeling converteren naar EDI transactie sets in een Hallo interchange serialiseert.
* Transactie set-header en trailer segmenten van toepassing is
* Genereren van een besturingselement interchange getal, een besturingselement groepsnummer en een getal voor het instellen van transactie voor elke uitgaande uitwisseling
* Vervangt scheidingstekens in Hallo-nettolading
* Valideert EDI en partner-specifieke eigenschappen
  * Schemavalidatie van Hallo transactie-set gegevenselementen tegen Schema het Hallo-bericht
  * EDI gevalideerd gegevenselementen transactie-set.
  * Uitgebreide validatie uitgevoerd op van de transactie-set-gegevenselementen
* Vraagt om bevestiging van de technische en/of functionele (indien geconfigureerd).
  * Een technische bevestiging genereert als gevolg van header-validatie. Hallo technische bevestiging rapporten Hallo status van Hallo verwerking van een DIF-header en trailer door Hallo adres ontvanger
  * Een functionele bevestiging genereert als gevolg van validatie van de hoofdtekst. Hallo rapporten functionele bevestiging elke fout is opgetreden bij het verwerken Hallo document ontvangen

## <a name="view-hello-swagger"></a>Weergave Hallo swagger
Zie Hallo [swagger details](/connectors/x12/). 

## <a name="next-steps"></a>Volgende stappen
[Meer informatie over Enterprise Integration Pack Hallo](logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack") 

