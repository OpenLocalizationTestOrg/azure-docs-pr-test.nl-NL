---
title: aaaCLI voorbeeld verplaatsen Azure SQL database-SQL elastische pool | Microsoft Docs
description: Azure CLI voorbeeld script toomove een SQL-database in een elastische SQL-groep
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
ms.date: 07/05/2017
ms.author: janeng
ms.openlocfilehash: 841eb57d2d49612c3fadd3a6424a2b0309c69719
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomove-an-azure-sql-database-in-a-sql-elastic-pool"></a><span data-ttu-id="f1f57-103">Gebruik CLI toomove een Azure SQL database in een elastische SQL-groep</span><span class="sxs-lookup"><span data-stu-id="f1f57-103">Use CLI toomove an Azure SQL database in a SQL elastic pool</span></span>

<span data-ttu-id="f1f57-104">In dit voorbeeld Azure CLI-script maakt twee elastische pools en een Azure SQL database in een elastische SQL-groep is verplaatst naar een andere elastische SQL-groep en gaat vervolgens Hallo database buiten het prestatieniveau van elastische pool tooa één Azure-database.</span><span class="sxs-lookup"><span data-stu-id="f1f57-104">This Azure CLI script example creates two elastic pools and moves an Azure SQL database from one SQL elastic pool into another SQL elastic pool, and then moves hello database out of elastic pool tooa single Azure database performance level.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f1f57-105">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f1f57-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f1f57-106">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="f1f57-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f1f57-107">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f1f57-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f1f57-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="f1f57-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f1f57-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="f1f57-109">Clean up deployment</span></span>

<span data-ttu-id="f1f57-110">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="f1f57-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f1f57-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="f1f57-111">Script explanation</span></span>

<span data-ttu-id="f1f57-112">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="f1f57-112">This script uses hello following commands.</span></span> <span data-ttu-id="f1f57-113">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="f1f57-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f1f57-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="f1f57-114">Command</span></span> | <span data-ttu-id="f1f57-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="f1f57-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f1f57-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="f1f57-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f1f57-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f1f57-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f1f57-118">AZ sql server maken</span><span class="sxs-lookup"><span data-stu-id="f1f57-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="f1f57-119">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="f1f57-119">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="f1f57-120">elastische sql van AZ-toepassingen maken</span><span class="sxs-lookup"><span data-stu-id="f1f57-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="f1f57-121">Maakt een elastische pool binnen Hallo logische server.</span><span class="sxs-lookup"><span data-stu-id="f1f57-121">Creates an elastic pool within hello logical server.</span></span> |
| [<span data-ttu-id="f1f57-122">AZ sql-database maken</span><span class="sxs-lookup"><span data-stu-id="f1f57-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="f1f57-123">Maakt een database in een logische server als één of een gegroepeerde database.</span><span class="sxs-lookup"><span data-stu-id="f1f57-123">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="f1f57-124">AZ sql database-update</span><span class="sxs-lookup"><span data-stu-id="f1f57-124">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="f1f57-125">Database-eigenschappen-updates of een database verplaatst naar, uit of tussen elastische pools.</span><span class="sxs-lookup"><span data-stu-id="f1f57-125">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="f1f57-126">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="f1f57-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="f1f57-127">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="f1f57-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f1f57-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f1f57-128">Next steps</span></span>

<span data-ttu-id="f1f57-129">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f1f57-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f1f57-130">Voorbeelden van aanvullende SQL Database CLI-script kunnen u vinden in Hallo [documentatie van Azure SQL Database](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f1f57-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>


