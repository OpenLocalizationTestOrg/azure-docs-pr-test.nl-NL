---
title: Azure PowerShell-Script Get-Azure Cosmos DB-verbindingsreeks voor MongoDB-apps | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - Get Azure Cosmos DB-verbindingsreeks voor MongoDB-apps
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
ms.openlocfilehash: e44e35cc7d11db48cd82e470ce8226b3c8cc220a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-powershell"></a><span data-ttu-id="25d79-103">Een Azure DB die Cosmos-verbindingsreeks ophalen voor MongoDB-apps met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="25d79-103">Get an Azure Cosmos DB connection string for MongoDB apps using PowerShell</span></span>

<span data-ttu-id="25d79-104">Dit voorbeeld wordt een Azure DB die Cosmos-verbindingsreeks voor MongoDB-apps met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25d79-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="25d79-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="25d79-105">Sample script</span></span>

<span data-ttu-id="25d79-106">[!code-powershell[belangrijkste](../../../powershell_scripts/cosmosdb/get-mongodb-connection-string/get-mongodb-connection-string.ps1?highlight=37-41 "de MongoDB-verbindingsreeks ophalen uit een Cosmos-DB Azure-account")]</span><span class="sxs-lookup"><span data-stu-id="25d79-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-mongodb-connection-string/get-mongodb-connection-string.ps1?highlight=37-41 "Get the MongoDB connection string from an Azure Cosmos DB account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="25d79-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="25d79-107">Clean up deployment</span></span>

<span data-ttu-id="25d79-108">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om te verwijderen van de resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="25d79-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="25d79-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="25d79-109">Script explanation</span></span>

<span data-ttu-id="25d79-110">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="25d79-110">This script uses the following commands.</span></span> <span data-ttu-id="25d79-111">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="25d79-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="25d79-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="25d79-112">Command</span></span> | <span data-ttu-id="25d79-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="25d79-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="25d79-114">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="25d79-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="25d79-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="25d79-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="25d79-116">Nieuwe AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="25d79-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="25d79-117">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="25d79-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="25d79-118">Aanroepen AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="25d79-118">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="25d79-119">Hiermee wordt een actie op de CosmosDB Azure-account.</span><span class="sxs-lookup"><span data-stu-id="25d79-119">Invokes an action on the Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="25d79-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="25d79-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="25d79-121">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="25d79-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="25d79-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="25d79-122">Next steps</span></span>

<span data-ttu-id="25d79-123">Zie voor meer informatie over Azure PowerShell [documentatie van Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="25d79-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="25d79-124">Voorbeelden van extra Azure Cosmos DB PowerShell-script kunnen worden gevonden in de [Azure Cosmos DB PowerShell-scripts](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="25d79-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>