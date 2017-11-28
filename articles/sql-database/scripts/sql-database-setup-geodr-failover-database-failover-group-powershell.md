---
title: "Failover van de voorbeeld-geo-replicatie PowerShell groep één Azure SQL Database | Microsoft Docs"
description: Azure PowerShell-voorbeeldscript voor het instellen van actieve geo-replicatie voor een enkele Azure SQL database
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
ms.openlocfilehash: 8db8540d9c4caeb53ea8f34d45d9498496d2b8ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-configure-an-active-geo-replication-failover-group-for-a-single-azure-sql-database"></a><span data-ttu-id="fabfc-103">PowerShell gebruiken voor het configureren van een groep actieve geo-replicatie failover voor een enkele Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="fabfc-103">Use PowerShell to configure an active geo-replication failover group for a single Azure SQL database</span></span>

<span data-ttu-id="fabfc-104">Voorbeeld van deze PowerShell-script configureert u een groep actieve geo-replicatie failover voor een enkele Azure SQL database en failover naar een secundaire replica van de Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="fabfc-104">This PowerShell script example configures an active geo-replication failover group for a single Azure SQL database and fails it over to a secondary replica of the Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="fabfc-105">Voorbeeldscripts</span><span class="sxs-lookup"><span data-stu-id="fabfc-105">Sample scripts</span></span>

<span data-ttu-id="fabfc-106">[!code-powershell[belangrijkste](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database-failover-group.ps1?highlight=19-22 "failover-groep voor één database instellen")]</span><span class="sxs-lookup"><span data-stu-id="fabfc-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database-failover-group.ps1?highlight=19-22 "Set up failover group for single database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="fabfc-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="fabfc-107">Clean up deployment</span></span>

<span data-ttu-id="fabfc-108">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om te verwijderen van de resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="fabfc-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="fabfc-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="fabfc-109">Script explanation</span></span>

<span data-ttu-id="fabfc-110">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="fabfc-110">This script uses the following commands.</span></span> <span data-ttu-id="fabfc-111">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="fabfc-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fabfc-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="fabfc-112">Command</span></span> | <span data-ttu-id="fabfc-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="fabfc-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fabfc-114">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fabfc-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="fabfc-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="fabfc-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fabfc-116">Nieuwe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="fabfc-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="fabfc-117">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="fabfc-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="fabfc-118">Nieuwe AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="fabfc-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="fabfc-119">Maakt een elastische pool in een logische server.</span><span class="sxs-lookup"><span data-stu-id="fabfc-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="fabfc-120">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="fabfc-120">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="fabfc-121">Database-eigenschappen-updates of een database verplaatst naar, uit of tussen elastische pools.</span><span class="sxs-lookup"><span data-stu-id="fabfc-121">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="fabfc-122">Nieuwe AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="fabfc-122">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="fabfc-123">Hiermee maakt u een secundaire database voor een bestaande database en start gegevensreplicatie.</span><span class="sxs-lookup"><span data-stu-id="fabfc-123">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="fabfc-124">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="fabfc-124">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="fabfc-125">Hiermee haalt u een of meer databases.</span><span class="sxs-lookup"><span data-stu-id="fabfc-125">Gets one or more databases.</span></span> |
| [<span data-ttu-id="fabfc-126">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="fabfc-126">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="fabfc-127">Een secundaire database als primaire initiëren failover verandert.</span><span class="sxs-lookup"><span data-stu-id="fabfc-127">Switches a secondary database to be primary to initiate failover.</span></span>|
| [<span data-ttu-id="fabfc-128">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="fabfc-128">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="fabfc-129">Hiermee haalt u de geo-replicatiekoppelingen tussen een Azure SQL Database en een resourcegroep of SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fabfc-129">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="fabfc-130">Verwijder AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="fabfc-130">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="fabfc-131">Beëindigt gegevensreplicatie tussen een SQL-Database en de opgegeven secundaire database.</span><span class="sxs-lookup"><span data-stu-id="fabfc-131">Terminates data replication between a SQL Database and the specified secondary database.</span></span> |
| [<span data-ttu-id="fabfc-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fabfc-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="fabfc-133">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="fabfc-133">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="fabfc-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fabfc-134">Next steps</span></span>

<span data-ttu-id="fabfc-135">Zie voor meer informatie over Azure PowerShell [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fabfc-135">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="fabfc-136">Voorbeelden van aanvullende SQL Database PowerShell-script kunnen worden gevonden in de [Azure SQL Database PowerShell-scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fabfc-136">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
