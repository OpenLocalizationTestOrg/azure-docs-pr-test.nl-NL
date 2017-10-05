---
title: Azure CLI Script-Multiregion replicatie voor de Azure DB die Cosmos | Microsoft Docs
description: Azure CLI-voorbeeldscript - Multiregion replicatie voor Azure Cosmos-DB
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
ms.openlocfilehash: ab716c28b88412438d0cea80377f9f0f40dc8bd6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-the-azure-cli"></a><span data-ttu-id="4e3d5-103">Een databaseaccount Azure Cosmos DB in meerdere regio's worden gerepliceerd en het configureren van failover prioriteiten met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4e3d5-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using the Azure CLI</span></span>

<span data-ttu-id="4e3d5-104">Dit voorbeeld wordt gerepliceerd elk soort account voor Azure DB die Cosmos-database in meerdere regio's en configureert u failover prioriteiten met de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4e3d5-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using the Azure CLI.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4e3d5-105">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4e3d5-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4e3d5-106">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="4e3d5-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="4e3d5-107">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4e3d5-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="4e3d5-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="4e3d5-108">Sample script</span></span>

<span data-ttu-id="4e3d5-109">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/cosmosdb/scale-cosmosdb-replicate-multiple-regions/scale-cosmosdb-replicate-multiple-regions.sh?highlight=21-31 "Scale Azure Cosmos DB naar meerdere regio's")]</span><span class="sxs-lookup"><span data-stu-id="4e3d5-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-replicate-multiple-regions/scale-cosmosdb-replicate-multiple-regions.sh?highlight=21-31 "Scale Azure Cosmos DB into multiple regions")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="4e3d5-110">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="4e3d5-110">Clean up deployment</span></span>

<span data-ttu-id="4e3d5-111">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om te verwijderen van de resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="4e3d5-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="4e3d5-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="4e3d5-112">Script explanation</span></span>

<span data-ttu-id="4e3d5-113">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="4e3d5-113">This script uses the following commands.</span></span> <span data-ttu-id="4e3d5-114">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="4e3d5-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4e3d5-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="4e3d5-115">Command</span></span> | <span data-ttu-id="4e3d5-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="4e3d5-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4e3d5-117">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="4e3d5-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="4e3d5-118">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4e3d5-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4e3d5-119">AZ cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="4e3d5-119">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="4e3d5-120">Een account voor Azure DB die Cosmos-updates.</span><span class="sxs-lookup"><span data-stu-id="4e3d5-120">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="4e3d5-121">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="4e3d5-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="4e3d5-122">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="4e3d5-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4e3d5-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4e3d5-123">Next steps</span></span>

<span data-ttu-id="4e3d5-124">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4e3d5-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4e3d5-125">Extra Azure Cosmos DB CLI scriptvoorbeelden vindt u in de [Azure Cosmos DB CLI documentatie](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4e3d5-125">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
