---
title: aaaAzure CLI Script-maakt een firewall voor Azure Cosmos DB | Microsoft Docs
description: 'Azure CLI-Script voorbeeld: een firewall maken voor Azure Cosmos-DB'
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: sammvcple
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: d4bee4f37906033c96826b9662d2ba396325c792
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-hello-azure-cli"></a><span data-ttu-id="d29e1-103">Azure Cosmos DB: Maak een firewall met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d29e1-103">Azure Cosmos DB: Create a firewall using hello Azure CLI</span></span>

<span data-ttu-id="d29e1-104">Dit voorbeeldscript CLI maakt een firewall-beleid voor elk soort Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="d29e1-104">This sample CLI script creates a firewall policy for any kind of Azure Cosmos DB account.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d29e1-105">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d29e1-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d29e1-106">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="d29e1-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d29e1-107">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d29e1-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="d29e1-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="d29e1-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-create-firewall/secure-cosmosdb-create-firewall.sh?highlight=38-42 "Create an Azure Cosmos DB firewall")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d29e1-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="d29e1-109">Clean up deployment</span></span>

<span data-ttu-id="d29e1-110">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="d29e1-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d29e1-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="d29e1-111">Script explanation</span></span>

<span data-ttu-id="d29e1-112">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="d29e1-112">This script uses hello following commands.</span></span> <span data-ttu-id="d29e1-113">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="d29e1-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d29e1-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="d29e1-114">Command</span></span> | <span data-ttu-id="d29e1-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="d29e1-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d29e1-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="d29e1-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d29e1-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d29e1-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d29e1-118">AZ cosmosdb maken</span><span class="sxs-lookup"><span data-stu-id="d29e1-118">az cosmosdb create</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#create) | <span data-ttu-id="d29e1-119">Maakt een CosmosDB Azure-account.</span><span class="sxs-lookup"><span data-stu-id="d29e1-119">Creates an Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="d29e1-120">AZ cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="d29e1-120">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="d29e1-121">Een Azure-CosmosDB account tooinclude firewall-instellingen voor updates.</span><span class="sxs-lookup"><span data-stu-id="d29e1-121">Updates an Azure CosmosDB account tooinclude firewall settings.</span></span> |
| [<span data-ttu-id="d29e1-122">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="d29e1-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="d29e1-123">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="d29e1-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d29e1-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d29e1-124">Next steps</span></span>

<span data-ttu-id="d29e1-125">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d29e1-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d29e1-126">Extra Azure Cosmos DB CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Cosmos DB CLI documentatie](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d29e1-126">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
