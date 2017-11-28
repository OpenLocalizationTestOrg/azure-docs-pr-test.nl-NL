---
title: SQL Server opgeslagen Procedure-activiteit
description: Meer informatie over hoe u de SQL Server opgeslagen Procedure activiteit kunt gebruiken om aan te roepen, een opgeslagen procedure in een Azure SQL Database of een Azure SQL Data Warehouse van een Data Factory-pijplijn.
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
ms.openlocfilehash: 6505d9aa2c7ae003bd928e2fa82cd923a9615394
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="60b01-103">SQL Server opgeslagen Procedure-activiteit</span><span class="sxs-lookup"><span data-stu-id="60b01-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="60b01-104">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="60b01-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="60b01-105">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="60b01-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="60b01-106">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="60b01-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="60b01-107">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="60b01-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="60b01-108">Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="60b01-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="60b01-109">Machine Learning-batchuitvoeringsactiviteit</span><span class="sxs-lookup"><span data-stu-id="60b01-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="60b01-110">Machine Learning-activiteit resources bijwerken</span><span class="sxs-lookup"><span data-stu-id="60b01-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="60b01-111">Opgeslagen procedureactiviteit</span><span class="sxs-lookup"><span data-stu-id="60b01-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="60b01-112">Data Lake Analytics U-SQL-activiteit</span><span class="sxs-lookup"><span data-stu-id="60b01-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="60b01-113">Aangepaste activiteit .NET</span><span class="sxs-lookup"><span data-stu-id="60b01-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="60b01-114">Overzicht</span><span class="sxs-lookup"><span data-stu-id="60b01-114">Overview</span></span>
<span data-ttu-id="60b01-115">U activiteiten voor gegevenstransformatie gebruiken in een Data Factory [pijplijn](data-factory-create-pipelines.md) transformeren en verwerken van onbewerkte gegevens in de voorspellingen en inzichten.</span><span class="sxs-lookup"><span data-stu-id="60b01-115">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) to transform and process raw data into predictions and insights.</span></span> <span data-ttu-id="60b01-116">De activiteit opgeslagen Procedure is een van de activiteiten voor gegevenstransformatie die ondersteuning biedt voor Data Factory.</span><span class="sxs-lookup"><span data-stu-id="60b01-116">The Stored Procedure Activity is one of the transformation activities that Data Factory supports.</span></span> <span data-ttu-id="60b01-117">In dit artikel is gebaseerd op de [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) artikel, hetgeen een algemeen overzicht van gegevenstransformatie en de ondersteunde transformatieactiviteiten in de Data Factory toont.</span><span class="sxs-lookup"><span data-stu-id="60b01-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="60b01-118">U kunt de activiteit opgeslagen Procedure gebruiken om aan te roepen een opgeslagen procedure in een van de volgende gegevens worden opgeslagen in uw onderneming of op Azure een virtuele machine (VM):</span><span class="sxs-lookup"><span data-stu-id="60b01-118">You can use the Stored Procedure Activity to invoke a stored procedure in one of the following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="60b01-119">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="60b01-119">Azure SQL Database</span></span>
- <span data-ttu-id="60b01-120">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="60b01-120">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="60b01-121">SQL Server-Database.</span><span class="sxs-lookup"><span data-stu-id="60b01-121">SQL Server Database.</span></span>  <span data-ttu-id="60b01-122">Als u van SQL Server gebruikmaakt, Data Management Gateway installeren op dezelfde computer die als host fungeert voor de database of op een afzonderlijke computer die toegang heeft tot de database.</span><span class="sxs-lookup"><span data-stu-id="60b01-122">If you are using SQL Server, install Data Management Gateway on the same machine that hosts the database or on a separate machine that has access to the database.</span></span> <span data-ttu-id="60b01-123">Data Management Gateway is een onderdeel dat wordt verbinding gemaakt op-premises/op virtuele machine van Azure met cloudservices gegevensbronnen op een manier veilig en beheerd.</span><span class="sxs-lookup"><span data-stu-id="60b01-123">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="60b01-124">Zie [Data Management Gateway](data-factory-data-management-gateway.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="60b01-124">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60b01-125">Wanneer gegevens worden gekopieerd naar Azure SQL Database of SQL Server, kunt u de **SqlSink** in een kopieeractiviteit om aan te roepen een opgeslagen procedure met behulp van de **sqlWriterStoredProcedureName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="60b01-125">When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="60b01-126">Zie voor meer informatie [aanroepen van opgeslagen procedure uit kopieeractiviteit](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="60b01-126">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="60b01-127">Zie voor meer informatie over de eigenschap connector artikelen te volgen: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="60b01-127">For details about the property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span> <span data-ttu-id="60b01-128">Een opgeslagen procedure aanroepen tijdens het kopiëren van gegevens in een Azure SQL Data Warehouse met behulp van een kopieeractiviteit wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="60b01-128">Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported.</span></span> <span data-ttu-id="60b01-129">Maar u kunt de activiteit opgeslagen procedure gebruiken om aan te roepen, een opgeslagen procedure in een SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="60b01-129">But, you can use the stored procedure activity to invoke a stored procedure in a SQL Data Warehouse.</span></span> 
>  
> <span data-ttu-id="60b01-130">Wanneer het kopiëren van gegevens van Azure SQL Database of SQL Server of Azure SQL Data Warehouse, kunt u configureren **SqlSource** in een kopieeractiviteit om aan te roepen, een opgeslagen procedure voor het lezen van gegevens uit de brondatabase met behulp van de  **sqlReaderStoredProcedureName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="60b01-130">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="60b01-131">Zie voor meer informatie de volgende artikelen voor de connector: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="60b01-131">For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          


<span data-ttu-id="60b01-132">De volgende procedure maakt gebruik van de activiteit opgeslagen Procedure in een pijplijn om aan te roepen, een opgeslagen procedure in een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="60b01-132">The following walkthrough uses the Stored Procedure Activity in a pipeline to invoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="60b01-133">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="60b01-133">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="60b01-134">Voorbeeldtabel en opgeslagen procedure</span><span class="sxs-lookup"><span data-stu-id="60b01-134">Sample table and stored procedure</span></span>
1. <span data-ttu-id="60b01-135">Maak de volgende **tabel** in uw Azure SQL Database met behulp van SQL Server Management Studio of een ander hulpmiddel u vertrouwd met bent.</span><span class="sxs-lookup"><span data-stu-id="60b01-135">Create the following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="60b01-136">De datum-kolom is de datum en tijd wanneer de bijbehorende ID wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="60b01-136">The datetimestamp column is the date and time when the corresponding ID is generated.</span></span>

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
    <span data-ttu-id="60b01-137">ID is uniek geïdentificeerd en de datum-kolom is de datum en tijd wanneer de bijbehorende ID wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="60b01-137">Id is the unique identified and the datetimestamp column is the date and time when the corresponding ID is generated.</span></span>
    
    ![Voorbeeldgegevens](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="60b01-139">In dit voorbeeld wordt de opgeslagen procedure is in een Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="60b01-139">In this sample, the stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="60b01-140">Als de opgeslagen procedure in een Azure SQL Data Warehouse en SQL Server-Database is, is de methode is vergelijkbaar.</span><span class="sxs-lookup"><span data-stu-id="60b01-140">If the stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, the approach is similar.</span></span> <span data-ttu-id="60b01-141">Voor een SQL Server-database, moet u een [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="60b01-141">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="60b01-142">Maak de volgende **opgeslagen procedure** die voegt de gegevens in voor de **sampletable**.</span><span class="sxs-lookup"><span data-stu-id="60b01-142">Create the following **stored procedure** that inserts data in to the **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="60b01-143">**Naam** en **hoofdlettergebruik** van de parameter (DateTime in dit voorbeeld) moet overeenkomen met die van de parameter die is opgegeven in de pipeline/JSON van de activiteit.</span><span class="sxs-lookup"><span data-stu-id="60b01-143">**Name** and **casing** of the parameter (DateTime in this example) must match that of parameter specified in the pipeline/activity JSON.</span></span> <span data-ttu-id="60b01-144">Zorg ervoor dat in de definitie van de opgeslagen procedure  **@**  wordt gebruikt als een voorvoegsel voor de parameter.</span><span class="sxs-lookup"><span data-stu-id="60b01-144">In the stored procedure definition, ensure that **@** is used as a prefix for the parameter.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="60b01-145">Een data factory maken</span><span class="sxs-lookup"><span data-stu-id="60b01-145">Create a data factory</span></span>
1. <span data-ttu-id="60b01-146">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="60b01-146">Log in to [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="60b01-147">Klik op **nieuw** Klik op het menu links op **Intelligence en analyse**, en klik op **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="60b01-147">Click **NEW** on the left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![Nieuwe gegevensfactory](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="60b01-149">In de **nieuwe gegevensfactory** blade Voer **SProcDF** voor de naam.</span><span class="sxs-lookup"><span data-stu-id="60b01-149">In the **New data factory** blade, enter **SProcDF** for the Name.</span></span> <span data-ttu-id="60b01-150">Azure Data Factory-namen zijn **globaal unieke**.</span><span class="sxs-lookup"><span data-stu-id="60b01-150">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="60b01-151">U moet het voorvoegsel van de naam van de gegevensfactory met de naam van uw de geslaagde maken van de fabriek inschakelen.</span><span class="sxs-lookup"><span data-stu-id="60b01-151">You need to prefix the name of the data factory with your name, to enable the successful creation of the factory.</span></span>

   ![Nieuwe gegevensfactory](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="60b01-153">Selecteer uw **Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="60b01-153">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="60b01-154">Voor **resourcegroep**, voer een van de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="60b01-154">For **Resource Group**, do one of the following steps:</span></span>
   1. <span data-ttu-id="60b01-155">Klik op **nieuw** en voer een naam voor de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="60b01-155">Click **Create new** and enter a name for the resource group.</span></span>
   2. <span data-ttu-id="60b01-156">Klik op **gebruik bestaande** en selecteer een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="60b01-156">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="60b01-157">Selecteer de **locatie** voor de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="60b01-157">Select the **location** for the data factory.</span></span>
7. <span data-ttu-id="60b01-158">Selecteer **vastmaken aan dashboard** zodat u de gegevensfactory op het dashboard volgende keer dat u zich ziet aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="60b01-158">Select **Pin to dashboard** so that you can see the data factory on the dashboard next time you log in.</span></span>
8. <span data-ttu-id="60b01-159">Klik op de blade **Nieuwe gegevensfactory** op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="60b01-159">Click **Create** on the **New data factory** blade.</span></span>
9. <span data-ttu-id="60b01-160">U ziet de gegevensfactory wordt gemaakt in de **dashboard** van de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="60b01-160">You see the data factory being created in the **dashboard** of the Azure portal.</span></span> <span data-ttu-id="60b01-161">Nadat de gegevensfactory is gemaakt, ziet u de gegevensfactorypagina. Hierop wordt de inhoud van de gegevensfactory weergegeven.</span><span class="sxs-lookup"><span data-stu-id="60b01-161">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>

   ![Data Factory-startpagina](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="60b01-163">Een Azure SQL gekoppelde service maken</span><span class="sxs-lookup"><span data-stu-id="60b01-163">Create an Azure SQL linked service</span></span>
<span data-ttu-id="60b01-164">Nadat de gegevensfactory is gemaakt, maakt u een Azure SQL gekoppelde service die is gekoppeld aan uw Azure SQL database met de tabel sampletable en sp_sample opgeslagen procedure aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="60b01-164">After creating the data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains the sampletable table and sp_sample stored procedure, to your data factory.</span></span>

1. <span data-ttu-id="60b01-165">Klik op **auteur en implementeren van** op de **Data Factory** blade voor **SProcDF** starten van de Data Factory-Editor.</span><span class="sxs-lookup"><span data-stu-id="60b01-165">Click **Author and deploy** on the **Data Factory** blade for **SProcDF** to launch the Data Factory Editor.</span></span>
2. <span data-ttu-id="60b01-166">Klik op **nieuwe gegevensopslag** op de opdracht en kies **Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="60b01-166">Click **New data store** on the command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="60b01-167">U ziet het JSON-script voor het maken van een Azure SQL gekoppelde service in de editor.</span><span class="sxs-lookup"><span data-stu-id="60b01-167">You should see the JSON script for creating an Azure SQL linked service in the editor.</span></span>

   ![Nieuwe gegevensopslag](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="60b01-169">Breng de volgende wijzigingen in de JSON-script:</span><span class="sxs-lookup"><span data-stu-id="60b01-169">In the JSON script, make the following changes:</span></span>

   1. <span data-ttu-id="60b01-170">Vervang `<servername>` met de naam van uw Azure SQL Database-server.</span><span class="sxs-lookup"><span data-stu-id="60b01-170">Replace `<servername>` with the name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="60b01-171">Vervang `<databasename>` met de database waarin u de tabel en de opgeslagen procedure hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="60b01-171">Replace `<databasename>` with the database in which you created the table and the stored procedure.</span></span>
   3. <span data-ttu-id="60b01-172">Vervang `<username@servername>` met het gebruikersaccount dat toegang tot de database heeft.</span><span class="sxs-lookup"><span data-stu-id="60b01-172">Replace `<username@servername>` with the user account that has access to the database.</span></span>
   4. <span data-ttu-id="60b01-173">Vervang `<password>` met het wachtwoord voor het gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="60b01-173">Replace `<password>` with the password for the user account.</span></span>

      ![Nieuwe gegevensopslag](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="60b01-175">Voor het implementeren van de gekoppelde service, klikt u op **implementeren** op de opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="60b01-175">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="60b01-176">Controleer of u de AzureSqlLinkedService in de structuurweergave links.</span><span class="sxs-lookup"><span data-stu-id="60b01-176">Confirm that you see the AzureSqlLinkedService in the tree view on the left.</span></span>

    ![structuurweergave met gekoppelde service](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="60b01-178">Een uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="60b01-178">Create an output dataset</span></span>
<span data-ttu-id="60b01-179">U kunt een uitvoergegevensset voor een activiteit opgeslagen procedure moet opgeven, zelfs als de opgeslagen procedure geen gegevens produceert.</span><span class="sxs-lookup"><span data-stu-id="60b01-179">You must specify an output dataset for a stored procedure activity even if the stored procedure does not produce any data.</span></span> <span data-ttu-id="60b01-180">Dat is omdat het de uitvoergegevensset die schijven van de planning van de activiteit (hoe vaak de activiteit wordt uitgevoerd - per uur, dagelijks, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="60b01-180">That's because it's the output dataset that drives the schedule of the activity (how often the activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="60b01-181">De uitvoergegevensset moet gebruiken een **gekoppelde service** die verwijst naar een Azure SQL Database of een Azure SQL Data Warehouse of een SQL Server-Database die u wilt de opgeslagen procedure om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="60b01-181">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="60b01-182">De uitvoergegevensset kan fungeren als een manier om door te geven het resultaat van de opgeslagen procedure voor verdere verwerking door een andere activiteit ([activiteiten chaining](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="60b01-182">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="60b01-183">Echter, Data Factory automatisch schrijft niet de uitvoer van een opgeslagen procedure bij deze dataset.</span><span class="sxs-lookup"><span data-stu-id="60b01-183">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="60b01-184">De opgeslagen procedure die naar een SQL-tabel die de uitvoergegevensset die naar verwijst schrijft is.</span><span class="sxs-lookup"><span data-stu-id="60b01-184">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="60b01-185">In sommige gevallen kan de uitvoergegevensset mag een **dummy gegevensset** (een gegevensset die verwijst naar een tabel die de uitvoer van de opgeslagen procedure niet echt bijhoudt).</span><span class="sxs-lookup"><span data-stu-id="60b01-185">In some cases, the output dataset can be a **dummy dataset** (a dataset that points to a table that does not really hold output of the stored procedure).</span></span> <span data-ttu-id="60b01-186">Dit dummy-gegevensset wordt alleen gebruikt om de planning voor het uitvoeren van de activiteit opgeslagen procedure opgeven.</span><span class="sxs-lookup"><span data-stu-id="60b01-186">This dummy dataset is used only to specify the schedule for running the stored procedure activity.</span></span> 

1. <span data-ttu-id="60b01-187">Klik op **... Meer** op de werkbalk klikt **nieuwe gegevensset**, en klik op **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="60b01-187">Click **... More** on the toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="60b01-188">**Nieuwe gegevensset** op de opdrachtbalk en selecteer **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="60b01-188">**New dataset** on the command bar and select **Azure SQL**.</span></span>

    ![structuurweergave met gekoppelde service](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="60b01-190">De volgende JSON-script in in de JSON-editor kopiëren en plakken.</span><span class="sxs-lookup"><span data-stu-id="60b01-190">Copy/paste the following JSON script in to the JSON editor.</span></span>

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
3. <span data-ttu-id="60b01-191">Voor het implementeren van de gegevensset, klikt u op **implementeren** op de opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="60b01-191">To deploy the dataset, click **Deploy** on the command bar.</span></span> <span data-ttu-id="60b01-192">Controleer of u de gegevensset in de structuurweergave.</span><span class="sxs-lookup"><span data-stu-id="60b01-192">Confirm that you see the dataset in the tree view.</span></span>

    ![Structuurweergave met gekoppelde services](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="60b01-194">Een pijplijn maken met SqlServerStoredProcedure activiteit</span><span class="sxs-lookup"><span data-stu-id="60b01-194">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="60b01-195">Nu gaan we een pijplijn maken met een activiteit opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="60b01-195">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="60b01-196">U ziet de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="60b01-196">Notice the following properties:</span></span> 

- <span data-ttu-id="60b01-197">De **type** eigenschap is ingesteld op **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="60b01-197">The **type** property is set to **SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="60b01-198">De **storedProcedureName** in het type eigenschappen is ingesteld op **sp_sample** (naam van de opgeslagen procedure).</span><span class="sxs-lookup"><span data-stu-id="60b01-198">The **storedProcedureName** in type properties is set to **sp_sample** (name of the stored procedure).</span></span>
- <span data-ttu-id="60b01-199">De **storedProcedureParameters** sectie bevat een parameter met de naam **datum/tijd**.</span><span class="sxs-lookup"><span data-stu-id="60b01-199">The **storedProcedureParameters** section contains one parameter named **DataTime**.</span></span> <span data-ttu-id="60b01-200">Naam en het hoofdlettergebruik van de parameter in JSON moeten overeenkomen met de naam en het hoofdlettergebruik van de parameter in de definitie van de opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="60b01-200">Name and casing of the parameter in JSON must match the name and casing of the parameter in the stored procedure definition.</span></span> <span data-ttu-id="60b01-201">Als u null zijn voor een parameter doorgeven moet, gebruikt u de syntaxis: `"param1": null` (alle kleine letters).</span><span class="sxs-lookup"><span data-stu-id="60b01-201">If you need pass null for a parameter, use the syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="60b01-202">Klik op **... Meer** op de opdrachtbalk klikken en op **nieuwe pijplijn**.</span><span class="sxs-lookup"><span data-stu-id="60b01-202">Click **... More** on the command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="60b01-203">Kopiëren en plakken in het volgende JSON-fragment:</span><span class="sxs-lookup"><span data-stu-id="60b01-203">Copy/paste the following JSON snippet:</span></span>   

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
3. <span data-ttu-id="60b01-204">Voor het implementeren van de pijplijn, klikt u op **implementeren** op de werkbalk.</span><span class="sxs-lookup"><span data-stu-id="60b01-204">To deploy the pipeline, click **Deploy** on the toolbar.</span></span>  

### <a name="monitor-the-pipeline"></a><span data-ttu-id="60b01-205">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="60b01-205">Monitor the pipeline</span></span>
1. <span data-ttu-id="60b01-206">Klik op **X** om de blades van de Data Factory-editor te sluiten en om terug te keren naar de Data Factory-blade. Klik op **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="60b01-206">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span></span>

    ![Tegel diagram](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="60b01-208">In de **diagramweergave** ziet u een overzicht van de pijplijnen en gegevenssets die voor deze zelfstudie worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="60b01-208">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![Tegel diagram](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="60b01-210">Dubbelklik in de diagramweergave op de gegevensset `sprocsampleout`.</span><span class="sxs-lookup"><span data-stu-id="60b01-210">In the Diagram View, double-click the dataset `sprocsampleout`.</span></span> <span data-ttu-id="60b01-211">U ziet de segmenten in de status Ready heeft.</span><span class="sxs-lookup"><span data-stu-id="60b01-211">You see the slices in Ready state.</span></span> <span data-ttu-id="60b01-212">Moet er vijf segmenten omdat een segment wordt geproduceerd voor elk uur tussen de begintijd en eindtijd van de JSON.</span><span class="sxs-lookup"><span data-stu-id="60b01-212">There should be five slices because a slice is produced for each hour between the start time and end time from the JSON.</span></span>

    ![Tegel diagram](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="60b01-214">Wanneer een segment is in **gereed** staat, voer een `select * from sampletable` -query op de Azure SQL database om te controleren dat de gegevens is ingevoegd in de tabel door de opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="60b01-214">When a slice is in **Ready** state, run a `select * from sampletable` query against the Azure SQL database to verify that the data was inserted in to the table by the stored procedure.</span></span>

   ![uitvoergegevens](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="60b01-216">Zie [bewaken van de pijplijn](data-factory-monitor-manage-pipelines.md) voor gedetailleerde informatie over het Azure Data Factory-pijplijnen bewaken.</span><span class="sxs-lookup"><span data-stu-id="60b01-216">See [Monitor the pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="60b01-217">Geef een invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="60b01-217">Specify an input dataset</span></span>
<span data-ttu-id="60b01-218">In dit overzicht heeft activiteit opgeslagen procedure geen eventuele invoergegevenssets.</span><span class="sxs-lookup"><span data-stu-id="60b01-218">In the walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="60b01-219">Als u een invoergegevensset opgeeft, wordt de activiteit opgeslagen procedure niet uitgevoerd totdat het segment met invoergegevensset beschikbaar (in de status Ready heeft is).</span><span class="sxs-lookup"><span data-stu-id="60b01-219">If you specify an input dataset, the stored procedure activity does not run until the slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="60b01-220">De gegevensset mag een externe gegevensset (die wordt niet gemaakt door een andere activiteit in de dezelfde pijplijn) of een interne gegevensset die wordt geproduceerd door een upstream-activiteit (de activiteit die wordt uitgevoerd voordat deze activiteit).</span><span class="sxs-lookup"><span data-stu-id="60b01-220">The dataset can be an external dataset (that is not produced by another activity in the same pipeline) or an internal dataset that is produced by an upstream activity (the activity that runs before this activity).</span></span> <span data-ttu-id="60b01-221">U kunt meerdere invoergegevenssets voor de activiteit opgeslagen procedure opgeven.</span><span class="sxs-lookup"><span data-stu-id="60b01-221">You can specify multiple input datasets for the stored procedure activity.</span></span> <span data-ttu-id="60b01-222">Als u doet dit, de activiteit opgeslagen procedure wordt alleen uitgevoerd als alle segmenten van de invoergegevensset beschikbaar (in de status Ready heeft zijn).</span><span class="sxs-lookup"><span data-stu-id="60b01-222">If you do so, the stored procedure activity runs only when all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="60b01-223">Invoergegevensset kan niet worden gebruikt in de opgeslagen procedure als een parameter.</span><span class="sxs-lookup"><span data-stu-id="60b01-223">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="60b01-224">Het wordt alleen gebruikt om te controleren van de afhankelijkheid voordat u de activiteit opgeslagen procedure start.</span><span class="sxs-lookup"><span data-stu-id="60b01-224">It is only used to check the dependency before starting the stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="60b01-225">Keten met andere activiteiten</span><span class="sxs-lookup"><span data-stu-id="60b01-225">Chaining with other activities</span></span>
<span data-ttu-id="60b01-226">Als u koppelen aan deze activiteit een upstream-activiteit wilt, geeft u de uitvoer van de upstream-activiteit als invoer van deze activiteit.</span><span class="sxs-lookup"><span data-stu-id="60b01-226">If you want to chain an upstream activity with this activity, specify the output of the upstream activity as an input of this activity.</span></span> <span data-ttu-id="60b01-227">Wanneer u doet dit, wordt de activiteit opgeslagen procedure niet uitvoeren totdat de upstream-activiteit is voltooid en de uitvoergegevensset van de upstream-activiteit (in de status gereed) dat beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="60b01-227">When you do so, the stored procedure activity does not run until the upstream activity completes and the output dataset of the upstream activity is available (in Ready status).</span></span> <span data-ttu-id="60b01-228">U kunt uitvoergegevenssets uit meerdere activiteiten van de upstream opgeven als invoer gegevenssets van de activiteit opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="60b01-228">You can specify output datasets of multiple upstream activities as input datasets of the stored procedure activity.</span></span> <span data-ttu-id="60b01-229">Wanneer u doet dit, de activiteit opgeslagen procedure wordt alleen uitgevoerd als alle segmenten van de invoergegevensset beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="60b01-229">When you do so, the stored procedure activity runs only when all the input dataset slices are available.</span></span>  

<span data-ttu-id="60b01-230">In het volgende voorbeeld wordt de uitvoer van de kopieerbewerking is: OutputDataset die invoer van de activiteit opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="60b01-230">In the following example, the output of the copy activity is: OutputDataset, which is an input of the stored procedure activity.</span></span> <span data-ttu-id="60b01-231">Daarom wordt de activiteit opgeslagen procedure niet uitvoeren totdat de kopieerbewerking is voltooid en het segment OutputDataset beschikbaar (in de status Ready heeft is).</span><span class="sxs-lookup"><span data-stu-id="60b01-231">Therefore, the stored procedure activity does not run until the copy activity completes and the OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="60b01-232">Als u meerdere invoergegevenssets opgeeft, wordt de activiteit opgeslagen procedure niet uitvoeren totdat alle segmenten van de invoergegevensset (in de status gereed) beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="60b01-232">If you specify multiple input datasets, the stored procedure activity does not run until all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="60b01-233">De invoer gegevenssets kan niet rechtstreeks worden gebruikt als parameters voor de activiteit opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="60b01-233">The input datasets cannot be used directly as parameters to the stored procedure activity.</span></span> 

<span data-ttu-id="60b01-234">Zie voor meer informatie over het koppelen van activiteiten [meerdere activiteiten in een pijplijn](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span><span class="sxs-lookup"><span data-stu-id="60b01-234">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob to blob",
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

<span data-ttu-id="60b01-235">Op deze manier om te koppelen van de activiteit van de procedure store met **downstream-activiteiten** (de activiteiten die worden uitgevoerd nadat de activiteit opgeslagen procedure is voltooid), de uitvoergegevensset van de activiteit opgeslagen procedure opgeven als invoer van de downstream activiteit in de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="60b01-235">Similarly, to link the store procedure activity with **downstream activities** (the activities that run after the stored procedure activity completes), specify the output dataset of the stored procedure activity as an input of the downstream activity in the pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60b01-236">Wanneer gegevens worden gekopieerd naar Azure SQL Database of SQL Server, kunt u de **SqlSink** in een kopieeractiviteit om aan te roepen een opgeslagen procedure met behulp van de **sqlWriterStoredProcedureName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="60b01-236">When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="60b01-237">Zie voor meer informatie [aanroepen van opgeslagen procedure uit kopieeractiviteit](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="60b01-237">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="60b01-238">Zie voor meer informatie over de eigenschap, de volgende artikelen voor de connector: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="60b01-238">For details about the property, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span>
>  
> <span data-ttu-id="60b01-239">Wanneer het kopiëren van gegevens van Azure SQL Database of SQL Server of Azure SQL Data Warehouse, kunt u configureren **SqlSource** in een kopieeractiviteit om aan te roepen, een opgeslagen procedure voor het lezen van gegevens uit de brondatabase met behulp van de  **sqlReaderStoredProcedureName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="60b01-239">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="60b01-240">Zie voor meer informatie de volgende artikelen voor de connector: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="60b01-240">For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          

## <a name="json-format"></a><span data-ttu-id="60b01-241">JSON-indeling</span><span class="sxs-lookup"><span data-stu-id="60b01-241">JSON format</span></span>
<span data-ttu-id="60b01-242">Hier volgt de JSON-indeling voor het definiëren van een activiteit opgeslagen Procedure:</span><span class="sxs-lookup"><span data-stu-id="60b01-242">Here is the JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of the stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

<span data-ttu-id="60b01-243">De volgende tabel beschrijft deze JSON-eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="60b01-243">The following table describes these JSON properties:</span></span>

| <span data-ttu-id="60b01-244">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="60b01-244">Property</span></span> | <span data-ttu-id="60b01-245">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="60b01-245">Description</span></span> | <span data-ttu-id="60b01-246">Vereist</span><span class="sxs-lookup"><span data-stu-id="60b01-246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60b01-247">naam</span><span class="sxs-lookup"><span data-stu-id="60b01-247">name</span></span> | <span data-ttu-id="60b01-248">Naam van de activiteit</span><span class="sxs-lookup"><span data-stu-id="60b01-248">Name of the activity</span></span> |<span data-ttu-id="60b01-249">Ja</span><span class="sxs-lookup"><span data-stu-id="60b01-249">Yes</span></span> |
| <span data-ttu-id="60b01-250">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="60b01-250">description</span></span> |<span data-ttu-id="60b01-251">Beschrijving van wat de activiteit wordt gebruikt</span><span class="sxs-lookup"><span data-stu-id="60b01-251">Text describing what the activity is used for</span></span> |<span data-ttu-id="60b01-252">Nee</span><span class="sxs-lookup"><span data-stu-id="60b01-252">No</span></span> |
| <span data-ttu-id="60b01-253">type</span><span class="sxs-lookup"><span data-stu-id="60b01-253">type</span></span> | <span data-ttu-id="60b01-254">Moet worden ingesteld op: **SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="60b01-254">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="60b01-255">Ja</span><span class="sxs-lookup"><span data-stu-id="60b01-255">Yes</span></span> |
| <span data-ttu-id="60b01-256">Invoer</span><span class="sxs-lookup"><span data-stu-id="60b01-256">inputs</span></span> | <span data-ttu-id="60b01-257">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="60b01-257">Optional.</span></span> <span data-ttu-id="60b01-258">Als u een invoergegevensset opgeeft, moet dit beschikbaar is (in de status 'Gereed') voor de activiteit opgeslagen procedure moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="60b01-258">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="60b01-259">Invoergegevensset kan niet worden gebruikt in de opgeslagen procedure als een parameter.</span><span class="sxs-lookup"><span data-stu-id="60b01-259">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="60b01-260">Het wordt alleen gebruikt om te controleren van de afhankelijkheid voordat u de activiteit opgeslagen procedure start.</span><span class="sxs-lookup"><span data-stu-id="60b01-260">It is only used to check the dependency before starting the stored procedure activity.</span></span> |<span data-ttu-id="60b01-261">Nee</span><span class="sxs-lookup"><span data-stu-id="60b01-261">No</span></span> |
| <span data-ttu-id="60b01-262">uitvoer</span><span class="sxs-lookup"><span data-stu-id="60b01-262">outputs</span></span> | <span data-ttu-id="60b01-263">U moet een uitvoergegevensset voor een activiteit opgeslagen procedure opgeven.</span><span class="sxs-lookup"><span data-stu-id="60b01-263">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="60b01-264">Uitvoergegevensset geeft de **planning** voor de activiteit opgeslagen procedure (elk uur, wekelijks, maandelijks, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="60b01-264">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="60b01-265">De uitvoergegevensset moet gebruiken een **gekoppelde service** die verwijst naar een Azure SQL Database of een Azure SQL Data Warehouse of een SQL Server-Database die u wilt de opgeslagen procedure om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="60b01-265">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <br/><br/><span data-ttu-id="60b01-266">De uitvoergegevensset kan fungeren als een manier om door te geven het resultaat van de opgeslagen procedure voor verdere verwerking door een andere activiteit ([activiteiten chaining](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="60b01-266">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="60b01-267">Echter, Data Factory automatisch schrijft niet de uitvoer van een opgeslagen procedure bij deze dataset.</span><span class="sxs-lookup"><span data-stu-id="60b01-267">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="60b01-268">De opgeslagen procedure die naar een SQL-tabel die de uitvoergegevensset die naar verwijst schrijft is.</span><span class="sxs-lookup"><span data-stu-id="60b01-268">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <br/><br/><span data-ttu-id="60b01-269">In sommige gevallen kan de uitvoergegevensset mag een **dummy gegevensset**, die wordt alleen gebruikt om de planning voor het uitvoeren van de activiteit opgeslagen procedure opgeven.</span><span class="sxs-lookup"><span data-stu-id="60b01-269">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span> |<span data-ttu-id="60b01-270">Ja</span><span class="sxs-lookup"><span data-stu-id="60b01-270">Yes</span></span> |
| <span data-ttu-id="60b01-271">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="60b01-271">storedProcedureName</span></span> |<span data-ttu-id="60b01-272">Geef de naam van de opgeslagen procedure in de Azure SQL database of Azure SQL Data Warehouse of SQL Server-database die wordt vertegenwoordigd door de gekoppelde service die gebruikmaakt van de uitvoertabel.</span><span class="sxs-lookup"><span data-stu-id="60b01-272">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="60b01-273">Ja</span><span class="sxs-lookup"><span data-stu-id="60b01-273">Yes</span></span> |
| <span data-ttu-id="60b01-274">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="60b01-274">storedProcedureParameters</span></span> |<span data-ttu-id="60b01-275">Geef waarden op voor parameters van opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="60b01-275">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="60b01-276">Als u null zijn voor een parameter doorgeven moet, gebruikt u de syntaxis: "param1": null (alle kleine letter).</span><span class="sxs-lookup"><span data-stu-id="60b01-276">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="60b01-277">Zie het volgende voorbeeld voor meer informatie over het gebruik van deze eigenschap.</span><span class="sxs-lookup"><span data-stu-id="60b01-277">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="60b01-278">Nee</span><span class="sxs-lookup"><span data-stu-id="60b01-278">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="60b01-279">Het doorgeven van een statische waarde</span><span class="sxs-lookup"><span data-stu-id="60b01-279">Passing a static value</span></span>
<span data-ttu-id="60b01-280">Nu we eens het toevoegen van een andere kolom met de naam 'Scenario' in de tabel met een statische waarde 'Document voorbeeld' genoemd.</span><span class="sxs-lookup"><span data-stu-id="60b01-280">Now, let’s consider adding another column named ‘Scenario’ in the table containing a static value called ‘Document sample’.</span></span>

![Voorbeeldgegevens 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="60b01-282">**Tabel:**</span><span class="sxs-lookup"><span data-stu-id="60b01-282">**Table:**</span></span>

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

<span data-ttu-id="60b01-283">**Opgeslagen procedure:**</span><span class="sxs-lookup"><span data-stu-id="60b01-283">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="60b01-284">Nu, geven de **Scenario** parameter en de waarde van de activiteit opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="60b01-284">Now, pass the **Scenario** parameter and the value from the stored procedure activity.</span></span> <span data-ttu-id="60b01-285">De **typeProperties** sectie in het voorgaande voorbeeld lijkt op het volgende fragment:</span><span class="sxs-lookup"><span data-stu-id="60b01-285">The **typeProperties** section in the preceding sample looks like the following snippet:</span></span>

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

<span data-ttu-id="60b01-286">**Data Factory-gegevensset:**</span><span class="sxs-lookup"><span data-stu-id="60b01-286">**Data Factory dataset:**</span></span>

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

<span data-ttu-id="60b01-287">**Data Factory-pijplijn**</span><span class="sxs-lookup"><span data-stu-id="60b01-287">**Data Factory pipeline**</span></span>

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