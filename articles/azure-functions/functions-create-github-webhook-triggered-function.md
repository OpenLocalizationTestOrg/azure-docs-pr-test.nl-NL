---
title: een functie in Azure geactiveerd door een GitHub webhook aaaCreate | Microsoft Docs
description: Azure Functions toocreate een zonder server-functie die wordt opgeroepen door een GitHub webhook gebruiken.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 8ffcde82c9310d749159ed53eab113658e38a030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a>Een door een GitHub-webhook geactiveerde functie maken

Meer informatie over hoe toocreate een functie die wordt veroorzaakt door een HTTP-webhook-aanvraag met een GitHub-specifieke nettolading.

![Github Webhook geactiveerd functie in hello Azure-portal](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Vereisten

+ Een GitHub-account met ten minste één project.
+ Een Azure-abonnement. Als u nog geen abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) voordat u begint.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Een Azure-functie-app maken

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![De functie-app is gemaakt.](./media/functions-create-first-azure-function/function-app-create-success.png)

Vervolgens maakt u een functie in nieuwe Hallo-functie-app.

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a>Een door een GitHub-webhook geactiveerde functie maken

1. Vouw de functie-app en klik op Hallo  **+**  knop naast te**functies**. Als dit eerste functie in uw app functie hello, selecteer **aangepaste functie**. De volledige set Hallo van functie-sjablonen worden weergegeven.

    ![Functies Quick Start-pagina in hello Azure-portal](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. Selecteer Hallo **GitHub WebHook** sjabloon voor de gewenste taal. **Geef de functie een naam** en selecteer vervolgens **Maken**.

     ![Maak een GitHub webhook geactiveerd-functie in hello Azure-portal](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. Klik in de nieuwe functie op **<> / Get function URL**, kopiëren en opslaan van Hallo waarden. Hetzelfde geldt voor Hallo **<> / ophalen van GitHub geheim**. U gebruikt deze waarden tooconfigure hello webhook in GitHub.

    ![Hallo functiecode bekijken](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

Vervolgens maakt u een webhook in uw GitHub-opslagplaats.

## <a name="configure-hello-webhook"></a>Hallo webhook configureren

1. Navigeer in GitHub, tooa opslagplaats waarvan u eigenaar. U kunt ook een opslagplaats gebruiken die u hebt gesplitst. Als u een opslagplaats toofork moet, gebruikt u <https://github.com/Azure-Samples/functions-quickstart>.

1. Klik achtereenvolgens op **Instellingen**, **Webhooks** en **Webhook toevoegen**.

    ![Een GitHub-webhook toevoegen](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. Instellingen zoals opgegeven in de tabel hello gebruiken en klik vervolgens op **webhook toevoegen**.

    ![Hallo webhook-URL en geheim instellen](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| Instelling | Voorgestelde waarde | Beschrijving |
|---|---|---|
| **URL van de nettolading** | Gekopieerde waarde | Hallo-waarde geretourneerd door **<> / Get function URL**. |
| **Geheim**   | Gekopieerde waarde | Hallo-waarde geretourneerd door **<> / ophalen van GitHub geheim**. |
| **Inhoudstype** | application/json | Hallo functie verwacht een JSON-nettolading. |
| Gebeurtenistriggers | Ik wil afzonderlijke gebeurtenissen selecteren | We willen alleen tootrigger op probleem Opmerking gebeurtenissen.  |
| | Opmerking bij actie item |  |

Nu Hallo webhook geconfigureerde tootrigger is de functie wanneer een nieuwe probleem opmerking wordt toegevoegd.

## <a name="test-hello-function"></a>Hallo functie testen

1. Open in uw GitHub-opslagplaats Hallo **problemen** tabblad in een nieuw browservenster.

1. Op het nieuwe venster Hallo **nieuwe probleem**, typt u een titel en klik vervolgens op **indienen van nieuwe probleem**.

1. Typ een opmerking in Hallo probleem, en klik op **Opmerking**.

    ![Voeg een opmerking bij de actie van het item van GitHub toe.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. Ga terug toohello portal en bekijk Hallo Logboeken. Hier ziet u een vermelding in het traceerlogboek door Hallo nieuwe opmerkingstekst.

     ![De tekst hello opmerking in Hallo logboeken weergeven.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a>Resources opschonen

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Volgende stappen

U hebt een functie gemaakt die wordt uitgevoerd wanneer er een aanvraag wordt ontvangen van een GitHub-webhook.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Zie [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md) (Azure Functions-HTTP- en webhookbindingen) voor meer informatie over webhooktriggers.
