---
title: Azure CLI Script-Maak een failoverbeleid voor maximale beschikbaarheid | Microsoft Docs
description: Azure CLI-Script steekproef - maken van een failover-beleid voor hoge beschikbaarheid
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
ms.openlocfilehash: 96083d66cc1a2ef179f9313c1b3ed04162c1c048
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-failover-policy-for-high-availability-using-the-azure-cli"></a><span data-ttu-id="2f65d-103">Maken van een failover-beleid voor hoge beschikbaarheid met behulp van de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2f65d-103">Create a failover policy for high availability using the Azure CLI</span></span>

<span data-ttu-id="2f65d-104">Dit voorbeeldscript CLI een Cosmos-DB Azure-account maakt en configureert deze voor maximale beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="2f65d-104">This sample CLI script creates an Azure Cosmos DB account, and then configures it for high availability.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2f65d-105">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="2f65d-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2f65d-106">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="2f65d-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="2f65d-107">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2f65d-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="2f65d-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="2f65d-108">Sample script</span></span>

<span data-ttu-id="2f65d-109">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/cosmosdb/high-availability-cosmosdb-configure-failover/high-availability-cosmosdb-configure-failover.sh?highlight=23-27 "een Azure Cosmos DB failover-beleid maken")]</span><span class="sxs-lookup"><span data-stu-id="2f65d-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/high-availability-cosmosdb-configure-failover/high-availability-cosmosdb-configure-failover.sh?highlight=23-27 "Create an Azure Cosmos DB failover policy")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2f65d-110">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="2f65d-110">Clean up deployment</span></span>

<span data-ttu-id="2f65d-111">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om te verwijderen van de resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="2f65d-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2f65d-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="2f65d-112">Script explanation</span></span>

<span data-ttu-id="2f65d-113">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="2f65d-113">This script uses the following commands.</span></span> <span data-ttu-id="2f65d-114">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="2f65d-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2f65d-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="2f65d-115">Command</span></span> | <span data-ttu-id="2f65d-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="2f65d-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2f65d-117">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="2f65d-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="2f65d-118">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2f65d-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2f65d-119">AZ cosmosdb maken</span><span class="sxs-lookup"><span data-stu-id="2f65d-119">az cosmosdb create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="2f65d-120">Maakt een Cosmos-DB Azure-account.</span><span class="sxs-lookup"><span data-stu-id="2f65d-120">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="2f65d-121">AZ cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="2f65d-121">az cosmosdb update</span></span>](/cli/azure/cosmosdb#update) | <span data-ttu-id="2f65d-122">Account voor Azure DB die Cosmos-updates.</span><span class="sxs-lookup"><span data-stu-id="2f65d-122">Updates Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="2f65d-123">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="2f65d-123">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="2f65d-124">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="2f65d-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2f65d-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f65d-125">Next steps</span></span>

<span data-ttu-id="2f65d-126">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2f65d-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2f65d-127">Extra Azure Cosmos DB CLI scriptvoorbeelden vindt u in de [Azure Cosmos DB CLI documentatie](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2f65d-127">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
