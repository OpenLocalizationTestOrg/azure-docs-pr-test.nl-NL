---
title: aaaCLI voorbeeld-monitor-scale-enkel Azure SQL database | Microsoft Docs
description: "Voorbeeld van Azure CLI toomonitor script en schalen van één Azure SQL database"
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
ms.openlocfilehash: 36031ddd46a947a80fe37884858a84eb66217270
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomonitor-and-scale-a-single-sql-database"></a><span data-ttu-id="37156-103">Gebruik CLI toomonitor en schalen van een enkele SQL-database</span><span class="sxs-lookup"><span data-stu-id="37156-103">Use CLI toomonitor and scale a single SQL database</span></span>

<span data-ttu-id="37156-104">In dit voorbeeld van Azure CLI script schaalt één Azure SQL database tooa verschillende prestatieniveau nadat het opvragen van informatie over de Hallo grootte van Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="37156-104">This Azure CLI script example scales a single Azure SQL database tooa different performance level after querying hello size information of hello database.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="37156-105">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="37156-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="37156-106">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="37156-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="37156-107">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="37156-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="37156-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="37156-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="37156-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="37156-109">Clean up deployment</span></span>

<span data-ttu-id="37156-110">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="37156-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="37156-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="37156-111">Script explanation</span></span>

<span data-ttu-id="37156-112">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="37156-112">This script uses hello following commands.</span></span> <span data-ttu-id="37156-113">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="37156-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="37156-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="37156-114">Command</span></span> | <span data-ttu-id="37156-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="37156-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="37156-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="37156-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="37156-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="37156-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="37156-118">AZ sql server maken</span><span class="sxs-lookup"><span data-stu-id="37156-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="37156-119">Maakt een logische server die als host fungeert voor een database.</span><span class="sxs-lookup"><span data-stu-id="37156-119">Creates a logical server that hosts a database.</span></span> |
| [<span data-ttu-id="37156-120">AZ sql db weergeven-gebruik</span><span class="sxs-lookup"><span data-stu-id="37156-120">az sql db show-usage</span></span>](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | <span data-ttu-id="37156-121">Bevat informatie over het gebruik Hallo grootte voor een database.</span><span class="sxs-lookup"><span data-stu-id="37156-121">Shows hello size usage information for a database.</span></span> |
| [<span data-ttu-id="37156-122">AZ sql database-update</span><span class="sxs-lookup"><span data-stu-id="37156-122">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="37156-123">Updates van de database-eigenschappen (zoals Hallo laag of prestaties serviceniveau) of een database verplaatst naar buiten of tussen elastische pools.</span><span class="sxs-lookup"><span data-stu-id="37156-123">Updates database properties (such as hello service tier or performance level) or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="37156-124">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="37156-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="37156-125">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="37156-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="37156-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="37156-126">Next steps</span></span>

<span data-ttu-id="37156-127">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="37156-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="37156-128">Voorbeelden van aanvullende SQL Database CLI-script kunnen u vinden in Hallo [documentatie van Azure SQL Database](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="37156-128">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
