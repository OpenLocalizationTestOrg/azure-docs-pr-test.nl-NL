---
title: aaaAzure CLI Script maakt een API van Azure Cosmos DB DocumentDB-account, database en verzameling | Microsoft Docs
description: 'Azure CLI-Script voorbeeld: een API van Azure Cosmos DB DocumentDB-account, database en verzameling maken'
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
ms.date: 06/06/2017
ms.author: mimig
ms.openlocfilehash: 53919a849e04fa69680219e51c0289b9f2affe07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-an-documentdb-api-account-using-cli"></a><span data-ttu-id="45e83-103">Azure Cosmos DB: Een DocumentDB-API-account maken met CLI</span><span class="sxs-lookup"><span data-stu-id="45e83-103">Azure Cosmos DB: Create an DocumentDB API account using CLI</span></span>

<span data-ttu-id="45e83-104">Dit voorbeeldscript CLI maakt een API van Azure Cosmos DB DocumentDB-account, database en verzameling.</span><span class="sxs-lookup"><span data-stu-id="45e83-104">This sample CLI script creates an Azure Cosmos DB DocumentDB API account, database, and collection.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="45e83-105">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="45e83-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="45e83-106">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="45e83-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="45e83-107">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="45e83-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="45e83-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="45e83-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/create-cosmosdb-account-database/create-cosmosdb-account-database.sh?highlight=15-35 "Create an Azure Cosmos DB DocumentDB API account, database, and collection")]

## <a name="clean-up-deployment"></a><span data-ttu-id="45e83-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="45e83-109">Clean up deployment</span></span>

<span data-ttu-id="45e83-110">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="45e83-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="45e83-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="45e83-111">Script explanation</span></span>

<span data-ttu-id="45e83-112">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="45e83-112">This script uses hello following commands.</span></span> <span data-ttu-id="45e83-113">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="45e83-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="45e83-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="45e83-114">Command</span></span> | <span data-ttu-id="45e83-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="45e83-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="45e83-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="45e83-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="45e83-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="45e83-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="45e83-118">AZ cosmosdb maken</span><span class="sxs-lookup"><span data-stu-id="45e83-118">az cosmosdb create</span></span>](/cli/azure/cosmosdb#create) | <span data-ttu-id="45e83-119">Maakt een Cosmos-DB Azure-account.</span><span class="sxs-lookup"><span data-stu-id="45e83-119">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="45e83-120">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="45e83-120">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="45e83-121">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="45e83-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="45e83-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="45e83-122">Next steps</span></span>

<span data-ttu-id="45e83-123">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="45e83-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="45e83-124">Extra Azure Cosmos DB CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Cosmos DB CLI documentatie](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="45e83-124">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
