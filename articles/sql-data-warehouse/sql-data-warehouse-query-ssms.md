---
title: aaaConnect tooAzure SQL Data Warehouse - SSMS | Microsoft Docs
description: Gebruik SQL Server Management Studio (SSMS) tooconnect tooand query Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a><span data-ttu-id="0afbc-103">Verbinding maken met SQL Server Management Studio (SSMS) met tooSQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0afbc-103">Connect tooSQL Data Warehouse with SQL Server Management Studio (SSMS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0afbc-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="0afbc-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="0afbc-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0afbc-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="0afbc-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0afbc-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="0afbc-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="0afbc-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="0afbc-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="0afbc-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="0afbc-109">Gebruik SQL Server Management Studio (SSMS) tooconnect tooand query Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0afbc-109">Use SQL Server Management Studio (SSMS) tooconnect tooand query Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0afbc-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0afbc-110">Prerequisites</span></span>
<span data-ttu-id="0afbc-111">toouse deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="0afbc-111">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="0afbc-112">Een bestaande SQL-datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="0afbc-112">An existing SQL data warehouse.</span></span> <span data-ttu-id="0afbc-113">toocreate, Zie [maken van een SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="0afbc-113">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="0afbc-114">SQL Server Management Studio (SSMS) geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="0afbc-114">SQL Server Management Studio (SSMS) installed.</span></span> <span data-ttu-id="0afbc-115">[Installeren van SSMS] [ Install SSMS] gratis als u nog geen hebt.</span><span class="sxs-lookup"><span data-stu-id="0afbc-115">[Install SSMS][Install SSMS] for free if you don't already have it.</span></span>
* <span data-ttu-id="0afbc-116">Hallo volledig gekwalificeerde naam van SQL server.</span><span class="sxs-lookup"><span data-stu-id="0afbc-116">hello fully qualified SQL server name.</span></span> <span data-ttu-id="0afbc-117">toofind deze, Zie [tooSQL datawarehouse verbinding][Connect tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="0afbc-117">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="0afbc-118">1. Verbinding maken met SQL Data Warehouse tooyour</span><span class="sxs-lookup"><span data-stu-id="0afbc-118">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="0afbc-119">Open SSMS.</span><span class="sxs-lookup"><span data-stu-id="0afbc-119">Open SSMS.</span></span>
2. <span data-ttu-id="0afbc-120">Object Explorer geopend.</span><span class="sxs-lookup"><span data-stu-id="0afbc-120">Open Object Explorer.</span></span> <span data-ttu-id="0afbc-121">toodo deze, selecteer **bestand** > **Objectverkenner verbinding**.</span><span class="sxs-lookup"><span data-stu-id="0afbc-121">toodo this, select **File** > **Connect Object Explorer**.</span></span>
   
    ![SQL Server-objectverkenner][1]
3. <span data-ttu-id="0afbc-123">Vul de velden Hallo Hallo Connect tooServer-venster.</span><span class="sxs-lookup"><span data-stu-id="0afbc-123">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![Verbinding maken met tooServer][2]
   
   * <span data-ttu-id="0afbc-125">**Server name** (Servernaam).</span><span class="sxs-lookup"><span data-stu-id="0afbc-125">**Server name**.</span></span> <span data-ttu-id="0afbc-126">Voer Hallo **servernaam** eerder hebt geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="0afbc-126">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="0afbc-127">**Authentication** (Verificatie).</span><span class="sxs-lookup"><span data-stu-id="0afbc-127">**Authentication**.</span></span> <span data-ttu-id="0afbc-128">Selecteer **SQL Server Authentication** (SQL Server-verificatie) of **Active Directory Integrated Authentication** (Geïntegreerde Active Directory-verificatie).</span><span class="sxs-lookup"><span data-stu-id="0afbc-128">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="0afbc-129">**User Name** (Gebruikersnaam) en **Password** (Wachtwoord).</span><span class="sxs-lookup"><span data-stu-id="0afbc-129">**User Name** and **Password**.</span></span> <span data-ttu-id="0afbc-130">Voer de gebruikersnaam en het wachtwoord in als u hierboven SQL Server-verificatie hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="0afbc-130">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="0afbc-131">Klik op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="0afbc-131">Click **Connect**.</span></span>
4. <span data-ttu-id="0afbc-132">tooexplore, vouw uw Azure SQL-server.</span><span class="sxs-lookup"><span data-stu-id="0afbc-132">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="0afbc-133">Hallo-databases die zijn gekoppeld aan het Hallo-server, kunt u weergeven.</span><span class="sxs-lookup"><span data-stu-id="0afbc-133">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="0afbc-134">Vouw AdventureWorksDW toosee Hallo tabellen in de voorbeelddatabase.</span><span class="sxs-lookup"><span data-stu-id="0afbc-134">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![AdventureWorksDW verkennen][3]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="0afbc-136">2. Een voorbeeldquery uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0afbc-136">2. Run a sample query</span></span>
<span data-ttu-id="0afbc-137">Nu dat een verbinding tot stand gebrachte tooyour database is, gaan we een query schrijven.</span><span class="sxs-lookup"><span data-stu-id="0afbc-137">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="0afbc-138">Klik met de rechtermuisknop op de database in SQL Server-objectverkenner.</span><span class="sxs-lookup"><span data-stu-id="0afbc-138">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="0afbc-139">Selecteer **New Query** (Nieuwe query).</span><span class="sxs-lookup"><span data-stu-id="0afbc-139">Select **New Query**.</span></span> <span data-ttu-id="0afbc-140">Een nieuwe queryvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="0afbc-140">A new query window opens.</span></span>
   
    ![Nieuwe query][4]
3. <span data-ttu-id="0afbc-142">Kopieer de volgende TSQL-query naar Hallo query-venster:</span><span class="sxs-lookup"><span data-stu-id="0afbc-142">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="0afbc-143">Hallo-query uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0afbc-143">Run hello query.</span></span> <span data-ttu-id="0afbc-144">toodo, klikt u op `Execute` of gebruik Hallo volgende snelkoppeling: `F5`.</span><span class="sxs-lookup"><span data-stu-id="0afbc-144">toodo this, click `Execute` or use hello following shortcut: `F5`.</span></span>
   
    ![Query uitvoeren][5]
5. <span data-ttu-id="0afbc-146">Bekijkt hello queryresultaten.</span><span class="sxs-lookup"><span data-stu-id="0afbc-146">Look at hello query results.</span></span> <span data-ttu-id="0afbc-147">In dit voorbeeld factinternetsales Hallo heeft tabel 60398 rijen.</span><span class="sxs-lookup"><span data-stu-id="0afbc-147">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![Queryresultaten][6]

## <a name="next-steps"></a><span data-ttu-id="0afbc-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0afbc-149">Next steps</span></span>
<span data-ttu-id="0afbc-150">Nu kunt u verbinding maken en een query, proberen [Hallo-gegevens met Power BI te visualiseren][visualizing hello data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="0afbc-150">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="0afbc-151">tooconfigure uw omgeving voor Azure Active Directory-verificatie, Zie [tooSQL Data Warehouse verifiëren][Authenticate tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="0afbc-151">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
