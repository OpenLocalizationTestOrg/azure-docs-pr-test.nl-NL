---
title: aaaPowerShell voorbeeld-monitor-scale-enkel Azure SQL database | Microsoft Docs
description: "Voorbeeld van een Azure PowerShell script toomonitor en schalen van één Azure SQL database"
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
ms.openlocfilehash: bd8f880fb47b1360ae4962d2b039faa742de258e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-single-sql-database"></a><span data-ttu-id="f2cf1-103">Gebruik PowerShell toomonitor en schalen van een enkele SQL-database</span><span class="sxs-lookup"><span data-stu-id="f2cf1-103">Use PowerShell toomonitor and scale a single SQL database</span></span>

<span data-ttu-id="f2cf1-104">Voorbeeld van deze PowerShell-script monitors Hallo maatstaven voor prestaties van een database, op schaal tooa hoger prestatieniveau en een waarschuwingsregel maakt op een van de maatstaven voor prestaties Hallo.</span><span class="sxs-lookup"><span data-stu-id="f2cf1-104">This PowerShell script example monitors hello performance metrics of a database, scales it tooa higher performance level, and creates an alert rule on one of hello performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="f2cf1-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="f2cf1-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f2cf1-106">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="f2cf1-106">Clean up deployment</span></span>

<span data-ttu-id="f2cf1-107">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="f2cf1-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="f2cf1-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="f2cf1-108">Script explanation</span></span>

<span data-ttu-id="f2cf1-109">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="f2cf1-109">This script uses hello following commands.</span></span> <span data-ttu-id="f2cf1-110">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="f2cf1-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f2cf1-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="f2cf1-111">Command</span></span> | <span data-ttu-id="f2cf1-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="f2cf1-112">Notes</span></span> |
|---|---|
 [<span data-ttu-id="f2cf1-113">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f2cf1-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f2cf1-114">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f2cf1-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f2cf1-115">Nieuwe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="f2cf1-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="f2cf1-116">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="f2cf1-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="f2cf1-117">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="f2cf1-117">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="f2cf1-118">Toont informatie over het gebruik Hallo grootte voor Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="f2cf1-118">Shows hello size usage information for hello database.</span></span>|
| [<span data-ttu-id="f2cf1-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="f2cf1-119">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="f2cf1-120">Database-eigenschappen-updates of een database verplaatst naar, uit of tussen elastische pools.</span><span class="sxs-lookup"><span data-stu-id="f2cf1-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="f2cf1-121">Voeg AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="f2cf1-121">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="f2cf1-122">Hiermee stelt u een waarschuwingsregel tooautomatically monitor dtu's in Hallo toekomstige.</span><span class="sxs-lookup"><span data-stu-id="f2cf1-122">Sets an alert rule tooautomatically monitor DTUs in hello future.</span></span> |
| [<span data-ttu-id="f2cf1-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f2cf1-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="f2cf1-124">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="f2cf1-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="f2cf1-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f2cf1-125">Next steps</span></span>

<span data-ttu-id="f2cf1-126">Zie voor meer informatie over hello Azure PowerShell [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f2cf1-126">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f2cf1-127">Voorbeelden van aanvullende SQL Database PowerShell-script kunnen worden gevonden in Hallo [Azure SQL Database PowerShell-scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f2cf1-127">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
