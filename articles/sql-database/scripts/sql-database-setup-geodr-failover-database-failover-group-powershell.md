---
title: "failover van de voorbeeld-geo-replicatie aaaPowerShell groep één Azure SQL Database | Microsoft Docs"
description: Azure PowerShell voorbeeld script tooset van actieve geo-replicatie voor een enkele Azure SQL database
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
ms.openlocfilehash: 0ea7afb1125b95370811ef7f80cb9eb7391b2443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-an-active-geo-replication-failover-group-for-a-single-azure-sql-database"></a><span data-ttu-id="df39c-103">PowerShell tooconfigure een actieve geo-replicatie, failover-groep gebruiken voor één Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="df39c-103">Use PowerShell tooconfigure an active geo-replication failover group for a single Azure SQL database</span></span>

<span data-ttu-id="df39c-104">Voorbeeld van deze PowerShell-script configureert u een failover-groep van actieve geo-replicatie voor een enkele Azure SQL database en failover tooa secundaire replica van hello Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="df39c-104">This PowerShell script example configures an active geo-replication failover group for a single Azure SQL database and fails it over tooa secondary replica of hello Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="df39c-105">Voorbeeldscripts</span><span class="sxs-lookup"><span data-stu-id="df39c-105">Sample scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database-failover-group.ps1?highlight=19-22 "Set up failover group for single database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="df39c-106">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="df39c-106">Clean up deployment</span></span>

<span data-ttu-id="df39c-107">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="df39c-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="df39c-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="df39c-108">Script explanation</span></span>

<span data-ttu-id="df39c-109">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="df39c-109">This script uses hello following commands.</span></span> <span data-ttu-id="df39c-110">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="df39c-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="df39c-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="df39c-111">Command</span></span> | <span data-ttu-id="df39c-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="df39c-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="df39c-113">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="df39c-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="df39c-114">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="df39c-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="df39c-115">Nieuwe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="df39c-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="df39c-116">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="df39c-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="df39c-117">Nieuwe AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="df39c-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="df39c-118">Maakt een elastische pool in een logische server.</span><span class="sxs-lookup"><span data-stu-id="df39c-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="df39c-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="df39c-119">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="df39c-120">Database-eigenschappen-updates of een database verplaatst naar, uit of tussen elastische pools.</span><span class="sxs-lookup"><span data-stu-id="df39c-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="df39c-121">Nieuwe AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="df39c-121">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="df39c-122">Hiermee maakt u een secundaire database voor een bestaande database en start gegevensreplicatie.</span><span class="sxs-lookup"><span data-stu-id="df39c-122">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="df39c-123">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="df39c-123">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="df39c-124">Hiermee haalt u een of meer databases.</span><span class="sxs-lookup"><span data-stu-id="df39c-124">Gets one or more databases.</span></span> |
| [<span data-ttu-id="df39c-125">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="df39c-125">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="df39c-126">Een secundaire database toobe primaire tooinitiate failover verandert.</span><span class="sxs-lookup"><span data-stu-id="df39c-126">Switches a secondary database toobe primary tooinitiate failover.</span></span>|
| [<span data-ttu-id="df39c-127">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="df39c-127">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="df39c-128">Hiermee haalt u Hallo geo-replicatiekoppelingen tussen een Azure SQL Database en een resourcegroep of SQL Server.</span><span class="sxs-lookup"><span data-stu-id="df39c-128">Gets hello geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="df39c-129">Verwijder AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="df39c-129">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="df39c-130">Beëindigt gegevensreplicatie tussen een SQL-Database en het Hallo opgegeven secundaire database.</span><span class="sxs-lookup"><span data-stu-id="df39c-130">Terminates data replication between a SQL Database and hello specified secondary database.</span></span> |
| [<span data-ttu-id="df39c-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="df39c-131">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="df39c-132">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="df39c-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="df39c-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="df39c-133">Next steps</span></span>

<span data-ttu-id="df39c-134">Zie voor meer informatie over hello Azure PowerShell [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="df39c-134">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="df39c-135">Voorbeelden van aanvullende SQL Database PowerShell-script kunnen worden gevonden in Hallo [Azure SQL Database PowerShell-scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="df39c-135">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
