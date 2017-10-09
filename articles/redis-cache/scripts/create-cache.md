---
title: aaaAzure voorbeeldscript CLI - Maak een Azure Redis-Cache | Microsoft Docs
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
ms.openlocfilehash: 85b007a426fbd4752034ec8663835963d140dd75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-redis-cache"></a><span data-ttu-id="819e1-103">Maak een Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="819e1-103">Create an Azure Redis Cache</span></span>

<span data-ttu-id="819e1-104">In dit scenario leert u hoe toocreate een Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="819e1-104">In this scenario, you learn how toocreate an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="819e1-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="819e1-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="819e1-106">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="819e1-106">Script explanation</span></span>

<span data-ttu-id="819e1-107">Dit script gebruikt Hallo opdrachten toocreate na een resourcegroep en een redis-cache.</span><span class="sxs-lookup"><span data-stu-id="819e1-107">This script uses hello following commands toocreate a resource group and a redis cache.</span></span> <span data-ttu-id="819e1-108">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="819e1-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="819e1-109">Opdracht</span><span class="sxs-lookup"><span data-stu-id="819e1-109">Command</span></span> | <span data-ttu-id="819e1-110">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="819e1-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="819e1-111">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="819e1-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="819e1-112">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="819e1-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="819e1-113">AZ redis maken</span><span class="sxs-lookup"><span data-stu-id="819e1-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="819e1-114">Redis-Cache-exemplaar maken.</span><span class="sxs-lookup"><span data-stu-id="819e1-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="819e1-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="819e1-115">Next steps</span></span>

<span data-ttu-id="819e1-116">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="819e1-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="819e1-117">Aanvullende voorbeelden van Azure Redis-Cache CLI script kunnen u vinden in Hallo [documentatie van Azure Redis-Cache](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="819e1-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
