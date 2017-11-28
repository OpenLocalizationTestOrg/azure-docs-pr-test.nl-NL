---
title: aaaPowerShell voorbeeld verplaatsen Azure SQL database-SQL elastische pool | Microsoft Docs
description: Azure PowerShell-voorbeeld script toomove een SQL-database tussen elastische pools met behulp van PowerShell
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
ms.openlocfilehash: 501e82ce93a31264d0625fb0243b4e44dcb2d007
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-elastic-pools-and-move-databases-between-elastic-pools"></a><span data-ttu-id="45b8f-103">Gebruik PowerShell toocreate elastische pools en databases verplaatsen tussen elastische pools</span><span class="sxs-lookup"><span data-stu-id="45b8f-103">Use PowerShell toocreate elastic pools and move databases between elastic pools</span></span>

<span data-ttu-id="45b8f-104">Voorbeeld van deze PowerShell-script maakt twee elastische pools en een database uit een elastische groep is verplaatst naar een andere elastische groep en vervolgens een database verplaatst buiten een prestatieniveau van elastische pool tooa één database.</span><span class="sxs-lookup"><span data-stu-id="45b8f-104">This PowerShell script example creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool tooa single database performance level.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="45b8f-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="45b8f-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="45b8f-106">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="45b8f-106">Clean up deployment</span></span>

<span data-ttu-id="45b8f-107">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="45b8f-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="45b8f-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="45b8f-108">Script explanation</span></span>

<span data-ttu-id="45b8f-109">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="45b8f-109">This script uses hello following commands.</span></span> <span data-ttu-id="45b8f-110">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="45b8f-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="45b8f-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="45b8f-111">Command</span></span> | <span data-ttu-id="45b8f-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="45b8f-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="45b8f-113">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="45b8f-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="45b8f-114">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="45b8f-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="45b8f-115">Nieuwe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="45b8f-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="45b8f-116">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="45b8f-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="45b8f-117">Nieuwe AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="45b8f-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="45b8f-118">Maakt een elastische pool in een logische server.</span><span class="sxs-lookup"><span data-stu-id="45b8f-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="45b8f-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="45b8f-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="45b8f-120">Maakt een database in een logische server als één of een gegroepeerde database.</span><span class="sxs-lookup"><span data-stu-id="45b8f-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="45b8f-121">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="45b8f-121">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="45b8f-122">Database-eigenschappen-updates of een database verplaatst naar, uit of tussen elastische pools.</span><span class="sxs-lookup"><span data-stu-id="45b8f-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="45b8f-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="45b8f-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="45b8f-124">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="45b8f-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="45b8f-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="45b8f-125">Next steps</span></span>

<span data-ttu-id="45b8f-126">Zie voor meer informatie over hello Azure PowerShell [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="45b8f-126">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="45b8f-127">Voorbeelden van aanvullende SQL Database PowerShell-script kunnen worden gevonden in Hallo [Azure SQL Database PowerShell-scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="45b8f-127">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
