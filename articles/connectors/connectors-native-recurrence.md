---
title: De trigger terugkeerpatroon in logic apps toevoegen | Microsoft Docs
description: Overzicht van de trigger terugkeerpatroon en het gebruik ervan met een Azure logic app.
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: fe558958c316c8dba42163e277ae01451f712e5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-recurrence-trigger"></a>Aan de slag met de trigger terugkeerpatroon
U kunt met behulp van de trigger terugkeerpatroon krachtige werkstromen maken in de cloud.

U kunt bijvoorbeeld:

* Een werkstroom wilt uitvoeren van een opgeslagen SQL-procedure elke dag plannen.
* Een samenvatting weer van alle tweets e gedurende de afgelopen week over een bepaalde hashtag.

Om te beginnen met de trigger terugkeerpatroon in een logische app, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-a-recurrence-trigger"></a>Gebruik een trigger terugkeerpatroon
Een trigger is een gebeurtenis die kan worden gebruikt om de werkstroom die is gedefinieerd in een logische app te starten. [Meer informatie over triggers](connectors-overview.md).

Hier volgt een voorbeeld van de volgorde van het instellen van een trigger terugkeerpatroon in een logische app:

1. Voeg de **terugkeerpatroon** trigger als de eerste stap in een logische app.
2. Vul in de parameters voor het terugkeerpatroon.

De logische app nu een uitgevoerd na elke tijdsinterval gestart.

![HTTP-trigger](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a>Details van de trigger
De trigger terugkeerpatroon heeft de volgende eigenschappen die u kunt configureren.

Er wordt een logische app geactiveerd na een opgegeven tijdsinterval.
A * houdt in dat een vereist veld.

| Weergavenaam | De naam van eigenschap | Beschrijving |
| --- | --- | --- |
| Frequentie * |Frequentie |De tijdseenheid: `Second`, `Minute`, `Hour`, `Day`, of `Year`. |
| Interval * |Interval |Het interval van de opgegeven frequentie voor het terugkeerpatroon. |
| Tijdzone |Tijdzone |Als een begintijd zonder een UTC-offset is opgegeven, is deze tijdzone wordt gebruikt. |
| Begintijd |startTime |De begintijd in [ISO 8601-notatie](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations). |

<br>

## <a name="next-steps"></a>Volgende stappen
Nu uitproberen van het platform en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md). U kunt de beschikbare connectors in logische apps door te kijken verkennen onze [API's lijst](apis-list.md).

