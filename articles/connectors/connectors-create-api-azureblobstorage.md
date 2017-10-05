---
title: Azure blob storage Connector in uw logische Apps toevoegen | Microsoft Docs
description: Aan de slag en de Azure blob storage-connector in een logische app configureren
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/02/2017
ms.author: mandia; ladocs
ms.openlocfilehash: bc7908868828bd1628633cf9e57f8c44f8000827
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-blob-storage-connector-in-a-logic-app"></a><span data-ttu-id="0530b-103">Gebruik de Azure blob storage-connector in een logische app</span><span class="sxs-lookup"><span data-stu-id="0530b-103">Use the Azure blob storage connector in a logic app</span></span>
<span data-ttu-id="0530b-104">De Azure Blob storage-connector gebruiken om te uploaden, bijwerken, ophalen en verwijderen van blobs in uw opslagaccount, alle binnen een logische app.</span><span class="sxs-lookup"><span data-stu-id="0530b-104">Use the Azure Blob storage connector to upload, update, get, and delete blobs in your storage account, all within a logic app.</span></span>  

<span data-ttu-id="0530b-105">Met Azure blob storage, u:</span><span class="sxs-lookup"><span data-stu-id="0530b-105">With Azure blob storage, you:</span></span>

* <span data-ttu-id="0530b-106">De werkstroom maken door nieuwe projecten uploaden of ophalen van bestanden die onlangs zijn bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="0530b-106">Build your workflow by uploading new projects, or getting files that have been recently updated.</span></span>
* <span data-ttu-id="0530b-107">Acties bestandsmetagegevens ophalen, verwijderen van een bestand en bestanden kopiëren gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0530b-107">Use actions to get file metadata, delete a file, copy files, and more.</span></span> <span data-ttu-id="0530b-108">Bijvoorbeeld wanneer een hulpprogramma is bijgewerkt in een Azure-website (een trigger), vervolgens bijwerken een bestand in blob storage (een actie).</span><span class="sxs-lookup"><span data-stu-id="0530b-108">For example, when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span></span> 

<span data-ttu-id="0530b-109">Dit onderwerp leest u het gebruik van de blob-opslag-connector in een logische app.</span><span class="sxs-lookup"><span data-stu-id="0530b-109">This topic shows you how to use the blob storage connector in a logic app.</span></span>

