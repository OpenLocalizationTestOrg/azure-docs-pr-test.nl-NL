---
title: een functie in Azure Blob storage geactiveerd aaaCreate | Microsoft Docs
description: Gebruik Azure Functions toocreate een zonder server-functie die wordt opgeroepen door items toegevoegd tooAzure Blob-opslag.
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: d6bff41c-a624-40c1-bbc7-80590df29ded
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: acb7d29abb07a22da11d0e65d2ed54591f8e3f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a>Een door Azure Blob Storage geactiveerde functie maken

Meer informatie over hoe toocreate een functie die wordt geactiveerd wanneer de bestanden zijn geüpload tooor bijgewerkt in Azure Blob-opslag.

![Bericht wordt weergegeven in Logboeken Hallo.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Vereisten

+ Download en installeer Hallo [Microsoft Azure Storage Explorer](http://storageexplorer.com/).
+ Een Azure-abonnement. Als u nog geen abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) voordat u begint.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Een Azure-functie-app maken

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![De functie-app is gemaakt.](./media/functions-create-first-azure-function/function-app-create-success.png)

Vervolgens maakt u een functie in nieuwe Hallo-functie-app.

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a>Een door Blob Storage geactiveerde functie maken

1. Vouw de functie-app en klik op Hallo  **+**  knop naast te**functies**. Als dit eerste functie in uw app functie hello, selecteer **aangepaste functie**. De volledige set Hallo van functie-sjablonen worden weergegeven.

    ![Functies Quick Start-pagina in hello Azure-portal](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. Selecteer Hallo **BlobTrigger** sjabloon voor de gewenste taal en Hallo-instellingen zoals opgegeven in de tabel hello gebruiken.

    ![Hallo Blob storage geactiveerd functie maken.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | Instelling | Voorgestelde waarde | Beschrijving |
    |---|---|---|
    | **Pad**   | mycontainer/{name}    | Locatie in Blob Storage die wordt bewaakt. Hallo-bestandsnaam van Hallo blob wordt doorgegeven Hallo-binding als Hallo _naam_ parameter.  |
    | **Opslagaccountverbinding** | AzureWebJobStorage | U kunt Hallo storage-account verbinding is al wordt gebruikt door de functie-app gebruiken of een nieuwe maken.  |
    | **Een naam voor de functie opgeven** | Uniek in uw functie-app | Naam van deze door Blob geactiveerde functie. |

3. Klik op **maken** toocreate uw functie.

Vervolgens maakt u verbinding tooyour Azure Storage-account en Hallo maken **mycontainer** container.

## <a name="create-hello-container"></a>Hallo-container maken

1. Klik in de functie op **Integreren**, vouw **Documentatie** uit en kopieer de **Accountnaam** en de **Accountsleutel**. U gebruikt deze referenties tooconnect toohello storage-account. Als u al uw storage-account hebt gekoppeld, slaat u toostep 4.

    ![Hallo Storage-account verbindingsreferenties ophalen.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. Hallo uitvoeren [Microsoft Azure Storage Explorer](http://storageexplorer.com/) hulpprogramma, klikt u op Hallo verbinding pictogram aan de linkerkant hello, kiest u **gebruik van een naam van het opslagaccount en de sleutel**, en klik op **volgende**.

    ![Hallo Account Opslagverkenner hulpprogramma uitvoeren.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. Voer Hallo **accountnaam** en **accountsleutel** uit stap 1, klikt u op **volgende** en vervolgens **Connect**. 

    ![Geef referenties op Hallo opslag en verbinding maken.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. Vouw Hallo gekoppeld opslagaccount, met de rechtermuisknop op **Blob-containers**, klikt u op **maken blob-container**, type `mycontainer`, en druk op enter.

    ![Maak een opslagwachtrij.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

Nu dat u een blob-container hebt, kunt u Hallo functie testen door het uploaden van een bestand toohello-container.

## <a name="test-hello-function"></a>Hallo functie testen

1. Terug in hello Azure-portal, vouw bladeren tooyour functie Hallo **logboeken** Hallo onderaan pagina Hallo en zorg ervoor dat in dit logboek streaming wordt niet onderbroken.

1. Vouw in Storage Explorer uw opslagaccount, **Blob-containers** en **mycontainer** uit. Klik op **Uploaden** en klik vervolgens op **Bestanden uploaden...**.

    ![Het uploaden van een bestand toohello blob-container.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. In Hallo **bestanden uploaden** dialoogvenster vak, klikt u op Hallo **bestanden** veld. Zoeken naar tooa-bestand op uw lokale computer, zoals een afbeeldingsbestand, te selecteren en op **Open** en vervolgens **uploaden**.

1. Ga terug tooyour functie Logboeken en controleer of dat Hallo blob is gelezen.

   ![Bericht wordt weergegeven in Logboeken Hallo.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > Wanneer de functie-app in Hallo verbruik standaardplan wordt uitgevoerd, kan er een vertraging van up tooseveral minuten tussen Hallo blob wordt toegevoegd of bijgewerkt en Hallo werken wordt geactiveerd. Overweeg om uw functie-app in een App Service-plan uit te voeren, als u lage latentie in uw door blob geactiveerde functies nodig hebt.

## <a name="clean-up-resources"></a>Resources opschonen

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Volgende stappen

U hebt gemaakt dat een functie die wordt uitgevoerd als een blob tooor bijgewerkt in de Blob-opslag is toegevoegd. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Zie [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md) (Blob-opslagbindingen in Azure Functions) voor meer informatie over de Blob-opslagtriggers.
