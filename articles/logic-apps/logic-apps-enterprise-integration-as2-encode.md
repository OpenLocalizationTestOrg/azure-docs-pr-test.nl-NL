---
title: berichten aaaEncode AS2 - Azure Logic Apps | Microsoft Docs
description: Hoe toouse AS2-codering in Hallo Enterprise Integration Pack Hallo voor Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 2b372c416512ffa9ea5dc50ce0f767bfd8aefbc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>AS2-berichten voor Azure Logic Apps Hello Enterprise Integration Pack coderen

tooestablish beveiliging en betrouwbaarheid tijdens de verzending van berichten, moet u Hallo coderen AS2 bericht connector gebruiken. Deze connector biedt digitale ondertekening, versleuteling en bevestigingen via bericht Disposition meldingen (MDN), wat ook toosupport voor niet-afwijzing leidt.

## <a name="before-you-start"></a>Voordat u begint

Hier volgt Hallo items die u nodig:

* Een Azure-account; kunt u een [gratis account](https://azure.microsoft.com/free)
* Een [integratie account](logic-apps-enterprise-integration-create-integration-account.md) die al is gedefinieerd en die zijn gekoppeld aan uw Azure-abonnement. U moet een connector integratie account toouse Hallo coderen AS2 bericht hebben.
* Ten minste twee [partners](logic-apps-enterprise-integration-partners.md) die al zijn gedefinieerd in uw account integratie
* Een [AS2-overeenkomst](logic-apps-enterprise-integration-as2.md) die al is gedefinieerd in uw account integratie

## <a name="encode-as2-messages"></a>AS2-berichten te coderen

1. [Een logische app maken](logic-apps-create-a-logic-app.md).

2. Hallo coderen AS2-bericht connector geen triggers, dus moet u een trigger voor het starten van uw logische app, zoals een aanvraag-trigger toevoegen. In Hallo Logic App-ontwerper, een trigger toevoegen en voeg vervolgens een actie tooyour logische app.

3.  Voer in het zoekvak hello, 'AS2' voor uw filter. Selecteer **AS2 - coderen AS2-bericht**.
   
    ![Zoek naar 'AS2'](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. Als u niet alle verbindingen eerder tooyour integratie account maakt, wordt u gevraagd toocreate nu dat connection. Naam van uw verbinding en Hallo integratie-account dat u wilt dat tooconnect selecteren. 
   
    ![verbinding toointegration-account maken](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    Eigenschappen met een sterretje zijn vereist.

    | Eigenschap | Details |
    | --- | --- |
    | Verbindingsnaam * |Voer een naam voor de verbinding. |
    | Integratie Account * |Voer een naam voor uw account integratie. Zorg ervoor dat uw account en logica app voor integratie in Hallo dezelfde Azure-locatie. |

5.  Wanneer u bent klaar, ziet uw Verbindingsdetails vergelijkbaar toothis voorbeeld. maken van uw verbinding toofinish kiezen **maken**.
   
    ![de verbindingsdetails integratie](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. Nadat de verbinding is gemaakt, zoals in dit voorbeeld, vindt u informatie voor **AS2-van**, **AS2-tooidentifiers** zoals geconfigureerd in de overeenkomst en **hoofdtekst**, die is Hallo-bericht nettolading.
   
    ![verplichte velden bieden](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a>AS2-encoder details

Hallo coderen AS2-connector voert deze taken uit: 

* AS2/HTTP-headers van toepassing is
* Tekenen uitgaande berichten (indien geconfigureerd)
* Versleutelt uitgaande berichten (indien geconfigureerd)
* Comprimeren van het Hallo-bericht (indien geconfigureerd)

## <a name="try-this-sample"></a>Probeer dit voorbeeld

een volledig operationeel logic app en voorbeeld AS2-scenario implementeren tootry Zie Hallo [AS2 logic app-sjabloon en het scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).

## <a name="view-hello-swagger"></a>Weergave Hallo swagger
Zie Hallo [swagger details](/connectors/as2/). 

## <a name="next-steps"></a>Volgende stappen
[Meer informatie over Enterprise Integration Pack Hallo](logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack") 

