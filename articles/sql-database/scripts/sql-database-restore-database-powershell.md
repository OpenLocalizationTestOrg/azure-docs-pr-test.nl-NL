---
title: aaaPowerShell voorbeeld, herstel, back-up, Azure SQL database | Microsoft Docs
description: Azure PowerShell-voorbeeld script toorestore een Azure SQL-database vanuit geografisch redundante back-ups
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
ms.openlocfilehash: 68becb89e8a8680aa2efc3de8ad947e674c5fc35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toorestore-an-azure-sql-database-from-backups"></a><span data-ttu-id="3b6cf-103">Gebruik PowerShell toorestore een Azure SQL-database vanuit back-ups</span><span class="sxs-lookup"><span data-stu-id="3b6cf-103">Use PowerShell toorestore an Azure SQL database from backups</span></span>

<span data-ttu-id="3b6cf-104">Voorbeeld van deze PowerShell-script een Azure SQL database herstelt vanuit een geografisch redundante back-up, herstelt u een verwijderde Azure SQL database tooits meest recente back-up en wordt hersteld van een Azure SQL database tooa bepaald punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="3b6cf-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database tooits latest backup, and restores an Azure SQL database tooa specific point in time.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="3b6cf-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="3b6cf-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3b6cf-106">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="3b6cf-106">Clean up deployment</span></span>

<span data-ttu-id="3b6cf-107">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="3b6cf-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="3b6cf-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="3b6cf-108">Script explanation</span></span>

<span data-ttu-id="3b6cf-109">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="3b6cf-109">This script uses hello following commands.</span></span> <span data-ttu-id="3b6cf-110">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="3b6cf-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3b6cf-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="3b6cf-111">Command</span></span> | <span data-ttu-id="3b6cf-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="3b6cf-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3b6cf-113">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3b6cf-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="3b6cf-114">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3b6cf-114">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="3b6cf-115">Nieuwe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="3b6cf-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="3b6cf-116">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="3b6cf-116">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="3b6cf-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="3b6cf-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="3b6cf-118">Maakt een database in een logische server als één of een gegroepeerde database.</span><span class="sxs-lookup"><span data-stu-id="3b6cf-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="3b6cf-119">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="3b6cf-119">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | <span data-ttu-id="3b6cf-120">Hiermee haalt u een geografisch redundante back-up van een database.</span><span class="sxs-lookup"><span data-stu-id="3b6cf-120">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="3b6cf-121">Restore-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="3b6cf-121">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | <span data-ttu-id="3b6cf-122">Een SQL-database herstelt.</span><span class="sxs-lookup"><span data-stu-id="3b6cf-122">Restores a SQL database.</span></span> |
|[<span data-ttu-id="3b6cf-123">Verwijder AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="3b6cf-123">Remove-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | <span data-ttu-id="3b6cf-124">Hiermee verwijdert u een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="3b6cf-124">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="3b6cf-125">Get-AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="3b6cf-125">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="3b6cf-126">Hiermee haalt u een verwijderde database die u kunt herstellen.</span><span class="sxs-lookup"><span data-stu-id="3b6cf-126">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="3b6cf-127">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3b6cf-127">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="3b6cf-128">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="3b6cf-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3b6cf-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3b6cf-129">Next steps</span></span>

<span data-ttu-id="3b6cf-130">Zie voor meer informatie over hello Azure PowerShell [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3b6cf-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="3b6cf-131">Voorbeelden van aanvullende SQL Database PowerShell-script kunnen worden gevonden in Hallo [Azure SQL Database PowerShell-scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3b6cf-131">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
