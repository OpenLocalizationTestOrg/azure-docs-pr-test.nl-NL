---
title: aaaCLI voorbeeld wordt een SQL elastische pool Azure SQL Database | Microsoft Docs
description: Azure CLI voorbeeld script tooscale een elastische SQL-groep in Azure SQL Database
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
ms.openlocfilehash: 436128b8183213f78b9abc2ec46efe2a3ed3c37c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-tooscale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="45165-103">CLI-tooscale een elastische SQL-groep in Azure SQL Database gebruiken</span><span class="sxs-lookup"><span data-stu-id="45165-103">Use CLI tooscale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="45165-104">In dit voorbeeld van Azure CLI script SQL elastische pools maakt, verplaatst gegroepeerde databases en elastische pool prestatieniveaus wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="45165-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="45165-105">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="45165-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="45165-106">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="45165-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="45165-107">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="45165-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="45165-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="45165-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="45165-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="45165-109">Clean up deployment</span></span>

<span data-ttu-id="45165-110">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="45165-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="45165-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="45165-111">Script explanation</span></span>

<span data-ttu-id="45165-112">Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, logische server, SQL-Database en firewallregels te volgen.</span><span class="sxs-lookup"><span data-stu-id="45165-112">This script uses hello following commands toocreate a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="45165-113">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="45165-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="45165-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="45165-114">Command</span></span> | <span data-ttu-id="45165-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="45165-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="45165-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="45165-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="45165-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="45165-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="45165-118">AZ sql server maken</span><span class="sxs-lookup"><span data-stu-id="45165-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="45165-119">Maakt een logische server dat hosts Hallo SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="45165-119">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="45165-120">elastische sql van AZ-toepassingen maken</span><span class="sxs-lookup"><span data-stu-id="45165-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="45165-121">Maakt een pool voor elastische databases binnen Hallo logische server.</span><span class="sxs-lookup"><span data-stu-id="45165-121">Creates an elastic database pool within hello logical server.</span></span> |
| [<span data-ttu-id="45165-122">AZ sql-database maken</span><span class="sxs-lookup"><span data-stu-id="45165-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="45165-123">Hallo SQL-Database in Hallo logische server gemaakt.</span><span class="sxs-lookup"><span data-stu-id="45165-123">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="45165-124">update van AZ sql elastische pools</span><span class="sxs-lookup"><span data-stu-id="45165-124">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="45165-125">Een pool voor elastische database, in dit voorbeeld wijzigingen Hallo toegewezen eDTU-updates.</span><span class="sxs-lookup"><span data-stu-id="45165-125">Updates an elastic database pool, in this example changes hello assigned eDTU.</span></span> |
| [<span data-ttu-id="45165-126">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="45165-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="45165-127">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="45165-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="45165-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="45165-128">Next steps</span></span>

<span data-ttu-id="45165-129">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="45165-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="45165-130">Voorbeelden van aanvullende SQL Database CLI-script kunnen u vinden in Hallo [documentatie van Azure SQL Database](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="45165-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
