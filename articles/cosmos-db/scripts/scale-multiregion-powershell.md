---
title: Azure PowerShell-Script-Multiregion replicatie voor de Azure DB die Cosmos | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - Multiregion replicatie voor Azure Cosmos-DB
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
ms.openlocfilehash: 3a469ba43e6c601f5eb0e13d588cd0bd4a0f8683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-powershell"></a><span data-ttu-id="78be2-103">Een databaseaccount Azure Cosmos DB in meerdere regio's worden gerepliceerd en het configureren van failover prioriteiten met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="78be2-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using PowerShell</span></span>

<span data-ttu-id="78be2-104">Dit voorbeeld elk soort account voor Azure DB die Cosmos-database in meerdere regio's worden gerepliceerd en failover prioriteiten met behulp van PowerShell configureert.</span><span class="sxs-lookup"><span data-stu-id="78be2-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="78be2-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="78be2-105">Sample script</span></span>

<span data-ttu-id="78be2-106">[!code-powershell[belangrijkste](../../../powershell_scripts/cosmosdb/replicate-database-multiple-regions/replicate-database-multiple-regions.ps1?highlight=37-44,47-48,51-55 "een Cosmos-DB Azure-account te repliceren over meerdere regio's")]</span><span class="sxs-lookup"><span data-stu-id="78be2-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/replicate-database-multiple-regions/replicate-database-multiple-regions.ps1?highlight=37-44,47-48,51-55 "Replicate an Azure Cosmos DB account across multiple regions")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="78be2-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="78be2-107">Clean up deployment</span></span>

<span data-ttu-id="78be2-108">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om te verwijderen van de resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="78be2-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="78be2-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="78be2-109">Script explanation</span></span>

<span data-ttu-id="78be2-110">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="78be2-110">This script uses the following commands.</span></span> <span data-ttu-id="78be2-111">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="78be2-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="78be2-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="78be2-112">Command</span></span> | <span data-ttu-id="78be2-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="78be2-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="78be2-114">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="78be2-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="78be2-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="78be2-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="78be2-116">Nieuwe AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="78be2-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="78be2-117">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="78be2-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="78be2-118">Set-AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="78be2-118">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="78be2-119">Hiermee wijzigt u de databaseaccount.</span><span class="sxs-lookup"><span data-stu-id="78be2-119">Modifies the database account.</span></span> |
| [<span data-ttu-id="78be2-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="78be2-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="78be2-121">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="78be2-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="78be2-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="78be2-122">Next steps</span></span>

<span data-ttu-id="78be2-123">Zie voor meer informatie over Azure PowerShell [documentatie van Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="78be2-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="78be2-124">Voorbeelden van extra Azure Cosmos DB PowerShell-script kunnen worden gevonden in de [Azure Cosmos DB PowerShell-scripts](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="78be2-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>