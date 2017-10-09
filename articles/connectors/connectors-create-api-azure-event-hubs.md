---
title: aaaSet up controleprogramma voor gebeurtenissen met Azure Event Hubs voor Azure Logic Apps | Microsoft Docs
description: Gegevensstromen tooreceive gebeurtenissen bewaken en verzenden van gebeurtenissen voor Azure Logic Apps met Azure Event Hubs
services: logic-apps
keywords: gegevensstroom, controleprogramma voor gebeurtenissen van event hubs
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 4aad2c2ac1134b4d4d440019b4773559e49be122
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-receive-and-send-events-with-hello-event-hubs-connector"></a>Bewaken, ontvangen en verzenden van gebeurtenissen met de Hallo Event Hubs-connector

tooset up controleprogramma voor gebeurtenissen, zodat uw logische app kunt detecteren van gebeurtenissen, gebeurtenissen ontvangen en verzenden van gebeurtenissen, verbinding tooan [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) van uw logische app. Meer informatie over [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).

## <a name="requirements"></a>Vereisten

* U hebt toohave een [Event Hubs-naamruimte en Event Hub](../event-hubs/event-hubs-create.md) in Azure. Meer informatie over [hoe toocreate een Event Hubs-naamruimte en Event Hub](../event-hubs/event-hubs-create.md). 

