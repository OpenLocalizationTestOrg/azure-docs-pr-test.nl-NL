---
title: Azure CLI - voorbeeldscript voor het beheren van opslaggroepen in Batch | Microsoft Docs
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
ms.openlocfilehash: 2556b02459886390b803407c5cb828687229a44e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="fe973-103">Het beheren van Azure Batch-pools met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fe973-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="fe973-104">Deze script laat zien van de hulpprogramma's die beschikbaar zijn in de Azure CLI maken en beheren van pools van rekenknooppunten in de Azure Batch-service.</span><span class="sxs-lookup"><span data-stu-id="fe973-104">These script demonstrates some of the tools available in the Azure CLI to create and manage pools of compute nodes in the Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="fe973-105">De opdrachten in dit voorbeeld maken Azure virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="fe973-105">The commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="fe973-106">VM's worden uitgevoerd, wordt de kosten voor je account doorlopen.</span><span class="sxs-lookup"><span data-stu-id="fe973-106">Running VMs will accrue charges to your account.</span></span> <span data-ttu-id="fe973-107">Verwijder de virtuele machines om te beperken deze kosten, zodra u klaar bent met het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="fe973-107">To minimize these charges, delete the VMs once you're done running the sample.</span></span> <span data-ttu-id="fe973-108">Zie [pools opschonen](#clean-up-pools).</span><span class="sxs-lookup"><span data-stu-id="fe973-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="fe973-109">Batch-pools kunnen worden geconfigureerd op twee manieren aan een Cloud Services-configuratie (alleen Windows) of de configuratie van een virtuele Machine (Windows en Linux).</span><span class="sxs-lookup"><span data-stu-id="fe973-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="fe973-110">De onderstaande voorbeeldscripts laten zien hoe groepen met beide configuraties te maken.</span><span class="sxs-lookup"><span data-stu-id="fe973-110">The sample scripts below show how to create pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe973-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fe973-111">Prerequisites</span></span>

- <span data-ttu-id="fe973-112">Installeer de Azure CLI met behulp van de instructies in de [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli), als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="fe973-112">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="fe973-113">Maak een Batch-account als u er nog geen hebt.</span><span class="sxs-lookup"><span data-stu-id="fe973-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="fe973-114">Zie [een Batch-account maken met de Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) voor een voorbeeld van een script dat een account maakt.</span><span class="sxs-lookup"><span data-stu-id="fe973-114">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="fe973-115">Configureer een toepassing voor uitvoering van een begintaak als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="fe973-115">Configure an application to run from a start task if you haven't yet done so.</span></span> <span data-ttu-id="fe973-116">Zie [toepassingen toevoegen aan Azure Batch met Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) voor een voorbeeld van een script dat een toepassing maakt en toepassingspakketten uploadt naar Azure.</span><span class="sxs-lookup"><span data-stu-id="fe973-116">See [Adding applications to Azure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package to Azure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="fe973-117">Groep met voorbeeldscript voor cloud service-configuratie</span><span class="sxs-lookup"><span data-stu-id="fe973-117">Pool with cloud service configuration sample script</span></span>

