---
title: aaaAzure voorbeeldscript CLI - ACS DC/OS-Cluster maken | Microsoft Docs
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
ms.openlocfilehash: 35213fd615b2145642add908dfc48516c33ff332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="0fddd-104">Een Azure Container Service DC/OS-Cluster maken</span><span class="sxs-lookup"><span data-stu-id="0fddd-104">Create an Azure Container Service DC/OS Cluster</span></span>

<span data-ttu-id="0fddd-105">In dit voorbeeld wordt een Azure Container Service-cluster DCOS uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0fddd-105">This sample creates an Azure Container Service cluster running DCOS.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0fddd-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="0fddd-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="0fddd-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="0fddd-107">Clean up deployment</span></span> 

<span data-ttu-id="0fddd-108">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0fddd-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="0fddd-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="0fddd-109">Script explanation</span></span>

<span data-ttu-id="0fddd-110">Dit script maakt gebruik van Hallo opdrachten toocreate Hallo implementatie te volgen.</span><span class="sxs-lookup"><span data-stu-id="0fddd-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="0fddd-111">Elk item in de tabel Hallo koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="0fddd-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0fddd-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="0fddd-112">Command</span></span> | <span data-ttu-id="0fddd-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="0fddd-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0fddd-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="0fddd-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0fddd-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="0fddd-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0fddd-116">AZ acs maken</span><span class="sxs-lookup"><span data-stu-id="0fddd-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="0fddd-117">Maakt en ACS-cluster.</span><span class="sxs-lookup"><span data-stu-id="0fddd-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0fddd-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0fddd-118">Next steps</span></span>

<span data-ttu-id="0fddd-119">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0fddd-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0fddd-120">Extra Azure Container Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Container Service documentatie](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0fddd-120">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>
