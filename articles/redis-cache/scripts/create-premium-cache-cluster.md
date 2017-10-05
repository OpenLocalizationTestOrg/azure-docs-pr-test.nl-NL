---
title: 'Azure CLI-Script voorbeeld: een Premium Azure Redis-Cache maken met clustering | Microsoft Docs'
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
ms.openlocfilehash: 87d0fe4c3eaa8f7b75343a36a069ecdac8241d74
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a><span data-ttu-id="51388-103">Maken van een Premium Azure Redis-Cache met clustering</span><span class="sxs-lookup"><span data-stu-id="51388-103">Create a Premium Azure Redis Cache with clustering</span></span>

<span data-ttu-id="51388-104">In dit scenario u meer informatie over het maken van een laag van 6 GB Premium Azure Redis-Cache met clusteren is ingeschakeld en twee shards.</span><span class="sxs-lookup"><span data-stu-id="51388-104">In this scenario, you learn how to create a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="51388-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="51388-105">Sample script</span></span>

<span data-ttu-id="51388-106">[!code-azurecli[belangrijkste](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis-Cache")]</span><span class="sxs-lookup"><span data-stu-id="51388-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="51388-107">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="51388-107">Script explanation</span></span>

<span data-ttu-id="51388-108">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep en een Premium-laag redis-cache met clustering inschakelen.</span><span class="sxs-lookup"><span data-stu-id="51388-108">This script uses the following commands to create a resource group and a Premium tier redis cache with clustering enable.</span></span> <span data-ttu-id="51388-109">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="51388-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="51388-110">Opdracht</span><span class="sxs-lookup"><span data-stu-id="51388-110">Command</span></span> | <span data-ttu-id="51388-111">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="51388-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="51388-112">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="51388-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="51388-113">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="51388-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="51388-114">AZ redis maken</span><span class="sxs-lookup"><span data-stu-id="51388-114">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="51388-115">Redis-Cache-exemplaar maken.</span><span class="sxs-lookup"><span data-stu-id="51388-115">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="51388-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="51388-116">Next steps</span></span>

<span data-ttu-id="51388-117">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="51388-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="51388-118">Aanvullende voorbeelden van Azure Redis-Cache CLI-script kunnen worden gevonden in de [documentatie van Azure Redis-Cache](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="51388-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>