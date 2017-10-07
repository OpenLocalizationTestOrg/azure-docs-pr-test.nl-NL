---
title: uw eerste functie van Azure Portal Hallo aaaCreate | Microsoft Docs
description: Meer informatie over hoe uw eerste Azure-functie voor het gebruik van zonder server worden uitgevoerd toocreate hello Azure-portal.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/07/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 84283d7d4bc6015061946af4589f9a70ae61f36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-in-hello-azure-portal"></a>Maken van uw eerste functie in hello Azure-portal

Azure Functions, kunt u uw code in een omgeving zonder server uitvoeren zonder toofirst een virtuele machine maken of een webtoepassing publiceert. In dit onderwerp informatie over hoe toouse functioneert toocreate een functie "Hallo wereld" in hello Azure-portal.

![Functie-app maken in hello Azure-portal](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a>Meld u bij tooAzure

Meld u bij toohello [Azure-portal](https://portal.azure.com/).

## <a name="create-a-function-app"></a>Een functie-app maken

U moet een functie-app toohost Hallo uitvoering van uw functies hebben. Met een functie-app kunt u functies groeperen in een logische eenheid, zodat u resources eenvoudiger kunt beheren, implementeren en delen. 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

Vervolgens maakt u een functie in nieuwe Hallo-functie-app.

## <a name="create-function"></a>Een door HTTP geactiveerde functie maken

1. Vouw uw nieuwe functie-app en klik op Hallo  **+**  knop naast te**functies**.

2.  In Hallo **snel aan de slag** pagina **WebHook + API**, **een taal kiezen** voor uw functie en klik op **maken van deze functie** . 
   
    ![Functies in Quick Start hello Azure-portal.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

Een functie wordt gemaakt in uw gekozen taal met Hallo-sjabloon voor een functie HTTP is geactiveerd. U kunt de nieuwe functie Hallo uitvoeren door een HTTP-aanvraag te verzenden.

## <a name="test-hello-function"></a>Hallo functie testen

1. Klik in de nieuwe functie op **</> Functie-URL ophalen**, selecteer **Standaard (functietoets)** en klik vervolgens op **Kopieer**. 

    ![Hallo function URL kopiëren van hello Azure-portal](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. Hallo function URL in de adresbalk van uw browser plakken. Hallo-queryreeks toevoegen `&name=<yourname>` toothis URL en druk op Hallo `Enter` sleutel op uw toetsenbord tooexecute Hallo-aanvraag. Hallo Hieronder volgt een voorbeeld van het Hallo-antwoord geretourneerd door de functie Hallo in de browser Edge Hallo:

    ![De reactie van de functie in Hallo browser.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    Hallo-aanvraag URL bevat een sleutel die is vereist, standaard tooaccess uw functie via HTTP.   

3. Wanneer de functie wordt uitgevoerd, is traceringsinformatie toohello Logboeken geschreven. toosee hello trace-uitvoer van de vorige uitvoering hello, tooyour functie in de portal Hallo retourneren en klik op Hallo pijl onderaan Hallo Hallo scherm tooexpand **logboeken**. 

   ![Functies melden viewer hello Azure-portal.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a>Resources opschonen

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Volgende stappen

U hebt een functie-app met een eenvoudige door HTTP geactiveerde functie gemaakt.  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Zie [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md) (Azure Functions-HTTP- en webhookbindingen) voor meer informatie.



