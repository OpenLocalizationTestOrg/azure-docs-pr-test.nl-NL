---
title: Event Hubs vastleggen aaaAzure inschakelen via de portal | Microsoft Docs
description: Inschakelen Hallo Event Hubs vastleggen via hello Azure-portal.
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 27c7528552c497a4d98873a22bd56a991c66247c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-event-hubs-capture-using-hello-azure-portal"></a><span data-ttu-id="ed9f2-103">Inschakelen van Event Hubs vastleggen met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="ed9f2-103">Enable Event Hubs Capture using hello Azure portal</span></span>

<span data-ttu-id="ed9f2-104">U kunt vastleggen configureren tijdens het Hallo event hub maken met behulp van Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ed9f2-104">You can configure Capture at hello event hub creation time using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ed9f2-105">U kunt beide vastleggen Hallo gegevens tooan Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container of tooan [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-105">You can either capture hello data tooan Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container, or tooan [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span></span>

## <a name="capture-data-tooan-azure-storage-account"></a><span data-ttu-id="ed9f2-106">Vastleggen van gegevens tooan Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="ed9f2-106">Capture data tooan Azure Storage account</span></span>  

<span data-ttu-id="ed9f2-107">Wanneer u een event hub maakt, kunt u vastleggen inschakelen door te klikken op Hallo **op** knop in Hallo **Event Hub maken** portalblade.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-107">When you create an event hub, you can enable Capture by clicking hello **On** button in hello **Create Event Hub** portal blade.</span></span> <span data-ttu-id="ed9f2-108">Vervolgens geeft u een Opslagaccount en container door te klikken op **Azure Storage** in Hallo **vastleggen Provider** vak.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-108">You then specify a Storage Account and container by clicking **Azure Storage** in hello **Capture Provider** box.</span></span> <span data-ttu-id="ed9f2-109">Omdat Event Hubs vastleggen gebruik maakt van verificatie van de service-naar-service met opslag, hoeft u geen toospecify een verbindingsreeks voor opslag.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-109">Because Event Hubs Capture uses service-to-service authentication with storage, you do not need toospecify a storage connection string.</span></span> <span data-ttu-id="ed9f2-110">Hallo resource objectkiezer Hallo resource-URI voor uw opslagaccount automatisch geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-110">hello resource picker selects hello resource URI for your storage account automatically.</span></span> <span data-ttu-id="ed9f2-111">Als u Azure Resource Manager gebruikt, moet u deze URI expliciet als een tekenreeks opgeven.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-111">If you use Azure Resource Manager, you must supply this URI explicitly as a string.</span></span>

<span data-ttu-id="ed9f2-112">tijdvenster voor Hallo standaard is 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-112">hello default time window is 5 minutes.</span></span> <span data-ttu-id="ed9f2-113">Hallo minimumwaarde is 1, Hallo maximaal 15.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-113">hello minimum value is 1, hello maximum 15.</span></span> <span data-ttu-id="ed9f2-114">Hallo **grootte** venster heeft een bereik van 10 500 MB.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-114">hello **Size** window has a range of 10-500 MB.</span></span>

![][1]

## <a name="capture-data-tooan-azure-data-lake-store-account"></a><span data-ttu-id="ed9f2-115">Gegevens tooan Azure Data Lake Store-account voor het vastleggen</span><span class="sxs-lookup"><span data-stu-id="ed9f2-115">Capture data tooan Azure Data Lake Store account</span></span>

<span data-ttu-id="ed9f2-116">toocapture gegevens tooAzure Data Lake Store die u maakt een Data Lake Store-account en een event hub:</span><span class="sxs-lookup"><span data-stu-id="ed9f2-116">toocapture data tooAzure Data Lake Store, you create a Data Lake Store account, and an event hub:</span></span>

### <a name="create-an-azure-data-lake-store-account-and-folders"></a><span data-ttu-id="ed9f2-117">Een Azure Data Lake Store-account en -mappen maken</span><span class="sxs-lookup"><span data-stu-id="ed9f2-117">Create an Azure Data Lake Store account and folders</span></span>

1. <span data-ttu-id="ed9f2-118">Maken van een Data Lake Store-account, Hallo-instructies in [aan de slag met Azure Data Lake Store met hello Azure-portal](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ed9f2-118">Create a Data Lake Store account, following hello instructions in [Get started with Azure Data Lake Store using hello Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span> 
2. <span data-ttu-id="ed9f2-119">Maak een map onder dit account, instructies te volgen Hallo in Hallo [mappen maken in Azure Data Lake Store-account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) sectie.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-119">Create a folder under this account, following hello instructions in hello [Create folders in Azure Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) section.</span></span>
3. <span data-ttu-id="ed9f2-120">Klik op Hallo Data Lake Store-accountblade **Data Explorer**.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-120">In hello Data Lake Store account blade, click **Data Explorer**.</span></span>
4. <span data-ttu-id="ed9f2-121">Klik op **Toegang**.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-121">Click **Access**.</span></span>
5. <span data-ttu-id="ed9f2-122">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-122">Click **Add**.</span></span>
6. <span data-ttu-id="ed9f2-123">In Hallo **zoeken op naam of e-mailadres** vak type **Microsoft.EventHubs** en selecteer deze optie.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-123">In hello **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span> 
7. <span data-ttu-id="ed9f2-124">Hallo **machtigingen** tabblad wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-124">hello **Permissions** tab appears.</span></span> <span data-ttu-id="ed9f2-125">Hallo-machtigingen instellen zoals weergegeven in de volgende afbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="ed9f2-125">Set hello permissions as shown in hello following figure:</span></span>

    ![][6]

8. <span data-ttu-id="ed9f2-126">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-126">Click **OK**.</span></span>
9. <span data-ttu-id="ed9f2-127">Maak nu een map in de hoofdmap Hallo door toohello doelmap bladeren en te klikken op Hallo mapnaam.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-127">Now, create a folder in hello root folder by browsing toohello target folder and clicking on hello folder name.</span></span>
10. <span data-ttu-id="ed9f2-128">Klik op **Toegang**.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-128">Click **Access**.</span></span>
11. <span data-ttu-id="ed9f2-129">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-129">Click **Add**.</span></span>
12. <span data-ttu-id="ed9f2-130">In Hallo **zoeken op naam of e-mailadres** vak type **Microsoft.EventHubs** en selecteer deze optie.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-130">In hello **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span>
13. <span data-ttu-id="ed9f2-131">Hallo **machtigingen** tabblad opnieuw wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-131">hello **Permissions** tab appears again.</span></span> <span data-ttu-id="ed9f2-132">Hallo-machtigingen instellen zoals weergegeven in de volgende afbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="ed9f2-132">Set hello permissions as shown in hello following figure:</span></span>

    ![][5]

### <a name="create-an-event-hub"></a><span data-ttu-id="ed9f2-133">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="ed9f2-133">Create an event hub</span></span>

1. <span data-ttu-id="ed9f2-134">Houd er rekening mee Hallo event hub moet Hallo dezelfde Azure-abonnement als hello Azure Data Lake Store u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-134">Note that hello event hub must be in hello same Azure subscription as hello Azure Data Lake Store you just created.</span></span> <span data-ttu-id="ed9f2-135">Maak Hallo event hub te klikken op Hallo **op** knop onder **vastleggen** in Hallo **Event Hub maken** portalblade.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-135">Create hello event hub, clicking hello **On** button under **Capture** in hello **Create Event Hub** portal blade.</span></span> 
2. <span data-ttu-id="ed9f2-136">In Hallo **Event Hub maken** portalblade, selecteer **Azure Data Lake Store** van Hallo **vastleggen Provider** vak.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-136">In hello **Create Event Hub** portal blade, select **Azure Data Lake Store** from hello **Capture Provider** box.</span></span>
3. <span data-ttu-id="ed9f2-137">In **Selecteer Data Lake Store**, geef Hallo Data Lake Store-account voor u eerder en in Hallo gemaakt **pad naar de Data Lake** Voer Hallo pad toohello gegevensmap u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-137">In **Select Data Lake Store**, specify hello Data Lake Store account you created previously, and in hello **Data Lake Path** field, enter hello path toohello data folder you created.</span></span>

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a><span data-ttu-id="ed9f2-138">Capture toevoegen of configureren op een bestaande Event Hub</span><span class="sxs-lookup"><span data-stu-id="ed9f2-138">Add or configure Capture on an existing event hub</span></span>

<span data-ttu-id="ed9f2-139">U kunt Capture configureren op bestaande Event Hubs in Event Hubs-naamruimten.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-139">You can configure Capture on existing event hubs that are in Event Hubs namespaces.</span></span> <span data-ttu-id="ed9f2-140">tooenable vastleggen van een bestaande event hub of toochange uw instellingen vastleggen, klikt u op Hallo naamruimte tooload hello **Essentials** blade, klikt u vervolgens op Hallo event hub die u wilt tooenable of Hallo vastleggen instelling wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-140">tooenable Capture on an existing event hub, or toochange your Capture settings, click hello namespace tooload hello **Essentials** blade, then click hello event hub for which you want tooenable or change hello Capture setting.</span></span> <span data-ttu-id="ed9f2-141">Tot slot op Hallo **eigenschappen** sectie Hallo blade geopend en bewerk vervolgens de instellingen voor het vastleggen van hello, zoals wordt weergegeven in de volgende cijfers Hallo:</span><span class="sxs-lookup"><span data-stu-id="ed9f2-141">Finally, click hello **Properties** section of hello open blade and then edit hello Capture settings, as shown in hello following figures:</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="ed9f2-142">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="ed9f2-142">Azure Blob Storage</span></span>

![][2]

### <a name="azure-data-lake-store"></a><span data-ttu-id="ed9f2-143">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ed9f2-143">Azure Data Lake Store</span></span>

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a><span data-ttu-id="ed9f2-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ed9f2-144">Next steps</span></span>

<span data-ttu-id="ed9f2-145">U kunt ook Event Hubs Capture configureren met behulp van Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="ed9f2-145">You can also configure Event Hubs Capture using Azure Resource Manager templates.</span></span> <span data-ttu-id="ed9f2-146">Zie voor meer informatie [Capture inschakelen met behulp van een Azure Resource Manager-sjabloon](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span><span class="sxs-lookup"><span data-stu-id="ed9f2-146">For more information, see [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span></span>
