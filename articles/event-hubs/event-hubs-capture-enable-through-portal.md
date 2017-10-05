---
title: Azure Event Hubs Capture inschakelen via de portal | Microsoft Docs
description: Schakel de functie Event Hubs Capture in met behulp van de Azure-portal.
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
ms.openlocfilehash: 0cbf45dce922647f2996f929d2c7cf885a2f4db4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="enable-event-hubs-capture-using-the-azure-portal"></a><span data-ttu-id="16386-103">Event Hubs Capture inschakelen met behulp van de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="16386-103">Enable Event Hubs Capture using the Azure portal</span></span>

<span data-ttu-id="16386-104">Wanneer u de gebeurtenishub maakt, kunt u Capture configureren met behulp van de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="16386-104">You can configure Capture at the event hub creation time using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="16386-105">U kunt de gegevens vastleggen in een [Blob Storage](https://azure.microsoft.com/services/storage/blobs/)-container van Azure of in een [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/)-account.</span><span class="sxs-lookup"><span data-stu-id="16386-105">You can either capture the data to an Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container, or to an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span></span>

## <a name="capture-data-to-an-azure-storage-account"></a><span data-ttu-id="16386-106">Gegevens vastleggen in een Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="16386-106">Capture data to an Azure Storage account</span></span>  

<span data-ttu-id="16386-107">Wanneer u een event hub maakt, kunt u vastleggen inschakelen door te klikken op de **op** knop in de **Event Hub maken** portalblade.</span><span class="sxs-lookup"><span data-stu-id="16386-107">When you create an event hub, you can enable Capture by clicking the **On** button in the **Create Event Hub** portal blade.</span></span> <span data-ttu-id="16386-108">Vervolgens geeft u een opslagaccount en een container op door in de lijst **Capture-provider** te klikken op **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="16386-108">You then specify a Storage Account and container by clicking **Azure Storage** in the **Capture Provider** box.</span></span> <span data-ttu-id="16386-109">Omdat Event Hubs Capture gebruikmaakt van service-naar-serviceverificatie met opslag, hoeft u geen verbindingsreeks voor opslag op te geven.</span><span class="sxs-lookup"><span data-stu-id="16386-109">Because Event Hubs Capture uses service-to-service authentication with storage, you do not need to specify a storage connection string.</span></span> <span data-ttu-id="16386-110">De objectkiezer selecteert automatisch de resource-URI voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="16386-110">The resource picker selects the resource URI for your storage account automatically.</span></span> <span data-ttu-id="16386-111">Als u Azure Resource Manager gebruikt, moet u deze URI expliciet als een tekenreeks opgeven.</span><span class="sxs-lookup"><span data-stu-id="16386-111">If you use Azure Resource Manager, you must supply this URI explicitly as a string.</span></span>

<span data-ttu-id="16386-112">Het standaardtijdvenster is 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="16386-112">The default time window is 5 minutes.</span></span> <span data-ttu-id="16386-113">De minimale waarde is 1, de maximale 15.</span><span class="sxs-lookup"><span data-stu-id="16386-113">The minimum value is 1, the maximum 15.</span></span> <span data-ttu-id="16386-114">Het venster **Grootte** heeft een bereik van 10-500 MB.</span><span class="sxs-lookup"><span data-stu-id="16386-114">The **Size** window has a range of 10-500 MB.</span></span>

![][1]

## <a name="capture-data-to-an-azure-data-lake-store-account"></a><span data-ttu-id="16386-115">Gegevens vastleggen in een Azure Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="16386-115">Capture data to an Azure Data Lake Store account</span></span>

<span data-ttu-id="16386-116">Als u gegevens wilt vastleggen in Azure Data Lake Store, maakt u een Data Lake Store-account en een Event Hub:</span><span class="sxs-lookup"><span data-stu-id="16386-116">To capture data to Azure Data Lake Store, you create a Data Lake Store account, and an event hub:</span></span>

### <a name="create-an-azure-data-lake-store-account-and-folders"></a><span data-ttu-id="16386-117">Een Azure Data Lake Store-account en -mappen maken</span><span class="sxs-lookup"><span data-stu-id="16386-117">Create an Azure Data Lake Store account and folders</span></span>

1. <span data-ttu-id="16386-118">Maak een Data Lake Store-account volgens de instructies in [Aan de slag met Azure Data Lake Store met Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="16386-118">Create a Data Lake Store account, following the instructions in [Get started with Azure Data Lake Store using the Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span> 
2. <span data-ttu-id="16386-119">Maak een map onder dit account, volgens de instructies in de sectie [Mappen maken in Azure Data Lake Store-account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder).</span><span class="sxs-lookup"><span data-stu-id="16386-119">Create a folder under this account, following the instructions in the [Create folders in Azure Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) section.</span></span>
3. <span data-ttu-id="16386-120">Klik in de blade Data Lake Store-account op **Data Explorer**.</span><span class="sxs-lookup"><span data-stu-id="16386-120">In the Data Lake Store account blade, click **Data Explorer**.</span></span>
4. <span data-ttu-id="16386-121">Klik op **Toegang**.</span><span class="sxs-lookup"><span data-stu-id="16386-121">Click **Access**.</span></span>
5. <span data-ttu-id="16386-122">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="16386-122">Click **Add**.</span></span>
6. <span data-ttu-id="16386-123">Typ **Microsoft.EventHubs** in het vak **Zoeken op naam of e-mailadres** en selecteer vervolgens deze optie.</span><span class="sxs-lookup"><span data-stu-id="16386-123">In the **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span> 
7. <span data-ttu-id="16386-124">Het tabblad **Machtigingen** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="16386-124">The **Permissions** tab appears.</span></span> <span data-ttu-id="16386-125">Stel de machtigingen in zoals weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="16386-125">Set the permissions as shown in the following figure:</span></span>

    ![][6]

8. <span data-ttu-id="16386-126">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="16386-126">Click **OK**.</span></span>
9. <span data-ttu-id="16386-127">Maak nu een map in de hoofdmap door naar de doelmap te bladeren en te klikken op de naam van de map.</span><span class="sxs-lookup"><span data-stu-id="16386-127">Now, create a folder in the root folder by browsing to the target folder and clicking on the folder name.</span></span>
10. <span data-ttu-id="16386-128">Klik op **Toegang**.</span><span class="sxs-lookup"><span data-stu-id="16386-128">Click **Access**.</span></span>
11. <span data-ttu-id="16386-129">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="16386-129">Click **Add**.</span></span>
12. <span data-ttu-id="16386-130">Typ **Microsoft.EventHubs** in het vak **Zoeken op naam of e-mailadres** en selecteer vervolgens deze optie.</span><span class="sxs-lookup"><span data-stu-id="16386-130">In the **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span>
13. <span data-ttu-id="16386-131">Het tabblad **Machtigingen** wordt opnieuw weergegeven.</span><span class="sxs-lookup"><span data-stu-id="16386-131">The **Permissions** tab appears again.</span></span> <span data-ttu-id="16386-132">Stel de machtigingen in zoals weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="16386-132">Set the permissions as shown in the following figure:</span></span>

    ![][5]

### <a name="create-an-event-hub"></a><span data-ttu-id="16386-133">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="16386-133">Create an event hub</span></span>

1. <span data-ttu-id="16386-134">De Event Hub moet deel uitmaken van het Azure-abonnement waarin de Azure Data Lake Store-account is opgenomen dat u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="16386-134">Note that the event hub must be in the same Azure subscription as the Azure Data Lake Store you just created.</span></span> <span data-ttu-id="16386-135">Maken van de event hub, te klikken op de **op** knop onder **vastleggen** in de **Event Hub maken** portalblade.</span><span class="sxs-lookup"><span data-stu-id="16386-135">Create the event hub, clicking the **On** button under **Capture** in the **Create Event Hub** portal blade.</span></span> 
2. <span data-ttu-id="16386-136">In de **Event Hub maken** portalblade, selecteer **Azure Data Lake Store** van de **vastleggen Provider** vak.</span><span class="sxs-lookup"><span data-stu-id="16386-136">In the **Create Event Hub** portal blade, select **Azure Data Lake Store** from the **Capture Provider** box.</span></span>
3. <span data-ttu-id="16386-137">Geef bij **Data Lake Store selecteren** het Data Lake Store-account op dat u eerder hebt gemaakt en voer vervolgens in het veld **Data Lake-pad** het pad in naar de gegevensmap die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="16386-137">In **Select Data Lake Store**, specify the Data Lake Store account you created previously, and in the **Data Lake Path** field, enter the path to the data folder you created.</span></span>

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a><span data-ttu-id="16386-138">Capture toevoegen of configureren op een bestaande Event Hub</span><span class="sxs-lookup"><span data-stu-id="16386-138">Add or configure Capture on an existing event hub</span></span>

<span data-ttu-id="16386-139">U kunt Capture configureren op bestaande Event Hubs in Event Hubs-naamruimten.</span><span class="sxs-lookup"><span data-stu-id="16386-139">You can configure Capture on existing event hubs that are in Event Hubs namespaces.</span></span> <span data-ttu-id="16386-140">Om Capture in te schakelen op een bestaande gebeurtenishub of de Capture-instellingen te wijzigen, klikt u op de naamruimte om de blade **Essentials** te laden en vervolgens klikt u op de gebeurtenishub waarvan u de Capture-instelling wilt inschakelen of wijzigen.</span><span class="sxs-lookup"><span data-stu-id="16386-140">To enable Capture on an existing event hub, or to change your Capture settings, click the namespace to load the **Essentials** blade, then click the event hub for which you want to enable or change the Capture setting.</span></span> <span data-ttu-id="16386-141">Ten slotte op de **eigenschappen** sectie van de blade open en bewerk vervolgens de instellingen voor vastlegging, zoals wordt weergegeven in de volgende afbeeldingen:</span><span class="sxs-lookup"><span data-stu-id="16386-141">Finally, click the **Properties** section of the open blade and then edit the Capture settings, as shown in the following figures:</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="16386-142">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="16386-142">Azure Blob Storage</span></span>

![][2]

### <a name="azure-data-lake-store"></a><span data-ttu-id="16386-143">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="16386-143">Azure Data Lake Store</span></span>

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a><span data-ttu-id="16386-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="16386-144">Next steps</span></span>

<span data-ttu-id="16386-145">U kunt ook Event Hubs Capture configureren met behulp van Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="16386-145">You can also configure Event Hubs Capture using Azure Resource Manager templates.</span></span> <span data-ttu-id="16386-146">Zie voor meer informatie [Capture inschakelen met behulp van een Azure Resource Manager-sjabloon](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span><span class="sxs-lookup"><span data-stu-id="16386-146">For more information, see [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span></span>
