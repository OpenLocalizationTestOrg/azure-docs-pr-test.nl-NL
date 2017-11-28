---
title: CLI - voorbeeldscript met een taak met Batch aaaAzure | Microsoft Docs
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
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="8734f-103">Taken uitgevoerd op Azure Batch met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8734f-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="8734f-104">Dit script maakt een Batch-job en een reeks taken toohello taak toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="8734f-104">This script creates a Batch job and adds a series of tasks toohello job.</span></span> <span data-ttu-id="8734f-105">U ziet ook hoe toomonitor een taak en de bijbehorende taken.</span><span class="sxs-lookup"><span data-stu-id="8734f-105">It also demonstrates how toomonitor a job and its tasks.</span></span> <span data-ttu-id="8734f-106">Ten slotte ziet hoe tooquery Hallo efficiënt voor informatie over Hallo projecttaken Batch-service.</span><span class="sxs-lookup"><span data-stu-id="8734f-106">Finally, it shows how tooquery hello Batch service efficiently for information about hello job's tasks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8734f-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8734f-107">Prerequisites</span></span>

- <span data-ttu-id="8734f-108">Installeer Azure CLI met behulp van de instructies in Hallo HALLO hallo [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli), als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="8734f-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="8734f-109">Maak een Batch-account als u er nog geen hebt.</span><span class="sxs-lookup"><span data-stu-id="8734f-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="8734f-110">Zie [een Batch-account maken met Azure CLI Hallo](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) voor een voorbeeld van een script dat een account maakt.</span><span class="sxs-lookup"><span data-stu-id="8734f-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="8734f-111">Een toepassing toorun uit een begintaak configureren als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="8734f-111">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="8734f-112">Zie [toe te voegen toepassingen tooAzure Batch met Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) voor een voorbeeld van een script dat een toepassing maakt en uploadt een tooAzure application-pakket.</span><span class="sxs-lookup"><span data-stu-id="8734f-112">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>
- <span data-ttu-id="8734f-113">Configureer een pool op welke Hallo taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8734f-113">Configure a pool on which hello job will run.</span></span> <span data-ttu-id="8734f-114">Zie [het beheer van Azure Batch-pools met Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) voor een voorbeeld van een script dat een pool met een Cloud Service-configuratie of de configuratie van een virtuele Machine maakt.</span><span class="sxs-lookup"><span data-stu-id="8734f-114">See [Managing Azure Batch pools with Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) for a sample script that creates a pool with either a Cloud Service Configuration or a Virtual Machine Configuration.</span></span>

## <a name="sample-script"></a><span data-ttu-id="8734f-115">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="8734f-115">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a><span data-ttu-id="8734f-116">Taak opschonen</span><span class="sxs-lookup"><span data-stu-id="8734f-116">Clean up job</span></span>

<span data-ttu-id="8734f-117">Na het uitvoeren van Hallo hierboven voorbeeldscript uitvoeren Hallo opdracht tooremove na de taak en alle bijbehorende taken.</span><span class="sxs-lookup"><span data-stu-id="8734f-117">After you run hello above sample script, run hello following command tooremove the job and all of its tasks.</span></span> <span data-ttu-id="8734f-118">Houd er rekening mee dat Hallo van toepassingen wordt toobe afzonderlijk worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8734f-118">Note that hello pool will need toobe deleted separately.</span></span> <span data-ttu-id="8734f-119">Zie [het beheer van Azure Batch-pools met Azure CLI](./batch-cli-sample-manage-pool.md) voor meer informatie over het maken en verwijderen van groepen.</span><span class="sxs-lookup"><span data-stu-id="8734f-119">See [Managing Azure Batch pools with Azure CLI](./batch-cli-sample-manage-pool.md) for more information on creating and deleting pools.</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="8734f-120">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="8734f-120">Script explanation</span></span>

<span data-ttu-id="8734f-121">Dit script gebruikt Hallo opdrachten toocreate na een Batch-job en taken.</span><span class="sxs-lookup"><span data-stu-id="8734f-121">This script uses hello following commands toocreate a Batch job and tasks.</span></span> <span data-ttu-id="8734f-122">Elke opdracht in Hallo tabel koppelingen toocommand-specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="8734f-122">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="8734f-123">Opdracht</span><span class="sxs-lookup"><span data-stu-id="8734f-123">Command</span></span> | <span data-ttu-id="8734f-124">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="8734f-124">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8734f-125">aanmeldingsnaam AZ batch-account</span><span class="sxs-lookup"><span data-stu-id="8734f-125">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="8734f-126">Verificatie uitvoeren tegen een Batch-account.</span><span class="sxs-lookup"><span data-stu-id="8734f-126">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="8734f-127">AZ batch-job maken</span><span class="sxs-lookup"><span data-stu-id="8734f-127">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="8734f-128">Maakt een Batch-job.</span><span class="sxs-lookup"><span data-stu-id="8734f-128">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="8734f-129">AZ batch taak instellen</span><span class="sxs-lookup"><span data-stu-id="8734f-129">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="8734f-130">Eigenschappen van een Batch-job-updates.</span><span class="sxs-lookup"><span data-stu-id="8734f-130">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="8734f-131">AZ batch-taak weergeven</span><span class="sxs-lookup"><span data-stu-id="8734f-131">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="8734f-132">Details van een opgegeven Batch-job opgehaald.</span><span class="sxs-lookup"><span data-stu-id="8734f-132">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="8734f-133">AZ batch-taak maken</span><span class="sxs-lookup"><span data-stu-id="8734f-133">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="8734f-134">Voegt dat een taak toohello opgegeven Batch-job.</span><span class="sxs-lookup"><span data-stu-id="8734f-134">Adds a task toohello specified Batch job.</span></span>  |
| [<span data-ttu-id="8734f-135">AZ batch-taak weergeven</span><span class="sxs-lookup"><span data-stu-id="8734f-135">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="8734f-136">Haalt Hallo details van een taak van Hallo opgegeven Batch-job.</span><span class="sxs-lookup"><span data-stu-id="8734f-136">Retrieves hello details of a task from hello specified Batch job.</span></span>  |
| [<span data-ttu-id="8734f-137">lijst van AZ batch-taak</span><span class="sxs-lookup"><span data-stu-id="8734f-137">az batch task list</span></span>](https://docs.microsoft.com/cli/azure/batch/task#list) | <span data-ttu-id="8734f-138">Geeft een lijst die zijn gekoppeld aan de opgegeven taak Hallo Hallo-taken.</span><span class="sxs-lookup"><span data-stu-id="8734f-138">Lists hello tasks associated with hello specified job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="8734f-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8734f-139">Next steps</span></span>

<span data-ttu-id="8734f-140">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8734f-140">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8734f-141">Aanvullende Batch CLI scriptvoorbeelden kunnen u vinden in Hallo [documentatie van Azure Batch CLI](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8734f-141">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
