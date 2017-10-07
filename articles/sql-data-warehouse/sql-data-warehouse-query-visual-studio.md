---
title: aaaConnect tooAzure SQL Data Warehouse - VSTS | Microsoft Docs
description: "Query’s uitvoeren bij SQL Data Warehouse met Visual Studio."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="caad4-103">Verbinding maken met tooSQL Data Warehouse met Visual Studio en SSDT</span><span class="sxs-lookup"><span data-stu-id="caad4-103">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="caad4-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="caad4-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="caad4-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="caad4-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="caad4-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="caad4-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="caad4-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="caad4-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="caad4-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="caad4-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="caad4-109">Gebruik Visual Studio tooquery Azure SQL Data Warehouse in een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="caad4-109">Use Visual Studio tooquery Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="caad4-110">Deze methode maakt gebruik van SQL Server Data Tools (SSDT)-extensie Hallo in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="caad4-110">This method uses hello SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="caad4-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="caad4-111">Prerequisites</span></span>
<span data-ttu-id="caad4-112">toouse deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="caad4-112">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="caad4-113">Een bestaande SQL-datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="caad4-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="caad4-114">toocreate, Zie [maken van een SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="caad4-114">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="caad4-115">SSDT voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="caad4-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="caad4-116">Als u Visual Studio hebt, hebt u dit waarschijnlijk al.</span><span class="sxs-lookup"><span data-stu-id="caad4-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="caad4-117">Zie [Visual Studio en SSDT installeren][Installing Visual Studio and SSDT] voor instructies en opties voor de installatie.</span><span class="sxs-lookup"><span data-stu-id="caad4-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="caad4-118">Hallo volledig gekwalificeerde naam van SQL server.</span><span class="sxs-lookup"><span data-stu-id="caad4-118">hello fully qualified SQL server name.</span></span> <span data-ttu-id="caad4-119">toofind deze, Zie [tooSQL datawarehouse verbinding][Connect tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="caad4-119">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="caad4-120">1. Verbinding maken met SQL Data Warehouse tooyour</span><span class="sxs-lookup"><span data-stu-id="caad4-120">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="caad4-121">Open Visual Studio 2013 of 2015.</span><span class="sxs-lookup"><span data-stu-id="caad4-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="caad4-122">Open SQL Server-objectverkenner.</span><span class="sxs-lookup"><span data-stu-id="caad4-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="caad4-123">toodo deze, selecteer **weergave** > **SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="caad4-123">toodo this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![SQL Server-objectverkenner][1]
3. <span data-ttu-id="caad4-125">Klik op Hallo **SQL-Server toevoegen** pictogram.</span><span class="sxs-lookup"><span data-stu-id="caad4-125">Click hello **Add SQL Server** icon.</span></span>
   
    ![SQL Server toevoegen][2]
4. <span data-ttu-id="caad4-127">Vul de velden Hallo Hallo Connect tooServer-venster.</span><span class="sxs-lookup"><span data-stu-id="caad4-127">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![Verbinding maken met tooServer][3]
   
   * <span data-ttu-id="caad4-129">**Server name** (Servernaam).</span><span class="sxs-lookup"><span data-stu-id="caad4-129">**Server name**.</span></span> <span data-ttu-id="caad4-130">Voer Hallo **servernaam** eerder hebt geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="caad4-130">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="caad4-131">**Authentication** (Verificatie).</span><span class="sxs-lookup"><span data-stu-id="caad4-131">**Authentication**.</span></span> <span data-ttu-id="caad4-132">Selecteer **SQL Server Authentication** (SQL Server-verificatie) of **Active Directory Integrated Authentication** (Geïntegreerde Active Directory-verificatie).</span><span class="sxs-lookup"><span data-stu-id="caad4-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="caad4-133">**User Name** (Gebruikersnaam) en **Password** (Wachtwoord).</span><span class="sxs-lookup"><span data-stu-id="caad4-133">**User Name** and **Password**.</span></span> <span data-ttu-id="caad4-134">Voer de gebruikersnaam en het wachtwoord in als u hierboven SQL Server-verificatie hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="caad4-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="caad4-135">Klik op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="caad4-135">Click **Connect**.</span></span>
5. <span data-ttu-id="caad4-136">tooexplore, vouw uw Azure SQL-server.</span><span class="sxs-lookup"><span data-stu-id="caad4-136">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="caad4-137">Hallo-databases die zijn gekoppeld aan het Hallo-server, kunt u weergeven.</span><span class="sxs-lookup"><span data-stu-id="caad4-137">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="caad4-138">Vouw AdventureWorksDW toosee Hallo tabellen in de voorbeelddatabase.</span><span class="sxs-lookup"><span data-stu-id="caad4-138">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![AdventureWorksDW verkennen][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="caad4-140">2. Een voorbeeldquery uitvoeren</span><span class="sxs-lookup"><span data-stu-id="caad4-140">2. Run a sample query</span></span>
<span data-ttu-id="caad4-141">Nu dat een verbinding tot stand gebrachte tooyour database is, gaan we een query schrijven.</span><span class="sxs-lookup"><span data-stu-id="caad4-141">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="caad4-142">Klik met de rechtermuisknop op de database in SQL Server-objectverkenner.</span><span class="sxs-lookup"><span data-stu-id="caad4-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="caad4-143">Selecteer **New Query** (Nieuwe query).</span><span class="sxs-lookup"><span data-stu-id="caad4-143">Select **New Query**.</span></span> <span data-ttu-id="caad4-144">Een nieuwe queryvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="caad4-144">A new query window opens.</span></span>
   
    ![Nieuwe query][5]
3. <span data-ttu-id="caad4-146">Kopieer de volgende TSQL-query naar Hallo query-venster:</span><span class="sxs-lookup"><span data-stu-id="caad4-146">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="caad4-147">Hallo-query uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="caad4-147">Run hello query.</span></span> <span data-ttu-id="caad4-148">toodo, klikt u op Hallo groene pijl of gebruik Hallo volgende snelkoppeling: `CTRL` + `SHIFT` + `E`.</span><span class="sxs-lookup"><span data-stu-id="caad4-148">toodo this, click hello green arrow or use hello following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![Query uitvoeren][6]
5. <span data-ttu-id="caad4-150">Bekijkt hello queryresultaten.</span><span class="sxs-lookup"><span data-stu-id="caad4-150">Look at hello query results.</span></span> <span data-ttu-id="caad4-151">In dit voorbeeld factinternetsales Hallo heeft tabel 60398 rijen.</span><span class="sxs-lookup"><span data-stu-id="caad4-151">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![Queryresultaten][7]

## <a name="next-steps"></a><span data-ttu-id="caad4-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="caad4-153">Next steps</span></span>
<span data-ttu-id="caad4-154">Nu kunt u verbinding maken en een query, proberen [Hallo-gegevens met Power BI te visualiseren][visualizing hello data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="caad4-154">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="caad4-155">tooconfigure uw omgeving voor Azure Active Directory-verificatie, Zie [tooSQL Data Warehouse verifiëren][Authenticate tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="caad4-155">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
