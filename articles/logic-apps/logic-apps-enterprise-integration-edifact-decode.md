---
title: aaaDecode EDIFACT berichten - Azure Logic Apps | Microsoft Docs
description: EDI valideren en genereren van bevestigingen met Hallo EDIFACT bericht decoder in Enterprise Integration Pack Hallo voor Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 0e61501d-21a2-4419-8c6c-88724d346e81
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 94faebdec4e4ffc8ad76ad1609495ddf9f002250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>EDIFACT-berichten voor Azure Logic Apps decoderen Hello Enterprise Integration Pack

Met Hallo decoderen EDIFACT bericht connector kunt u valideren EDI- en partner-specifieke eigenschappen, uitgewisseld in transacties sets splitsen of behouden van de hele uitgewisseld en genereren van bevestigingen voor verwerkte transacties. toouse deze connector, moet u Hallo connector tooan bestaande trigger in uw logische app toevoegen.

## <a name="before-you-start"></a>Voordat u begint

Hier volgt Hallo items die u nodig:

* Een Azure-account; kunt u een [gratis account](https://azure.microsoft.com/free)
* Een [integratie account](logic-apps-enterprise-integration-create-integration-account.md) die al is gedefinieerd en die zijn gekoppeld aan uw Azure-abonnement. U moet een connector integratie account toouse Hallo decoderen EDIFACT bericht hebben. 
* Ten minste twee [partners](logic-apps-enterprise-integration-partners.md) die al zijn gedefinieerd in uw account integratie
* Een [EDIFACT overeenkomst](logic-apps-enterprise-integration-edifact.md) die al is gedefinieerd in uw account integratie

## <a name="decode-edifact-messages"></a>EDIFACT-berichten worden gedecodeerd

1. [Een logische app maken](logic-apps-create-a-logic-app.md).

2. Hallo decoderen EDIFACT bericht connector geen triggers, dus moet u een trigger voor het starten van uw logische app, zoals een aanvraag-trigger toevoegen. In Hallo Logic App-ontwerper, een trigger toevoegen en voeg vervolgens een actie tooyour logische app.

3. Voer in het zoekvak hello, 'EDIFACT' als filter. Selecteer **decoderen EDIFACT bericht**.
   
    ![EDIFACT zoeken](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. Als u niet alle verbindingen eerder tooyour integratie account maakt, wordt u gevraagd toocreate nu dat connection. Naam van uw verbinding en Hallo integratie-account dat u wilt dat tooconnect selecteren.
   
    ![integratie-account maken](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    Eigenschappen met een sterretje zijn vereist.

    | Eigenschap | Details |
    | --- | --- |
    | Verbindingsnaam * |Voer een naam voor de verbinding. |
    | Integratie Account * |Voer een naam voor uw account integratie. Zorg ervoor dat uw account en logica app voor integratie in Hallo dezelfde Azure-locatie. |

4. Wanneer u klaar bent met het maken van uw verbinding toofinish kiezen **maken**. De verbindingsdetails ziet vergelijkbaar toothis voorbeeld:

    ![de accountdetails integratie](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. Nadat de verbinding is gemaakt, zoals in dit voorbeeld, selecteer toodecode Hallo EDIFACT plat bestand-bericht.

    ![integratie-account verbinding is gemaakt](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    Bijvoorbeeld:

    ![Selecteer EDIFACT plat bestand-bericht voor het decoderen van](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a>EDIFACT decoder details

Hallo decoderen EDIFACT connector voert deze taken uit: 

* Hallo envelop tegen trading partner agreement valideert.
* Oplossing Hallo overeenkomst door overeenkomende Hallo afzender kwalificatie & -id en ontvanger kwalificatie & -id.
* Een knooppunt in meerdere transacties splitst wanneer Hallo interchange heeft meer dan één transactie op basis van het Hallo-overeenkomst instellingen configuratie ontvangen.
* Hallo interchange ontleed.
* Valideert EDI en partner-specifieke eigenschappen, waaronder:
  * Validatie van Hallo interchange envelop structuur
  * Schemavalidatie van Hallo envelop volgens het schema voor Hallo-besturingselement
  * Schemavalidatie van Hallo transactie-set gegevenselementen volgens het schema voor Hallo-bericht
  * EDI-validatie wordt uitgevoerd op transactie-set gegevenselementen
* Verifieert dat Hallo interchange, groep en transactie set besturingselement getallen niet identiek zijn (indien geconfigureerd) 
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
* Genereert een technische (beheer) en/of functionele bevestiging (indien geconfigureerd).
  * Een technische bevestigings- of Hallo CONTRL ACK rapporten Hallo resultaten van een syntactische controle van de uitwisseling Hallo voltooid ontvangen.
  * Een functionele bevestiging erkent accepteren of weigeren van een ontvangen interchange of een groep

## <a name="view-swagger-file"></a>Swagger-bestand weergeven
tooview hello Swagger voor Hallo EDIFACT connector, Zie [EDIFACT](/connectors/edifact/).

## <a name="next-steps"></a>Volgende stappen
[Meer informatie over Enterprise Integration Pack Hallo](logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack") 

