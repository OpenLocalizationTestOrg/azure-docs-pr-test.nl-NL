---
title: Het voorbeeldscript Azure CLI - verwijderen van een Azure Redis-Cache | Microsoft Docs
description: Het voorbeeldscript Azure CLI - verwijderen van een Azure Redis-Cache
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 7beded7a-d2c9-43a6-b3b4-b8079c11de4a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: f959823b3a7c5b0262f693ecad1e6efc4eec4f35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="delete-an-azure-redis-cache"></a><span data-ttu-id="4bb38-103">Verwijderen van een Azure Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="4bb38-103">Delete an Azure Redis Cache</span></span>

<span data-ttu-id="4bb38-104">In dit scenario wordt informatie over het verwijderen van een Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="4bb38-104">In this scenario, you learn how to delete an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="4bb38-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="4bb38-105">Sample script</span></span>

<span data-ttu-id="4bb38-106">[!code-azurecli[belangrijkste](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis-Cache")]</span><span class="sxs-lookup"><span data-stu-id="4bb38-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="4bb38-107">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="4bb38-107">Script explanation</span></span>

<span data-ttu-id="4bb38-108">Dit script wordt de volgende opdrachten om te verwijderen van een Azure Redis-Cache-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="4bb38-108">This script uses the following commands to delete an Azure Redis Cache instance.</span></span> <span data-ttu-id="4bb38-109">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="4bb38-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4bb38-110">Opdracht</span><span class="sxs-lookup"><span data-stu-id="4bb38-110">Command</span></span> | <span data-ttu-id="4bb38-111">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="4bb38-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4bb38-112">AZ redis verwijderen</span><span class="sxs-lookup"><span data-stu-id="4bb38-112">az redis delete</span></span>](https://docs.microsoft.com/cli/azure/redis#delete) | <span data-ttu-id="4bb38-113">Verwijderen van Redis-Cache-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="4bb38-113">Delete Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="4bb38-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4bb38-114">Next steps</span></span>

<span data-ttu-id="4bb38-115">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4bb38-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4bb38-116">Aanvullende voorbeelden van Azure Redis-Cache CLI-script kunnen worden gevonden in de [documentatie van Azure Redis-Cache](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4bb38-116">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>