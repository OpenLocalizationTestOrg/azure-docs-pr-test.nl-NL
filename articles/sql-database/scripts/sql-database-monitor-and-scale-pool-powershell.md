---
title: PowerShell voorbeeld-monitor-scale-SQL elastische pool Azure SQL Database | Microsoft Docs
description: Azure PowerShell-voorbeeldscript om te bewaken en schalen van een elastische SQL-groep in Azure SQL Database
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
ms.openlocfilehash: 7b6a5bd43aadbed33882cf0736ec70436ffdb47b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-monitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="a7af4-103">PowerShell gebruiken om te bewaken en schalen van een elastische SQL-groep in Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="a7af4-103">Use PowerShell to monitor and scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="a7af4-104">Voorbeeld van deze PowerShell-script de maatstaven voor prestaties van een pool voor elastische bewaakt, naar een hoger prestatieniveau op schaal en een waarschuwingsregel maakt op een van de maatstaven voor prestaties.</span><span class="sxs-lookup"><span data-stu-id="a7af4-104">This PowerShell script example monitors the performance metrics of an elastic pool, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="a7af4-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="a7af4-105">Sample script</span></span>

<span data-ttu-id="a7af4-106">[!code-powershell[belangrijkste](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "bewaken en schalen één SQL-Database")]</span><span class="sxs-lookup"><span data-stu-id="a7af4-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a7af4-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="a7af4-107">Clean up deployment</span></span>

<span data-ttu-id="a7af4-108">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om te verwijderen van de resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="a7af4-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="a7af4-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="a7af4-109">Script explanation</span></span>

<span data-ttu-id="a7af4-110">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="a7af4-110">This script uses the following commands.</span></span> <span data-ttu-id="a7af4-111">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="a7af4-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a7af4-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="a7af4-112">Command</span></span> | <span data-ttu-id="a7af4-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="a7af4-113">Notes</span></span> |
|---|---|
 [<span data-ttu-id="a7af4-114">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a7af4-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a7af4-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a7af4-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a7af4-116">Nieuwe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="a7af4-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="a7af4-117">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="a7af4-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="a7af4-118">Nieuwe AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="a7af4-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="a7af4-119">Maakt een elastische pool in een logische server.</span><span class="sxs-lookup"><span data-stu-id="a7af4-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="a7af4-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="a7af4-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="a7af4-121">Maakt een database in een logische server als één of een gegroepeerde database.</span><span class="sxs-lookup"><span data-stu-id="a7af4-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="a7af4-122">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="a7af4-122">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="a7af4-123">Toont de gebruiksgegevens van de grootte voor de database.</span><span class="sxs-lookup"><span data-stu-id="a7af4-123">Shows the size usage information for the database.</span></span>|
| [<span data-ttu-id="a7af4-124">Voeg AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="a7af4-124">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="a7af4-125">Wordt toegevoegd of updates van een waarschuwingsregel op basis van metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="a7af4-125">Adds or updates a metric-based alert rule.</span></span> |
| [<span data-ttu-id="a7af4-126">Set-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="a7af4-126">Set-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | <span data-ttu-id="a7af4-127">Eigenschappen van de elastische groep updates</span><span class="sxs-lookup"><span data-stu-id="a7af4-127">Updates elastic pool properties</span></span> |
| [<span data-ttu-id="a7af4-128">Voeg AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="a7af4-128">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="a7af4-129">Hiermee stelt u een waarschuwingsregel automatisch dtu's in de toekomst te bewaken.</span><span class="sxs-lookup"><span data-stu-id="a7af4-129">Sets an alert rule to automatically monitor DTUs in the future.</span></span> |
| [<span data-ttu-id="a7af4-130">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a7af4-130">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="a7af4-131">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="a7af4-131">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="a7af4-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a7af4-132">Next steps</span></span>

<span data-ttu-id="a7af4-133">Zie voor meer informatie over Azure PowerShell [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a7af4-133">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a7af4-134">Voorbeelden van aanvullende SQL Database PowerShell-script kunnen worden gevonden in de [Azure SQL Database PowerShell-scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a7af4-134">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
