---
title: aaaAzure voorbeeldscript CLI - maakt een Premium Azure Redis-Cache met clustering | Microsoft Docs
description: Azure CLI-Script steekproef - maken van een laag Premium Azure Redis-Cache met clustering
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 07bcceae-2521-4fe3-b88f-ed833104ddd2
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: ca34d40059b282cb2abc7e3e2b8771226029744c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a><span data-ttu-id="205bb-103">Maken van een Premium Azure Redis-Cache met clustering</span><span class="sxs-lookup"><span data-stu-id="205bb-103">Create a Premium Azure Redis Cache with clustering</span></span>

<span data-ttu-id="205bb-104">In dit scenario leert u hoe toocreate 6 GB Premium laag Azure Redis-Cache met clustering ingeschakeld en twee shards.</span><span class="sxs-lookup"><span data-stu-id="205bb-104">In this scenario, you learn how toocreate a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="205bb-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="205bb-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="205bb-106">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="205bb-106">Script explanation</span></span>

<span data-ttu-id="205bb-107">Dit script gebruikt Hallo opdrachten toocreate na een resourcegroep en een Premium-laag redis-cache met clustering inschakelen.</span><span class="sxs-lookup"><span data-stu-id="205bb-107">This script uses hello following commands toocreate a resource group and a Premium tier redis cache with clustering enable.</span></span> <span data-ttu-id="205bb-108">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="205bb-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="205bb-109">Opdracht</span><span class="sxs-lookup"><span data-stu-id="205bb-109">Command</span></span> | <span data-ttu-id="205bb-110">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="205bb-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="205bb-111">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="205bb-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="205bb-112">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="205bb-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="205bb-113">AZ redis maken</span><span class="sxs-lookup"><span data-stu-id="205bb-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="205bb-114">Redis-Cache-exemplaar maken.</span><span class="sxs-lookup"><span data-stu-id="205bb-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="205bb-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="205bb-115">Next steps</span></span>

<span data-ttu-id="205bb-116">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="205bb-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="205bb-117">Aanvullende voorbeelden van Azure Redis-Cache CLI script kunnen u vinden in Hallo [documentatie van Azure Redis-Cache](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="205bb-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
