---
title: aaaLearn hoe toouse Hallo Twitter-connector in logic apps | Microsoft Docs
description: Overzicht van Twitter-connector met de parameters van de REST-API
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a>Aan de slag met Hallo Twitter-connector
U kunt met Hallo Twitter-connector:

* Tweets post en get-tweets
* Pc-gebruikers en toegang tijdlijnen, vrienden
* Uitvoeren van Hallo andere acties en de triggers die hieronder wordt beschreven  

toouse [elke connector](apis-list.md), moet u eerst toocreate een logische app. U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).  

## <a name="connect-tootwitter"></a>Verbinding maken met tooTwitter
Om uw logische app toegang alle services tot, moet u eerst toocreate een *verbinding* toohello service. Een [verbinding](connectors-overview.md) biedt connectiviteit tussen een logische app en een andere service.  

### <a name="create-a-connection-tootwitter"></a>Een tooTwitter verbinding maken
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a>Gebruik een trigger Twitter
Een trigger is een gebeurtenis die gebruikt toostart Hallo werkstroom gedefinieerd in een logische app worden kan. [Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

In dit voorbeeld, leest u hoe toouse hello **wanneer een nieuwe tweet wordt gepost** toosearch voor #Seattle activeren en, als #Seattle wordt gevonden, een bestand in Dropbox bijwerken met de tekst hello uit Hallo tweet. In een enterprise-voorbeeld, kan u Hallo-naam van uw bedrijf zoeken en een SQL-database bijwerken met de tekst hello van Hallo tweet.

1. Voer *twitter* Selecteer in het zoekvak Hallo op Hallo logic apps designer Hallo **Twitter - wanneer een nieuwe tweet wordt teruggepost** trigger   
   ![Twitter triggerafbeelding 1](./media/connectors-create-api-twitter/trigger-1.png)  
2. Voer *#Seattle* in Hallo **zoektekst** besturingselement  
   ![Afbeelding van de trigger Twitter 2](./media/connectors-create-api-twitter/trigger-2.png) 

Op dit moment is uw logische app geconfigureerd met een trigger die een uitvoering van Hallo andere triggers en acties in Hallo-werkstroom begint. 

> [!NOTE]
> Voor een logische app toobe functionele, moet er ten minste één trigger en één actie bevatten. Hallo stappen in de volgende sectie tooadd een actie van Hallo.  
> 
> 

## <a name="add-a-condition"></a>Een voorwaarde toevoegen
Omdat we alleen geïnteresseerd in tweets van gebruikers met meer dan 50 van gebruikers bent, moet een voorwaarde waarmee wordt bevestigd Hallo aantal pc-gebruikers dat eerst worden toegevoegd toohello logische app.  

1. Selecteer **+ een nieuwe stap** tooadd Hallo actie u wilt dat tootake wanneer #Seattle in een nieuwe tweet wordt gevonden  
   ![Afbeelding 1 Twitter](../../includes/media/connectors-create-api-twitter/action-1.png)  
2. Selecteer Hallo **een voorwaarde toevoegen** koppeling.  
   ![Twitter voorwaarde afbeelding 1](../../includes/media/connectors-create-api-twitter/condition-1.png)   
   Hiermee opent u Hallo **voorwaarde** besturingselement waarin kunt u voorwaarden zoals controleren *gelijk is aan*, *is minder dan*, *is groter dan*, *bevat*, enzovoort.  
   ![Afbeelding van de voorwaarde Twitter 2](../../includes/media/connectors-create-api-twitter/condition-2.png)   
3. Selecteer Hallo **kiest u een waarde** besturingselement.  
   In dit besturingselement kunt u een of meer van de Hallo eigenschappen van de vorige acties of triggers als Hallo waarde waarvan de voorwaarde geëvalueerd tootrue of ONWAAR is.
   ![Twitter voorwaarde afbeelding 3](../../includes/media/connectors-create-api-twitter/condition-3.png)   
4. Selecteer Hallo **...**  tooexpand Hallo lijst met eigenschappen zodat u ziet alle Hallo-eigenschappen die beschikbaar zijn.        
   ![Twitter voorwaarde afbeelding 4](../../includes/media/connectors-create-api-twitter/condition-4.png)   
5. Selecteer Hallo **pc-gebruikers aantal** eigenschap.    
   ![Twitter voorwaarde afbeelding 5](../../includes/media/connectors-create-api-twitter/condition-5.png)   
6. U ziet Hallo pc-gebruikers eigenschap count nu in Hallo waarde besturingselement is.    
   ![Twitter voorwaarde afbeelding 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. Selecteer **is groter dan** uit Hallo operators lijst.    
   ![Twitter voorwaarde afbeelding 7](../../includes/media/connectors-create-api-twitter/condition-7.png)   
8. Voer 50 zoals operand voor Hallo Hallo *is groter dan* operator.  
   Hallo-voorwaarde is nu toegevoegd. Sla uw werk met Hallo **opslaan** op Hallo menu bovenstaande koppeling.    
   ![Twitter voorwaarde afbeelding 8](../../includes/media/connectors-create-api-twitter/condition-8.png)   

## <a name="use-a-twitter-action"></a>Gebruik een Twitter-actie
Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app. [Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Nu u een trigger hebt toegevoegd, volgt u deze stappen tooadd een actie die een nieuwe tweet met inhoud Hallo Hallo tweets gevonden door Hallo trigger wordt geplaatst. Voor de toepassing hello van deze procedure wordt alleen tweets van gebruikers met meer dan 50 pc-gebruikers worden geplaatst.  

In de volgende stap hello voegt u een Twitter-actie die een tweet gebruikmakend van Hallo eigenschappen van elke tweet die is geplaatst door een gebruiker die meer dan 50 pc-gebruikers heeft wordt geplaatst.  

1. Selecteer **een actie toevoegen**. Hiermee opent u Hallo zoekbesturing waar u naar andere acties en triggers zoeken kunt.  
   ![Twitter voorwaarde afbeelding 9](../../includes/media/connectors-create-api-twitter/condition-9.png)   
2. Voer *twitter* selecteert in het zoekvak Hallo Hallo **Twitter - een tweet boeken** in te grijpen. Hiermee opent u Hallo **een tweet boeken** bepalen waar u alle details wordt invoeren voor Hallo tweet wordt geplaatst.      
   ![Actie afbeelding 1-5 Twitter](../../includes/media/connectors-create-api-twitter/action-1-5.png)   
3. Selecteer Hallo **Tweet tekst** besturingselement. Alle uitvoerwaarden van de vorige acties en triggers in Hallo logische app worden nu weergegeven. U kunt een van deze selecteren en ze als onderdeel van Hallo tweet tekst van de nieuwe tweet hello gebruiken.     
   ![Afbeelding 2 Twitter](../../includes/media/connectors-create-api-twitter/action-2.png)   
4. Selecteer **gebruikersnaam**   
5. Voer *zegt:* in Hallo tweet tekstbesturingselement. Doe dit direct na de gebruikersnaam.  
6. Selecteer *Tweet tekst*.       
   ![Afbeelding 3 Twitter](../../includes/media/connectors-create-api-twitter/action-3.png)   
7. Sla uw werk en verzend een tweet met Hallo #Seattle hashtag tooactivate uw werkstroom.  


## <a name="connector-specific-details"></a>Connector-specifieke details

Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/twitterconnector/). 

## <a name="next-steps"></a>Volgende stappen
[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md)

