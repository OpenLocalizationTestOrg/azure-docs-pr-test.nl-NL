---
title: aaaAdd hello OneDrive-connector in uw logische Apps | Microsoft Docs
description: Overzicht van Hallo OneDrive connector met de parameters van de REST-API
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a>Aan de slag met Hallo OneDrive-connector
Verbinding maken met de bestanden, waaronder het uploaden, ophalen en verwijder bestanden tooOneDrive toomanage. 

Met OneDrive, u: 

* Het bouwen van uw werkstroom door het opslaan van bestanden in OneDrive of bijwerken van bestaande bestanden in OneDrive. 
* Triggers toostart uw werkstroom gebruiken wanneer een bestand wordt gemaakt of binnen uw OneDrive bijgewerkt.
* Acties toocreate een bestand gebruiken en verwijderen van een bestand en meer. Bijvoorbeeld wanneer een nieuwe Office 365-e-mail is ontvangen met een bijlage (een trigger), maakt u een nieuw bestand in OneDrive (een actie).

Dit onderwerp leest u hoe toouse OneDrive-connector in een logische app Hallo en ook een lijst met Hallo triggers en acties.

toolearn meer informatie over Logic Apps, Zie [wat zijn logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooonedrive"></a>Verbinding maken met tooOneDrive
Om uw logische app toegang alle services tot, maakt u eerst een *verbinding* toohello service. Een verbinding biedt connectiviteit tussen een logische app en een andere service. Bijvoorbeeld, tooconnect tooOneDrive, moet u eerst een OneDrive *verbinding*. een verbinding toocreate Geef referenties op Hallo u normaal gesproken tooaccess Hallo service tooconnect te gewenste gebruiken. Voer dus met OneDrive, Hallo referenties tooyour OneDrive-account toocreate Hallo verbinding.

### <a name="create-hello-connection"></a>Hallo verbinding maken
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a>Een trigger te gebruiken
Een trigger is een gebeurtenis die gebruikt toostart Hallo werkstroom gedefinieerd in een logische app worden kan. Triggers pollen' ' Hallo-service op het interval en de gewenste frequentie. [Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Typ in Hallo logische app, 'onedrive' tooget een lijst met Hallo-triggers:  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. Selecteer **wanneer een bestand wordt gewijzigd**. Als er al een verbinding bestaat, selecteert u Hallo objectkiezer tonen knop tooselect een map.
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    Als u na vragen aan gebruiker toosign in, voert u Hallo aanmelding in details toocreate Hallo verbinding. [Hallo verbinding maken](connectors-create-api-onedrive.md#create-the-connection) in dit onderwerp vindt u Hallo stappen. 
   
   > [!NOTE]
   > In dit voorbeeld Hallo logische app wordt uitgevoerd als een bestand in Hallo-map die u kiest, wordt bijgewerkt. toosee hello resultaten van deze trigger toevoegen nog een actie die u een e-mailbericht verzendt. Bijvoorbeeld, voeg Hallo Outlook van Office 365 *e-mailbericht verzenden* actie die u e-mailberichten wanneer een bestand wordt bijgewerkt. 

3. Selecteer Hallo **bewerken** knop en stel Hallo **frequentie** en **Interval** waarden. Bijvoorbeeld, als u wilt dat Hallo trigger toopoll om de 15 minuten, wordt ingesteld Hallo **frequentie** te**minuut**, en set Hallo **Interval** te**15**. 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. **Sla** uw wijzigingen (linksboven Hallo werkbalk). Uw logische app wordt opgeslagen en automatisch kan worden ingeschakeld.

## <a name="use-an-action"></a>Gebruik een actie
Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app. [Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Selecteer Hallo plus -teken. Ziet u verschillende mogelijkheden: **een actie toevoegen**, **een voorwaarde toevoegen**, of een van de Hallo **meer** opties.
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. Kies **een actie toevoegen**.
3. Typ in het tekstvak hello, 'onedrive' tooget een lijst met alle beschikbare Hallo-acties.
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. Kies in ons voorbeeld **OneDrive - bestand maken**. Als er al een verbinding bestaat, selecteert u Hallo **mappad** tooput Hallo bestand, Voer Hallo **bestandsnaam**, en kies Hallo **bestandsinhoud** gewenste:  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    Als u wordt gevraagd om de verbindingsgegevens hello, voert u Hallo details toocreate Hallo verbinding. [Hallo verbinding maken](connectors-create-api-onedrive.md#create-the-connection) in dit onderwerp beschrijft deze eigenschappen. 
   
   > [!NOTE]
   > In dit voorbeeld maken we een nieuw bestand in een map OneDrive. U kunt uitvoer vanuit een ander trigger toocreate hello OneDrive-bestand. Bijvoorbeeld, voeg Hallo Outlook van Office 365 *wanneer een nieuw e-mailadres binnenkomt* trigger. Voeg vervolgens Hallo OneDrive *Create file* actie die gebruikmaakt van de Content-Type-velden en Hallo bijlagen binnen een ForEach toocreate Hallo nieuw bestand in OneDrive. 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. **Sla** uw wijzigingen (linksboven Hallo werkbalk). Uw logische app wordt opgeslagen en automatisch kan worden ingeschakeld.


## <a name="connector-specific-details"></a>Connector-specifieke details

Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/onedriveconnector/).

## <a name="more-connectors"></a>Meer connectors
Ga terug toohello [API's lijst](apis-list.md).
