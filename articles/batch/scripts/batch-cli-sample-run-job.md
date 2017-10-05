---
title: Azure CLI-voorbeeldscript - een taak wordt uitgevoerd met Batch | Microsoft Docs
description: Azure CLI-voorbeeldscript - een taak met Batch wordt uitgevoerd
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 5fe1e3595d9459e60b2fd54d6f17f6822731f453
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="e0266-103">Taken uitgevoerd op Azure Batch met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e0266-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="e0266-104">Dit script maakt een Batch-job en voegt u een reeks taken toe aan de taak.</span><span class="sxs-lookup"><span data-stu-id="e0266-104">This script creates a Batch job and adds a series of tasks to the job.</span></span> <span data-ttu-id="e0266-105">U ziet ook het controleren van een taak en de bijbehorende taken.</span><span class="sxs-lookup"><span data-stu-id="e0266-105">It also demonstrates how to monitor a job and its tasks.</span></span> <span data-ttu-id="e0266-106">Ten slotte het laat zien hoe de Batch-service efficiënt voor informatie over de taken van de taak query uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e0266-106">Finally, it shows how to query the Batch service efficiently for information about the job's tasks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0266-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e0266-107">Prerequisites</span></span>

- <span data-ttu-id="e0266-108">Installeer de Azure CLI met behulp van de instructies in de [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli), als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="e0266-108">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="e0266-109">Maak een Batch-account als u er nog geen hebt.</span><span class="sxs-lookup"><span data-stu-id="e0266-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="e0266-110">Zie [een Batch-account maken met de Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) voor een voorbeeld van een script dat een account maakt.</span><span class="sxs-lookup"><span data-stu-id="e0266-110">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="e0266-111">Configureer een toepassing voor uitvoering van een begintaak als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="e0266-111">Configure an application to run from a start task if you haven't yet done so.</span></span> <span data-ttu-id="e0266-112">Zie [toepassingen toevoegen aan Azure Batch met Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) voor een voorbeeld van een script dat een toepassing maakt en toepassingspakketten uploadt naar Azure.</span><span class="sxs-lookup"><span data-stu-id="e0266-112">See [Adding applications to Azure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package to Azure.</span></span>
- <span data-ttu-id="e0266-113">Configureer een pool op waarop de taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e0266-113">Configure a pool on which the job will run.</span></span> <span data-ttu-id="e0266-114">Zie [het beheer van Azure Batch-pools met Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) voor een voorbeeld van een script dat een pool met een Cloud Service-configuratie of de configuratie van een virtuele Machine maakt.</span><span class="sxs-lookup"><span data-stu-id="e0266-114">See [Managing Azure Batch pools with Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) for a sample script that creates a pool with either a Cloud Service Configuration or a Virtual Machine Configuration.</span></span>

## <a name="sample-script"></a><span data-ttu-id="e0266-115">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="e0266-115">Sample script</span></span>

<span data-ttu-id="e0266-116">[!code-azurecli[belangrijkste](../../../cli_scripts/batch/run-job/run-job.sh "taak uitvoeren")]</span><span class="sxs-lookup"><span data-stu-id="e0266-116">[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]</span></span>

## <a name="clean-up-job"></a><span data-ttu-id="e0266-117">Taak opschonen</span><span class="sxs-lookup"><span data-stu-id="e0266-117">Clean up job</span></span>

<span data-ttu-id="e0266-118">Nadat u het bovenstaande voorbeeld van een script uitgevoerd, voer de volgende opdracht om de taak en alle bijbehorende taken te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e0266-118">After you run the above sample script, run the following command to remove the job and all of its tasks.</span></span> <span data-ttu-id="e0266-119">Houd er rekening mee dat de groep moet afzonderlijk worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="e0266-119">Note that the pool will need to be deleted separately.</span></span> <span data-ttu-id="e0266-120">Zie [het beheer van Azure Batch-pools met Azure CLI](./batch-cli-sample-manage-pool.md) voor meer informatie over het maken en verwijderen van groepen.</span><span class="sxs-lookup"><span data-stu-id="e0266-120">See [Managing Azure Batch pools with Azure CLI](./batch-cli-sample-manage-pool.md) for more information on creating and deleting pools.</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="e0266-121">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="e0266-121">Script explanation</span></span>

<span data-ttu-id="e0266-122">Dit script maakt gebruik van de volgende opdrachten om een Batch-job en taken te maken.</span><span class="sxs-lookup"><span data-stu-id="e0266-122">This script uses the following commands to create a Batch job and tasks.</span></span> <span data-ttu-id="e0266-123">Elke opdracht in de tabel is gekoppeld aan de opdracht specifieke documentatie bij.</span><span class="sxs-lookup"><span data-stu-id="e0266-123">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="e0266-124">Opdracht</span><span class="sxs-lookup"><span data-stu-id="e0266-124">Command</span></span> | <span data-ttu-id="e0266-125">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="e0266-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e0266-126">aanmeldingsnaam AZ batch-account</span><span class="sxs-lookup"><span data-stu-id="e0266-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="e0266-127">Verificatie uitvoeren tegen een Batch-account.</span><span class="sxs-lookup"><span data-stu-id="e0266-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="e0266-128">AZ batch-job maken</span><span class="sxs-lookup"><span data-stu-id="e0266-128">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="e0266-129">Maakt een Batch-job.</span><span class="sxs-lookup"><span data-stu-id="e0266-129">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="e0266-130">AZ batch taak instellen</span><span class="sxs-lookup"><span data-stu-id="e0266-130">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="e0266-131">Eigenschappen van een Batch-job-updates.</span><span class="sxs-lookup"><span data-stu-id="e0266-131">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="e0266-132">AZ batch-taak weergeven</span><span class="sxs-lookup"><span data-stu-id="e0266-132">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="e0266-133">Details van een opgegeven Batch-job opgehaald.</span><span class="sxs-lookup"><span data-stu-id="e0266-133">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="e0266-134">AZ batch-taak maken</span><span class="sxs-lookup"><span data-stu-id="e0266-134">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="e0266-135">Hiermee voegt u een taak toe aan de opgegeven Batch-taak.</span><span class="sxs-lookup"><span data-stu-id="e0266-135">Adds a task to the specified Batch job.</span></span>  |
| [<span data-ttu-id="e0266-136">AZ batch-taak weergeven</span><span class="sxs-lookup"><span data-stu-id="e0266-136">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="e0266-137">Haalt de details van een taak van de opgegeven Batch-taak.</span><span class="sxs-lookup"><span data-stu-id="e0266-137">Retrieves the details of a task from the specified Batch job.</span></span>  |
| [<span data-ttu-id="e0266-138">lijst van AZ batch-taak</span><span class="sxs-lookup"><span data-stu-id="e0266-138">az batch task list</span></span>](https://docs.microsoft.com/cli/azure/batch/task#list) | <span data-ttu-id="e0266-139">Geeft een lijst van de taken die zijn gekoppeld aan de opgegeven taak.</span><span class="sxs-lookup"><span data-stu-id="e0266-139">Lists the tasks associated with the specified job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="e0266-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e0266-140">Next steps</span></span>

<span data-ttu-id="e0266-141">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e0266-141">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e0266-142">Aanvullende Batch CLI scriptvoorbeelden vindt u in de [documentatie van Azure Batch CLI](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e0266-142">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