* toouse [elke connector](https://docs.microsoft.com/azure/connectors/apis-list) in uw logische app, hebt u toocreate een logische app eerst. Meer informatie over [hoe toocreate een logische app](../logic-apps/logic-apps-create-a-logic-app.md).

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-hello-connection-string"></a>Controleer machtigingen voor Event Hubs-naamruimte en Hallo verbindingsreeks vinden

Een service voor uw logische app tooaccess, hebt u toocreate een [ *verbinding* ](./connectors-overview.md) tussen uw logische app en Hallo service, als u dat nog niet gedaan hebt. Deze verbinding toestaat uw logische app tooaccess-gegevens.
Voor uw logische app tooaccess uw Event Hub, hebt u toohave **beheren** machtigingen en Hallo-verbindingsreeks voor de naamruimte van uw Event Hubs.

toocheck uw machtigingen en de verbindingsreeks voor get hello, als volgt te werk.

1.  Meld u aan toohello [Azure-portal](https://portal.azure.com "Azure-portal"). 

2.  Ga tooyour Event Hubs *naamruimte*, niet Hallo specifieke Event Hub. Op Hallo naamruimte blade onder **instellingen**, kies **gedeeld toegangsbeleid**. Onder **Claims**, Controleer of u hebt **beheren** machtigingen voor die naamruimte.

    ![Machtigingen voor uw Event Hub-naamruimte beheren](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  toocopy Hallo-verbindingsreeks voor de naamruimte van de Event Hubs hello, kies **RootManageSharedAccessKey**. Volgende tooyour primaire sleutel van de verbindingsreeks, kiest u de knop kopiëren Hallo.

    ![Kopieer de verbindingsreeks voor Event Hubs-naamruimte](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > tooconfirm of de verbindingsreeks is gekoppeld aan de naamruimte van uw Event Hubs of met een specifieke Event Hub, Controleer de verbindingsreeks Hallo voor Hallo `EntityPath` parameter. Als u deze parameter vinden, Hallo-verbindingsreeks is voor een specifieke Event Hub 'entiteit' en is geen Hallo juiste tekenreeks toouse met uw logische app.

4.  Wanneer u wordt gevraagd om referenties na het toevoegen van een Event Hubs trigger of actie tooyour logische app, kunt u nu tooyour Event Hubs naamruimte verbinding. Geef een naam op voor de verbinding, voert u Hallo verbindingsreeks die u hebt gekopieerd en kies **maken**.

    ![Geef de verbindingsreeks voor Event Hubs-naamruimte](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    Nadat u uw verbinding maakt, wordt in Hallo Event Hubs trigger of actie Hallo verbindingsnaam weergegeven. 
    Vervolgens kunt u doorgaan met de overige stappen in uw logische app Hallo.

    ![Event Hubs naamruimte verbinding is gemaakt](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a>Werkstroom starten wanneer uw Event Hub nieuwe gebeurtenissen ontvangt

Een [ *trigger* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is een gebeurtenis die een werkstroom in uw logische app start. Volg deze stappen voor het Hallo-trigger die deze gebeurtenis detecteert toevoegen voor het starten van een werkstroom wanneer nieuwe gebeurtenissen tooyour Event Hub worden verzonden.

1.  In Hallo [Azure-portal](https://portal.azure.com "Azure-portal"), gaat u het bestaande logische app tooyour of een lege logische app maken.

2.  Voer in het zoekvak voor Hallo Logic App-ontwerper Hallo `event hubs` voor uw filter. Selecteer deze trigger: **wanneer gebeurtenissen zijn beschikbaar in de Event Hub**

    ![Selecteer de trigger voor wanneer de nieuwe gebeurtenissen voor het ontvangen van uw Event Hub](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    Als u nog een verbinding tooyour Event Hubs-naamruimte hebt, wordt u gevraagd toocreate nu deze verbinding. Geef een naam op voor uw verbinding en Voer Hallo-verbindingsreeks voor de naamruimte van uw Event Hubs. 
    Indien nodig, meer [hoe toofind de verbindingsreeks](#permissions-connection-string).

    ![Geef de verbindingsreeks voor Event Hubs-naamruimte](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    Nadat u Hallo verbinding maakt, instellingen voor Hallo Hallo **wanneer een gebeurtenis in beschikbaar zijn in een Event Hub** trigger worden weergegeven.

    ![De instellingen van de trigger voor wanneer de nieuwe gebeurtenissen voor het ontvangen van uw Event Hub](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  Typ of Selecteer de naam Hallo voor Hallo Event Hub die u toomonitor wilt. Selecteer Hallo frequentie en het interval voor hoe vaak toocheck Hallo Event Hub.

    > [!TIP]
    > toooptionally een consumergroep selecteert voor het lezen van gebeurtenissen, kiest u **geavanceerde opties weergeven**. 

    ![Geef een Event Hub of klantengroep](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    U hebt nu ingesteld een trigger toostart een werkstroom voor uw logische app. 
    Uw logische app controleert Hallo opgegeven Event Hub, op basis van Hallo door u ingesteld schema. 
    Als uw app vindt de nieuwe gebeurtenissen in Hallo Event Hub, voert Hallo trigger andere acties of triggers op uw logische app.

## <a name="send-events-tooyour-event-hub-from-your-logic-app"></a>Gebeurtenissen tooyour Event Hub van uw logische app verzenden

Een [*actie*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is een taak die wordt uitgevoerd tijdens de werkstroom voor de logische app. Nadat u een trigger tooyour logische app hebt toegevoegd, kunt u een actie tooperform bewerkingen kunt toevoegen met gegevens die zijn gegenereerd door deze trigger. toosend een gebeurtenis tooyour Event Hub van uw logische app, volg deze stappen.

1.  In Logic App Designer onder uw logische app worden geactiveerd, kies **nieuwe stap** > **een actie toevoegen**.

    ![Kies 'Nieuwe stap' vervolgens 'Een actie toevoegen'](./media/connectors-create-api-azure-event-hubs/add-action.png)

    U kunt nu Zoek en selecteer een actie tooperform. 
    Hoewel u geen actie, bijvoorbeeld, willen we Hallo Event Hubs actie toosend gebeurtenissen.

2.  Voer in het zoekvak Hallo `event hubs` voor uw filter.
Deze actie selecteert: **verzendgebeurtenis**

    ![Selecteer 'Event Hubs - verzendgebeurtenis' actie](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  Voer Hallo vereist voor Hallo gebeurtenis, zoals de naam van de Hallo voor Hallo Event Hub waar u toosend Hallo gebeurtenis. Voer een optionele details over Hallo gebeurtenis, zoals inhoud voor die gebeurtenis.

    > [!TIP]
    > toooptionally opgeven Hallo Event Hub-partitie waar toosend Hallo gebeurtenis, kies **geavanceerde opties weergeven**. 

    ![Event Hub-naam en optionele Gebeurtenisdetails invoeren](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  Sla uw wijzigingen op.

    ![Uw logische app opslaan](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    U hebt nu een actie toosend gebeurtenissen instellen van uw logische app. 

## <a name="connector-specific-details"></a>Connector-specifieke details

Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/eventhubs/). 

## <a name="get-help"></a>Help opvragen

tooask vragen, antwoorden op vragen, en zien welke andere Azure Logic Apps-gebruikers doen, gaat u naar Hallo [Azure Logic Apps-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp Logic Apps en connectors verbeteren, stem of ideeën op Hallo indienen [Logic Apps gebruiker feedback site](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Volgende stappen

*  [Andere connectors voor Azure Logic apps zoeken](./apis-list.md)