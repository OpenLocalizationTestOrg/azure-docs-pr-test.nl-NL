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
# <a name="create-a-function-triggered-by-azure-blob-storage"></a><span data-ttu-id="34774-103">Een door Azure Blob Storage geactiveerde functie maken</span><span class="sxs-lookup"><span data-stu-id="34774-103">Create a function triggered by Azure Blob storage</span></span>

<span data-ttu-id="34774-104">Meer informatie over hoe toocreate een functie die wordt geactiveerd wanneer de bestanden zijn geüpload tooor bijgewerkt in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="34774-104">Learn how toocreate a function triggered when files are uploaded tooor updated in Azure Blob storage.</span></span>

![Bericht wordt weergegeven in Logboeken Hallo.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="34774-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="34774-106">Prerequisites</span></span>

+ <span data-ttu-id="34774-107">Download en installeer Hallo [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="34774-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
+ <span data-ttu-id="34774-108">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="34774-108">An Azure subscription.</span></span> <span data-ttu-id="34774-109">Als u nog geen abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="34774-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="34774-110">Een Azure-functie-app maken</span><span class="sxs-lookup"><span data-stu-id="34774-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![De functie-app is gemaakt.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="34774-112">Vervolgens maakt u een functie in nieuwe Hallo-functie-app.</span><span class="sxs-lookup"><span data-stu-id="34774-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a><span data-ttu-id="34774-113">Een door Blob Storage geactiveerde functie maken</span><span class="sxs-lookup"><span data-stu-id="34774-113">Create a Blob storage triggered function</span></span>

1. <span data-ttu-id="34774-114">Vouw de functie-app en klik op Hallo  **+**  knop naast te**functies**.</span><span class="sxs-lookup"><span data-stu-id="34774-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="34774-115">Als dit eerste functie in uw app functie hello, selecteer **aangepaste functie**.</span><span class="sxs-lookup"><span data-stu-id="34774-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="34774-116">De volledige set Hallo van functie-sjablonen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="34774-116">This displays hello complete set of function templates.</span></span>

    ![Functies Quick Start-pagina in hello Azure-portal](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. <span data-ttu-id="34774-118">Selecteer Hallo **BlobTrigger** sjabloon voor de gewenste taal en Hallo-instellingen zoals opgegeven in de tabel hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34774-118">Select hello **BlobTrigger** template for your desired language, and use hello settings as specified in hello table.</span></span>

    ![Hallo Blob storage geactiveerd functie maken.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | <span data-ttu-id="34774-120">Instelling</span><span class="sxs-lookup"><span data-stu-id="34774-120">Setting</span></span> | <span data-ttu-id="34774-121">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="34774-121">Suggested value</span></span> | <span data-ttu-id="34774-122">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34774-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="34774-123">**Pad**</span><span class="sxs-lookup"><span data-stu-id="34774-123">**Path**</span></span>   | <span data-ttu-id="34774-124">mycontainer/{name}</span><span class="sxs-lookup"><span data-stu-id="34774-124">mycontainer/{name}</span></span>    | <span data-ttu-id="34774-125">Locatie in Blob Storage die wordt bewaakt.</span><span class="sxs-lookup"><span data-stu-id="34774-125">Location in Blob storage being monitored.</span></span> <span data-ttu-id="34774-126">Hallo-bestandsnaam van Hallo blob wordt doorgegeven Hallo-binding als Hallo _naam_ parameter.</span><span class="sxs-lookup"><span data-stu-id="34774-126">hello file name of hello blob is passed in hello binding as hello _name_ parameter.</span></span>  |
    | <span data-ttu-id="34774-127">**Opslagaccountverbinding**</span><span class="sxs-lookup"><span data-stu-id="34774-127">**Storage account connection**</span></span> | <span data-ttu-id="34774-128">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="34774-128">AzureWebJobStorage</span></span> | <span data-ttu-id="34774-129">U kunt Hallo storage-account verbinding is al wordt gebruikt door de functie-app gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="34774-129">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="34774-130">**Een naam voor de functie opgeven**</span><span class="sxs-lookup"><span data-stu-id="34774-130">**Name your function**</span></span> | <span data-ttu-id="34774-131">Uniek in uw functie-app</span><span class="sxs-lookup"><span data-stu-id="34774-131">Unique in your function app</span></span> | <span data-ttu-id="34774-132">Naam van deze door Blob geactiveerde functie.</span><span class="sxs-lookup"><span data-stu-id="34774-132">Name of this blob triggered function.</span></span> |

3. <span data-ttu-id="34774-133">Klik op **maken** toocreate uw functie.</span><span class="sxs-lookup"><span data-stu-id="34774-133">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="34774-134">Vervolgens maakt u verbinding tooyour Azure Storage-account en Hallo maken **mycontainer** container.</span><span class="sxs-lookup"><span data-stu-id="34774-134">Next, you connect tooyour Azure Storage account and create hello **mycontainer** container.</span></span>

## <a name="create-hello-container"></a><span data-ttu-id="34774-135">Hallo-container maken</span><span class="sxs-lookup"><span data-stu-id="34774-135">Create hello container</span></span>

1. <span data-ttu-id="34774-136">Klik in de functie op **Integreren**, vouw **Documentatie** uit en kopieer de **Accountnaam** en de **Accountsleutel**.</span><span class="sxs-lookup"><span data-stu-id="34774-136">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="34774-137">U gebruikt deze referenties tooconnect toohello storage-account.</span><span class="sxs-lookup"><span data-stu-id="34774-137">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="34774-138">Als u al uw storage-account hebt gekoppeld, slaat u toostep 4.</span><span class="sxs-lookup"><span data-stu-id="34774-138">If you have already connected your storage account, skip toostep 4.</span></span>

    ![Hallo Storage-account verbindingsreferenties ophalen.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. <span data-ttu-id="34774-140">Hallo uitvoeren [Microsoft Azure Storage Explorer](http://storageexplorer.com/) hulpprogramma, klikt u op Hallo verbinding pictogram aan de linkerkant hello, kiest u **gebruik van een naam van het opslagaccount en de sleutel**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="34774-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Hallo Account Opslagverkenner hulpprogramma uitvoeren.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="34774-142">Voer Hallo **accountnaam** en **accountsleutel** uit stap 1, klikt u op **volgende** en vervolgens **Connect**.</span><span class="sxs-lookup"><span data-stu-id="34774-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span> 

    ![Geef referenties op Hallo opslag en verbinding maken.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="34774-144">Vouw Hallo gekoppeld opslagaccount, met de rechtermuisknop op **Blob-containers**, klikt u op **maken blob-container**, type `mycontainer`, en druk op enter.</span><span class="sxs-lookup"><span data-stu-id="34774-144">Expand hello attached storage account, right-click **Blob containers**, click **Create blob container**, type `mycontainer`, and then press enter.</span></span>

    ![Maak een opslagwachtrij.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

<span data-ttu-id="34774-146">Nu dat u een blob-container hebt, kunt u Hallo functie testen door het uploaden van een bestand toohello-container.</span><span class="sxs-lookup"><span data-stu-id="34774-146">Now that you have a blob container, you can test hello function by uploading a file toohello container.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="34774-147">Hallo functie testen</span><span class="sxs-lookup"><span data-stu-id="34774-147">Test hello function</span></span>

1. <span data-ttu-id="34774-148">Terug in hello Azure-portal, vouw bladeren tooyour functie Hallo **logboeken** Hallo onderaan pagina Hallo en zorg ervoor dat in dit logboek streaming wordt niet onderbroken.</span><span class="sxs-lookup"><span data-stu-id="34774-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="34774-149">Vouw in Storage Explorer uw opslagaccount, **Blob-containers** en **mycontainer** uit.</span><span class="sxs-lookup"><span data-stu-id="34774-149">In Storage Explorer, expand your storage account, **Blob containers**, and **mycontainer**.</span></span> <span data-ttu-id="34774-150">Klik op **Uploaden** en klik vervolgens op **Bestanden uploaden...**.</span><span class="sxs-lookup"><span data-stu-id="34774-150">Click **Upload** and then **Upload files...**.</span></span>

    ![Het uploaden van een bestand toohello blob-container.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. <span data-ttu-id="34774-152">In Hallo **bestanden uploaden** dialoogvenster vak, klikt u op Hallo **bestanden** veld.</span><span class="sxs-lookup"><span data-stu-id="34774-152">In hello **Upload files** dialog box, click hello **Files** field.</span></span> <span data-ttu-id="34774-153">Zoeken naar tooa-bestand op uw lokale computer, zoals een afbeeldingsbestand, te selecteren en op **Open** en vervolgens **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="34774-153">Browse tooa file on your local computer, such as an image file, select it and click **Open** and then **Upload**.</span></span>

1. <span data-ttu-id="34774-154">Ga terug tooyour functie Logboeken en controleer of dat Hallo blob is gelezen.</span><span class="sxs-lookup"><span data-stu-id="34774-154">Go back tooyour function logs and verify that hello blob has been read.</span></span>

   ![Bericht wordt weergegeven in Logboeken Hallo.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > <span data-ttu-id="34774-156">Wanneer de functie-app in Hallo verbruik standaardplan wordt uitgevoerd, kan er een vertraging van up tooseveral minuten tussen Hallo blob wordt toegevoegd of bijgewerkt en Hallo werken wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="34774-156">When your function app runs in hello default Consumption plan, there may be a delay of up tooseveral minutes between hello blob being added or updated and hello function being triggered.</span></span> <span data-ttu-id="34774-157">Overweeg om uw functie-app in een App Service-plan uit te voeren, als u lage latentie in uw door blob geactiveerde functies nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="34774-157">If you need low latency in your blob triggered functions, consider running your function app in an App Service plan.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="34774-158">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="34774-158">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="34774-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="34774-159">Next steps</span></span>

<span data-ttu-id="34774-160">U hebt gemaakt dat een functie die wordt uitgevoerd als een blob tooor bijgewerkt in de Blob-opslag is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="34774-160">You have created a function that runs when a blob is added tooor updated in Blob storage.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="34774-161">Zie [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md) (Blob-opslagbindingen in Azure Functions) voor meer informatie over de Blob-opslagtriggers.</span><span class="sxs-lookup"><span data-stu-id="34774-161">For more information about Blob storage triggers, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>
