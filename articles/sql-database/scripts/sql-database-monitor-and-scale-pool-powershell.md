---
title: aaaPowerShell voorbeeld-monitor-scale-SQL elastische pool-Azure SQL Database | Microsoft Docs
description: Voorbeeld van een Azure PowerShell script toomonitor en schalen van een elastische SQL-groep in Azure SQL Database
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
ms.openlocfilehash: 149a45174ccb8072ea21753364196c7f98fd4101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="a9a8f-103">Gebruik PowerShell toomonitor en schalen van een elastische SQL-groep in Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="a9a8f-103">Use PowerShell toomonitor and scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="a9a8f-104">Voorbeeld van deze PowerShell-script monitors Hallo maatstaven voor prestaties van een elastische pool tooa hoger prestatieniveau op schaal en een waarschuwingsregel maakt op een Hallo-maatstaven voor prestaties.</span><span class="sxs-lookup"><span data-stu-id="a9a8f-104">This PowerShell script example monitors hello performance metrics of an elastic pool, scales it tooa higher performance level, and creates an alert rule on one of hello performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="a9a8f-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="a9a8f-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a9a8f-106">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="a9a8f-106">Clean up deployment</span></span>

<span data-ttu-id="a9a8f-107">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="a9a8f-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="a9a8f-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="a9a8f-108">Script explanation</span></span>

<span data-ttu-id="a9a8f-109">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="a9a8f-109">This script uses hello following commands.</span></span> <span data-ttu-id="a9a8f-110">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="a9a8f-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a9a8f-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="a9a8f-111">Command</span></span> | <span data-ttu-id="a9a8f-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="a9a8f-112">Notes</span></span> |
|---|---|
 [<span data-ttu-id="a9a8f-113">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a9a8f-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a9a8f-114">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a9a8f-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a9a8f-115">Nieuwe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="a9a8f-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="a9a8f-116">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="a9a8f-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="a9a8f-117">Nieuwe AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="a9a8f-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="a9a8f-118">Maakt een elastische pool in een logische server.</span><span class="sxs-lookup"><span data-stu-id="a9a8f-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="a9a8f-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="a9a8f-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="a9a8f-120">Maakt een database in een logische server als één of een gegroepeerde database.</span><span class="sxs-lookup"><span data-stu-id="a9a8f-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="a9a8f-121">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="a9a8f-121">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="a9a8f-122">Toont informatie over het gebruik Hallo grootte voor Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="a9a8f-122">Shows hello size usage information for hello database.</span></span>|
| [<span data-ttu-id="a9a8f-123">Voeg AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="a9a8f-123">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="a9a8f-124">Wordt toegevoegd of updates van een waarschuwingsregel op basis van metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="a9a8f-124">Adds or updates a metric-based alert rule.</span></span> |
| [<span data-ttu-id="a9a8f-125">Set-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="a9a8f-125">Set-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | <span data-ttu-id="a9a8f-126">Eigenschappen van de elastische groep updates</span><span class="sxs-lookup"><span data-stu-id="a9a8f-126">Updates elastic pool properties</span></span> |
| [<span data-ttu-id="a9a8f-127">Voeg AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="a9a8f-127">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="a9a8f-128">Hiermee stelt u een waarschuwingsregel tooautomatically monitor dtu's in Hallo toekomstige.</span><span class="sxs-lookup"><span data-stu-id="a9a8f-128">Sets an alert rule tooautomatically monitor DTUs in hello future.</span></span> |
| [<span data-ttu-id="a9a8f-129">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a9a8f-129">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="a9a8f-130">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="a9a8f-130">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="a9a8f-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a9a8f-131">Next steps</span></span>

<span data-ttu-id="a9a8f-132">Zie voor meer informatie over hello Azure PowerShell [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a9a8f-132">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a9a8f-133">Voorbeelden van aanvullende SQL Database PowerShell-script kunnen worden gevonden in Hallo [Azure SQL Database PowerShell-scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a9a8f-133">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
