---
title: aaaPowerShell voorbeeld-actieve geo-replicatie gegroepeerde Azure SQL database | Microsoft Docs
description: Azure PowerShell voorbeeld script tooset van actieve geo-replicatie voor een gegroepeerde Azure SQL database
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/25/2017
ms.author: carlrab
ms.openlocfilehash: 9d183f08dcc07ba864e42fe70a562fef8bd572f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-active-geo-replication-for-a-pooled-azure-sql-database"></a><span data-ttu-id="5903d-103">Gebruik PowerShell tooconfigure actieve geo-replicatie voor een gegroepeerde Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="5903d-103">Use PowerShell tooconfigure active geo-replication for a pooled Azure SQL database</span></span>

<span data-ttu-id="5903d-104">Voorbeeld van deze PowerShell-script actieve geo-replicatie voor een Azure SQL database in een elastische pool configureert en failover toohello secundaire replica van hello Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="5903d-104">This PowerShell script example configures active geo-replication for an Azure SQL database in an elastic pool and fails it over toohello secondary replica of hello Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="5903d-105">Voorbeeldscripts</span><span class="sxs-lookup"><span data-stu-id="5903d-105">Sample scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Set up active geo-replication for elastic pool")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5903d-106">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="5903d-106">Clean up deployment</span></span>

<span data-ttu-id="5903d-107">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="5903d-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="5903d-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="5903d-108">Script explanation</span></span>

<span data-ttu-id="5903d-109">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="5903d-109">This script uses hello following commands.</span></span> <span data-ttu-id="5903d-110">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="5903d-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5903d-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="5903d-111">Command</span></span> | <span data-ttu-id="5903d-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="5903d-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5903d-113">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5903d-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5903d-114">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5903d-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5903d-115">Nieuwe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="5903d-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="5903d-116">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="5903d-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="5903d-117">Nieuwe AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="5903d-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="5903d-118">Maakt een elastische pool in een logische server.</span><span class="sxs-lookup"><span data-stu-id="5903d-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="5903d-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="5903d-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="5903d-120">Maakt een database in een logische server als één of een gegroepeerde database.</span><span class="sxs-lookup"><span data-stu-id="5903d-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="5903d-121">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="5903d-121">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="5903d-122">Database-eigenschappen-updates of een database verplaatst naar, uit of tussen elastische pools.</span><span class="sxs-lookup"><span data-stu-id="5903d-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="5903d-123">Nieuwe AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="5903d-123">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="5903d-124">Hiermee maakt u een secundaire database voor een bestaande database en start gegevensreplicatie.</span><span class="sxs-lookup"><span data-stu-id="5903d-124">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="5903d-125">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="5903d-125">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="5903d-126">Hiermee haalt u een of meer databases.</span><span class="sxs-lookup"><span data-stu-id="5903d-126">Gets one or more databases.</span></span> |
| [<span data-ttu-id="5903d-127">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="5903d-127">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="5903d-128">Een secundaire database toobe primaire switches in volgorde tooinitiate failover.</span><span class="sxs-lookup"><span data-stu-id="5903d-128">Switches a secondary database toobe primary in order tooinitiate failover.</span></span>|
| [<span data-ttu-id="5903d-129">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="5903d-129">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="5903d-130">Hiermee haalt u Hallo geo-replicatiekoppelingen tussen een Azure SQL Database en een resourcegroep of SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5903d-130">Gets hello geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="5903d-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5903d-131">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5903d-132">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="5903d-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="5903d-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5903d-133">Next steps</span></span>

<span data-ttu-id="5903d-134">Zie voor meer informatie over hello Azure PowerShell [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5903d-134">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5903d-135">Voorbeelden van aanvullende SQL Database PowerShell-script kunnen worden gevonden in Hallo [Azure SQL Database PowerShell-scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5903d-135">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
