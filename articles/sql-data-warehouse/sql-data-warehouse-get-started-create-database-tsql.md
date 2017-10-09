---
title: aaaCreate een SQL Data Warehouse met TSQL | Microsoft Docs
description: Meer informatie over hoe toocreate een Azure SQL Data Warehouse met TSQL
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: a4e2e68e-aa9c-4dd3-abb0-f7df997d237a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 81ef59a66c61452ff8a2aca29837f155e87d017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a><span data-ttu-id="5ac93-103">Een SQL Data Warehouse-database maken met behulp van Transact-SQL (TSQL)</span><span class="sxs-lookup"><span data-stu-id="5ac93-103">Create a SQL Data Warehouse database by using Transact-SQL (TSQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5ac93-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5ac93-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="5ac93-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="5ac93-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="5ac93-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ac93-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="5ac93-107">Dit artikel laat zien hoe toocreate een SQL Data Warehouse met T-SQL.</span><span class="sxs-lookup"><span data-stu-id="5ac93-107">This article shows you how toocreate a SQL Data Warehouse using T-SQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ac93-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5ac93-108">Prerequisites</span></span>
<span data-ttu-id="5ac93-109">tooget gestart, moet u de:</span><span class="sxs-lookup"><span data-stu-id="5ac93-109">tooget started, you need:</span></span>

* <span data-ttu-id="5ac93-110">**Azure-account**: Ga naar [gratis proefversie van Azure] [ Azure Free Trial] of [Azure-tegoed met MSDN] [ MSDN Azure Credits] toocreate een account.</span><span class="sxs-lookup"><span data-stu-id="5ac93-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="5ac93-111">**Azure SQL-server**: Zie [maken een logische Azure SQL Database-server met hello Azure Portal] [maken van een logische Azure SQL Database-server met hello Azure Portal] of [maken van een logische Azure SQL Database-server met PowerShell] [maken van een SQL Azure Database-logische server met PowerShell] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5ac93-111">**Azure SQL server**:  See [Create an Azure SQL Database logical server with hello Azure Portal][Create an Azure SQL Database logical server with hello Azure Portal] or [Create an Azure SQL Database logical server with PowerShell][Create an Azure SQL Database logical server with PowerShell] for more details.</span></span>
* <span data-ttu-id="5ac93-112">**Resourcegroep**: gebruik Hallo dezelfde resource groeperen als uw Azure SQL-server of Zie [hoe toocreate een resourcegroep][how toocreate a resource group].</span><span class="sxs-lookup"><span data-stu-id="5ac93-112">**Resource group**: Either use hello same resource group as your Azure SQL server or see [how toocreate a resource group][how toocreate a resource group].</span></span>
* <span data-ttu-id="5ac93-113">**Omgeving tooexecute T-SQL**: U kunt [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], of [SSMS] [ SSMS] tooexecute T-SQL.</span><span class="sxs-lookup"><span data-stu-id="5ac93-113">**Environment tooexecute T-SQL**: You can use [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], or [SSMS][SSMS] tooexecute T-SQL.</span></span>

> [!NOTE]
> <span data-ttu-id="5ac93-114">Het maken van een SQL Data Warehouse kan leiden tot een nieuwe factureerbare service.</span><span class="sxs-lookup"><span data-stu-id="5ac93-114">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="5ac93-115">Zie [Prijzen van SQL Data Warehouse][SQL Data Warehouse pricing] voor meer informatie over prijzen.</span><span class="sxs-lookup"><span data-stu-id="5ac93-115">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-database-with-visual-studio"></a><span data-ttu-id="5ac93-116">Een database maken met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5ac93-116">Create a database with Visual Studio</span></span>
<span data-ttu-id="5ac93-117">Als u nieuwe tooVisual Studio, Zie Hallo artikel [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span><span class="sxs-lookup"><span data-stu-id="5ac93-117">If you are new tooVisual Studio, see hello article [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span></span>  <span data-ttu-id="5ac93-118">toostart, opent u SQL Server-Objectverkenner in Visual Studio en maak verbinding toohello-server die als host voor uw SQL Data Warehouse-database fungeert.</span><span class="sxs-lookup"><span data-stu-id="5ac93-118">toostart, open SQL Server Object Explorer in Visual Studio and connect toohello server that will host your SQL Data Warehouse database.</span></span>  <span data-ttu-id="5ac93-119">Eenmaal zijn verbonden, kunt u een SQL Data Warehouse maken door het uitvoeren van de volgende SQL-opdracht tegen Hallo Hallo **master** database.</span><span class="sxs-lookup"><span data-stu-id="5ac93-119">Once connected, you can create a SQL Data Warehouse by running hello following SQL command against hello **master** database.</span></span>  <span data-ttu-id="5ac93-120">Deze opdracht Hallo database MySqlDwDb gemaakt met een Serviceniveaudoelstelling van DW400 en Hallo database toogrow tooa maximale grootte van 10 TB toestaan.</span><span class="sxs-lookup"><span data-stu-id="5ac93-120">This command creates hello database MySqlDwDb with a Service Objective of DW400 and allow hello database toogrow tooa maximum size of 10 TB.</span></span>

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a><span data-ttu-id="5ac93-121">Een database maken met sqlcmd</span><span class="sxs-lookup"><span data-stu-id="5ac93-121">Create a database with sqlcmd</span></span>
<span data-ttu-id="5ac93-122">U kunt ook uitvoeren Hallo dezelfde opdracht met sqlcmd door te voeren Hallo bij een opdrachtprompt te volgen.</span><span class="sxs-lookup"><span data-stu-id="5ac93-122">Alternatively, you can run hello same command with sqlcmd by running hello following at a command prompt.</span></span>

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

<span data-ttu-id="5ac93-123">Hallo standaardsortering als niet is opgegeven is COLLATE SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="5ac93-123">hello default collation when not specified is COLLATE SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="5ac93-124">Hallo `MAXSIZE` mag tussen 250 GB en 240 TB.</span><span class="sxs-lookup"><span data-stu-id="5ac93-124">hello `MAXSIZE` can be between 250 GB and 240 TB.</span></span>  <span data-ttu-id="5ac93-125">Hallo `SERVICE_OBJECTIVE` mag tussen DW100 en dw2000 zijn [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="5ac93-125">hello `SERVICE_OBJECTIVE` can be between DW100 and DW2000 [DWU][DWU].</span></span>  <span data-ttu-id="5ac93-126">Zie voor een lijst van alle geldige waarden Hallo MSDN-documentatie voor [CREATE DATABASE][CREATE DATABASE].</span><span class="sxs-lookup"><span data-stu-id="5ac93-126">For a list of all valid values, see hello MSDN documentation for [CREATE DATABASE][CREATE DATABASE].</span></span>  <span data-ttu-id="5ac93-127">Zowel Hallo MAXSIZE en SERVICE_OBJECTIVE kunnen worden gewijzigd met een [ALTER DATABASE] [ ALTER DATABASE] T-SQL-opdracht.</span><span class="sxs-lookup"><span data-stu-id="5ac93-127">Both hello MAXSIZE and SERVICE_OBJECTIVE can be changed with an [ALTER DATABASE][ALTER DATABASE] T-SQL command.</span></span>  <span data-ttu-id="5ac93-128">Hallo-sortering van een database kan niet worden gewijzigd nadat de is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5ac93-128">hello collation of a database cannot be changed after creation.</span></span>   <span data-ttu-id="5ac93-129">Waarschuwing moet worden gebruikt als veranderende Hallo SERVICE_OBJECTIVE als DWU gewijzigd zorgt ervoor dat het opnieuw opstarten van services, die alle query's tijdens de vlucht annuleert.</span><span class="sxs-lookup"><span data-stu-id="5ac93-129">Caution should be used when changing hello SERVICE_OBJECTIVE as changing DWU causes a restart of services, which cancels all queries in flight.</span></span>  <span data-ttu-id="5ac93-130">Voor een verandering van MAXSIZE hoeven services niet opnieuw te worden gestart, omdat dit een eenvoudige metagegevensbewerking is.</span><span class="sxs-lookup"><span data-stu-id="5ac93-130">Changing MAXSIZE does not restart services as it is just a simple metadata operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ac93-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5ac93-131">Next steps</span></span>
<span data-ttu-id="5ac93-132">Nadat uw SQL Data Warehouse is voltooid, u kunt inrichting [voorbeeldgegevens laden] [ load sample data] of te zoeken over[ontwikkelen][develop], [laden][load], of [migreren][migrate].</span><span class="sxs-lookup"><span data-stu-id="5ac93-132">After your SQL Data Warehouse has finished provisioning you can [load sample data][load sample data] or check out how too[develop][develop], [load][load], or [migrate][migrate].</span></span>

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how toocreate a SQL Data Warehouse from hello Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--MSDN references-->
[CREATE DATABASE]: https://msdn.microsoft.com/library/mt204021.aspx
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
