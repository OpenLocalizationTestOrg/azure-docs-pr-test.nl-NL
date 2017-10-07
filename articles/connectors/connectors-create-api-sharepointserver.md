---
title: aaaUse hello SharePoint Server-Connector in uw logische Apps | Microsoft Docs
description: Aan de slag met Hallo Hallo SharePoint Server-Connector in Logic apps
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 0238a060-d592-4719-b7a2-26064c437a1a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3b814f42611e4971ff5c94ae3b021829217911dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sharepoint-connector"></a>Aan de slag met Hallo SharePoint-connector
Hallo SharePoint Connector biedt een manier toowork met lijsten in SharePoint.

Aan de slag door het maken van een logische app; Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-toosharepoint"></a>Een tooSharePoint verbinding maken
toouse Hallo SharePoint-Connector, maakt u eerst een **verbinding** vervolgens Hallo informatie opgeven voor deze eigenschappen: 

| Eigenschap | Vereist | Beschrijving |
| --- | --- | --- |
| Token |Ja |SharePoint-referenties opgeven |

tooconnect te**SharePoint**, Voer uw tooSharePoint identiteit (gebruikersnaam en wachtwoord, smartcard-referenties, enzovoort). Zodra u hebt geverifieerd, kunt u toouse Hallo SharePoint connector doorgaan in uw logische app. 

Terwijl op Hallo ontwerper van uw logische app, volgt u deze stappen toosign in SharePoint toocreate Hallo verbinding **verbinding** voor gebruik in uw logische app:

1. Voer SharePoint in het zoekvak Hallo en Hallo zoeken tooreturn wacht totdat alle vermeldingen met SharePoint in Hallo-naam:   
   ![SharePoint configureren][1]  
2. Selecteer **SharePoint - als een bestand is gemaakt**   
3. Selecteer **tooSharePoint aanmelden**:   
   ![SharePoint configureren][2]    
4. Geef uw SharePoint-referenties toosign in tooauthenticate met SharePoint   
   ![SharePoint configureren][3]     
5. Nadat het Hallo-verificatie is voltooid, moet u omgeleide tooyour logic app toocomplete door het configureren van SharePoint **wanneer een bestand wordt gemaakt** dialoogvenster.          
   ![SharePoint configureren][4]  
6. Vervolgens kunt u andere triggers en acties die u toocomplete uw logische app moet toevoegen.   
7. Sla uw werk door te selecteren **opslaan** op Hallo menubalk hierboven.  

## <a name="connector-specific-details"></a>Connector-specifieke details

Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/sharepoint/).

## <a name="more-connectors"></a>Meer connectors
Ga terug toohello [API's lijst](apis-list.md).

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
