---
title: een functie in Azure geactiveerd door Wachtrijberichten aaaCreate | Microsoft Docs
description: Gebruik Azure Functions toocreate een zonder server-functie die wordt opgeroepen door een berichten verzonden tooan Azure Storage-wachtrij.
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361da2a4-15d1-4903-bdc4-cc4b27fc3ff4
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e9501ed336b502eaeee3fa62ec4ae085c76de0ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a>Een door Azure Queue Storage geactiveerde functie maken

Meer informatie over hoe toocreate een functie die wordt geactiveerd wanneer berichten worden verzonden tooan Azure Storage-wachtrij.

![Bericht wordt weergegeven in Logboeken Hallo.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Vereisten

- Download en installeer Hallo [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

- Een Azure-abonnement. Als u nog geen abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) voordat u begint.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Een Azure-functie-app maken

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![De functie-app is gemaakt.](./media/functions-create-first-azure-function/function-app-create-success.png)

Vervolgens maakt u een functie in nieuwe Hallo-functie-app.

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a>Een door een wachtrij geactiveerde functie maken

1. Vouw de functie-app en klik op Hallo  **+**  knop naast te**functies**. Als dit eerste functie in uw app functie hello, selecteer **aangepaste functie**. De volledige set Hallo van functie-sjablonen worden weergegeven.

    ![Functies Quick Start-pagina in hello Azure-portal](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. Selecteer Hallo **QueueTrigger** sjabloon voor de gewenste taal en Hallo-instellingen zoals opgegeven in de tabel hello gebruiken.

    ![De opslagfunctie wachtrij geactiveerd Hallo maken.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | Instelling | Voorgestelde waarde | Beschrijving |
    |---|---|---|
    | **Wachtrijnaam**   | myqueue-items    | Naam van Hallo wachtrij tooconnect tooin uw Storage-account. |
    | **Opslagaccountverbinding** | AzureWebJobStorage | U kunt Hallo storage-account verbinding is al wordt gebruikt door de functie-app gebruiken of een nieuwe maken.  |
    | **Een naam voor de functie opgeven** | Uniek in uw functie-app | Naam van deze door een wachtrij geactiveerde functie. |

3. Klik op **maken** toocreate uw functie.

Vervolgens maakt u verbinding tooyour Azure Storage-account en Hallo maken **rapportberichten items** storage-wachtrij.

## <a name="create-hello-queue"></a>Hallo wachtrij maken

1. Klik in de functie op **Integreren**, vouw **Documentatie** uit en kopieer de **Accountnaam** en de **Accountsleutel**. U gebruikt deze referenties tooconnect toohello storage-account. Als u al uw storage-account hebt gekoppeld, slaat u toostep 4.

    ![Hallo Storage-account verbindingsreferenties ophalen.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)v

1. Hallo uitvoeren [Microsoft Azure Storage Explorer](http://storageexplorer.com/) hulpprogramma, klikt u op Hallo verbinding pictogram aan de linkerkant hello, kiest u **gebruik van een naam van het opslagaccount en de sleutel**, en klik op **volgende**.

    ![Hallo Account Opslagverkenner hulpprogramma uitvoeren.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. Voer Hallo **accountnaam** en **accountsleutel** uit stap 1, klikt u op **volgende** en vervolgens **Connect**.

    ![Geef referenties op Hallo opslag en verbinding maken.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. Vouw Hallo gekoppeld opslagaccount, met de rechtermuisknop op **wachtrijen**, klikt u op **wachtrij maken**, type `myqueue-items`, en druk op enter.

    ![Maak een opslagwachtrij.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

Nu dat u een opslagwachtrij hebt, kunt u Hallo functie testen door een berichtenwachtrij toohello toe te voegen.

## <a name="test-hello-function"></a>Hallo functie testen

1. Terug in hello Azure-portal, vouw bladeren tooyour functie Hallo **logboeken** Hallo onderaan pagina Hallo en zorg ervoor dat in dit logboek streaming wordt niet onderbroken.

1. Vouw in Storage Explorer uw opslagaccount, **Wachtrijen** en **myqueue-items** uit en klik vervolgens op **Bericht toevoegen**.

    ![Een berichtenwachtrij toohello toevoegen.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. Typ uw "Hallo wereld"- bericht in **Berichttekst** en klik op **OK**.

1. Wacht een paar seconden en vervolgens gaat u terug tooyour functie Logboeken en controleer of dat nieuwe Hallo-bericht is gelezen uit de wachtrij Hallo.

    ![Bericht wordt weergegeven in Logboeken Hallo.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. Klik in Opslagverkenner op **vernieuwen** en controleer of het Hallo-bericht dat is verwerkt en is niet langer in de wachtrij Hallo.

## <a name="clean-up-resources"></a>Resources opschonen

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Volgende stappen

U kunt een functie die wordt uitgevoerd als er een bericht wordt toegevoegd tooa opslagwachtrij hebt gemaakt.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Zie [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md) (Opslagwachtrijbindingen van Azure Functions) voor meer informatie over activeringen van Queue Storage.