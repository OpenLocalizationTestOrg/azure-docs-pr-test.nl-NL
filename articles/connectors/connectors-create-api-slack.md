---
title: aaaUse hello Slack-Connector in Azure logic apps | Microsoft Docs
description: Verbinding maken met tooSlack in logic apps
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a>Aan de slag met Slack Hallo-connector
Vertraging is een hulpprogramma team communicatie, die samenbrengt alle van uw team communicatie in een plaatst, onmiddellijk doorzoekbare en beschikbaar waar u ook bent. 

Aan de slag door het maken van een logische app nu; Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-tooslack"></a>Een tooSlack verbinding maken
toouse hello Slack-connector maakt u eerst een **verbinding** vervolgens Hallo informatie opgeven voor deze eigenschappen: 

| Eigenschap | Vereist | Beschrijving |
| --- | --- | --- |
| Token |Ja |Toegestane referenties opgeven |

Volg deze stappen toosign in Slack en configuratie van de volledige Hallo Hallo Slack **verbinding** in uw logische app:

1. Selecteer **terugkeerpatroon**
2. Selecteer een **frequentie** en voer een **Interval**
3. Selecteer **een actie toevoegen**  
   ![Vertraging configureren][1]  
4. Vertraging in het zoekvak Hallo invoeren en wachten op Hallo zoeken tooreturn alle vermeldingen met Slack in Hallo naam
5. Selecteer **Slack - bericht posten**
6. Selecteer **tooSlack aanmelden**:  
   ![Vertraging configureren][2]
7. Geef uw toosign toegestane referenties in tooauthorize Hallo toepassing    
   ![Vertraging configureren][3]  
8. U zult de aanmeldingspagina van de organisatie van de omgeleide tooyour. **Autoriseren** toegestane toointeract met uw logische app:      
   ![Vertraging configureren][5] 
9. Nadat het Hallo-autorisatie is voltooid, moet u omgeleide tooyour logic app toocomplete door het configureren van Hallo **vertraging - alle berichten ophalen** sectie. Toevoegen van andere triggers en acties die u nodig hebt.  
   ![Vertraging configureren][6]
10. Sla uw werk door te selecteren **opslaan** op Hallo menubalk hierboven.

## <a name="connector-specific-details"></a>Connector-specifieke details

Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/slack/).

## <a name="more-connectors"></a>Meer connectors
Ga terug toohello [API's lijst](apis-list.md).

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
