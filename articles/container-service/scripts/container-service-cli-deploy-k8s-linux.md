---
title: Azure CLI Sample Script - ACS Linux Kubernetes Cluster maken | Microsoft Docs
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
ms.openlocfilehash: 46bc37ab9949d070d19a3d8946fd5b00acf7f5d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-container-service-kubernetes-linux-cluster"></a><span data-ttu-id="05627-104">Een Azure Container Service Kubernetes Linux-Cluster maken</span><span class="sxs-lookup"><span data-stu-id="05627-104">Create an Azure Container Service Kubernetes Linux Cluster</span></span>

<span data-ttu-id="05627-105">In dit voorbeeld wordt een Azure Container Service-cluster Kubernetes uitgevoerd voor op basis van Linux-containers.</span><span class="sxs-lookup"><span data-stu-id="05627-105">This sample creates an Azure Container Service cluster running Kubernetes for Linux based containers.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="05627-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="05627-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type kubernetes \
  --resource-group myResourceGroup \
  --name myK8SCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="05627-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="05627-107">Clean up deployment</span></span> 

<span data-ttu-id="05627-108">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="05627-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="05627-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="05627-109">Script explanation</span></span>

<span data-ttu-id="05627-110">Dit script maakt gebruik van de volgende opdrachten om de implementatie te maken.</span><span class="sxs-lookup"><span data-stu-id="05627-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="05627-111">Elk item in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="05627-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="05627-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="05627-112">Command</span></span> | <span data-ttu-id="05627-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="05627-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="05627-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="05627-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="05627-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="05627-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="05627-116">AZ acs maken</span><span class="sxs-lookup"><span data-stu-id="05627-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="05627-117">Maakt en ACS-cluster.</span><span class="sxs-lookup"><span data-stu-id="05627-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="05627-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="05627-118">Next steps</span></span>

<span data-ttu-id="05627-119">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="05627-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="05627-120">Extra Azure Container Service CLI scriptvoorbeelden vindt u in de [Azure Container Service documentatie](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="05627-120">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>

