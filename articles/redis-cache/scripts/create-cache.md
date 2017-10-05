---
title: Azure CLI Sample Script - maken van een Azure Redis-Cache | Microsoft Docs
description: Azure CLI Script voorbeeld - een Azure Redis-Cache maken
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: afd7f6e0-9297-4c98-a95e-597be939cef7
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: c6b153d80de4cbf2bec1bc70d67be7befa0c5ec3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-redis-cache"></a><span data-ttu-id="af15b-103">Maak een Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="af15b-103">Create an Azure Redis Cache</span></span>

<span data-ttu-id="af15b-104">In dit scenario wordt informatie over het maken van een Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="af15b-104">In this scenario, you learn how to create an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="af15b-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="af15b-105">Sample script</span></span>

<span data-ttu-id="af15b-106">[!code-azurecli[belangrijkste](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis-Cache")]</span><span class="sxs-lookup"><span data-stu-id="af15b-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="af15b-107">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="af15b-107">Script explanation</span></span>

<span data-ttu-id="af15b-108">Dit script maakt gebruik van de volgende opdrachten om een resourcegroep en een redis-cache te maken.</span><span class="sxs-lookup"><span data-stu-id="af15b-108">This script uses the following commands to create a resource group and a redis cache.</span></span> <span data-ttu-id="af15b-109">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="af15b-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="af15b-110">Opdracht</span><span class="sxs-lookup"><span data-stu-id="af15b-110">Command</span></span> | <span data-ttu-id="af15b-111">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="af15b-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="af15b-112">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="af15b-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="af15b-113">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="af15b-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="af15b-114">AZ redis maken</span><span class="sxs-lookup"><span data-stu-id="af15b-114">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="af15b-115">Redis-Cache-exemplaar maken.</span><span class="sxs-lookup"><span data-stu-id="af15b-115">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="af15b-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="af15b-116">Next steps</span></span>

<span data-ttu-id="af15b-117">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="af15b-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="af15b-118">Aanvullende voorbeelden van Azure Redis-Cache CLI-script kunnen worden gevonden in de [documentatie van Azure Redis-Cache](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="af15b-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>