---
title: aaaAdd hello Outlook van Office 365-connector in uw logische Apps | Microsoft Docs
description: 'Logische apps maken met Office 365-connector tooenable interactie met Office 365. Bijvoorbeeld: maken, bewerken en bijwerken van contactpersonen en agenda-items.'
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 86a573c9c54701de3d3f0500d19eaf545e0710ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-outlook-connector"></a>Aan de slag met Hallo Outlook van Office 365-connector
Hallo Outlook van Office 365-connector kan interactie met Outlook in Office 365. Gebruik deze connector toocreate, bewerken, en update contactpersonen en agenda-items, en ook ophalen, verzenden en antwoorden tooemail.

Met Office 365 Outlook u:

* Bouw uw werkstroom met behulp van Hallo e-mail en agenda-functies in Office 365. 
* Gebruik activeert toostart uw werkstroom wanneer er een nieuw e-mailadres, wanneer een agenda-item wordt bijgewerkt en meer.
* Acties toosend een e-mailbericht gebruikmaken, maakt u een nieuwe gebeurtenis en meer. Bijvoorbeeld, wanneer er een nieuw object in Salesforce (een trigger), een e-mail sturen tooyour Outlook van Office 365 (een actie). 

Dit onderwerp leest u hoe toouse Outlook van Office 365-connector in een logische app Hallo en ook een lijst met Hallo triggers en acties.

> [!NOTE]
> Deze versie van Hallo artikel geldt tooLogic Apps algemene beschikbaarheid (GA).
> 
> 

toolearn meer informatie over Logic Apps, Zie [wat zijn logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toooffice-365"></a>Verbinding maken met tooOffice 365
Om uw logische app toegang alle services tot, maakt u eerst een *verbinding* toohello service. Een verbinding biedt connectiviteit tussen een logische app en een andere service. Bijvoorbeeld: tooconnect tooOffice 365 Outlook, moet u eerst een Office 365 *verbinding*. een verbinding toocreate Geef referenties op Hallo u normaal gesproken tooaccess Hallo service tooconnect te gewenste gebruiken. Voer dus Hallo referenties tooyour Office 365-account toocreate Hallo verbinding met Office 365 Outlook.

## <a name="create-hello-connection"></a>Hallo verbinding maken
> [!INCLUDE [Steps toocreate a connection tooOffice 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a>Een trigger te gebruiken
Een trigger is een gebeurtenis die gebruikt toostart Hallo werkstroom gedefinieerd in een logische app worden kan. Triggers pollen' ' Hallo-service op het interval en de gewenste frequentie. [Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Typ 'office 365' tooget een lijst met Hallo triggers in Hallo logic app:  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. Selecteer **Office 365 Outlook - bij het snel starten van een aanstaande gebeurtenis**. Als er al een verbinding bestaat, selecteert u een kalender uit de vervolgkeuzelijst Hallo.
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    Als u na vragen aan gebruiker toosign in, voert u Hallo aanmelding in details toocreate Hallo verbinding. [Hallo verbinding maken](connectors-create-api-office365-outlook.md#create-the-connection) in dit onderwerp vindt u Hallo stappen. 
   
   > [!NOTE]
   > In dit voorbeeld wordt Hallo logische app uitgevoerd wanneer een gebeurtenis wordt bijgewerkt. toosee hello resultaten van deze trigger toevoegen nog een actie die u een SMS-bericht verzonden. Bijvoorbeeld, voeg Hallo Twilio *bericht verzenden* actie die de tekst die u als hello agenda-gebeurtenis wordt gestart binnen 15 minuten. 
   > 
   > 
3. Selecteer Hallo **bewerken** knop en stel Hallo **frequentie** en **Interval** waarden. Bijvoorbeeld, als u wilt dat Hallo trigger toopoll om de 15 minuten, wordt ingesteld Hallo **frequentie** te**minuut**, en set Hallo **Interval** te**15**. 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. **Sla** uw wijzigingen (linksboven Hallo werkbalk). Uw logische app wordt opgeslagen en automatisch kan worden ingeschakeld.

## <a name="use-an-action"></a>Gebruik een actie
Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app. [Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Selecteer Hallo plus -teken. Ziet u verschillende mogelijkheden: **een actie toevoegen**, **een voorwaarde toevoegen**, of een van de Hallo **meer** opties.
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. Kies **een actie toevoegen**.
3. Typ in het tekstvak hello, 'office 365' tooget een lijst met alle beschikbare Hallo-acties.
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. Kies in ons voorbeeld **Outlook van Office 365 - maken contact op met**. Als er al een verbinding bestaat, kiest u Hallo **map-ID**, **voornaam**, en andere eigenschappen:  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    Als u wordt gevraagd om de verbindingsgegevens hello, voert u Hallo details toocreate Hallo verbinding. [Hallo verbinding maken](connectors-create-api-office365-outlook.md#create-the-connection) in dit onderwerp beschrijft deze eigenschappen. 
   
   > [!NOTE]
   > In dit voorbeeld maken we een nieuwe contactpersoon in Outlook van Office 365. U kunt de uitvoer van een andere trigger toocreate Hallo contactpersoon. Bijvoorbeeld, voeg Hallo SalesForce *wanneer een object wordt gemaakt* trigger. Voeg vervolgens Hallo Outlook van Office 365 *maken contact op met* actie die gebruikmaakt van Hallo SalesForce velden toocreate Hallo nieuwe nieuwe contactpersoon in Office 365. 
   > 
   > 
5. **Sla** uw wijzigingen (linksboven Hallo werkbalk). Uw logische app wordt opgeslagen en automatisch kan worden ingeschakeld.

## <a name="connector-specific-details"></a>Connector-specifieke details

Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/office365connector/). 

## <a name="next-steps"></a>Volgende stappen
[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md). Verken Hallo van andere beschikbare connectors in Logic Apps op onze [API's lijst](apis-list.md).

