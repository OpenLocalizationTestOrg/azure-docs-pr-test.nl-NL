---
title: aaaSMTP-connector in Azure Logic Apps | Microsoft Docs
description: Logic apps maken met Azure App service. Verbinding maken met tooSMTP toosend e-mailbericht.
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a>Aan de slag met Hallo SMTP-connector
Verbinding maken met tooSMTP toosend e-mailbericht.

toouse [elke connector](apis-list.md), moet u eerst toocreate een logische app. U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toosmtp"></a>Verbinding maken met tooSMTP
Om uw logische app toegang alle services tot, moet u eerst toocreate een *verbinding* toohello service. Een [verbinding](connectors-overview.md) biedt connectiviteit tussen een logische app en een andere service. Bijvoorbeeld, tooconnect tooSMTP, moet u eerst een SMTP *verbinding*. een verbinding toocreate Geef referenties op Hallo u normaal gesproken tooaccess Hallo service u verbinding met maken. Voer dus in Hallo SMTP bijvoorbeeld Hallo referenties tooyour verbindingsnaam SMTP-serveradres en gebruiker aanmelding informatie toocreate Hallo verbinding tooSMTP.  

### <a name="create-a-connection-toosmtp"></a>Een tooSMTP verbinding maken
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a>Gebruik een SMTP-trigger
Een trigger is een gebeurtenis die gebruikt toostart Hallo werkstroom gedefinieerd in een logische app worden kan. [Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

In dit voorbeeld omdat SMTP niet over een trigger van een eigen beschikt, gebruiken we Hallo **Salesforce - wanneer een object wordt gemaakt** trigger. Deze trigger wordt geactiveerd wanneer een nieuw object in Salesforce maakt. In ons voorbeeld stellen we het zo dat elke keer wanneer een nieuwe lead wordt gemaakt in Salesforce, een *e-mail verzenden* actie plaatsvindt via Hallo SMTP-connector met een melding van de nieuwe lead hello wordt gemaakt.

1. Voer *salesforce* Selecteer in het zoekvak Hallo op Hallo logic apps designer Hallo **Salesforce - wanneer een object wordt gemaakt** trigger.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. Hallo **wanneer een object wordt gemaakt** besturingselement wordt weergegeven.
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. Selecteer Hallo **objecttype** Selecteer *leiden* uit Hallo lijst met objecten. In deze stap geeft u aan dat u een trigger die uw logische app ontvangt een melding maakt wanneer er een nieuwe lead wordt gemaakt in Salesforce.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. Hallo-trigger is gemaakt.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a>Gebruik een SMTP-actie
Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app. [Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Nu hello trigger is toegevoegd, volgt u deze stappen tooadd een SMTP-actie die wordt uitgevoerd wanneer een nieuwe lead in Salesforce wordt gemaakt.

1. Selecteer **+ een nieuwe stap** tooadd Hallo actie u wilt dat tootake wanneer een nieuwe lead wordt gemaakt.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. Selecteer **een actie toevoegen**. Dit wordt geopend Hallo zoekvak waarin u naar elke actie u zoeken kunt graag tootake.  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. Voer *smtp* toosearch voor verwante tooSMTP acties.  
4. Selecteer **SMTP - e-mailbericht verzenden** zoals actie tootake Hallo wanneer nieuwe lead hello wordt gemaakt. Hallo actie besturingselement blok wordt geopend. U hebt tooestablish uw SMTP-verbinding in de ontwerpfunctie blok Hallo als u dit eerder niet hebt gedaan.  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. Voer uw gewenste e-informatie in Hallo **SMTP - e-mailbericht verzenden** blok.  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. Sla uw werk in volgorde tooactivate uw werkstroom.  

## <a name="connector-specific-details"></a>Connector-specifieke details

Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/smtpconnector/).

## <a name="more-connectors"></a>Meer connectors
Ga terug toohello [API's lijst](apis-list.md).
