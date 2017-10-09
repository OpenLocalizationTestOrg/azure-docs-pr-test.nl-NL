---
title: aaaAdd hello terugkeerpatroon trigger in logic apps | Microsoft Docs
description: Overzicht van Hallo terugkeerpatroon geactiveerd, en hoe toouse deze met een logische Azure-app.
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
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a>Aan de slag met Hallo terugkeerpatroon trigger
Hallo terugkeerpatroon door trigger te gebruiken, kunt u krachtige werkstromen in Hallo cloud.

U kunt bijvoorbeeld:

* Een werkstroom toorun opgeslagen SQL-procedure elke dag plannen.
* Een samenvatting weer van alle tweets binnen de afgelopen week over een bepaalde hashtag Hallo e.

tooget de slag met Hallo terugkeerpatroon trigger in een logische app, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-a-recurrence-trigger"></a>Gebruik een trigger terugkeerpatroon
Een trigger is een gebeurtenis die kan worden gebruikt toostart Hallo werkstroom die is gedefinieerd in een logische app. [Meer informatie over triggers](connectors-overview.md).

Hier volgt een van de voorbeeldreeks hoe tooset van een terugkeerpatroon in een logische app activeren:

1. Hallo toevoegen **terugkeerpatroon** trigger als Hallo eerste stap in een logische app.
2. Hallo parameters invullen voor Hallo terugkeerpatroon.

Hallo logische app nu een uitgevoerd na elke tijdsinterval gestart.

![HTTP-trigger](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a>Details van de trigger
Hallo terugkeerpatroon trigger heeft Hallo volgende eigenschappen die u kunt configureren.

Er wordt een logische app geactiveerd na een opgegeven tijdsinterval.
A * houdt in dat een vereist veld.

| Weergavenaam | De naam van eigenschap | Beschrijving |
| --- | --- | --- |
| Frequentie * |frequency |Hallo tijdseenheid: `Second`, `Minute`, `Hour`, `Day`, of `Year`. |
| Interval * |interval |Hallo tijdsinterval Hallo opgegeven frequentie voor Hallo terugkeerpatroon. |
| Tijdzone |Tijdzone |Als een begintijd zonder een UTC-offset is opgegeven, is deze tijdzone wordt gebruikt. |
| Begintijd |startTime |Hallo begintijd in [ISO 8601-notatie](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations). |

<br>

## <a name="next-steps"></a>Volgende stappen
Nu uitproberen Hallo-platform en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md). U kunt verkennen Hallo van andere beschikbare connectors in logische apps door te kijken onze [API's lijst](apis-list.md).

