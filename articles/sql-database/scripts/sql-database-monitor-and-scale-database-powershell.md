---
title: PowerShell-voorbeeld-monitor-scale-enkel Azure SQL database | Microsoft Docs
description: "Azure PowerShell-voorbeeldscript om te bewaken en schalen van één Azure SQL database"
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
ms.openlocfilehash: 5d08335f4b1d6c5c6a120cbfb86ab2c62b79bb9f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-monitor-and-scale-a-single-sql-database"></a><span data-ttu-id="c98e2-103">PowerShell gebruiken om te bewaken en schalen van een enkele SQL-database</span><span class="sxs-lookup"><span data-stu-id="c98e2-103">Use PowerShell to monitor and scale a single SQL database</span></span>

<span data-ttu-id="c98e2-104">Voorbeeld van deze PowerShell-script bewaakt de maatstaven voor prestaties van een database naar een hoger prestatieniveau op schaal en een waarschuwingsregel maakt op een van de maatstaven voor prestaties.</span><span class="sxs-lookup"><span data-stu-id="c98e2-104">This PowerShell script example monitors the performance metrics of a database, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="c98e2-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="c98e2-105">Sample script</span></span>

<span data-ttu-id="c98e2-106">[!code-powershell[belangrijkste](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "bewaken en schalen één SQL-Database")]</span><span class="sxs-lookup"><span data-stu-id="c98e2-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c98e2-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="c98e2-107">Clean up deployment</span></span>

<span data-ttu-id="c98e2-108">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om te verwijderen van de resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="c98e2-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="c98e2-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="c98e2-109">Script explanation</span></span>

<span data-ttu-id="c98e2-110">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="c98e2-110">This script uses the following commands.</span></span> <span data-ttu-id="c98e2-111">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="c98e2-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c98e2-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="c98e2-112">Command</span></span> | <span data-ttu-id="c98e2-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="c98e2-113">Notes</span></span> |
|---|---|
 [<span data-ttu-id="c98e2-114">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c98e2-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c98e2-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c98e2-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c98e2-116">Nieuwe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="c98e2-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="c98e2-117">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="c98e2-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="c98e2-118">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="c98e2-118">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="c98e2-119">Toont de gebruiksgegevens van de grootte voor de database.</span><span class="sxs-lookup"><span data-stu-id="c98e2-119">Shows the size usage information for the database.</span></span>|
| [<span data-ttu-id="c98e2-120">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="c98e2-120">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="c98e2-121">Database-eigenschappen-updates of een database verplaatst naar, uit of tussen elastische pools.</span><span class="sxs-lookup"><span data-stu-id="c98e2-121">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="c98e2-122">Voeg AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="c98e2-122">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="c98e2-123">Hiermee stelt u een waarschuwingsregel automatisch dtu's in de toekomst te bewaken.</span><span class="sxs-lookup"><span data-stu-id="c98e2-123">Sets an alert rule to automatically monitor DTUs in the future.</span></span> |
| [<span data-ttu-id="c98e2-124">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c98e2-124">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c98e2-125">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="c98e2-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="c98e2-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c98e2-126">Next steps</span></span>

<span data-ttu-id="c98e2-127">Zie voor meer informatie over Azure PowerShell [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c98e2-127">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c98e2-128">Voorbeelden van aanvullende SQL Database PowerShell-script kunnen worden gevonden in de [Azure SQL Database PowerShell-scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c98e2-128">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
