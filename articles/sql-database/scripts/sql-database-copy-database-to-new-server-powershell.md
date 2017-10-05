---
title: "PowerShell voorbeeld-kopiëren-Azure SQL database-nieuwe server | Microsoft Docs"
description: "Azure PowerShell-voorbeeldscript om te kopiëren van een SQL-database naar een nieuwe server"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 005ea2e782f8e1cff29f743d9584eb2af2c77509
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-copy-a-sql-database-to-a-new-server"></a><span data-ttu-id="2d3d2-103">PowerShell gebruiken voor het kopiëren van een SQL-database naar een nieuwe server</span><span class="sxs-lookup"><span data-stu-id="2d3d2-103">Use PowerShell to copy a SQL database to a new server</span></span>

<span data-ttu-id="2d3d2-104">Voorbeeld van deze PowerShell-script maakt een kopie van een bestaande database in een nieuwe server.</span><span class="sxs-lookup"><span data-stu-id="2d3d2-104">This PowerShell script example creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-to-a-new-server"></a><span data-ttu-id="2d3d2-105">Een database kopiëren naar een nieuwe server</span><span class="sxs-lookup"><span data-stu-id="2d3d2-105">Copy a database to a new server</span></span>

<span data-ttu-id="2d3d2-106">[!code-powershell[belangrijkste](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "database kopiëren naar nieuwe server")]</span><span class="sxs-lookup"><span data-stu-id="2d3d2-106">[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database to new server")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2d3d2-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="2d3d2-107">Clean up deployment</span></span>

<span data-ttu-id="2d3d2-108">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om te verwijderen van de resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="2d3d2-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="2d3d2-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="2d3d2-109">Script explanation</span></span>

<span data-ttu-id="2d3d2-110">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="2d3d2-110">This script uses the following commands.</span></span> <span data-ttu-id="2d3d2-111">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="2d3d2-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2d3d2-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="2d3d2-112">Command</span></span> | <span data-ttu-id="2d3d2-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="2d3d2-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2d3d2-114">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2d3d2-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="2d3d2-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2d3d2-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2d3d2-116">Nieuwe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="2d3d2-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="2d3d2-117">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="2d3d2-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="2d3d2-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="2d3d2-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="2d3d2-119">Maakt een database in een logische server als één of een gegroepeerde database.</span><span class="sxs-lookup"><span data-stu-id="2d3d2-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="2d3d2-120">Nieuwe AzureRmSqlDatabaseCopy</span><span class="sxs-lookup"><span data-stu-id="2d3d2-120">New-AzureRmSqlDatabaseCopy</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | <span data-ttu-id="2d3d2-121">Maakt een kopie van een database die gebruikmaakt van de momentopname bij de huidige tijd.</span><span class="sxs-lookup"><span data-stu-id="2d3d2-121">Creates a copy of a database that uses the snapshot at the current time.</span></span> |
| [<span data-ttu-id="2d3d2-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2d3d2-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="2d3d2-123">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="2d3d2-123">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="2d3d2-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2d3d2-124">Next steps</span></span>

<span data-ttu-id="2d3d2-125">Zie voor meer informatie over Azure PowerShell [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2d3d2-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2d3d2-126">Voorbeelden van aanvullende SQL Database PowerShell-script kunnen worden gevonden in de [Azure SQL Database PowerShell-scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2d3d2-126">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
