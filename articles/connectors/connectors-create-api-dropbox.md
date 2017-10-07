---
title: aaaDropbox-connector in Azure Logic Apps | Microsoft Docs
description: Logic apps maken met Azure App service. Verbinding maken met uw bestanden tooDropbox toomanage. U kunt uitvoeren van verschillende acties zoals het uploaden, bijwerken, ophalen en verwijderen van bestanden in Dropbox.
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1f307477836104c0bc0008341604a1400860987f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-dropbox-connector"></a>Aan de slag met Hallo Dropbox-connector
Verbinding maken met uw bestanden tooDropbox toomanage. U kunt uitvoeren van verschillende acties zoals het uploaden, bijwerken, ophalen en verwijderen van bestanden in Dropbox.

toouse [elke connector](apis-list.md), moet u eerst toocreate een logische app. U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toodropbox"></a>Verbinding maken met tooDropbox
Om uw logische app toegang alle services tot, moet u eerst toocreate een *verbinding* toohello service. Een verbinding biedt connectiviteit tussen een logische app en een andere service. Bijvoorbeeld, in volgorde tooconnect tooDropbox, moet u eerst een Dropbox *verbinding*. toocreate een verbinding, moet u tooprovide Hallo referenties u normaal gesproken tooaccess Hallo service tooconnect te gewenste gebruiken. In voorbeeld Hallo Dropbox moet u dus Hallo referenties tooyour Dropbox-account in volgorde toocreate Hallo verbinding tooDropbox. [Meer informatie over verbindingen]()

### <a name="create-a-connection-toodropbox"></a>Een tooDropbox verbinding maken
> [!INCLUDE [Steps toocreate a connection tooDropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a>Gebruik een trigger Dropbox
Een trigger is een gebeurtenis die gebruikt toostart Hallo werkstroom gedefinieerd in een logische app worden kan. [Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

In dit voorbeeld gebruiken we Hallo **wanneer een bestand wordt gemaakt** trigger. Wanneer deze trigger optreedt, noemen we Hallo **ophalen met behulp van pad bestandsinhoud** Dropbox-actie. 

1. Voer *dropbox* in het zoekvak Hallo op Hallo Logic Apps designer, selecteer vervolgens Hallo **Dropbox - wanneer een bestand wordt gemaakt** trigger.      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. Hallo-map die u maken van het bestand tootrack wilt selecteren. Selecteren... (aangeduid in rood Hallo vak) en bladeren toohello map die u wenst tooselect voor Hallo trigger de invoer.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a>Gebruik een Dropbox-actie
Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app. [Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Nu hello trigger is toegevoegd, volgt u deze stappen tooadd een actie die Hallo nieuwe inhoud van bestand krijgen.

1. Selecteer **+ een nieuwe stap** tooadd Hallo actie u wilt dat tootake wanneer een nieuw bestand wordt gemaakt.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. Selecteer **een actie toevoegen**. Dit wordt geopend Hallo zoekvak waarin u naar elke actie u zoeken kunt graag tootake.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. Voer *dropbox* toosearch voor verwante tooDropbox acties.  
4. Selecteer **Dropbox - bestandsinhoud ophalen met behulp van pad** zoals actie tootake Hallo wanneer een nieuw bestand wordt gemaakt in Hallo Dropbox-map geselecteerd. Hallo actie besturingselement blok wordt geopend. U na vragen aan gebruiker tooauthorize uw logische app tooaccess uw Dropbox-account als u dit eerder niet hebt gedaan worden.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. Selecteren... (zich aan de rechterkant Hallo Hallo **bestandspad** besturingselement) en het bestandspad toohello u toouse wilt bladeren. Of gebruik Hallo **bestandspad** token toospeed van uw logische app maken.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. Sla uw werk op en maak een nieuw bestand in Dropbox tooactivate uw werkstroom.  

## <a name="connector-specific-details"></a>Connector-specifieke details

Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/dropbox/).

## <a name="more-connectors"></a>Meer connectors
Ga terug toohello [API's lijst](apis-list.md).
