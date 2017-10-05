---
title: PowerShell voorbeeld verplaatsen Azure SQL database-SQL elastische pool | Microsoft Docs
description: Azure PowerShell-voorbeeldscript een SQL-database verplaatsen tussen elastische pools met behulp van PowerShell
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 58f14dc668f25f17e93fcaf30f72b15a46d71484
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-create-elastic-pools-and-move-databases-between-elastic-pools"></a><span data-ttu-id="911bd-103">PowerShell gebruiken voor het maken van elastische pools en databases verplaatsen tussen elastische pools</span><span class="sxs-lookup"><span data-stu-id="911bd-103">Use PowerShell to create elastic pools and move databases between elastic pools</span></span>

<span data-ttu-id="911bd-104">Voorbeeld van deze PowerShell-script maakt twee elastische pools en een database uit een elastische groep is verplaatst naar een andere elastische pool en gaat vervolgens door een database buiten een elastische groep naar een prestatieniveau van één database.</span><span class="sxs-lookup"><span data-stu-id="911bd-104">This PowerShell script example creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool to a single database performance level.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="911bd-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="911bd-105">Sample script</span></span>

<span data-ttu-id="911bd-106">[!code-powershell[belangrijkste](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "verplaatsen van de database tussen mediagroepen")]</span><span class="sxs-lookup"><span data-stu-id="911bd-106">[!code-powershell[main](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="911bd-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="911bd-107">Clean up deployment</span></span>

<span data-ttu-id="911bd-108">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om te verwijderen van de resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="911bd-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="911bd-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="911bd-109">Script explanation</span></span>

<span data-ttu-id="911bd-110">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="911bd-110">This script uses the following commands.</span></span> <span data-ttu-id="911bd-111">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="911bd-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="911bd-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="911bd-112">Command</span></span> | <span data-ttu-id="911bd-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="911bd-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="911bd-114">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="911bd-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="911bd-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="911bd-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="911bd-116">Nieuwe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="911bd-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="911bd-117">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="911bd-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="911bd-118">Nieuwe AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="911bd-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="911bd-119">Maakt een elastische pool in een logische server.</span><span class="sxs-lookup"><span data-stu-id="911bd-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="911bd-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="911bd-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="911bd-121">Maakt een database in een logische server als één of een gegroepeerde database.</span><span class="sxs-lookup"><span data-stu-id="911bd-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="911bd-122">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="911bd-122">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="911bd-123">Database-eigenschappen-updates of een database verplaatst naar, uit of tussen elastische pools.</span><span class="sxs-lookup"><span data-stu-id="911bd-123">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="911bd-124">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="911bd-124">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="911bd-125">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="911bd-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="911bd-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="911bd-126">Next steps</span></span>

<span data-ttu-id="911bd-127">Zie voor meer informatie over Azure PowerShell [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="911bd-127">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="911bd-128">Voorbeelden van aanvullende SQL Database PowerShell-script kunnen worden gevonden in de [Azure SQL Database PowerShell-scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="911bd-128">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
