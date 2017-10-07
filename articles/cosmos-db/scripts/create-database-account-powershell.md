---
title: aaaAzure PowerShell Script-account maken voor een Azure Cosmos DB DocumentDB-API | Microsoft Docs
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
ms.openlocfilehash: f0751faeca3c1de5906b675e736c58f3d5beaea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-documentdb-api-account-using-powershell"></a><span data-ttu-id="4b4ed-103">Azure Cosmos DB: Een DocumentDB-API-account maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b4ed-103">Azure Cosmos DB: Create a DocumentDB API account using PowerShell</span></span>

<span data-ttu-id="4b4ed-104">Dit voorbeeld PowerShell-script maakt een Cosmos DB-API van Azure-account.</span><span class="sxs-lookup"><span data-stu-id="4b4ed-104">This sample PowerShell script creates an Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="4b4ed-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="4b4ed-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-and-configure-database/create-and-configure-database.ps1?highlight=9,12-15,18,21-23,26-29,32-37 "Create an Azure Cosmos DB account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4b4ed-106">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="4b4ed-106">Clean up deployment</span></span>

<span data-ttu-id="4b4ed-107">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="4b4ed-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="4b4ed-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="4b4ed-108">Script explanation</span></span>

<span data-ttu-id="4b4ed-109">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="4b4ed-109">This script uses hello following commands.</span></span> <span data-ttu-id="4b4ed-110">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="4b4ed-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4b4ed-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="4b4ed-111">Command</span></span> | <span data-ttu-id="4b4ed-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="4b4ed-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4b4ed-113">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4b4ed-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="4b4ed-114">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4b4ed-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4b4ed-115">Nieuwe AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="4b4ed-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="4b4ed-116">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="4b4ed-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="4b4ed-117">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4b4ed-117">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="4b4ed-118">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="4b4ed-118">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="4b4ed-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4b4ed-119">Next steps</span></span>

<span data-ttu-id="4b4ed-120">Zie voor meer informatie over hello Azure PowerShell [documentatie van Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="4b4ed-120">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="4b4ed-121">Voorbeelden van extra Azure Cosmos DB PowerShell-script kunnen u vinden in Hallo [Azure Cosmos DB PowerShell-scripts](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4b4ed-121">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
