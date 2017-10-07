---
title: aaaCreate een functie die wordt uitgevoerd volgens een schema in Azure | Microsoft Docs
description: Meer informatie over hoe toocreate een functie in Azure die wordt uitgevoerd op basis van een planning die u definieert.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 793b06a65a154466dfd4c121bcc88082227cd597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a>Maak een functie in Azure die wordt geactiveerd door een timer

Meer informatie over hoe toouse Azure Functions toocreate een functie die wordt uitgevoerd op basis van een planning die u definieert.

![Functie-app maken in hello Azure-portal](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie:

+ Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Een Azure-functie-app maken

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![De functie-app is gemaakt.](./media/functions-create-first-azure-function/function-app-create-success.png)

Vervolgens maakt u een functie in nieuwe Hallo-functie-app.

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a>Een door een timer geactiveerde functie maken

1. Vouw de functie-app en klik op Hallo  **+**  knop naast te**functies**. Als dit eerste functie in uw app functie hello, selecteer **aangepaste functie**. De volledige set Hallo van functie-sjablonen worden weergegeven.

    ![Functies Quick Start-pagina in hello Azure-portal](./media/functions-create-scheduled-function/add-first-function.png)

2. Selecteer Hallo **TimerTrigger** sjabloon voor de gewenste taal. Gebruik vervolgens Hallo instellingen zoals opgegeven in de tabel Hallo:

    ![Maak een geactiveerd door de timerfunctie in hello Azure-portal.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | Instelling | Voorgestelde waarde | Beschrijving |
    |---|---|---|
    | **Een naam voor de functie opgeven** | TimerTriggerCSharp1 | Hallo-naam van de timerfunctie geactiveerd definieert. |
    | **[Planning](http://en.wikipedia.org/wiki/Cron#CRON_expression)** | 0 \*/1 \* \* \* \* | Een veld zes [CRON expressie](http://en.wikipedia.org/wiki/Cron#CRON_expression) die uw toorun functie plant u elke minuut. |

2. Klik op **Create**. Er wordt een functie gemaakt in uw gekozen taal en deze wordt elke minuut uitgevoerd.

3. Controleer of u kan worden uitgevoerd door toohello Logboeken geschreven traceringsinformatie weer te geven.

    ![Functies melden viewer hello Azure-portal.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

U kunt nu de planning van de functie Hallo wijzigen zodat deze minder vaak zoals één keer per uur wordt uitgevoerd. 

## <a name="update-hello-timer-schedule"></a>Hallo timer schema bijwerken

1. Vouw de functie uit en klik op **Integreren**. Dit is waar u definieert u welke invoer en uitvoer van de bindingen voor de functie en ook Hallo-planning instellen. 

2. Voer voor de nieuwe **Planning** een waarde van `0 0 */1 * * *` in en klik vervolgens op **Opslaan**.  

![Functies bijwerken in hello Azure-portal timer planning.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

U hebt nu een functie die één keer per uur wordt uitgevoerd. 

## <a name="clean-up-resources"></a>Resources opschonen

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Volgende stappen

U hebt een functie gemaakt die wordt uitgevoerd op basis van een schema.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Zie voor meer informatie over timeractiveringen [Schedule code execution with Azure Functions](functions-bindings-timer.md) (Code-uitvoering plannen met Azure Functions).