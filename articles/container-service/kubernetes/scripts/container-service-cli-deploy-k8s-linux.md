---
title: aaaAzure voorbeeldscript CLI - ACS Linux Kubernetes Cluster maken | Microsoft Docs
description: Azure CLI Sample Script - ACS Linux Kubernetes Cluster maken
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
ms.openlocfilehash: cf3798ea8b08e3fc32acb35dabab4b2fbea179dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-container-service-kubernetes-linux-cluster"></a><span data-ttu-id="efa0c-104">Een Azure Container Service Kubernetes Linux-Cluster maken</span><span class="sxs-lookup"><span data-stu-id="efa0c-104">Create an Azure Container Service Kubernetes Linux Cluster</span></span>

<span data-ttu-id="efa0c-105">In dit voorbeeld wordt een Azure Container Service-cluster Kubernetes uitgevoerd voor op basis van Linux-containers.</span><span class="sxs-lookup"><span data-stu-id="efa0c-105">This sample creates an Azure Container Service cluster running Kubernetes for Linux based containers.</span></span>

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="efa0c-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="efa0c-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type kubernetes \
  --resource-group myResourceGroup \
  --name myK8SCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="efa0c-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="efa0c-107">Clean up deployment</span></span> 

<span data-ttu-id="efa0c-108">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="efa0c-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="efa0c-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="efa0c-109">Script explanation</span></span>

<span data-ttu-id="efa0c-110">Dit script maakt gebruik van Hallo opdrachten toocreate Hallo implementatie te volgen.</span><span class="sxs-lookup"><span data-stu-id="efa0c-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="efa0c-111">Elk item in de tabel Hallo koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="efa0c-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="efa0c-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="efa0c-112">Command</span></span> | <span data-ttu-id="efa0c-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="efa0c-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="efa0c-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="efa0c-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="efa0c-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="efa0c-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="efa0c-116">AZ acs maken</span><span class="sxs-lookup"><span data-stu-id="efa0c-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="efa0c-117">Maakt en ACS-cluster.</span><span class="sxs-lookup"><span data-stu-id="efa0c-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="efa0c-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="efa0c-118">Next steps</span></span>

<span data-ttu-id="efa0c-119">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="efa0c-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="efa0c-120">Extra Azure Container Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Container Service documentatie](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="efa0c-120">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>

