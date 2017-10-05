---
title: Verbinding maken met Azure SQL Data Warehouse - VSTS| Microsoft Docs
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
ms.openlocfilehash: 1e44c6c3c47034a892753c69c5ef22a5eac18c0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="4bd4b-103">Verbinding maken met SQL Data Warehouse met Visual Studio en SSDT</span><span class="sxs-lookup"><span data-stu-id="4bd4b-103">Connect to SQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4bd4b-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="4bd4b-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="4bd4b-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4bd4b-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="4bd4b-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4bd4b-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="4bd4b-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="4bd4b-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="4bd4b-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="4bd4b-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="4bd4b-109">Gebruik Visual Studio om binnen enkele minuten query’s uit te voeren bij Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-109">Use Visual Studio to query Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="4bd4b-110">Bij deze methode wordt gebruikgemaakt van de SSDT-uitbreiding (SQL Server Data Tools) in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-110">This method uses the SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4bd4b-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4bd4b-111">Prerequisites</span></span>
<span data-ttu-id="4bd4b-112">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="4bd4b-112">To use this tutorial, you need:</span></span>

* <span data-ttu-id="4bd4b-113">Een bestaande SQL-datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="4bd4b-114">Zie [Een SQL-datawarehouse maken][Create a SQL Data Warehouse] om een datawarehouse te maken.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-114">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="4bd4b-115">SSDT voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="4bd4b-116">Als u Visual Studio hebt, hebt u dit waarschijnlijk al.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="4bd4b-117">Zie [Visual Studio en SSDT installeren][Installing Visual Studio and SSDT] voor instructies en opties voor de installatie.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="4bd4b-118">De volledig gekwalificeerde SQL-servernaam.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-118">The fully qualified SQL server name.</span></span> <span data-ttu-id="4bd4b-119">Zie [Verbinding maken met SQL Data Warehouse][Connect to SQL Data Warehouse] om dit te vinden.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-119">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

## <a name="1-connect-to-your-sql-data-warehouse"></a><span data-ttu-id="4bd4b-120">1. Verbinding maken met uw SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4bd4b-120">1. Connect to your SQL Data Warehouse</span></span>
1. <span data-ttu-id="4bd4b-121">Open Visual Studio 2013 of 2015.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="4bd4b-122">Open SQL Server-objectverkenner.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="4bd4b-123">Daartoe selecteert u **View** > **SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-123">To do this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![SQL Server-objectverkenner][1]
3. <span data-ttu-id="4bd4b-125">Klik op het pictogram **SQL Server toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-125">Click the **Add SQL Server** icon.</span></span>
   
    ![SQL Server toevoegen][2]
4. <span data-ttu-id="4bd4b-127">Vul de velden in het venster Connect to Server (Verbinding maken met server) in.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-127">Fill in the fields in the Connect to Server window.</span></span>
   
    ![Verbinding maken met server][3]
   
   * <span data-ttu-id="4bd4b-129">**Server name** (Servernaam).</span><span class="sxs-lookup"><span data-stu-id="4bd4b-129">**Server name**.</span></span> <span data-ttu-id="4bd4b-130">Voer de eerder vastgestelde **servernaam** in.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-130">Enter the **server name** previously identified.</span></span>
   * <span data-ttu-id="4bd4b-131">**Authentication** (Verificatie).</span><span class="sxs-lookup"><span data-stu-id="4bd4b-131">**Authentication**.</span></span> <span data-ttu-id="4bd4b-132">Selecteer **SQL Server Authentication** (SQL Server-verificatie) of **Active Directory Integrated Authentication** (Geïntegreerde Active Directory-verificatie).</span><span class="sxs-lookup"><span data-stu-id="4bd4b-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="4bd4b-133">**User Name** (Gebruikersnaam) en **Password** (Wachtwoord).</span><span class="sxs-lookup"><span data-stu-id="4bd4b-133">**User Name** and **Password**.</span></span> <span data-ttu-id="4bd4b-134">Voer de gebruikersnaam en het wachtwoord in als u hierboven SQL Server-verificatie hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="4bd4b-135">Klik op **Connect** (Verbinden).</span><span class="sxs-lookup"><span data-stu-id="4bd4b-135">Click **Connect**.</span></span>
5. <span data-ttu-id="4bd4b-136">U kunt de Azure SQL-server uitvouwen als u deze wilt verkennen.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-136">To explore, expand your Azure SQL server.</span></span> <span data-ttu-id="4bd4b-137">U kunt de databases weergeven die aan de server zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-137">You can view the databases associated with the server.</span></span> <span data-ttu-id="4bd4b-138">Vouw AdventureWorksDW uit als u de tabellen in de voorbeelddatabase wilt zien.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-138">Expand AdventureWorksDW to see the tables in your sample database.</span></span>
   
    ![AdventureWorksDW verkennen][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="4bd4b-140">2. Een voorbeeldquery uitvoeren</span><span class="sxs-lookup"><span data-stu-id="4bd4b-140">2. Run a sample query</span></span>
<span data-ttu-id="4bd4b-141">Nu er een verbinding met uw database is ingesteld, gaat u een query schrijven.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-141">Now that a connection has been established to your database, let's write a query.</span></span>

1. <span data-ttu-id="4bd4b-142">Klik met de rechtermuisknop op de database in SQL Server-objectverkenner.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="4bd4b-143">Selecteer **New Query** (Nieuwe query).</span><span class="sxs-lookup"><span data-stu-id="4bd4b-143">Select **New Query**.</span></span> <span data-ttu-id="4bd4b-144">Een nieuwe queryvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-144">A new query window opens.</span></span>
   
    ![Nieuwe query][5]
3. <span data-ttu-id="4bd4b-146">Kopieer de volgende TSQL-query naar het queryvenster:</span><span class="sxs-lookup"><span data-stu-id="4bd4b-146">Copy this TSQL query into the query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="4bd4b-147">Voer de query uit.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-147">Run the query.</span></span> <span data-ttu-id="4bd4b-148">Daartoe klikt u op de groene pijl of gebruikt u de volgende snelkoppeling: `CTRL`+`SHIFT`+`E`.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-148">To do this, click the green arrow or use the following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![Query uitvoeren][6]
5. <span data-ttu-id="4bd4b-150">Bekijk de resultaten van de query.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-150">Look at the query results.</span></span> <span data-ttu-id="4bd4b-151">In dit voorbeeld heeft de tabel FactInternetSales 60398 rijen.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-151">In this example, the FactInternetSales table has 60398 rows.</span></span>
   
    ![Queryresultaten][7]

## <a name="next-steps"></a><span data-ttu-id="4bd4b-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4bd4b-153">Next steps</span></span>
<span data-ttu-id="4bd4b-154">Nu u weet hoe u verbinding maakt en een query uitvoert, kunt u proberen [de gegevens te visualiseren met Power BI][visualizing the data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="4bd4b-154">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span></span>

<span data-ttu-id="4bd4b-155">Zie [Verifiëren bij SQL Data Warehouse][Authenticate to SQL Data Warehouse] om uw omgeving te configureren voor Azure Active Directory-verificatie.</span><span class="sxs-lookup"><span data-stu-id="4bd4b-155">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

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
