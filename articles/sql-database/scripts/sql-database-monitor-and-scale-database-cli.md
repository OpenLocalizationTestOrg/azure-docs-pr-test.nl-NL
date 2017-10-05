---
title: CLI voorbeeld-monitor-scale-enkel Azure SQL database | Microsoft Docs
description: "Azure CLI-voorbeeldscript om te bewaken en schalen van één Azure SQL database"
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
ms.openlocfilehash: 01911b85268244a8fddb32aa726f8a870abbaf77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-monitor-and-scale-a-single-sql-database"></a><span data-ttu-id="a684f-103">CLI gebruiken om te bewaken en schalen van een enkele SQL-database</span><span class="sxs-lookup"><span data-stu-id="a684f-103">Use CLI to monitor and scale a single SQL database</span></span>

<span data-ttu-id="a684f-104">In dit voorbeeld van Azure CLI script schaalt één Azure SQL database naar een andere prestatieniveau na het uitvoeren van query's de informatie over de grootte van de database.</span><span class="sxs-lookup"><span data-stu-id="a684f-104">This Azure CLI script example scales a single Azure SQL database to a different performance level after querying the size information of the database.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a684f-105">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="a684f-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a684f-106">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="a684f-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="a684f-107">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a684f-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a684f-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="a684f-108">Sample script</span></span>

<span data-ttu-id="a684f-109">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "bewaken en schalen één SQL-Database")]</span><span class="sxs-lookup"><span data-stu-id="a684f-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a684f-110">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="a684f-110">Clean up deployment</span></span>

<span data-ttu-id="a684f-111">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om te verwijderen van de resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="a684f-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="a684f-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="a684f-112">Script explanation</span></span>

<span data-ttu-id="a684f-113">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="a684f-113">This script uses the following commands.</span></span> <span data-ttu-id="a684f-114">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="a684f-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a684f-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="a684f-115">Command</span></span> | <span data-ttu-id="a684f-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="a684f-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a684f-117">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="a684f-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a684f-118">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a684f-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a684f-119">AZ sql server maken</span><span class="sxs-lookup"><span data-stu-id="a684f-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="a684f-120">Maakt een logische server die als host fungeert voor een database.</span><span class="sxs-lookup"><span data-stu-id="a684f-120">Creates a logical server that hosts a database.</span></span> |
| [<span data-ttu-id="a684f-121">AZ sql db weergeven-gebruik</span><span class="sxs-lookup"><span data-stu-id="a684f-121">az sql db show-usage</span></span>](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | <span data-ttu-id="a684f-122">Toont de gebruiksgegevens van de grootte voor een database.</span><span class="sxs-lookup"><span data-stu-id="a684f-122">Shows the size usage information for a database.</span></span> |
| [<span data-ttu-id="a684f-123">AZ sql database-update</span><span class="sxs-lookup"><span data-stu-id="a684f-123">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="a684f-124">Updates van de database-eigenschappen (zoals het serviceniveau voor de servicelaag of prestaties) of een database verplaatst naar buiten of tussen elastische pools.</span><span class="sxs-lookup"><span data-stu-id="a684f-124">Updates database properties (such as the service tier or performance level) or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="a684f-125">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="a684f-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="a684f-126">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="a684f-126">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="a684f-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a684f-127">Next steps</span></span>

<span data-ttu-id="a684f-128">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a684f-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a684f-129">Voorbeelden van aanvullende SQL Database CLI-script kunnen worden gevonden in de [documentatie van Azure SQL Database](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a684f-129">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
