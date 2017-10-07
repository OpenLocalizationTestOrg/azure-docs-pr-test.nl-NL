---
title: aaaDecode X12 berichten - Azure Logic Apps | Microsoft Docs
description: EDI valideren en genereren van bevestigingen met Hallo X12 bericht decoder in Enterprise Integration Pack Hallo voor Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 4fd48d2d-2008-4080-b6a1-8ae183b48131
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 1ffececca1ff835b319b64c85f86c421395833c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Decoderen X12 berichten voor Azure Logic Apps Hello Enterprise Integration Pack

Met Hallo decoderen X12 bericht-connector, kunt u valideren Hallo envelop tegen een handelspartnerovereenkomst, valideren EDI- en partner-specifieke eigenschappen uitgewisseld in transacties sets splitsen of volledige uitgewisseld behouden en genereren ontvangstbevestigingen voor transacties verwerkt. toouse deze connector, moet u Hallo connector tooan bestaande trigger in uw logische app toevoegen.

## <a name="before-you-start"></a>Voordat u begint

Hier volgt Hallo items die u nodig:

* Een Azure-account; kunt u een [gratis account](https://azure.microsoft.com/free)
* Een [integratie account](logic-apps-enterprise-integration-create-integration-account.md) die al is gedefinieerd en die zijn gekoppeld aan uw Azure-abonnement. U moet een connector integratie account toouse Hallo decoderen X12 bericht hebben.
* Ten minste twee [partners](logic-apps-enterprise-integration-partners.md) die al zijn gedefinieerd in uw account integratie
* Een [X12 overeenkomst](logic-apps-enterprise-integration-x12.md) die al is gedefinieerd in uw account integratie

## <a name="decode-x12-messages"></a>Decoderen X12 berichten

1. [Een logische app maken](logic-apps-create-a-logic-app.md).

2. Hallo decoderen X12 bericht connector geen triggers, dus moet u een trigger voor het starten van uw logische app, zoals een aanvraag-trigger toevoegen. In Hallo Logic App-ontwerper, een trigger toevoegen en voeg vervolgens een actie tooyour logische app.

3.  Voer in het zoekvak hello, 'x12' voor uw filter. Selecteer **X12-decoderen X12 bericht**.
   
    ![Zoek naar 'x12'](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. Als u niet alle verbindingen eerder tooyour integratie account maakt, wordt u gevraagd toocreate nu dat connection. Naam van uw verbinding en Hallo integratie-account dat u wilt dat tooconnect selecteren. 

    ![Bieden integratie Verbindingsdetails voor account](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    Eigenschappen met een sterretje zijn vereist.

    | Eigenschap | Details |
    | --- | --- |
    | Verbindingsnaam * |Voer een naam voor de verbinding. |
    | Integratie Account * |Voer een naam voor uw account integratie. Zorg ervoor dat uw account en logica app voor integratie in Hallo dezelfde Azure-locatie. |

5.  Wanneer u bent klaar, ziet uw Verbindingsdetails vergelijkbaar toothis voorbeeld. maken van uw verbinding toofinish kiezen **maken**.
   
    ![de accountdetails verbinding integratie](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. Nadat de verbinding is gemaakt, zoals in dit voorbeeld, selecteer Hallo X12 plat bestand-bericht toodecode.

    ![integratie-account verbinding is gemaakt](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    Bijvoorbeeld:

    ![Selecteer X12 platte bericht voor het decoderen van bestand](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a>X12 decoderen details

Hallo X12 decoderen connector voert deze taken uit:

* Valideert Hallo envelop tegen trading partner agreement
* Valideert EDI en partner-specifieke eigenschappen
  * Structurele EDI-validatie en uitgebreide schemavalidatie
  * Validatie van de structuur van Hallo interchange envelop Hallo.
  * Schemavalidatie van Hallo envelop volgens het schema voor Hallo-besturingselement.
  * Schemavalidatie van Hallo transactie-set gegevenselementen volgens het schema voor Hallo-bericht.
  * EDI-validatie wordt uitgevoerd op transactie-set gegevenselementen 
* Controleert of Hallo interchange, groep en transactie set besturingselement getallen zijn niet identiek
  * Hallo interchange controle-aantal tegen eerder ontvangen uitgewisseld controleert.
  * Hallo groepsnummer beheer op basis van andere getallen groep besturingselement in Hallo interchange controleert.
  * Controleert Hallo transactie controle-aantal ingesteld op basis van andere cijfers voor het instellen van transactie in die groep.
* Hallo interchange in transactie sets splitst of behoudt de gehele uitwisseling Hallo:
  * Gesplitste Interchange als transaction sets - transactie sets onderbreken bij fout: splitsingen interchange in transactie wordt ingesteld en wordt elke transactie set geparseerd. 
  Hallo X12 decoderen actie levert die transactie-sets die validatie niet doorstaan te`badMessages`, en levert Hallo resterende transacties te worden ingesteld als`goodMessages`.
  * Gesplitste Interchange als transaction sets - uitwisseling onderbreken bij fout: splitsingen interchange in transactie wordt ingesteld en wordt elke transactie set geparseerd. 
  Als een of meer transactie wordt ingesteld in Hallo interchange mislukken validatie, Hallo X12 decoderen actie levert alle Hallo transactie stelt in dat interchange te`badMessages`.
  * Behouden DIF - transactie sets onderbreken bij fout: Preserve Hallo interchange en proces Hallo hele batch interchange. 
  Hallo X12 decoderen actie levert die transactie-sets die validatie niet doorstaan te`badMessages`, en levert Hallo resterende transacties te worden ingesteld als`goodMessages`.
  * Behouden DIF - uitwisseling onderbreken bij fout: Preserve Hallo interchange en proces Hallo hele batch interchange. 
  Als een of meer transactie wordt ingesteld in Hallo interchange mislukken validatie, Hallo X12 decoderen actie levert alle Hallo transactie stelt in dat interchange te`badMessages`. 
* Genereert een bevestiging technische en/of functionele (indien geconfigureerd).
  * Een technische bevestiging genereert als gevolg van header-validatie. Hallo technische bevestiging gerapporteerd Hallo van Hallo verwerking van een DIF-header en trailer door Hallo adres ontvanger.
  * Een functionele bevestiging genereert als gevolg van validatie van de hoofdtekst. Hallo rapporten functionele bevestiging elke fout is opgetreden bij het verwerken Hallo document ontvangen

## <a name="view-hello-swagger"></a>Weergave Hallo swagger
Zie Hallo [swagger details](/connectors/x12/). 

## <a name="next-steps"></a>Volgende stappen
[Meer informatie over Enterprise Integration Pack Hallo](../logic-apps/logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack") 

