---
title: aaaAdd hello queryactie in logic apps | Microsoft Docs
description: Overzicht van Hallo queryactie voor het uitvoeren van acties zoals matrix van filter.
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a>Aan de slag met Hallo queryactie
Met behulp van de actie query Hallo, kunt u met de batches en matrices tooaccomplish werkstromen te werken:

* Een taak maken voor alle hoge prioriteit records uit een database.
* Sla alle PDF-bijlagen voor e-mailberichten naar een Azure-blob.

tooget gestart met Hallo queryactie in een logische app, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-query-action"></a>Gebruik Hallo queryactie
Een actie is een bewerking die wordt uitgevoerd door Hallo werkstroom die is gedefinieerd in een logische app. [Meer informatie over acties](connectors-overview.md).  

Hallo queryactie heeft momenteel een bewerking, Hallo filter matrix, die wordt weergegeven in de ontwerpfunctie Hallo aangeroepen. Dit kunt u een matrix tooquery en een set gefilterde resultaten geretourneerd.

Hier ziet u hoe u deze in een logische app kunt toevoegen:

1. Selecteer Hallo **nieuwe stap** knop.
2. Kies **een actie toevoegen**.
3. Typ in het zoekvak Hallo actie, **filter** toolist hello **matrix van Filter** in te grijpen.
   
    ![Selecteer Hallo queryactie](./media/connectors-native-query/using-action-1.png)
4. Selecteer een toofilter matrix. (hello volgende schermafbeelding ziet u Hallo-matrix van resultaten van een zoekopdracht Twitter.)
5. Maak een voorwaarde tooevaluate op elk item. (Hallo schermopname na filters tweets van gebruikers die beschikken over meer dan 100 PC-gebruikers.)
   
    ![Actie voltooid Hallo-query](./media/connectors-native-query/using-action-2.png)
   
    Hallo-actie wordt een nieuwe matrix die alleen de resultaten die voldoen aan de vereisten voor Hallo filter bevat uitvoer.
6. Klik op Hallo linkerbovenhoek van Hallo werkbalk toosave en uw logische app worden beide opslaan en publiceren (activeren).

## <a name="query-action"></a>Queryactie
Hier vindt u details Hallo voor Hallo-actie die ondersteuning biedt voor deze connector. Hallo-connector heeft een mogelijke actie.

| Actie | Beschrijving |
| --- | --- |
| Matrix van filter |Evalueert een voorwaarde voor elk item in een matrix en Hallo resultaten retourneert |

## <a name="action-details"></a>Actiedetails
Hallo queryactie wordt geleverd met een mogelijke actie. Hallo volgende tabellen worden beschreven Hallo vereiste en optionele invoervelden voor Hallo actie en het bijbehorende uitvoerdetails hello, die gekoppeld zijn aan het Hallo-actie.

### <a name="filter-array"></a>Matrix van filter
Hallo volgen invoervelden voor Hallo actie, waardoor een uitgaande HTTP-aanvraag.
A * houdt in dat een vereist veld.

| Weergavenaam | De naam van eigenschap | Beschrijving |
| --- | --- | --- |
| Van * |Van |Hallo matrix toofilter |
| Voorwaarde * |waar |Hallo voorwaarde tooevaluate voor elk item |

<br>

### <a name="output-details"></a>Uitvoerdetails
Hallo hieronder vindt u uitvoerdetails voor Hallo HTTP-antwoord.

| De naam van eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| Gefilterde matrix |matrix |Een matrix met een object voor elk gefilterde resultaat |

## <a name="next-steps"></a>Volgende stappen
Nu uitproberen Hallo-platform en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md). U kunt verkennen Hallo van andere beschikbare connectors in logische apps door te kijken onze [API's lijst](apis-list.md).