<span data-ttu-id="fe973-118">[!code-azurecli[belangrijkste](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Cloud Services-groepen beheren")]</span><span class="sxs-lookup"><span data-stu-id="fe973-118">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]</span></span>

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="fe973-119">Groep met de virtuele machine configuratie voorbeeldscript</span><span class="sxs-lookup"><span data-stu-id="fe973-119">Pool with virtual machine configuration sample script</span></span>

<span data-ttu-id="fe973-120">[!code-azurecli[belangrijkste](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Virtual Machine-groepen beheren")]</span><span class="sxs-lookup"><span data-stu-id="fe973-120">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]</span></span>

## <a name="clean-up-pools"></a><span data-ttu-id="fe973-121">Opschonen van groepen</span><span class="sxs-lookup"><span data-stu-id="fe973-121">Clean up pools</span></span>

<span data-ttu-id="fe973-122">Voer de volgende opdracht om de groepen verwijderen na het uitvoeren van script in het bovenstaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="fe973-122">After you run the above sample script, run the following command to delete the pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="fe973-123">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="fe973-123">Script explanation</span></span>

<span data-ttu-id="fe973-124">Dit script maakt gebruik van de volgende opdrachten om te maken en manipuleren van Batch-pools.</span><span class="sxs-lookup"><span data-stu-id="fe973-124">This script uses the following commands to create and manipulate Batch pools.</span></span>
<span data-ttu-id="fe973-125">Elke opdracht in de tabel is gekoppeld aan de opdracht specifieke documentatie bij.</span><span class="sxs-lookup"><span data-stu-id="fe973-125">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="fe973-126">Opdracht</span><span class="sxs-lookup"><span data-stu-id="fe973-126">Command</span></span> | <span data-ttu-id="fe973-127">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="fe973-127">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fe973-128">aanmeldingsnaam AZ batch-account</span><span class="sxs-lookup"><span data-stu-id="fe973-128">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="fe973-129">Verificatie uitvoeren tegen een Batch-account.</span><span class="sxs-lookup"><span data-stu-id="fe973-129">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="fe973-130">overzicht van de AZ batch-toepassing</span><span class="sxs-lookup"><span data-stu-id="fe973-130">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="fe973-131">Lijst van de beschikbare toepassingen in de Batch-account.</span><span class="sxs-lookup"><span data-stu-id="fe973-131">List the available applications in the Batch account.</span></span>  |
| [<span data-ttu-id="fe973-132">AZ batch-pool maken</span><span class="sxs-lookup"><span data-stu-id="fe973-132">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="fe973-133">Een pool van virtuele machines maken.</span><span class="sxs-lookup"><span data-stu-id="fe973-133">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="fe973-134">AZ batch pool instellen</span><span class="sxs-lookup"><span data-stu-id="fe973-134">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="fe973-135">Eigenschappen van een groep bijwerken.</span><span class="sxs-lookup"><span data-stu-id="fe973-135">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="fe973-136">lijst van AZ batch pool knooppunt-agent-SKU 's</span><span class="sxs-lookup"><span data-stu-id="fe973-136">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="fe973-137">Lijst met beschikbare knooppunt agent SKU's en informatie over de afbeelding.</span><span class="sxs-lookup"><span data-stu-id="fe973-137">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="fe973-138">AZ batch-pool formaat wijzigen</span><span class="sxs-lookup"><span data-stu-id="fe973-138">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="fe973-139">De grootte van het aantal VM's worden uitgevoerd in de opgegeven groep.</span><span class="sxs-lookup"><span data-stu-id="fe973-139">Resize the number of running VMs in the specified pool.</span></span>  |
| [<span data-ttu-id="fe973-140">AZ batch pool weergeven</span><span class="sxs-lookup"><span data-stu-id="fe973-140">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="fe973-141">De eigenschappen van een groep weergeven.</span><span class="sxs-lookup"><span data-stu-id="fe973-141">Display the properties of a pool.</span></span>  |
| [<span data-ttu-id="fe973-142">AZ batch pool verwijderen</span><span class="sxs-lookup"><span data-stu-id="fe973-142">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="fe973-143">Verwijder de opgegeven groep.</span><span class="sxs-lookup"><span data-stu-id="fe973-143">Delete the specified pool.</span></span>  |
| [<span data-ttu-id="fe973-144">AZ batch-pool automatisch schalen inschakelen</span><span class="sxs-lookup"><span data-stu-id="fe973-144">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="fe973-145">Automatische schaling inschakelen op een pool en toepassen van een formule.</span><span class="sxs-lookup"><span data-stu-id="fe973-145">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="fe973-146">AZ batch-pool automatisch schalen uitschakelen</span><span class="sxs-lookup"><span data-stu-id="fe973-146">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="fe973-147">Schakel automatisch schalen op een groep.</span><span class="sxs-lookup"><span data-stu-id="fe973-147">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="fe973-148">lijst met knooppunten AZ-batch</span><span class="sxs-lookup"><span data-stu-id="fe973-148">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="fe973-149">Lijst van het rekenknooppunt in de opgegeven groep.</span><span class="sxs-lookup"><span data-stu-id="fe973-149">List all the compute node in the specified pool.</span></span>  |
| [<span data-ttu-id="fe973-150">AZ batch knooppunt opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="fe973-150">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="fe973-151">Het opgegeven computerknooppunt opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="fe973-151">Reboot the specified compute node.</span></span>  |
| [<span data-ttu-id="fe973-152">AZ batch knooppunt verwijderen</span><span class="sxs-lookup"><span data-stu-id="fe973-152">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="fe973-153">Verwijder de vermelde knooppunten van de opgegeven groep.</span><span class="sxs-lookup"><span data-stu-id="fe973-153">Delete the listed nodes from the specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="fe973-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fe973-154">Next steps</span></span>

<span data-ttu-id="fe973-155">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fe973-155">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fe973-156">Aanvullende Batch CLI scriptvoorbeelden vindt u in de [documentatie van Azure Batch CLI](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fe973-156">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

