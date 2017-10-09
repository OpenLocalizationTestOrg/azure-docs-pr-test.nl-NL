---
title: Activiteiten van de Server opgeslagen Procedure aaaSQL
description: Meer informatie over hoe u kunt Hallo activiteit opgeslagen Procedure van SQL Server tooinvoke een opgeslagen procedure in een Azure SQL Database of een Azure SQL Data Warehouse van een Data Factory-pijplijn.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="1a765-103">SQL Server opgeslagen Procedure-activiteit</span><span class="sxs-lookup"><span data-stu-id="1a765-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="1a765-104">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="1a765-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="1a765-105">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="1a765-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="1a765-106">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="1a765-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="1a765-107">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="1a765-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="1a765-108">Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="1a765-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="1a765-109">Machine Learning-batchuitvoeringsactiviteit</span><span class="sxs-lookup"><span data-stu-id="1a765-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="1a765-110">Machine Learning-activiteit resources bijwerken</span><span class="sxs-lookup"><span data-stu-id="1a765-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="1a765-111">Opgeslagen procedureactiviteit</span><span class="sxs-lookup"><span data-stu-id="1a765-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="1a765-112">Data Lake Analytics U-SQL-activiteit</span><span class="sxs-lookup"><span data-stu-id="1a765-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="1a765-113">Aangepaste activiteit .NET</span><span class="sxs-lookup"><span data-stu-id="1a765-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="1a765-114">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1a765-114">Overview</span></span>
<span data-ttu-id="1a765-115">U activiteiten voor gegevenstransformatie gebruiken in een Data Factory [pijplijn](data-factory-create-pipelines.md) tootransform en proces onbewerkte gegevens in de voorspellingen en inzichten.</span><span class="sxs-lookup"><span data-stu-id="1a765-115">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) tootransform and process raw data into predictions and insights.</span></span> <span data-ttu-id="1a765-116">Hallo is activiteit opgeslagen Procedure een van activiteiten voor gegevenstransformatie Hallo die ondersteuning biedt voor Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a765-116">hello Stored Procedure Activity is one of hello transformation activities that Data Factory supports.</span></span> <span data-ttu-id="1a765-117">In dit artikel is gebaseerd op Hallo [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) artikel, hetgeen een algemeen overzicht van gegevenstransformatie en Hallo ondersteund activiteiten voor gegevenstransformatie in Data Factory toont.</span><span class="sxs-lookup"><span data-stu-id="1a765-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="1a765-118">Hallo activiteit opgeslagen Procedure tooinvoke een opgeslagen procedure in een Hallo volgt gegevens worden opgeslagen in uw onderneming of op Azure een virtuele machine (VM), kunt u gebruiken:</span><span class="sxs-lookup"><span data-stu-id="1a765-118">You can use hello Stored Procedure Activity tooinvoke a stored procedure in one of hello following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="1a765-119">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="1a765-119">Azure SQL Database</span></span>
- <span data-ttu-id="1a765-120">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1a765-120">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="1a765-121">SQL Server-Database.</span><span class="sxs-lookup"><span data-stu-id="1a765-121">SQL Server Database.</span></span>  <span data-ttu-id="1a765-122">Als u SQL Server gebruikt, moet u Data Management Gateway installeren op dezelfde machine dat hosts Hallo database of op een afzonderlijke computer die toegang toohello database Hallo.</span><span class="sxs-lookup"><span data-stu-id="1a765-122">If you are using SQL Server, install Data Management Gateway on hello same machine that hosts hello database or on a separate machine that has access toohello database.</span></span> <span data-ttu-id="1a765-123">Data Management Gateway is een onderdeel dat wordt verbinding gemaakt op-premises/op virtuele machine van Azure met cloudservices gegevensbronnen op een manier veilig en beheerd.</span><span class="sxs-lookup"><span data-stu-id="1a765-123">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="1a765-124">Zie [Data Management Gateway](data-factory-data-management-gateway.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1a765-124">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a765-125">Wanneer gegevens worden gekopieerd naar Azure SQL Database of SQL Server, kunt u Hallo **SqlSink** in kopiëren activiteit tooinvoke een opgeslagen procedure met behulp van Hallo **sqlWriterStoredProcedureName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="1a765-125">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="1a765-126">Zie voor meer informatie [aanroepen van opgeslagen procedure uit kopieeractiviteit](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="1a765-126">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="1a765-127">Voor meer informatie over het Hallo-eigenschap, Zie de volgende artikelen connector: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a765-127">For details about hello property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span> <span data-ttu-id="1a765-128">Een opgeslagen procedure aanroepen tijdens het kopiëren van gegevens in een Azure SQL Data Warehouse met behulp van een kopieeractiviteit wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="1a765-128">Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported.</span></span> <span data-ttu-id="1a765-129">Maar u kunt Hallo opgeslagen procedure activiteit tooinvoke een opgeslagen procedure gebruiken in een SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1a765-129">But, you can use hello stored procedure activity tooinvoke a stored procedure in a SQL Data Warehouse.</span></span> 
>  
> <span data-ttu-id="1a765-130">Wanneer het kopiëren van gegevens van Azure SQL Database of SQL Server of Azure SQL Data Warehouse, kunt u configureren **SqlSource** in kopiëren activiteit tooinvoke een opgeslagen procedure tooread gegevens uit de brondatabase Hallo via Hallo  **sqlReaderStoredProcedureName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="1a765-130">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="1a765-131">Zie voor meer informatie, Hallo connector artikelen te volgen: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="1a765-131">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          


