---
title: PowerShell Script-maakt een firewall voor Azure Cosmos DB aaaAzure | Microsoft Docs
description: 'Azure PowerShell-Script voorbeeld: een firewall maken voor Azure Cosmos-DB'
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
ms.openlocfilehash: 00dd2dd847c7ed0e35f5555c2b87b90977f137f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-powershell"></a><span data-ttu-id="c4e90-103">Azure Cosmos DB: Maak een firewall met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4e90-103">Azure Cosmos DB: Create a firewall using PowerShell</span></span>

<span data-ttu-id="c4e90-104">Dit voorbeeld PowerShell-script maakt een firewall voor elk soort Cosmos DB-API van Azure-account.</span><span class="sxs-lookup"><span data-stu-id="c4e90-104">This sample PowerShell script creates a firewall for any kind of Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="c4e90-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="c4e90-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "Create a firewall for Azure Cosmos DB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c4e90-106">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="c4e90-106">Clean up deployment</span></span>

<span data-ttu-id="c4e90-107">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="c4e90-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="c4e90-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="c4e90-108">Script explanation</span></span>

<span data-ttu-id="c4e90-109">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="c4e90-109">This script uses hello following commands.</span></span> <span data-ttu-id="c4e90-110">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="c4e90-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c4e90-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="c4e90-111">Command</span></span> | <span data-ttu-id="c4e90-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="c4e90-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c4e90-113">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c4e90-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="c4e90-114">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c4e90-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c4e90-115">Nieuwe AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="c4e90-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="c4e90-116">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="c4e90-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="c4e90-117">Set-AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="c4e90-117">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="c4e90-118">Hallo-databaseaccount wijzigt.</span><span class="sxs-lookup"><span data-stu-id="c4e90-118">Modifies hello database account.</span></span> |
| [<span data-ttu-id="c4e90-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c4e90-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="c4e90-120">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="c4e90-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="c4e90-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c4e90-121">Next steps</span></span>

<span data-ttu-id="c4e90-122">Zie voor meer informatie over hello Azure PowerShell [documentatie van Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="c4e90-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="c4e90-123">Voorbeelden van extra Azure Cosmos DB PowerShell-script kunnen u vinden in Hallo [Azure Cosmos DB PowerShell-scripts](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c4e90-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
