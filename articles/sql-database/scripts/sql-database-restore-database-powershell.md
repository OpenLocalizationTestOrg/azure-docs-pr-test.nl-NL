---
title: PowerShell-voorbeeld, herstel, back-up, Azure SQL-database | Microsoft Docs
description: Azure PowerShell-voorbeeldscript om terug te zetten van een Azure SQL database vanuit geografisch redundante back-ups
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: ae1d0c828ae1e7e1e7e07dcc7d6157187a3859d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-restore-an-azure-sql-database-from-backups"></a><span data-ttu-id="fce52-103">PowerShell gebruiken voor het herstellen van een Azure SQL database vanuit back-ups</span><span class="sxs-lookup"><span data-stu-id="fce52-103">Use PowerShell to restore an Azure SQL database from backups</span></span>

<span data-ttu-id="fce52-104">In dit voorbeeld van de PowerShell-script een Azure SQL database herstelt vanuit een geografisch redundante back-up, een verwijderde Azure SQL-database herstelt naar de meest recente back-up en wordt een Azure SQL database hersteld naar een bepaald punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="fce52-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database to its latest backup, and restores an Azure SQL database to a specific point in time.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="fce52-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="fce52-105">Sample script</span></span>

<span data-ttu-id="fce52-106">[!code-powershell[belangrijkste](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "SQL-Database maken")]</span><span class="sxs-lookup"><span data-stu-id="fce52-106">[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="fce52-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="fce52-107">Clean up deployment</span></span>

<span data-ttu-id="fce52-108">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om te verwijderen van de resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="fce52-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="fce52-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="fce52-109">Script explanation</span></span>

<span data-ttu-id="fce52-110">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="fce52-110">This script uses the following commands.</span></span> <span data-ttu-id="fce52-111">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="fce52-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fce52-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="fce52-112">Command</span></span> | <span data-ttu-id="fce52-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="fce52-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fce52-114">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fce52-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="fce52-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="fce52-115">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="fce52-116">Nieuwe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="fce52-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="fce52-117">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="fce52-117">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="fce52-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="fce52-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="fce52-119">Maakt een database in een logische server als één of een gegroepeerde database.</span><span class="sxs-lookup"><span data-stu-id="fce52-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="fce52-120">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="fce52-120">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | <span data-ttu-id="fce52-121">Hiermee haalt u een geografisch redundante back-up van een database.</span><span class="sxs-lookup"><span data-stu-id="fce52-121">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="fce52-122">Restore-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="fce52-122">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | <span data-ttu-id="fce52-123">Een SQL-database herstelt.</span><span class="sxs-lookup"><span data-stu-id="fce52-123">Restores a SQL database.</span></span> |
|[<span data-ttu-id="fce52-124">Verwijder AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="fce52-124">Remove-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | <span data-ttu-id="fce52-125">Hiermee verwijdert u een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="fce52-125">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="fce52-126">Get-AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="fce52-126">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="fce52-127">Hiermee haalt u een verwijderde database die u kunt herstellen.</span><span class="sxs-lookup"><span data-stu-id="fce52-127">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="fce52-128">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fce52-128">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="fce52-129">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="fce52-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fce52-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fce52-130">Next steps</span></span>

<span data-ttu-id="fce52-131">Zie voor meer informatie over Azure PowerShell [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fce52-131">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="fce52-132">Voorbeelden van aanvullende SQL Database PowerShell-script kunnen worden gevonden in de [Azure SQL Database PowerShell-scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fce52-132">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
