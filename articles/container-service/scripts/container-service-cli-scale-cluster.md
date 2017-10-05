---
title: Azure CLI-voorbeeldscript - schaal een ACS-Cluster | Microsoft Docs
description: Azure CLI-voorbeeldscript - schaal een ACS-Cluster
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
ms.openlocfilehash: 0ea2c73436e650fdb37535538baccc565369fa9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="9b461-104">Een Azure Container Service-Cluster schalen</span><span class="sxs-lookup"><span data-stu-id="9b461-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="9b461-105">In dit voorbeeld kan worden geschaald en Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="9b461-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9b461-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="9b461-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="9b461-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="9b461-107">Clean up deployment</span></span> 

<span data-ttu-id="9b461-108">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9b461-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9b461-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="9b461-109">Script explanation</span></span>

<span data-ttu-id="9b461-110">Dit script maakt gebruik van de volgende opdrachten om de implementatie te maken.</span><span class="sxs-lookup"><span data-stu-id="9b461-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="9b461-111">Elk item in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="9b461-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9b461-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="9b461-112">Command</span></span> | <span data-ttu-id="9b461-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="9b461-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9b461-114">AZ acs schaal</span><span class="sxs-lookup"><span data-stu-id="9b461-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="9b461-115">De schaal van een ACS-cluster.</span><span class="sxs-lookup"><span data-stu-id="9b461-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9b461-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9b461-116">Next steps</span></span>

<span data-ttu-id="9b461-117">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9b461-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9b461-118">Extra Azure Container Service CLI scriptvoorbeelden vindt u in de [Azure Container Service documentatie](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9b461-118">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>

