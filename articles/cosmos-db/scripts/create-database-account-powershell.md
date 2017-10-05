---
title: Azure PowerShell Script-account maken voor een Azure Cosmos DB DocumentDB-API | Microsoft Docs
description: 'Azure PowerShell-Script voorbeeld: een API van Azure Cosmos DB DocumentDB-account maken'
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 9b54236ce3446fe1c6a2a30b31f6d91ad43a92d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-create-a-documentdb-api-account-using-powershell"></a><span data-ttu-id="8d40a-103">Azure Cosmos DB: Een DocumentDB-API-account maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d40a-103">Azure Cosmos DB: Create a DocumentDB API account using PowerShell</span></span>

<span data-ttu-id="8d40a-104">Dit voorbeeld PowerShell-script maakt een Cosmos DB-API van Azure-account.</span><span class="sxs-lookup"><span data-stu-id="8d40a-104">This sample PowerShell script creates an Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="8d40a-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="8d40a-105">Sample script</span></span>

<span data-ttu-id="8d40a-106">[!code-powershell[belangrijkste](../../../powershell_scripts/cosmosdb/create-and-configure-database/create-and-configure-database.ps1?highlight=9,12-15,18,21-23,26-29,32-37 "een Cosmos-DB Azure-account maken")]</span><span class="sxs-lookup"><span data-stu-id="8d40a-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-and-configure-database/create-and-configure-database.ps1?highlight=9,12-15,18,21-23,26-29,32-37 "Create an Azure Cosmos DB account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="8d40a-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="8d40a-107">Clean up deployment</span></span>

<span data-ttu-id="8d40a-108">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om te verwijderen van de resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8d40a-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="8d40a-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="8d40a-109">Script explanation</span></span>

<span data-ttu-id="8d40a-110">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="8d40a-110">This script uses the following commands.</span></span> <span data-ttu-id="8d40a-111">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="8d40a-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8d40a-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="8d40a-112">Command</span></span> | <span data-ttu-id="8d40a-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="8d40a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8d40a-114">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8d40a-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="8d40a-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8d40a-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8d40a-116">Nieuwe AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="8d40a-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="8d40a-117">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="8d40a-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="8d40a-118">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8d40a-118">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="8d40a-119">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="8d40a-119">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="8d40a-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8d40a-120">Next steps</span></span>

<span data-ttu-id="8d40a-121">Zie voor meer informatie over Azure PowerShell [documentatie van Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="8d40a-121">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="8d40a-122">Voorbeelden van extra Azure Cosmos DB PowerShell-script kunnen worden gevonden in de [Azure Cosmos DB PowerShell-scripts](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8d40a-122">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>