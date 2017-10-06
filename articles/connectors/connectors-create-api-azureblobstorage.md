---
title: aaaAdd hello Azure blob-opslag-Connector in uw logische Apps | Microsoft Docs
description: Aan de slag en hello Azure blob storage-connector in een logische app configureren
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
ms.openlocfilehash: add61287ef1b2228ef9d3f54ce082807bad6858b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-blob-storage-connector-in-a-logic-app"></a><span data-ttu-id="341a9-103">Hello Azure blob storage-connector in een logische app gebruiken</span><span class="sxs-lookup"><span data-stu-id="341a9-103">Use hello Azure blob storage connector in a logic app</span></span>
<span data-ttu-id="341a9-104">Gebruik hello Azure Blob storage-connector tooupload, bijwerken, ophalen en verwijderen van blobs in uw opslagaccount, alle binnen een logische app.</span><span class="sxs-lookup"><span data-stu-id="341a9-104">Use hello Azure Blob storage connector tooupload, update, get, and delete blobs in your storage account, all within a logic app.</span></span>  

<span data-ttu-id="341a9-105">Met Azure blob storage, u:</span><span class="sxs-lookup"><span data-stu-id="341a9-105">With Azure blob storage, you:</span></span>

* <span data-ttu-id="341a9-106">De werkstroom maken door nieuwe projecten uploaden of ophalen van bestanden die onlangs zijn bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="341a9-106">Build your workflow by uploading new projects, or getting files that have been recently updated.</span></span>
* <span data-ttu-id="341a9-107">Acties tooget bestandsmetagegevens gebruiken en verwijderen van een bestand en bestanden kopiëren.</span><span class="sxs-lookup"><span data-stu-id="341a9-107">Use actions tooget file metadata, delete a file, copy files, and more.</span></span> <span data-ttu-id="341a9-108">Bijvoorbeeld wanneer een hulpprogramma is bijgewerkt in een Azure-website (een trigger), vervolgens bijwerken een bestand in blob storage (een actie).</span><span class="sxs-lookup"><span data-stu-id="341a9-108">For example, when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span></span> 

<span data-ttu-id="341a9-109">Dit onderwerp leest u hoe toouse Hallo blob-opslag-connector in een logische app.</span><span class="sxs-lookup"><span data-stu-id="341a9-109">This topic shows you how toouse hello blob storage connector in a logic app.</span></span>

