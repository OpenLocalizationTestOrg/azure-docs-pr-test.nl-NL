---
title: Azure CLI Script-opnieuw genereren Azure Cosmos DB accountsleutel | Microsoft Docs
description: Azure CLI-voorbeeldscript - opnieuw genereren accountcode Azure Cosmos-DB
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
ms.openlocfilehash: 1a0ff3f8b8fb3eaf398d9fa925ef027b2481d47a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="regenerate-an-azure-cosmos-db-account-key-using-the-azure-cli"></a><span data-ttu-id="f9309-103">Opnieuw genereren met de Azure CLI accountcode Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="f9309-103">Regenerate an Azure Cosmos DB account key using the Azure CLI</span></span>

<span data-ttu-id="f9309-104">Dit voorbeeld wordt opnieuw gegenereerd elk soort sleutel voor Azure DB die Cosmos-account met de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f9309-104">This sample regenerates any kind of Azure Cosmos DB account key using the Azure CLI.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f9309-105">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="f9309-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f9309-106">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="f9309-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="f9309-107">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f9309-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f9309-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="f9309-108">Sample script</span></span>

<span data-ttu-id="f9309-109">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/cosmosdb/secure-cosmosdb-regenerate-keys/secure-cosmosdb-regenerate-keys.sh?highlight=27-31 "Azure Cosmos-DB opnieuw genereren van sleutels")]</span><span class="sxs-lookup"><span data-stu-id="f9309-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-regenerate-keys/secure-cosmosdb-regenerate-keys.sh?highlight=27-31 "Regenerate Azure Cosmos DB account keys")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f9309-110">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="f9309-110">Clean up deployment</span></span>

<span data-ttu-id="f9309-111">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om te verwijderen van de resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="f9309-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f9309-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="f9309-112">Script explanation</span></span>

<span data-ttu-id="f9309-113">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="f9309-113">This script uses the following commands.</span></span> <span data-ttu-id="f9309-114">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="f9309-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f9309-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="f9309-115">Command</span></span> | <span data-ttu-id="f9309-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="f9309-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f9309-117">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="f9309-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="f9309-118">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f9309-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f9309-119">AZ cosmosdb maken</span><span class="sxs-lookup"><span data-stu-id="f9309-119">az cosmosdb create</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#create) | <span data-ttu-id="f9309-120">Een account voor Azure DB die Cosmos-updates.</span><span class="sxs-lookup"><span data-stu-id="f9309-120">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="f9309-121">AZ cosmosdb opnieuw genereren-sleutel</span><span class="sxs-lookup"><span data-stu-id="f9309-121">az cosmosdb regenerate-key</span></span>](/cli/azure/cosmosdb/regenerate-key) | <span data-ttu-id="f9309-122">Toegangscodes Regeneratates Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f9309-122">Regeneratates Azure Cosmos DB account keys.</span></span> |
| [<span data-ttu-id="f9309-123">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="f9309-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="f9309-124">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="f9309-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f9309-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f9309-125">Next steps</span></span>

<span data-ttu-id="f9309-126">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f9309-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f9309-127">Extra Azure Cosmos DB CLI scriptvoorbeelden vindt u in de [Azure Cosmos DB CLI documentatie](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f9309-127">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
