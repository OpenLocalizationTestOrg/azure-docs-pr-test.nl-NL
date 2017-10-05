---
title: Azure CLI Sample Script - ACS DC/OS-Cluster maken | Microsoft Docs
description: Azure CLI Sample Script - ACS DC/OS-Cluster maken
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: nepeters
ms.openlocfilehash: ff90aee308a993ae0d36288191d1496affacce2a
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="create-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="fdcd8-104">Een Azure Container Service DC/OS-Cluster maken</span><span class="sxs-lookup"><span data-stu-id="fdcd8-104">Create an Azure Container Service DC/OS Cluster</span></span>

<span data-ttu-id="fdcd8-105">In dit voorbeeld wordt een Azure Container Service-cluster DCOS uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fdcd8-105">This sample creates an Azure Container Service cluster running DCOS.</span></span>

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fdcd8-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="fdcd8-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="fdcd8-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="fdcd8-107">Clean up deployment</span></span> 

<span data-ttu-id="fdcd8-108">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="fdcd8-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="fdcd8-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="fdcd8-109">Script explanation</span></span>

<span data-ttu-id="fdcd8-110">Dit script maakt gebruik van de volgende opdrachten om de implementatie te maken.</span><span class="sxs-lookup"><span data-stu-id="fdcd8-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="fdcd8-111">Elk item in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="fdcd8-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fdcd8-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="fdcd8-112">Command</span></span> | <span data-ttu-id="fdcd8-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="fdcd8-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fdcd8-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="fdcd8-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fdcd8-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="fdcd8-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fdcd8-116">AZ acs maken</span><span class="sxs-lookup"><span data-stu-id="fdcd8-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="fdcd8-117">Maakt en ACS-cluster.</span><span class="sxs-lookup"><span data-stu-id="fdcd8-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fdcd8-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fdcd8-118">Next steps</span></span>

<span data-ttu-id="fdcd8-119">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fdcd8-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fdcd8-120">Extra Azure Container Service CLI scriptvoorbeelden vindt u in de [Azure Container Service documentatie](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fdcd8-120">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>