---
title: CLI-voorbeeld wordt een SQL elastische pool Azure SQL Database | Microsoft Docs
description: Azure CLI-voorbeeldscript voor het schalen van een elastische SQL-groep in Azure SQL Database
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 888d2b7b7c118fede82d39881570a3b3d7b09961
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="use-cli-to-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="3a661-103">CLI gebruiken voor het schalen van een elastische SQL-groep in Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="3a661-103">Use CLI to scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="3a661-104">In dit voorbeeld van Azure CLI script SQL elastische pools maakt, verplaatst gegroepeerde databases en elastische pool prestatieniveaus wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="3a661-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3a661-105">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="3a661-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3a661-106">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="3a661-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="3a661-107">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3a661-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3a661-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="3a661-108">Sample script</span></span>

<span data-ttu-id="3a661-109">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "verplaatsen van de database tussen mediagroepen")]</span><span class="sxs-lookup"><span data-stu-id="3a661-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="3a661-110">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="3a661-110">Clean up deployment</span></span>

<span data-ttu-id="3a661-111">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om te verwijderen van de resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="3a661-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="3a661-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="3a661-112">Script explanation</span></span>

<span data-ttu-id="3a661-113">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, logische server, SQL-Database en firewall-regels.</span><span class="sxs-lookup"><span data-stu-id="3a661-113">This script uses the following commands to create a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="3a661-114">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="3a661-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3a661-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="3a661-115">Command</span></span> | <span data-ttu-id="3a661-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="3a661-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3a661-117">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="3a661-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3a661-118">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3a661-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3a661-119">AZ sql server maken</span><span class="sxs-lookup"><span data-stu-id="3a661-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="3a661-120">Maakt een logische server die als host fungeert voor de SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="3a661-120">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="3a661-121">elastische sql van AZ-toepassingen maken</span><span class="sxs-lookup"><span data-stu-id="3a661-121">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="3a661-122">Maakt een pool voor elastische database in de logische server.</span><span class="sxs-lookup"><span data-stu-id="3a661-122">Creates an elastic database pool within the logical server.</span></span> |
| [<span data-ttu-id="3a661-123">AZ sql-database maken</span><span class="sxs-lookup"><span data-stu-id="3a661-123">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="3a661-124">De SQL-Database wordt gemaakt in de logische server.</span><span class="sxs-lookup"><span data-stu-id="3a661-124">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="3a661-125">update van AZ sql elastische pools</span><span class="sxs-lookup"><span data-stu-id="3a661-125">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="3a661-126">Een pool voor elastische database updates, het toegewezen aantal edtu's in dit voorbeeld wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="3a661-126">Updates an elastic database pool, in this example changes the assigned eDTU.</span></span> |
| [<span data-ttu-id="3a661-127">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="3a661-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="3a661-128">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="3a661-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3a661-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3a661-129">Next steps</span></span>

<span data-ttu-id="3a661-130">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3a661-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3a661-131">Voorbeelden van aanvullende SQL Database CLI-script kunnen worden gevonden in de [documentatie van Azure SQL Database](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3a661-131">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
