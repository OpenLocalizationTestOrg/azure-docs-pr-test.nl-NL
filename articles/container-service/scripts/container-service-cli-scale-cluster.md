---
title: aaaAzure voorbeeldscript CLI - schalen een ACS-Cluster | Microsoft Docs
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
ms.openlocfilehash: b1c214d7cca615257ec8cd6e9993cd15f694289b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="3f8bb-104">Een Azure Container Service-Cluster schalen</span><span class="sxs-lookup"><span data-stu-id="3f8bb-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="3f8bb-105">In dit voorbeeld kan worden geschaald en Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="3f8bb-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3f8bb-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="3f8bb-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="3f8bb-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="3f8bb-107">Clean up deployment</span></span> 

<span data-ttu-id="3f8bb-108">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3f8bb-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="3f8bb-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="3f8bb-109">Script explanation</span></span>

<span data-ttu-id="3f8bb-110">Dit script maakt gebruik van Hallo opdrachten toocreate Hallo implementatie te volgen.</span><span class="sxs-lookup"><span data-stu-id="3f8bb-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="3f8bb-111">Elk item in de tabel Hallo koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="3f8bb-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3f8bb-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="3f8bb-112">Command</span></span> | <span data-ttu-id="3f8bb-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="3f8bb-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3f8bb-114">AZ acs schaal</span><span class="sxs-lookup"><span data-stu-id="3f8bb-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="3f8bb-115">De schaal van een ACS-cluster.</span><span class="sxs-lookup"><span data-stu-id="3f8bb-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3f8bb-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3f8bb-116">Next steps</span></span>

<span data-ttu-id="3f8bb-117">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3f8bb-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3f8bb-118">Extra Azure Container Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Container Service documentatie](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3f8bb-118">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>

