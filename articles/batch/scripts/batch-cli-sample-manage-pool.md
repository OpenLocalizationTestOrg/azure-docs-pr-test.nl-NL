---
title: aaaAzure voorbeeldscript CLI - groepen beheren in een Batch | Microsoft Docs
description: Azure CLI-voorbeeldscript - opslaggroepen in Batch beheren
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
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="3c193-103">Het beheren van Azure Batch-pools met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3c193-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="3c193-104">Deze script toont een aantal beschikbare in hello Azure CLI toocreate Hallo hulpprogramma's en groepen beheren van rekenknooppunten in hello Azure Batch-service.</span><span class="sxs-lookup"><span data-stu-id="3c193-104">These script demonstrates some of hello tools available in hello Azure CLI toocreate and manage pools of compute nodes in hello Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="3c193-105">Hallo-opdrachten in dit voorbeeld maken Azure virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="3c193-105">hello commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="3c193-106">VM's worden uitgevoerd, wordt de kosten tooyour account doorlopen.</span><span class="sxs-lookup"><span data-stu-id="3c193-106">Running VMs will accrue charges tooyour account.</span></span> <span data-ttu-id="3c193-107">toominimize deze kosten verwijderen Hallo VM's wanneer u klaar bent met actieve Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="3c193-107">toominimize these charges, delete hello VMs once you're done running hello sample.</span></span> <span data-ttu-id="3c193-108">Zie [pools opschonen](#clean-up-pools).</span><span class="sxs-lookup"><span data-stu-id="3c193-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="3c193-109">Batch-pools kunnen worden geconfigureerd op twee manieren aan een Cloud Services-configuratie (alleen Windows) of de configuratie van een virtuele Machine (Windows en Linux).</span><span class="sxs-lookup"><span data-stu-id="3c193-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="3c193-110">Hallo-voorbeeldscripts hieronder laten zien hoe toocreate voor groepen met beide configuraties.</span><span class="sxs-lookup"><span data-stu-id="3c193-110">hello sample scripts below show how toocreate pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c193-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3c193-111">Prerequisites</span></span>

- <span data-ttu-id="3c193-112">Installeer Azure CLI met behulp van de instructies in Hallo HALLO hallo [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli), als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="3c193-112">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="3c193-113">Maak een Batch-account als u er nog geen hebt.</span><span class="sxs-lookup"><span data-stu-id="3c193-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="3c193-114">Zie [een Batch-account maken met Azure CLI Hallo](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) voor een voorbeeld van een script dat een account maakt.</span><span class="sxs-lookup"><span data-stu-id="3c193-114">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="3c193-115">Een toepassing toorun uit een begintaak configureren als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="3c193-115">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="3c193-116">Zie [toe te voegen toepassingen tooAzure Batch met Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) voor een voorbeeld van een script dat een toepassing maakt en uploadt een tooAzure application-pakket.</span><span class="sxs-lookup"><span data-stu-id="3c193-116">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="3c193-117">Groep met voorbeeldscript voor cloud service-configuratie</span><span class="sxs-lookup"><span data-stu-id="3c193-117">Pool with cloud service configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="3c193-118">Groep met de virtuele machine configuratie voorbeeldscript</span><span class="sxs-lookup"><span data-stu-id="3c193-118">Pool with virtual machine configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a><span data-ttu-id="3c193-119">Opschonen van groepen</span><span class="sxs-lookup"><span data-stu-id="3c193-119">Clean up pools</span></span>

<span data-ttu-id="3c193-120">Na het uitvoeren van Hallo hierboven voorbeeldscript uitvoeren Hallo opdracht toodelete Hallo pools te volgen.</span><span class="sxs-lookup"><span data-stu-id="3c193-120">After you run hello above sample script, run hello following command toodelete hello pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="3c193-121">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="3c193-121">Script explanation</span></span>

<span data-ttu-id="3c193-122">Dit script gebruikt Hallo opdrachten toocreate te volgen en manipuleren van Batch-pools.</span><span class="sxs-lookup"><span data-stu-id="3c193-122">This script uses hello following commands toocreate and manipulate Batch pools.</span></span>
<span data-ttu-id="3c193-123">Elke opdracht in Hallo tabel koppelingen toocommand-specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="3c193-123">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="3c193-124">Opdracht</span><span class="sxs-lookup"><span data-stu-id="3c193-124">Command</span></span> | <span data-ttu-id="3c193-125">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="3c193-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3c193-126">aanmeldingsnaam AZ batch-account</span><span class="sxs-lookup"><span data-stu-id="3c193-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="3c193-127">Verificatie uitvoeren tegen een Batch-account.</span><span class="sxs-lookup"><span data-stu-id="3c193-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="3c193-128">overzicht van de AZ batch-toepassing</span><span class="sxs-lookup"><span data-stu-id="3c193-128">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="3c193-129">Lijst van beschikbare toepassingen in de Batch-account Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="3c193-129">List hello available applications in hello Batch account.</span></span>  |
| [<span data-ttu-id="3c193-130">AZ batch-pool maken</span><span class="sxs-lookup"><span data-stu-id="3c193-130">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="3c193-131">Een pool van virtuele machines maken.</span><span class="sxs-lookup"><span data-stu-id="3c193-131">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="3c193-132">AZ batch pool instellen</span><span class="sxs-lookup"><span data-stu-id="3c193-132">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="3c193-133">Eigenschappen van een groep bijwerken.</span><span class="sxs-lookup"><span data-stu-id="3c193-133">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="3c193-134">lijst van AZ batch pool knooppunt-agent-SKU 's</span><span class="sxs-lookup"><span data-stu-id="3c193-134">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="3c193-135">Lijst met beschikbare knooppunt agent SKU's en informatie over de afbeelding.</span><span class="sxs-lookup"><span data-stu-id="3c193-135">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="3c193-136">AZ batch-pool formaat wijzigen</span><span class="sxs-lookup"><span data-stu-id="3c193-136">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="3c193-137">Formaat Hallo aantal virtuele machines in Hallo opgegeven groep van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="3c193-137">Resize hello number of running VMs in hello specified pool.</span></span>  |
| [<span data-ttu-id="3c193-138">AZ batch pool weergeven</span><span class="sxs-lookup"><span data-stu-id="3c193-138">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="3c193-139">Hallo-eigenschappen van een groep weergeven.</span><span class="sxs-lookup"><span data-stu-id="3c193-139">Display hello properties of a pool.</span></span>  |
| [<span data-ttu-id="3c193-140">AZ batch pool verwijderen</span><span class="sxs-lookup"><span data-stu-id="3c193-140">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="3c193-141">Hallo opgegeven verwijderen van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="3c193-141">Delete hello specified pool.</span></span>  |
| [<span data-ttu-id="3c193-142">AZ batch-pool automatisch schalen inschakelen</span><span class="sxs-lookup"><span data-stu-id="3c193-142">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="3c193-143">Automatische schaling inschakelen op een pool en toepassen van een formule.</span><span class="sxs-lookup"><span data-stu-id="3c193-143">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="3c193-144">AZ batch-pool automatisch schalen uitschakelen</span><span class="sxs-lookup"><span data-stu-id="3c193-144">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="3c193-145">Schakel automatisch schalen op een groep.</span><span class="sxs-lookup"><span data-stu-id="3c193-145">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="3c193-146">lijst met knooppunten AZ-batch</span><span class="sxs-lookup"><span data-stu-id="3c193-146">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="3c193-147">De lijst alle Hallo rekenknooppunt in Hallo opgegeven groep van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="3c193-147">List all hello compute node in hello specified pool.</span></span>  |
| [<span data-ttu-id="3c193-148">AZ batch knooppunt opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="3c193-148">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="3c193-149">Hallo opgegeven computerknooppunt opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="3c193-149">Reboot hello specified compute node.</span></span>  |
| [<span data-ttu-id="3c193-150">AZ batch knooppunt verwijderen</span><span class="sxs-lookup"><span data-stu-id="3c193-150">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="3c193-151">Delete Hallo vermeld knooppunten uit Hallo opgegeven groep van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="3c193-151">Delete hello listed nodes from hello specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="3c193-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3c193-152">Next steps</span></span>

<span data-ttu-id="3c193-153">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3c193-153">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3c193-154">Aanvullende Batch CLI scriptvoorbeelden kunnen u vinden in Hallo [documentatie van Azure Batch CLI](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3c193-154">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

