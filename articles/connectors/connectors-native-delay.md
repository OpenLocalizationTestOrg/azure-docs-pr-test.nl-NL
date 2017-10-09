---
title: aaaAdd een vertraging in logic apps | Microsoft Docs
description: Overzicht van Hallo vertraging en vertraging-totdat acties, en hoe toouse ze aan een Azure logic app.
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a>Aan de slag met Hallo vertraging en vertraging-totdat acties
Met behulp van Hallo vertraging en ' vertraging-totdat ' acties, werkstroom-scenario's kan worden voltooid.

U kunt bijvoorbeeld:

* Wacht totdat een weekdag toosend status bijwerken via e-mail.
* Vertraging Hallo werkstroom totdat een HTTP-aanroep heeft tijd toofinish voordat wordt hervat en ophalen van het Hallo-resultaat.

tooget gestart met Hallo vertraging actie in een logische app, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-delay-actions"></a>Hallo vertraging acties gebruiken
Een actie is een bewerking die wordt uitgevoerd door Hallo werkstroom die is gedefinieerd in een logische app. [Meer informatie over acties](connectors-overview.md).

Hier volgt een van de voorbeeldreeks hoe toouse een vertraging stap in een logische app:

1. Klik na het toevoegen van een trigger **nieuwe stap** tooadd een actie.
2. Zoeken naar **vertraging** toobring Hallo vertraging acties. In dit voorbeeld selecteren we **vertraging**.
   
    ![Vertraging acties](./media/connectors-native-delay/using-action-1.png)
3. Voltooi alle Hallo actie eigenschappen tooconfigure Hallo vertraging.
   
    ![Vertraging config](./media/connectors-native-delay/using-action-2.png)
4. Klik op **opslaan** toopublish en Hallo logische app activeren.

## <a name="action-details"></a>Actiedetails
Hallo terugkeerpatroon trigger heeft Hallo volgende eigenschappen die kunnen worden geconfigureerd.

### <a name="delay-action"></a>Vertraging actie
Deze actie vertragingen hello uitvoeren voor een bepaalde periode.
A * houdt in dat een vereist veld.

| Weergavenaam | De naam van eigenschap | Beschrijving |
| --- | --- | --- |
| Aantal * |Aantal |het aantal keer eenheden toodelay Hallo |
| Eenheid * |eenheid |Hallo tijdseenheid: `Second`, `Minute`, `Hour`, of`Day` |

<br>

### <a name="delay-until-action"></a>Vertraging-totdat de actie
Deze actie een vertraging Hallo uitgevoerd totdat het een opgegeven datum/tijd.
A * houdt in dat een vereist veld.

| Weergavenaam | De naam van eigenschap | Beschrijving |
| --- | --- | --- |
| Jaar * |tijdstempel |Hallo jaar toodelay tot (GMT) |
| Maand * |tijdstempel |Hallo maand toodelay tot (GMT) |
| Dag * |tijdstempel |Hallo dag toodelay tot (GMT) |

<br>

## <a name="next-steps"></a>Volgende stappen
Nu uitproberen Hallo-platform en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md). U kunt verkennen Hallo van andere beschikbare connectors in logische apps door te kijken onze [API's lijst](apis-list.md).

