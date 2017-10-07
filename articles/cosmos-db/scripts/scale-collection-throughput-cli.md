---
title: aaaAzure CLI Script Scale Azure Cosmos DB container doorvoer | Microsoft Docs
description: Azure CLI-voorbeeldscript - Scale Azure Cosmos DB contianer doorvoer
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: b1a60feaf43f555a9f6ba20e5e0617f73521c0a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-cosmos-db-container-throughput-using-hello-azure-cli"></a><span data-ttu-id="3abf1-103">Scale Azure Cosmos DB container doorvoer hello Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="3abf1-103">Scale Azure Cosmos DB container throughput using hello Azure CLI</span></span>

<span data-ttu-id="3abf1-104">Dit voorbeeld wordt geschaald container doorvoer voor elk soort Azure DB die Cosmos-container.</span><span class="sxs-lookup"><span data-stu-id="3abf1-104">This sample scales container throughput for any kind of Azure Cosmos DB container.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3abf1-105">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3abf1-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3abf1-106">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="3abf1-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3abf1-107">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3abf1-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3abf1-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="3abf1-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "Scale Azure Cosmos DB throughput")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3abf1-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="3abf1-109">Clean up deployment</span></span>

<span data-ttu-id="3abf1-110">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="3abf1-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="3abf1-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="3abf1-111">Script explanation</span></span>

<span data-ttu-id="3abf1-112">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="3abf1-112">This script uses hello following commands.</span></span> <span data-ttu-id="3abf1-113">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="3abf1-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3abf1-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="3abf1-114">Command</span></span> | <span data-ttu-id="3abf1-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="3abf1-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3abf1-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="3abf1-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="3abf1-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3abf1-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3abf1-118">AZ cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="3abf1-118">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="3abf1-119">Een account voor Azure DB die Cosmos-updates.</span><span class="sxs-lookup"><span data-stu-id="3abf1-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="3abf1-120">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="3abf1-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="3abf1-121">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="3abf1-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3abf1-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3abf1-122">Next steps</span></span>

<span data-ttu-id="3abf1-123">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3abf1-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3abf1-124">Extra Azure Cosmos DB CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Cosmos DB CLI documentatie](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3abf1-124">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
