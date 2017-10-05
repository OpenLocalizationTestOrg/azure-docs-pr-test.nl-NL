---
title: Azure CLI-voorbeeldscript - Get de hostnaam, poorten en sleutels voor Azure Redis-Cache | Microsoft Docs
description: Azure CLI-voorbeeldscript - Get de hostnaam, poorten en sleutels voor een Azure Redis-Cache-exemplaar
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: cd9adc784bceb0fff5e7c2bbee2be0950c51c8f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-hostname-ports-and-keys-for-azure-redis-cache"></a><span data-ttu-id="abcfd-103">Ophalen van de hostnaam, poorten en sleutels voor Azure Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="abcfd-103">Get the hostname, ports, and keys for Azure Redis Cache</span></span>

<span data-ttu-id="abcfd-104">In dit scenario u informatie over het ophalen van de hostnaam, poorten en sleutels die verbinding maken met een Azure Redis-Cache-exemplaar worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="abcfd-104">In this scenario, you learn how to retrieve the hostname, ports, and keys used to connect to an Azure Redis Cache instance.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="abcfd-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="abcfd-105">Sample script</span></span>

<span data-ttu-id="abcfd-106">[!code-azurecli[belangrijkste](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis-Cache")]</span><span class="sxs-lookup"><span data-stu-id="abcfd-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="abcfd-107">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="abcfd-107">Script explanation</span></span>

<span data-ttu-id="abcfd-108">Dit script maakt gebruik van de volgende opdrachten voor het ophalen van de hostnaam, sleutels en poorten van een Azure Redis-Cache-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="abcfd-108">This script uses the following commands to retrieve the hostname, keys, and ports of an Azure Redis Cache instance.</span></span> <span data-ttu-id="abcfd-109">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="abcfd-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="abcfd-110">Opdracht</span><span class="sxs-lookup"><span data-stu-id="abcfd-110">Command</span></span> | <span data-ttu-id="abcfd-111">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="abcfd-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="abcfd-112">AZ redis weergeven</span><span class="sxs-lookup"><span data-stu-id="abcfd-112">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="abcfd-113">Ophalen van gegevens van een Azure Redis-Cache-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="abcfd-113">Retrieve details of an Azure Redis Cache instance.</span></span> |
| [<span data-ttu-id="abcfd-114">AZ redis lijst-sleutels</span><span class="sxs-lookup"><span data-stu-id="abcfd-114">az redis list-keys</span></span>](https://docs.microsoft.com/cli/azure/redis#list-keys) | <span data-ttu-id="abcfd-115">Sneltoetsen voor een Azure Redis-Cache-exemplaar worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="abcfd-115">Retrieve access keys for an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="abcfd-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="abcfd-116">Next steps</span></span>

<span data-ttu-id="abcfd-117">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="abcfd-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="abcfd-118">Aanvullende voorbeelden van Azure Redis-Cache CLI-script kunnen worden gevonden in de [documentatie van Azure Redis-Cache](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="abcfd-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>