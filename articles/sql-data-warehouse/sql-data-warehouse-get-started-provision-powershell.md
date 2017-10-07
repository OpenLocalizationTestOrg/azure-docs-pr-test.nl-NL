---
title: aaaCreate SQL Data Warehouse met behulp van PowerShell | Microsoft Docs
description: SQL Data Warehouse maken met Powershell
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 97434863-7938-4129-8949-5a119f5949e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d8af29ec285a11285785ab5474e4dfc8c36bc3ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a><span data-ttu-id="90019-103">SQL Data Warehouse maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="90019-103">Create SQL Data Warehouse using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="90019-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="90019-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="90019-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="90019-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="90019-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="90019-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="90019-107">Dit artikel laat zien hoe toocreate een SQL Data Warehouse met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90019-107">This article shows you how toocreate a SQL Data Warehouse using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90019-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="90019-108">Prerequisites</span></span>
<span data-ttu-id="90019-109">tooget gestart, moet u de:</span><span class="sxs-lookup"><span data-stu-id="90019-109">tooget started, you need:</span></span>

* <span data-ttu-id="90019-110">**Azure-account**: Ga naar [gratis proefversie van Azure] [ Azure Free Trial] of [Azure-tegoed met MSDN] [ MSDN Azure Credits] toocreate een account.</span><span class="sxs-lookup"><span data-stu-id="90019-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="90019-111">**Azure SQL-server**: Zie [maken van een Azure SQL database in Azure Portal Hallo] [ Create an Azure SQL database in hello Azure Portal] of [een Azure SQL database maken met PowerShell] [ Create an Azure SQL database with PowerShell] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="90019-111">**Azure SQL server**:  See [Create an Azure SQL database in hello Azure Portal][Create an Azure SQL database in hello Azure Portal] or [Create an Azure SQL database with PowerShell][Create an Azure SQL database with PowerShell] for more details.</span></span>
* <span data-ttu-id="90019-112">**Resourcegroep**: gebruik Hallo dezelfde resource groeperen als uw Azure SQL-server of Zie [hoe toocreate een resourcegroep](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="90019-112">**Resource group**: Either use hello same resource group as your Azure SQL server or see [how toocreate a resource group](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="90019-113">**PowerShell-versie 1.0.3 of hoger**: u kunt uw versie controleren door **Get-Module - ListAvailable-Name Azure** uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="90019-113">**PowerShell version 1.0.3 or greater**:  You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="90019-114">de meest recente versie Hallo kan worden geïnstalleerd vanaf [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="90019-114">hello latest version can be installed from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="90019-115">Zie voor meer informatie over het installeren van de meest recente versie Hallo [hoe tooinstall en configureren van Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="90019-115">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

> [!NOTE]
> <span data-ttu-id="90019-116">Het maken van een SQL Data Warehouse kan leiden tot een nieuwe factureerbare service.</span><span class="sxs-lookup"><span data-stu-id="90019-116">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="90019-117">Zie [Prijzen van SQL Data Warehouse][SQL Data Warehouse pricing] voor meer informatie over prijzen.</span><span class="sxs-lookup"><span data-stu-id="90019-117">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="90019-118">Een SQL Data Warehouse maken</span><span class="sxs-lookup"><span data-stu-id="90019-118">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="90019-119">Open Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90019-119">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="90019-120">Deze cmdlet toologin tooAzure Resource Manager worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="90019-120">Run this cmdlet toologin tooAzure Resource Manager.</span></span>

    ```Powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="90019-121">Selecteer het gewenste toouse voor de huidige sessie Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="90019-121">Select hello subscription you want toouse for your current session.</span></span>

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. <span data-ttu-id="90019-122">Maak database.</span><span class="sxs-lookup"><span data-stu-id="90019-122">Create database.</span></span> <span data-ttu-id="90019-123">In dit voorbeeld maakt een database met naam 'mynewsqldw' met servicedoelstellingsniveau 'DW400' toohello server met de naam 'sqldwserver1', dat zich in Hallo resourcegroep 'mywesteuroperesgp1 bevindt'.</span><span class="sxs-lookup"><span data-stu-id="90019-123">This example creates a database named "mynewsqldw", with service objective level "DW400", toohello server named "sqldwserver1", which is in hello resource group named "mywesteuroperesgp1".</span></span>

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

<span data-ttu-id="90019-124">De vereiste parameters zijn:</span><span class="sxs-lookup"><span data-stu-id="90019-124">Required Parameters are:</span></span>

* <span data-ttu-id="90019-125">**RequestedServiceObjectiveName**: Hallo hoeveelheid [DWU] [ DWU] u hebt aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="90019-125">**RequestedServiceObjectiveName**: hello amount of [DWU][DWU] you are requesting.</span></span>  <span data-ttu-id="90019-126">De ondersteunde waarden zijn: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 en DW6000.</span><span class="sxs-lookup"><span data-stu-id="90019-126">Supported values are: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000, and DW6000.</span></span>
* <span data-ttu-id="90019-127">**DatabaseName**: naam Hallo Hallo SQL Data Warehouse die u maakt.</span><span class="sxs-lookup"><span data-stu-id="90019-127">**DatabaseName**: hello name of hello SQL Data Warehouse that you are creating.</span></span>
* <span data-ttu-id="90019-128">**ServerName**: Hallo-naam van Hallo-server die u gebruikt voor het maken van (moet V12 zijn).</span><span class="sxs-lookup"><span data-stu-id="90019-128">**ServerName**: hello name of hello server that you are using for creation (must be V12).</span></span>
* <span data-ttu-id="90019-129">**ResourceGroupName**: de resourcegroep die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="90019-129">**ResourceGroupName**: Resource group you are using.</span></span>  <span data-ttu-id="90019-130">toofind beschikbare resourcegroepen in uw abonnement gebruik Get-AzureResource.</span><span class="sxs-lookup"><span data-stu-id="90019-130">toofind available resource groups in your subscription use Get-AzureResource.</span></span>
* <span data-ttu-id="90019-131">**Editie**: moet 'DataWarehouse' toocreate een SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="90019-131">**Edition**: Must be "DataWarehouse" toocreate a SQL Data Warehouse.</span></span>

<span data-ttu-id="90019-132">De optionele parameters zijn:</span><span class="sxs-lookup"><span data-stu-id="90019-132">Optional Parameters are:</span></span>

* <span data-ttu-id="90019-133">**CollationName**: Hallo standaardsortering als niet wordt opgegeven is SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="90019-133">**CollationName**: hello default collation if not specified is SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="90019-134">De sortering kan niet worden gewijzigd voor een database.</span><span class="sxs-lookup"><span data-stu-id="90019-134">Collation cannot be changed on a database.</span></span>
* <span data-ttu-id="90019-135">**MaxSizeBytes**: Hallo standaard maximale grootte van een database is 10 GB.</span><span class="sxs-lookup"><span data-stu-id="90019-135">**MaxSizeBytes**: hello default max size of a database is 10 GB.</span></span>

<span data-ttu-id="90019-136">Zie voor meer informatie over de parameteropties Hallo [New-AzureRmSqlDatabase] [ New-AzureRmSqlDatabase] en [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span><span class="sxs-lookup"><span data-stu-id="90019-136">For more details on hello parameter options, see [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase] and [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span></span>

## <a name="next-steps"></a><span data-ttu-id="90019-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="90019-137">Next steps</span></span>
<span data-ttu-id="90019-138">Nadat uw SQL Data Warehouse is voltooid de inrichting dat u wilt maken van tootry [voorbeeldgegevens te laden] [ loading sample data] of te zoeken over[ontwikkelen] [ develop] , [laden][load], of [migreren][migrate].</span><span class="sxs-lookup"><span data-stu-id="90019-138">After your SQL Data Warehouse has finished provisioning you may want tootry [loading sample data][loading sample data] or check out how too[develop][develop], [load][load], or [migrate][migrate].</span></span>

<span data-ttu-id="90019-139">Als u geïnteresseerd bent in meer informatie over het artikel over het toomanage SQL Data Warehouse programmatisch uitchecken toouse [PowerShell-cmdlets en REST API's][PowerShell cmdlets and REST APIs].</span><span class="sxs-lookup"><span data-stu-id="90019-139">If you're interested in more on how toomanage SQL Data Warehouse programmatically, check out our article on how toouse [PowerShell cmdlets and REST APIs][PowerShell cmdlets and REST APIs].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how toocreate a SQL Data Warehouse from hello Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
