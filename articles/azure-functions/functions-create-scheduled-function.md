---
title: Een functie maken in Azure die volgens een schema wordt uitgevoerd | Microsoft Docs
description: Ontdek hoe u in Azure een functie maakt die wordt uitgevoerd op basis van een schema dat u definieert.
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/03/2018
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 33f6cd9e10782bb8ff1b0ddf6d047aebc83f8008
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/04/2018
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a>Maak een functie in Azure die wordt geactiveerd door een timer

Ontdek hoe u Azure Functions gebruikt om een [serverloze](https://azure.microsoft.com/overview/serverless-computing/) functie te maken die wordt uitgevoerd op basis van een schema dat u definieert.

![Functie-app maken in Azure Portal](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Vereisten

Vereisten voor het voltooien van deze zelfstudie:

+ Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Een Azure-functie-app maken

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![De functie-app is gemaakt.](./media/functions-create-first-azure-function/function-app-create-success.png)

Vervolgens maakt u een functie in de nieuwe functie-app.

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a>Een door een timer geactiveerde functie maken

1. Vouw de functie-app uit en klik op de knop **+** naast **Functies**. Als dit de eerste functie in de functie-app is, selecteert u **Aangepaste functie**. U ziet nu de volledige set het functiesjablonen.

    ![De Quick Start-pagina van Functions in Azure Portal](./media/functions-create-scheduled-function/add-first-function.png)

2. Typ `timer` in het zoekveld en kies vervolgens de gewenste taal voor de trigger-sjabloon voor de timer. 

    ![Kies de door een timer geactiveerde functiesjabloon.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

3. Configureer de nieuwe trigger met de instellingen zoals opgegeven in de tabel onder de afbeelding.

    ![Maak een door een timer geactiveerde functie in Azure Portal.](./media/functions-create-scheduled-function/functions-create-timer-trigger-2.png)

    | Instelling | Voorgestelde waarde | Beschrijving |
    |---|---|---|
    | **Naam** | Standaard | Bepaalt de naam van de door de timer geactiveerde functie. |
    | **[Planning](http://en.wikipedia.org/wiki/Cron#CRON_expression)** | 0 \*/1 \* \* \* \* | Een [CRON-expressie](http://en.wikipedia.org/wiki/Cron#CRON_expression) met zes velden aan de hand waarvan uw functie elke minuut wordt uitgevoerd. |

2. Klik op **Create**. Er wordt een functie gemaakt in uw gekozen taal en deze wordt elke minuut uitgevoerd.

3. Controleer of dit correct wordt uitgevoerd door de traceringsinformatie die naar logboeken wordt geschreven te bekijken.

    ![De viewer voor functielogboeken in Azure Portal.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

U kunt het schema van de functie nu wijzigen zodat deze één keer per uur wordt uitgevoerd in plaats van elke minuut. 

## <a name="update-the-timer-schedule"></a>Het timerschema bijwerken

1. Vouw de functie uit en klik op **Integreren**. Dit is waar u de invoer- en uitvoerbindingen voor de functie definieert en het schema instelt. 

2. Voer een nieuwe waarde voor **Planning** per uur in van `0 0 */1 * * *` in, en klik vervolgens op **Opslaan**.  

![Het timerschema voor het bijwerken van functies in Azure Portal.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

U hebt nu een functie die één keer per uur wordt uitgevoerd. 

## <a name="clean-up-resources"></a>Resources opschonen

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Volgende stappen

U hebt een functie gemaakt die wordt uitgevoerd op basis van een schema.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Zie voor meer informatie over timeractiveringen [Schedule code execution with Azure Functions](functions-bindings-timer.md) (Code-uitvoering plannen met Azure Functions).