<span data-ttu-id="1a765-132">Hallo volgen stapsgewijze Kennismaking gebruikt Hallo activiteit opgeslagen Procedure in een pijplijn tooinvoke een opgeslagen procedure in een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="1a765-132">hello following walkthrough uses hello Stored Procedure Activity in a pipeline tooinvoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="1a765-133">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="1a765-133">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="1a765-134">Voorbeeldtabel en opgeslagen procedure</span><span class="sxs-lookup"><span data-stu-id="1a765-134">Sample table and stored procedure</span></span>
1. <span data-ttu-id="1a765-135">Maak de volgende Hallo **tabel** in uw Azure SQL Database met behulp van SQL Server Management Studio of een ander hulpmiddel u vertrouwd met bent.</span><span class="sxs-lookup"><span data-stu-id="1a765-135">Create hello following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="1a765-136">Hallo datum kolom is Hallo-datum en tijd wanneer de bijbehorende ID hello wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="1a765-136">hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    <span data-ttu-id="1a765-137">ID is uniek geïdentificeerd Hallo en Hallo datum kolom is Hallo-datum en tijd wanneer de bijbehorende ID hello wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="1a765-137">Id is hello unique identified and hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>
    
    ![Voorbeeldgegevens](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="1a765-139">Hallo opgeslagen procedure wordt in dit voorbeeld wordt een Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="1a765-139">In this sample, hello stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="1a765-140">Als hello opgeslagen procedure in een Azure SQL Data Warehouse en SQL Server-Database is, lijkt Hallo benadering.</span><span class="sxs-lookup"><span data-stu-id="1a765-140">If hello stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, hello approach is similar.</span></span> <span data-ttu-id="1a765-141">Voor een SQL Server-database, moet u een [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="1a765-141">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="1a765-142">Maak de volgende Hallo **opgeslagen procedure** die voegt de gegevens in toohello **sampletable**.</span><span class="sxs-lookup"><span data-stu-id="1a765-142">Create hello following **stored procedure** that inserts data in toohello **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="1a765-143">**Naam** en **hoofdlettergebruik** Hallo parameter (DateTime in dit voorbeeld) moet overeenkomen met die van de parameter die is opgegeven in de Hallo pijplijn activiteit JSON.</span><span class="sxs-lookup"><span data-stu-id="1a765-143">**Name** and **casing** of hello parameter (DateTime in this example) must match that of parameter specified in hello pipeline/activity JSON.</span></span> <span data-ttu-id="1a765-144">In de definitie van de opgeslagen procedure hello, zorg ervoor dat  **@**  wordt gebruikt als een voorvoegsel voor Hallo-parameter.</span><span class="sxs-lookup"><span data-stu-id="1a765-144">In hello stored procedure definition, ensure that **@** is used as a prefix for hello parameter.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="1a765-145">Een data factory maken</span><span class="sxs-lookup"><span data-stu-id="1a765-145">Create a data factory</span></span>
1. <span data-ttu-id="1a765-146">Meld u bij te[Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1a765-146">Log in too[Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1a765-147">Klik op **nieuw** op Hallo menu links, klikt u op **Intelligence en analyse**, en klik op **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="1a765-147">Click **NEW** on hello left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![Nieuwe gegevensfactory](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="1a765-149">In Hallo **nieuwe gegevensfactory** blade Voer **SProcDF** voor Hallo naam.</span><span class="sxs-lookup"><span data-stu-id="1a765-149">In hello **New data factory** blade, enter **SProcDF** for hello Name.</span></span> <span data-ttu-id="1a765-150">Azure Data Factory-namen zijn **globaal unieke**.</span><span class="sxs-lookup"><span data-stu-id="1a765-150">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="1a765-151">U moet tooprefix Hallo-naam van gegevensfactory Hallo met de naam van uw tooenable Hallo gemaakt Hallo factory.</span><span class="sxs-lookup"><span data-stu-id="1a765-151">You need tooprefix hello name of hello data factory with your name, tooenable hello successful creation of hello factory.</span></span>

   ![Nieuwe gegevensfactory](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="1a765-153">Selecteer uw **Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="1a765-153">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="1a765-154">Voor **resourcegroep**, doe Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1a765-154">For **Resource Group**, do one of hello following steps:</span></span>
   1. <span data-ttu-id="1a765-155">Klik op **nieuw** en voer een naam voor de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="1a765-155">Click **Create new** and enter a name for hello resource group.</span></span>
   2. <span data-ttu-id="1a765-156">Klik op **gebruik bestaande** en selecteer een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="1a765-156">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="1a765-157">Selecteer Hallo **locatie** voor Hallo data factory.</span><span class="sxs-lookup"><span data-stu-id="1a765-157">Select hello **location** for hello data factory.</span></span>
7. <span data-ttu-id="1a765-158">Selecteer **pincode toodashboard** zodat u Hallo gegevensfactory op Hallo dashboard volgende keer dat u zich zien kunt aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="1a765-158">Select **Pin toodashboard** so that you can see hello data factory on hello dashboard next time you log in.</span></span>
8. <span data-ttu-id="1a765-159">Klik op **maken** op Hallo **nieuwe gegevensfactory** blade.</span><span class="sxs-lookup"><span data-stu-id="1a765-159">Click **Create** on hello **New data factory** blade.</span></span>
9. <span data-ttu-id="1a765-160">Zie van Hallo gegevensfactory wordt gemaakt in Hallo **dashboard** Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1a765-160">You see hello data factory being created in hello **dashboard** of hello Azure portal.</span></span> <span data-ttu-id="1a765-161">Nadat het Hallo-gegevensfactory is gemaakt, ziet u Hallo data factory-pagina waarop u inhoud van de gegevensfactory Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="1a765-161">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![Data Factory-startpagina](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="1a765-163">Een Azure SQL gekoppelde service maken</span><span class="sxs-lookup"><span data-stu-id="1a765-163">Create an Azure SQL linked service</span></span>
<span data-ttu-id="1a765-164">Na het maken van de gegevensfactory hello, moet u een Azure SQL gekoppelde service die is gekoppeld aan uw Azure SQL-database waarin Hallo sampletable tabel en sp_sample opgeslagen procedure, tooyour data factory maken.</span><span class="sxs-lookup"><span data-stu-id="1a765-164">After creating hello data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains hello sampletable table and sp_sample stored procedure, tooyour data factory.</span></span>

1. <span data-ttu-id="1a765-165">Klik op **auteur en implementeren van** op Hallo **Data Factory** blade voor **SProcDF** toolaunch Hallo Data Factory-Editor.</span><span class="sxs-lookup"><span data-stu-id="1a765-165">Click **Author and deploy** on hello **Data Factory** blade for **SProcDF** toolaunch hello Data Factory Editor.</span></span>
2. <span data-ttu-id="1a765-166">Klik op **nieuwe gegevensopslag** op Hallo opdrachtbalk en kies **Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="1a765-166">Click **New data store** on hello command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="1a765-167">U ziet Hallo JSON-script voor het maken van een Azure SQL gekoppelde service in Hallo-editor.</span><span class="sxs-lookup"><span data-stu-id="1a765-167">You should see hello JSON script for creating an Azure SQL linked service in hello editor.</span></span>

   ![Nieuwe gegevensopslag](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="1a765-169">Controleer in Hallo JSON-script, Hallo volgende wijzigingen:</span><span class="sxs-lookup"><span data-stu-id="1a765-169">In hello JSON script, make hello following changes:</span></span>

   1. <span data-ttu-id="1a765-170">Vervang `<servername>` met Hallo-naam van uw Azure SQL Database-server.</span><span class="sxs-lookup"><span data-stu-id="1a765-170">Replace `<servername>` with hello name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="1a765-171">Vervang `<databasename>` opgeslagen procedure met Hallo-database waarin u Hallo tabel en Hallo gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1a765-171">Replace `<databasename>` with hello database in which you created hello table and hello stored procedure.</span></span>
   3. <span data-ttu-id="1a765-172">Vervang `<username@servername>` met Hallo-gebruikersaccount dat toegang toohello database heeft.</span><span class="sxs-lookup"><span data-stu-id="1a765-172">Replace `<username@servername>` with hello user account that has access toohello database.</span></span>
   4. <span data-ttu-id="1a765-173">Vervang `<password>` met wachtwoord voor gebruikersaccount Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="1a765-173">Replace `<password>` with hello password for hello user account.</span></span>

      ![Nieuwe gegevensopslag](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="1a765-175">toodeploy Hallo gekoppelde service, klikt u op **implementeren** op Hallo opdrachtbalk klikken.</span><span class="sxs-lookup"><span data-stu-id="1a765-175">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="1a765-176">Controleer of u Hallo AzureSqlLinkedService in Hallo structuur op Hallo links weergeven.</span><span class="sxs-lookup"><span data-stu-id="1a765-176">Confirm that you see hello AzureSqlLinkedService in hello tree view on hello left.</span></span>

    ![structuurweergave met gekoppelde service](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="1a765-178">Een uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="1a765-178">Create an output dataset</span></span>
<span data-ttu-id="1a765-179">Geef dat een uitvoergegevensset voor een activiteit opgeslagen procedure zelfs als Hallo procedure opgeslagen geen produceert geen gegevens.</span><span class="sxs-lookup"><span data-stu-id="1a765-179">You must specify an output dataset for a stored procedure activity even if hello stored procedure does not produce any data.</span></span> <span data-ttu-id="1a765-180">Dat komt doordat de Hallo uitvoergegevensset die stations Hallo planning van Hallo activiteit (hoe vaak hello activiteit wordt uitgevoerd - per uur, dagelijks, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="1a765-180">That's because it's hello output dataset that drives hello schedule of hello activity (how often hello activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="1a765-181">Hallo uitvoergegevensset moet gebruiken een **gekoppelde service** die tooan Azure SQL Database of een Azure SQL Data Warehouse of een SQL Server-Database die u wilt opgeslagen procedure toorun Hallo verwijst.</span><span class="sxs-lookup"><span data-stu-id="1a765-181">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="1a765-182">Hallo uitvoergegevensset kan fungeren als een manier toopass Hallo resultaat van Hallo opgeslagen procedure voor verdere verwerking door een andere activiteit ([activiteiten chaining](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="1a765-182">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="1a765-183">Data Factory biedt Hallo-uitvoer van een gegevensset met de opgeslagen procedure toothis echter automatisch niet schrijven.</span><span class="sxs-lookup"><span data-stu-id="1a765-183">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="1a765-184">Het is Hallo opgeslagen procedure dat SQL-tabel voor schrijfbewerkingen tooa Hallo uitvoer gegevensset verwijst naar.</span><span class="sxs-lookup"><span data-stu-id="1a765-184">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="1a765-185">In sommige gevallen Hallo uitvoergegevensset mag een **dummy gegevensset** (een gegevensset die tooa tabel waarop geen echt uitvoer Hallo verwijst opgeslagen procedure).</span><span class="sxs-lookup"><span data-stu-id="1a765-185">In some cases, hello output dataset can be a **dummy dataset** (a dataset that points tooa table that does not really hold output of hello stored procedure).</span></span> <span data-ttu-id="1a765-186">Dit dummy-gegevensset wordt alleen toospecify Hallo schema voor het uitvoeren van Hallo procedure-activiteit opgeslagen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1a765-186">This dummy dataset is used only toospecify hello schedule for running hello stored procedure activity.</span></span> 

1. <span data-ttu-id="1a765-187">Klik op **... Meer** op de werkbalk Hallo **nieuwe gegevensset**, en klik op **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="1a765-187">Click **... More** on hello toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="1a765-188">**Nieuwe gegevensset** op Hallo opdracht en selecteer **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="1a765-188">**New dataset** on hello command bar and select **Azure SQL**.</span></span>

    ![structuurweergave met gekoppelde service](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="1a765-190">Kopiëren en plakken hello volgende JSON-script in toohello JSON-editor.</span><span class="sxs-lookup"><span data-stu-id="1a765-190">Copy/paste hello following JSON script in toohello JSON editor.</span></span>

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="1a765-191">toodeploy Hallo gegevensset, klikt u op **implementeren** op Hallo opdrachtbalk klikken.</span><span class="sxs-lookup"><span data-stu-id="1a765-191">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="1a765-192">Controleer of u Hallo gegevensset in de structuurweergave Hallo.</span><span class="sxs-lookup"><span data-stu-id="1a765-192">Confirm that you see hello dataset in hello tree view.</span></span>

    ![Structuurweergave met gekoppelde services](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="1a765-194">Een pijplijn maken met SqlServerStoredProcedure activiteit</span><span class="sxs-lookup"><span data-stu-id="1a765-194">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="1a765-195">Nu gaan we een pijplijn maken met een activiteit opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="1a765-195">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="1a765-196">U ziet Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="1a765-196">Notice hello following properties:</span></span> 

- <span data-ttu-id="1a765-197">Hallo **type** eigenschap is ingesteld, te**SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="1a765-197">hello **type** property is set too**SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="1a765-198">Hallo **storedProcedureName** in het type-eigenschappen te ingesteld**sp_sample** (naam van Hallo opgeslagen procedure).</span><span class="sxs-lookup"><span data-stu-id="1a765-198">hello **storedProcedureName** in type properties is set too**sp_sample** (name of hello stored procedure).</span></span>
- <span data-ttu-id="1a765-199">Hallo **storedProcedureParameters** sectie bevat een parameter met de naam **datum/tijd**.</span><span class="sxs-lookup"><span data-stu-id="1a765-199">hello **storedProcedureParameters** section contains one parameter named **DataTime**.</span></span> <span data-ttu-id="1a765-200">Naam en het hoofdlettergebruik van Hallo-parameter in JSON moeten overeenkomen met Hallo naam en het hoofdlettergebruik van Hallo-parameter in de definitie van Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="1a765-200">Name and casing of hello parameter in JSON must match hello name and casing of hello parameter in hello stored procedure definition.</span></span> <span data-ttu-id="1a765-201">Als u null zijn voor een parameter doorgeven moet, Hallo syntaxis gebruiken: `"param1": null` (alle kleine letters).</span><span class="sxs-lookup"><span data-stu-id="1a765-201">If you need pass null for a parameter, use hello syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="1a765-202">Klik op **... Meer** op Hallo opdrachtbalk en klik op **nieuwe pijplijn**.</span><span class="sxs-lookup"><span data-stu-id="1a765-202">Click **... More** on hello command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="1a765-203">Kopiëren en plakken Hallo volgende JSON-fragment:</span><span class="sxs-lookup"><span data-stu-id="1a765-203">Copy/paste hello following JSON snippet:</span></span>   

    ```JSON
    {
        "name": "SprocActivitySamplePipeline",
        "properties": {
            "activities": [
                {
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
                        "storedProcedureName": "sp_sample",
                        "storedProcedureParameters": {
                            "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                        }
                    },
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. <span data-ttu-id="1a765-204">toodeploy hello pipeline, klikt u op **implementeren** op Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="1a765-204">toodeploy hello pipeline, click **Deploy** on hello toolbar.</span></span>  

### <a name="monitor-hello-pipeline"></a><span data-ttu-id="1a765-205">Hallo-pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="1a765-205">Monitor hello pipeline</span></span>
1. <span data-ttu-id="1a765-206">Klik op **X** tooclose Data Factory-Editor blades toonavigate back-toohello Data Factory-blade en klik op **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="1a765-206">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![Tegel diagram](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="1a765-208">In Hallo **diagramweergave**, ziet u een overzicht van Hallo pijplijnen en gegevenssets gebruikt in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="1a765-208">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![Tegel diagram](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="1a765-210">Dubbelklik in de diagramweergave hello, op Hallo gegevensset `sprocsampleout`.</span><span class="sxs-lookup"><span data-stu-id="1a765-210">In hello Diagram View, double-click hello dataset `sprocsampleout`.</span></span> <span data-ttu-id="1a765-211">U ziet Hallo segmenten in de status Ready heeft.</span><span class="sxs-lookup"><span data-stu-id="1a765-211">You see hello slices in Ready state.</span></span> <span data-ttu-id="1a765-212">Moet er vijf segmenten omdat een segment wordt geproduceerd voor elk uur tussen Hallo-begintijd en eindtijd van Hallo JSON.</span><span class="sxs-lookup"><span data-stu-id="1a765-212">There should be five slices because a slice is produced for each hour between hello start time and end time from hello JSON.</span></span>

    ![Tegel diagram](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="1a765-214">Wanneer een segment is in **gereed** staat, voer een `select * from sampletable` -query op Hallo Azure SQL database tooverify die gegevens Hallo is ingevoegd in de tabel toohello door Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="1a765-214">When a slice is in **Ready** state, run a `select * from sampletable` query against hello Azure SQL database tooverify that hello data was inserted in toohello table by hello stored procedure.</span></span>

   ![uitvoergegevens](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="1a765-216">Zie [Hallo-pijplijn bewaken](data-factory-monitor-manage-pipelines.md) voor gedetailleerde informatie over het Azure Data Factory-pijplijnen bewaken.</span><span class="sxs-lookup"><span data-stu-id="1a765-216">See [Monitor hello pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="1a765-217">Geef een invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="1a765-217">Specify an input dataset</span></span>
<span data-ttu-id="1a765-218">In scenario Hallo heeft activiteit opgeslagen procedure geen eventuele invoergegevenssets.</span><span class="sxs-lookup"><span data-stu-id="1a765-218">In hello walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="1a765-219">Als u een invoergegevensset opgeeft, hello activiteit opgeslagen procedure wordt niet uitgevoerd totdat Hallo segment van de invoergegevensset beschikbaar (in de status Ready heeft is).</span><span class="sxs-lookup"><span data-stu-id="1a765-219">If you specify an input dataset, hello stored procedure activity does not run until hello slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="1a765-220">Hallo dataset kan een externe gegevensset zijn (dat niet wordt geproduceerd door een andere activiteit in Hallo dezelfde pijplijn) of een interne gegevensset die wordt geproduceerd door een upstream-activiteit (Hallo-activiteit die wordt uitgevoerd voordat deze activiteit).</span><span class="sxs-lookup"><span data-stu-id="1a765-220">hello dataset can be an external dataset (that is not produced by another activity in hello same pipeline) or an internal dataset that is produced by an upstream activity (hello activity that runs before this activity).</span></span> <span data-ttu-id="1a765-221">U kunt meerdere invoergegevenssets voor Hallo opgeslagen procedure activiteit opgeven.</span><span class="sxs-lookup"><span data-stu-id="1a765-221">You can specify multiple input datasets for hello stored procedure activity.</span></span> <span data-ttu-id="1a765-222">Als u doet dit, hello activiteit opgeslagen procedure wordt alleen uitgevoerd als alle Hallo invoergegevensset segmenten beschikbaar (in de status Ready heeft zijn).</span><span class="sxs-lookup"><span data-stu-id="1a765-222">If you do so, hello stored procedure activity runs only when all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="1a765-223">Hallo invoergegevensset kan niet worden gebruikt in Hallo opgeslagen procedure als een parameter.</span><span class="sxs-lookup"><span data-stu-id="1a765-223">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="1a765-224">Het is alleen gebruikte toocheck Hallo afhankelijkheid voordat begin Hallo procedure-activiteit opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1a765-224">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="1a765-225">Keten met andere activiteiten</span><span class="sxs-lookup"><span data-stu-id="1a765-225">Chaining with other activities</span></span>
<span data-ttu-id="1a765-226">Als u een upstream-activiteit met deze activiteit toochain wilt, geef Hallo-uitvoer van de upstream-activiteit Hallo als invoer van deze activiteit.</span><span class="sxs-lookup"><span data-stu-id="1a765-226">If you want toochain an upstream activity with this activity, specify hello output of hello upstream activity as an input of this activity.</span></span> <span data-ttu-id="1a765-227">Wanneer u doet dit, hello activiteit opgeslagen procedure wordt niet uitgevoerd totdat de Hallo upstream-activiteit is voltooid en de uitvoergegevensset Hallo van Hallo upstream-activiteit (in de status gereed) beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="1a765-227">When you do so, hello stored procedure activity does not run until hello upstream activity completes and hello output dataset of hello upstream activity is available (in Ready status).</span></span> <span data-ttu-id="1a765-228">U kunt uitvoergegevenssets uit meerdere activiteiten van de upstream opgeven als invoer gegevenssets van de activiteit van Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="1a765-228">You can specify output datasets of multiple upstream activities as input datasets of hello stored procedure activity.</span></span> <span data-ttu-id="1a765-229">Wanneer u dit doet, Hallo opgeslagen procedure activiteit wordt alleen uitgevoerd als alle Hallo invoergegevensset segmenten beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="1a765-229">When you do so, hello stored procedure activity runs only when all hello input dataset slices are available.</span></span>  

<span data-ttu-id="1a765-230">In Hallo voorbeeld te volgen, is het Hallo-uitvoer van de kopieeractiviteit Hallo: OutputDataset die invoer Hallo opgeslagen procedure-activiteit.</span><span class="sxs-lookup"><span data-stu-id="1a765-230">In hello following example, hello output of hello copy activity is: OutputDataset, which is an input of hello stored procedure activity.</span></span> <span data-ttu-id="1a765-231">Daarom hello activiteit opgeslagen procedure wordt niet uitgevoerd totdat Hallo kopieeractiviteit is voltooid en Hallo OutputDataset segment (op status gereed) beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="1a765-231">Therefore, hello stored procedure activity does not run until hello copy activity completes and hello OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="1a765-232">Als u meerdere invoergegevenssets opgeeft, hello activiteit opgeslagen procedure wordt niet uitgevoerd totdat alle Hallo invoergegevensset segmenten beschikbaar (in de status Ready heeft zijn).</span><span class="sxs-lookup"><span data-stu-id="1a765-232">If you specify multiple input datasets, hello stored procedure activity does not run until all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="1a765-233">Hallo invoergegevenssets kan niet rechtstreeks worden gebruikt als parameters toohello opgeslagen procedure activiteit.</span><span class="sxs-lookup"><span data-stu-id="1a765-233">hello input datasets cannot be used directly as parameters toohello stored procedure activity.</span></span> 

<span data-ttu-id="1a765-234">Zie voor meer informatie over het koppelen van activiteiten [meerdere activiteiten in een pijplijn](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span><span class="sxs-lookup"><span data-stu-id="1a765-234">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

<span data-ttu-id="1a765-235">Op deze manier toolink Hallo store activiteit procedure met **downstream-activiteiten** (Hallo activiteiten die worden uitgevoerd nadat hello activiteit opgeslagen procedure is voltooid), geef de uitvoergegevensset Hallo van Hallo opgeslagen procedure activiteit als een invoer van Hallo downstream activiteit in Hallo-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="1a765-235">Similarly, toolink hello store procedure activity with **downstream activities** (hello activities that run after hello stored procedure activity completes), specify hello output dataset of hello stored procedure activity as an input of hello downstream activity in hello pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a765-236">Wanneer gegevens worden gekopieerd naar Azure SQL Database of SQL Server, kunt u Hallo **SqlSink** in kopiëren activiteit tooinvoke een opgeslagen procedure met behulp van Hallo **sqlWriterStoredProcedureName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="1a765-236">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="1a765-237">Zie voor meer informatie [aanroepen van opgeslagen procedure uit kopieeractiviteit](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="1a765-237">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="1a765-238">Zie voor meer informatie over de eigenschap Hallo Hallo connector artikelen te volgen: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a765-238">For details about hello property, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span>
>  
> <span data-ttu-id="1a765-239">Wanneer het kopiëren van gegevens van Azure SQL Database of SQL Server of Azure SQL Data Warehouse, kunt u configureren **SqlSource** in kopiëren activiteit tooinvoke een opgeslagen procedure tooread gegevens uit de brondatabase Hallo via Hallo  **sqlReaderStoredProcedureName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="1a765-239">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="1a765-240">Zie voor meer informatie, Hallo connector artikelen te volgen: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="1a765-240">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          

## <a name="json-format"></a><span data-ttu-id="1a765-241">JSON-indeling</span><span class="sxs-lookup"><span data-stu-id="1a765-241">JSON format</span></span>
<span data-ttu-id="1a765-242">Hier volgt Hallo JSON-indeling voor het definiëren van een activiteit opgeslagen Procedure:</span><span class="sxs-lookup"><span data-stu-id="1a765-242">Here is hello JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

<span data-ttu-id="1a765-243">Hallo volgende tabel beschrijft deze JSON-eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="1a765-243">hello following table describes these JSON properties:</span></span>

| <span data-ttu-id="1a765-244">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="1a765-244">Property</span></span> | <span data-ttu-id="1a765-245">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1a765-245">Description</span></span> | <span data-ttu-id="1a765-246">Vereist</span><span class="sxs-lookup"><span data-stu-id="1a765-246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a765-247">naam</span><span class="sxs-lookup"><span data-stu-id="1a765-247">name</span></span> | <span data-ttu-id="1a765-248">Naam van de activiteit Hallo</span><span class="sxs-lookup"><span data-stu-id="1a765-248">Name of hello activity</span></span> |<span data-ttu-id="1a765-249">Ja</span><span class="sxs-lookup"><span data-stu-id="1a765-249">Yes</span></span> |
| <span data-ttu-id="1a765-250">description</span><span class="sxs-lookup"><span data-stu-id="1a765-250">description</span></span> |<span data-ttu-id="1a765-251">Tekst die beschrijft wat Hallo-activiteit wordt gebruikt voor</span><span class="sxs-lookup"><span data-stu-id="1a765-251">Text describing what hello activity is used for</span></span> |<span data-ttu-id="1a765-252">Nee</span><span class="sxs-lookup"><span data-stu-id="1a765-252">No</span></span> |
| <span data-ttu-id="1a765-253">type</span><span class="sxs-lookup"><span data-stu-id="1a765-253">type</span></span> | <span data-ttu-id="1a765-254">Moet worden ingesteld op: **SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="1a765-254">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="1a765-255">Ja</span><span class="sxs-lookup"><span data-stu-id="1a765-255">Yes</span></span> |
| <span data-ttu-id="1a765-256">Invoer</span><span class="sxs-lookup"><span data-stu-id="1a765-256">inputs</span></span> | <span data-ttu-id="1a765-257">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="1a765-257">Optional.</span></span> <span data-ttu-id="1a765-258">Als u een invoergegevensset opgeeft, moet dit beschikbaar is (in de status 'Gereed') voor Hallo opgeslagen procedure activiteit toorun.</span><span class="sxs-lookup"><span data-stu-id="1a765-258">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="1a765-259">Hallo invoergegevensset kan niet worden gebruikt in Hallo opgeslagen procedure als een parameter.</span><span class="sxs-lookup"><span data-stu-id="1a765-259">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="1a765-260">Het is alleen gebruikte toocheck Hallo afhankelijkheid voordat begin Hallo procedure-activiteit opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1a765-260">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> |<span data-ttu-id="1a765-261">Nee</span><span class="sxs-lookup"><span data-stu-id="1a765-261">No</span></span> |
| <span data-ttu-id="1a765-262">uitvoer</span><span class="sxs-lookup"><span data-stu-id="1a765-262">outputs</span></span> | <span data-ttu-id="1a765-263">U moet een uitvoergegevensset voor een activiteit opgeslagen procedure opgeven.</span><span class="sxs-lookup"><span data-stu-id="1a765-263">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="1a765-264">Uitvoergegevensset geeft Hallo **planning** voor Hallo opgeslagen procedure activiteit (elk uur, wekelijks, maandelijks, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="1a765-264">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="1a765-265">Hallo uitvoergegevensset moet gebruiken een **gekoppelde service** die tooan Azure SQL Database of een Azure SQL Data Warehouse of een SQL Server-Database die u wilt opgeslagen procedure toorun Hallo verwijst.</span><span class="sxs-lookup"><span data-stu-id="1a765-265">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <br/><br/><span data-ttu-id="1a765-266">Hallo uitvoergegevensset kan fungeren als een manier toopass Hallo resultaat van Hallo opgeslagen procedure voor verdere verwerking door een andere activiteit ([activiteiten chaining](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="1a765-266">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="1a765-267">Data Factory biedt Hallo-uitvoer van een gegevensset met de opgeslagen procedure toothis echter automatisch niet schrijven.</span><span class="sxs-lookup"><span data-stu-id="1a765-267">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="1a765-268">Het is Hallo opgeslagen procedure dat SQL-tabel voor schrijfbewerkingen tooa Hallo uitvoer gegevensset verwijst naar.</span><span class="sxs-lookup"><span data-stu-id="1a765-268">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <br/><br/><span data-ttu-id="1a765-269">In sommige gevallen Hallo uitvoergegevensset mag een **dummy gegevensset**, waarmee alleen toospecify Hallo schema voor het uitvoeren van Hallo procedure-activiteit opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1a765-269">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span> |<span data-ttu-id="1a765-270">Ja</span><span class="sxs-lookup"><span data-stu-id="1a765-270">Yes</span></span> |
| <span data-ttu-id="1a765-271">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="1a765-271">storedProcedureName</span></span> |<span data-ttu-id="1a765-272">Hallo naam opgeven van Hallo opgeslagen procedure in hello Azure SQL database- of Azure SQL Data Warehouse of SQL Server-database die wordt vertegenwoordigd door Hallo gekoppelde service die Hallo uitvoer tabel gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1a765-272">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="1a765-273">Ja</span><span class="sxs-lookup"><span data-stu-id="1a765-273">Yes</span></span> |
| <span data-ttu-id="1a765-274">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="1a765-274">storedProcedureParameters</span></span> |<span data-ttu-id="1a765-275">Geef waarden op voor parameters van opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="1a765-275">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="1a765-276">Als u toopass null voor een parameter moet, Hallo syntaxis gebruiken: "param1": null (alle kleine letter).</span><span class="sxs-lookup"><span data-stu-id="1a765-276">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="1a765-277">Zie Hallo toolearn voorbeeld over het gebruik van deze eigenschap te volgen.</span><span class="sxs-lookup"><span data-stu-id="1a765-277">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="1a765-278">Nee</span><span class="sxs-lookup"><span data-stu-id="1a765-278">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="1a765-279">Het doorgeven van een statische waarde</span><span class="sxs-lookup"><span data-stu-id="1a765-279">Passing a static value</span></span>
<span data-ttu-id="1a765-280">Nu we eens het toevoegen van een andere kolom met de naam 'Scenario' in met een statische waarde met de naam 'Document voorbeeld' Hallo-tabel.</span><span class="sxs-lookup"><span data-stu-id="1a765-280">Now, let’s consider adding another column named ‘Scenario’ in hello table containing a static value called ‘Document sample’.</span></span>

![Voorbeeldgegevens 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="1a765-282">**Tabel:**</span><span class="sxs-lookup"><span data-stu-id="1a765-282">**Table:**</span></span>

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

<span data-ttu-id="1a765-283">**Opgeslagen procedure:**</span><span class="sxs-lookup"><span data-stu-id="1a765-283">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="1a765-284">Nu doorgeven Hallo **Scenario** parameter en de Hallo van Hallo opgeslagen procedure-activiteit.</span><span class="sxs-lookup"><span data-stu-id="1a765-284">Now, pass hello **Scenario** parameter and hello value from hello stored procedure activity.</span></span> <span data-ttu-id="1a765-285">Hallo **typeProperties** sectie in het voorgaande voorbeeld lijkt erop volgende codefragment Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="1a765-285">hello **typeProperties** section in hello preceding sample looks like hello following snippet:</span></span>

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

<span data-ttu-id="1a765-286">**Data Factory-gegevensset:**</span><span class="sxs-lookup"><span data-stu-id="1a765-286">**Data Factory dataset:**</span></span>

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="1a765-287">**Data Factory-pijplijn**</span><span class="sxs-lookup"><span data-stu-id="1a765-287">**Data Factory pipeline**</span></span>

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```