<span data-ttu-id="0530b-110">Zie voor meer informatie over Logic Apps, [wat zijn logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0530b-110">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="0530b-111">Zie voor meer informatie over Logic Apps, [wat zijn logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0530b-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-azure-blob-storage"></a><span data-ttu-id="0530b-112">Verbinding maken met Azure blob-opslag</span><span class="sxs-lookup"><span data-stu-id="0530b-112">Connect to Azure blob storage</span></span>
<span data-ttu-id="0530b-113">Om uw logische app toegang alle services tot, maakt u eerst een *verbinding* naar de service.</span><span class="sxs-lookup"><span data-stu-id="0530b-113">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="0530b-114">Een verbinding biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="0530b-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="0530b-115">Bijvoorbeeld, als u wilt verbinding maken met een opslagaccount, u eerst maken een blob-opslag *verbinding*.</span><span class="sxs-lookup"><span data-stu-id="0530b-115">For example, to connect to a storage account, you first create a blob storage *connection*.</span></span> <span data-ttu-id="0530b-116">Voer de referenties die u gebruikt om toegang tot de service die u verbinding met maakt een verbinding wilt maken.</span><span class="sxs-lookup"><span data-stu-id="0530b-116">To create a connection, enter the credentials you normally use to access the service you are connecting to.</span></span> <span data-ttu-id="0530b-117">Voer dus de referenties naar uw storage-account om de verbinding te maken met Azure storage.</span><span class="sxs-lookup"><span data-stu-id="0530b-117">So with Azure storage, enter the credentials to your storage account to create the connection.</span></span> 

#### <a name="create-the-connection"></a><span data-ttu-id="0530b-118">De verbinding maken</span><span class="sxs-lookup"><span data-stu-id="0530b-118">Create the connection</span></span>
> [!INCLUDE [Create a connection to Azure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a><span data-ttu-id="0530b-119">Een trigger te gebruiken</span><span class="sxs-lookup"><span data-stu-id="0530b-119">Use a trigger</span></span>
<span data-ttu-id="0530b-120">Deze connector heeft geen triggers bestaan niet.</span><span class="sxs-lookup"><span data-stu-id="0530b-120">This connector does not have any triggers.</span></span> <span data-ttu-id="0530b-121">Met andere triggers kunt starten van de logische app, zoals een trigger terugkeerpatroon, een HTTP-Webhook-trigger, triggers beschikbaar met andere connectors en meer.</span><span class="sxs-lookup"><span data-stu-id="0530b-121">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="0530b-122">[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md) bevat een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="0530b-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="0530b-123">Gebruik een actie</span><span class="sxs-lookup"><span data-stu-id="0530b-123">Use an action</span></span>
<span data-ttu-id="0530b-124">Een actie is een bewerking uitgevoerd door de werkstroom die is gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="0530b-124">An action is an operation carried out by the workflow defined in a logic app.</span></span>

1. <span data-ttu-id="0530b-125">Selecteer het plusteken.</span><span class="sxs-lookup"><span data-stu-id="0530b-125">Select the plus sign.</span></span> <span data-ttu-id="0530b-126">Ziet u verschillende mogelijkheden: **een actie toevoegen**, **een voorwaarde toevoegen**, of een van de **meer** opties.</span><span class="sxs-lookup"><span data-stu-id="0530b-126">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. <span data-ttu-id="0530b-127">Kies **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="0530b-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="0530b-128">Typ 'blob' om een lijst met alle beschikbare acties in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="0530b-128">In the text box, type “blob” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. <span data-ttu-id="0530b-129">Kies in ons voorbeeld **AzureBlob - metagegevens van bestand ophalen met behulp van pad**.</span><span class="sxs-lookup"><span data-stu-id="0530b-129">In our example, choose **AzureBlob - Get file metadata using path**.</span></span> <span data-ttu-id="0530b-130">Als er al een verbinding bestaat, selecteert u de **...** Knop (objectkiezer weergeven) om een bestand te selecteren.</span><span class="sxs-lookup"><span data-stu-id="0530b-130">If a connection already exists, then select the **...** (Show Picker) button to select a file.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    <span data-ttu-id="0530b-131">Als u wordt gevraagd om de verbindingsinformatie, voert u de details om de verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="0530b-131">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="0530b-132">[De verbinding](connectors-create-api-azureblobstorage.md#create-the-connection) in dit onderwerp beschrijft deze eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="0530b-132">[Create the connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="0530b-133">In dit voorbeeld wordt de metagegevens van een bestand ophalen.</span><span class="sxs-lookup"><span data-stu-id="0530b-133">In this example, we get the metadata of a file.</span></span> <span data-ttu-id="0530b-134">Overzicht van de metagegevens, een andere actie die u maakt een nieuw bestand met een andere connector toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0530b-134">To see the metadata, add another action that creates a new file using another connector.</span></span> <span data-ttu-id="0530b-135">Bijvoorbeeld, een OneDrive-actie die u een nieuw bestand maakt 'test' op basis van de metagegevens toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0530b-135">For example, add a OneDrive action that creates a new "test" file based on the metadata.</span></span> 


5. <span data-ttu-id="0530b-136">**Sla** uw wijzigingen (linkerbovenhoek van de werkbalk).</span><span class="sxs-lookup"><span data-stu-id="0530b-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="0530b-137">Uw logische app wordt opgeslagen en automatisch kan worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="0530b-137">Your logic app is saved and may be automatically enabled.</span></span>

> [!TIP]
> <span data-ttu-id="0530b-138">[Opslagverkenner](http://storageexplorer.com/) is een uitstekend hulpprogramma voor het beheren van meerdere opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="0530b-138">[Storage Explorer](http://storageexplorer.com/) is a great tool to  manage multiple storage accounts.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="0530b-139">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="0530b-139">Connector-specific details</span></span>

<span data-ttu-id="0530b-140">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/azureblobconnector/).</span><span class="sxs-lookup"><span data-stu-id="0530b-140">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/azureblobconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0530b-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0530b-141">Next steps</span></span>
<span data-ttu-id="0530b-142">[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0530b-142">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="0530b-143">Bekijk de beschikbare connectors in Logic Apps op onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="0530b-143">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