<span data-ttu-id="341a9-110">toolearn meer informatie over Logic Apps, Zie [wat zijn logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="341a9-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="341a9-111">toolearn meer informatie over Logic Apps, Zie [wat zijn logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="341a9-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-blob-storage"></a><span data-ttu-id="341a9-112">Verbinding maken met tooAzure blob-opslag</span><span class="sxs-lookup"><span data-stu-id="341a9-112">Connect tooAzure blob storage</span></span>
<span data-ttu-id="341a9-113">Om uw logische app toegang alle services tot, maakt u eerst een *verbinding* toohello service.</span><span class="sxs-lookup"><span data-stu-id="341a9-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="341a9-114">Een verbinding biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="341a9-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="341a9-115">Bijvoorbeeld: tooconnect tooa storage-account, u eerst maken een blob-opslag *verbinding*.</span><span class="sxs-lookup"><span data-stu-id="341a9-115">For example, tooconnect tooa storage account, you first create a blob storage *connection*.</span></span> <span data-ttu-id="341a9-116">toocreate een verbinding, geef referenties op Hallo u normaal gesproken tooaccess Hallo service u verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="341a9-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="341a9-117">Voer dus Hallo referenties tooyour storage account toocreate Hallo verbinding met Azure storage.</span><span class="sxs-lookup"><span data-stu-id="341a9-117">So with Azure storage, enter hello credentials tooyour storage account toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="341a9-118">Hallo verbinding maken</span><span class="sxs-lookup"><span data-stu-id="341a9-118">Create hello connection</span></span>
> [!INCLUDE [Create a connection tooAzure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a><span data-ttu-id="341a9-119">Een trigger te gebruiken</span><span class="sxs-lookup"><span data-stu-id="341a9-119">Use a trigger</span></span>
<span data-ttu-id="341a9-120">Deze connector heeft geen triggers bestaan niet.</span><span class="sxs-lookup"><span data-stu-id="341a9-120">This connector does not have any triggers.</span></span> <span data-ttu-id="341a9-121">Gebruik andere triggers toostart Hallo logische app, zoals een trigger terugkeerpatroon, een HTTP-Webhook-trigger, triggers beschikbaar met andere connectors en meer.</span><span class="sxs-lookup"><span data-stu-id="341a9-121">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="341a9-122">[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md) bevat een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="341a9-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="341a9-123">Gebruik een actie</span><span class="sxs-lookup"><span data-stu-id="341a9-123">Use an action</span></span>
<span data-ttu-id="341a9-124">Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="341a9-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span>

1. <span data-ttu-id="341a9-125">Selecteer Hallo plus -teken.</span><span class="sxs-lookup"><span data-stu-id="341a9-125">Select hello plus sign.</span></span> <span data-ttu-id="341a9-126">Ziet u verschillende mogelijkheden: **een actie toevoegen**, **een voorwaarde toevoegen**, of een van de Hallo **meer** opties.</span><span class="sxs-lookup"><span data-stu-id="341a9-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. <span data-ttu-id="341a9-127">Kies **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="341a9-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="341a9-128">Typ 'blob' tooget een lijst met alle beschikbare Hallo-acties in Hallo tekstvak.</span><span class="sxs-lookup"><span data-stu-id="341a9-128">In hello text box, type “blob” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. <span data-ttu-id="341a9-129">Kies in ons voorbeeld **AzureBlob - metagegevens van bestand ophalen met behulp van pad**.</span><span class="sxs-lookup"><span data-stu-id="341a9-129">In our example, choose **AzureBlob - Get file metadata using path**.</span></span> <span data-ttu-id="341a9-130">Als er al een verbinding bestaat, selecteert u Hallo **...** (Objectkiezer tonen) knop tooselect een bestand.</span><span class="sxs-lookup"><span data-stu-id="341a9-130">If a connection already exists, then select hello **...** (Show Picker) button tooselect a file.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    <span data-ttu-id="341a9-131">Als u wordt gevraagd om de verbindingsgegevens hello, voert u Hallo details toocreate Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="341a9-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="341a9-132">[Hallo verbinding maken](connectors-create-api-azureblobstorage.md#create-the-connection) in dit onderwerp beschrijft deze eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="341a9-132">[Create hello connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="341a9-133">In dit voorbeeld ophalen we Hallo metagegevens van een bestand.</span><span class="sxs-lookup"><span data-stu-id="341a9-133">In this example, we get hello metadata of a file.</span></span> <span data-ttu-id="341a9-134">toosee Hallo metagegevens, een andere actie die u maakt een nieuw bestand met een andere connector toevoegen.</span><span class="sxs-lookup"><span data-stu-id="341a9-134">toosee hello metadata, add another action that creates a new file using another connector.</span></span> <span data-ttu-id="341a9-135">Bijvoorbeeld, een OneDrive-actie die u een nieuw bestand maakt 'test' op basis van metagegevens Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="341a9-135">For example, add a OneDrive action that creates a new "test" file based on hello metadata.</span></span> 


5. <span data-ttu-id="341a9-136">**Sla** uw wijzigingen (linksboven Hallo werkbalk).</span><span class="sxs-lookup"><span data-stu-id="341a9-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="341a9-137">Uw logische app wordt opgeslagen en automatisch kan worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="341a9-137">Your logic app is saved and may be automatically enabled.</span></span>

> [!TIP]
> <span data-ttu-id="341a9-138">[Opslagverkenner](http://storageexplorer.com/) is een uitstekend hulpprogramma meerdere opslagaccounts te beheren.</span><span class="sxs-lookup"><span data-stu-id="341a9-138">[Storage Explorer](http://storageexplorer.com/) is a great tool too manage multiple storage accounts.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="341a9-139">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="341a9-139">Connector-specific details</span></span>

<span data-ttu-id="341a9-140">Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/azureblobconnector/).</span><span class="sxs-lookup"><span data-stu-id="341a9-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/azureblobconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="341a9-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="341a9-141">Next steps</span></span>
<span data-ttu-id="341a9-142">[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="341a9-142">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="341a9-143">Verken Hallo van andere beschikbare connectors in Logic Apps op onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="341a9-143">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

