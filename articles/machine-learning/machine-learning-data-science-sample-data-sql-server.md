---
title: Voorbeeldgegevens in SQL Server op Azure | Microsoft Docs
description: Voorbeeldgegevens in SQL Server op Azure
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 33c030d4-5cca-4cc9-99d7-2bd13a3926af
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 1bdcc7175dac325de1144d805e977264524b3fbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="0a908-103"><a name="heading"></a>Voorbeeldgegevens in SQL Server op Azure</span><span class="sxs-lookup"><span data-stu-id="0a908-103"><a name="heading"></a>Sample data in SQL Server on Azure</span></span>
<span data-ttu-id="0a908-104">Dit document wordt beschreven hoe voorbeeldgegevens die zijn opgeslagen in SQL Server op Azure met SQL of de programmeertaal Python.</span><span class="sxs-lookup"><span data-stu-id="0a908-104">This document shows how to sample data stored in SQL Server on Azure using either SQL or the Python programming language.</span></span> <span data-ttu-id="0a908-105">Ook ziet u hoe steekproefgegevens verplaatsen naar Azure Machine Learning door op een bestand op te slaan, uploaden naar een Azure-blob en vervolgens te lezen in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="0a908-105">It also shows how to move sampled data into Azure Machine Learning by saving it to a file, uploading it to an Azure blob, and then reading it into Azure Machine Learning Studio.</span></span>

<span data-ttu-id="0a908-106">De steekproeven van Python gebruikt de [pyodbc](https://code.google.com/p/pyodbc/) ODBC-bibliotheek verbinding maken met SQL Server op Azure en de [Pandas](http://pandas.pydata.org/) bibliotheek te doen de steekproeven.</span><span class="sxs-lookup"><span data-stu-id="0a908-106">The Python sampling uses the [pyodbc](https://code.google.com/p/pyodbc/) ODBC library to connect to SQL Server on Azure and the [Pandas](http://pandas.pydata.org/) library to do the sampling.</span></span>

> [!NOTE]
> <span data-ttu-id="0a908-107">De SQL-voorbeeldcode in dit document wordt ervan uitgegaan dat de gegevens zich in een SQL-Server op Azure.</span><span class="sxs-lookup"><span data-stu-id="0a908-107">The sample SQL code in this document assumes that the data is in a SQL Server on Azure.</span></span> <span data-ttu-id="0a908-108">Als dit niet het geval is, raadpleegt u [gegevens verplaatsen naar SQL Server op Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) onderwerp voor instructies over het verplaatsen van uw gegevens naar SQL Server op Azure.</span><span class="sxs-lookup"><span data-stu-id="0a908-108">If it is not, please refer to [Move data to SQL Server on Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) topic for instructions on how to move your data to SQL Server on Azure.</span></span>
> 
> 

<span data-ttu-id="0a908-109">De volgende **menu** koppelingen naar onderwerpen waarin wordt beschreven hoe u voorbeeldgegevens uit verschillende omgevingen voor opslag.</span><span class="sxs-lookup"><span data-stu-id="0a908-109">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="0a908-110">**Waarom een steekproef nemen uit uw gegevens?**</span><span class="sxs-lookup"><span data-stu-id="0a908-110">**Why sample your data?**</span></span>
<span data-ttu-id="0a908-111">Als de gegevensset die u wilt analyseren groot is, is het meestal een goed idee om de gegevens om deze aan de grootte van een kleinere maar representatief en gemakkelijker down-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="0a908-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="0a908-112">Dit vereenvoudigt het begrip van de gegevens, exploratie en functie-engineering.</span><span class="sxs-lookup"><span data-stu-id="0a908-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="0a908-113">De rol in de [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is het inschakelen van snel maken van een prototype van de functies voor het verwerken van gegevens en machine learning-modellen.</span><span class="sxs-lookup"><span data-stu-id="0a908-113">Its role in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="0a908-114">Deze taak steekproeven is een stap in de [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="0a908-114">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <span data-ttu-id="0a908-115"><a name="SQL"></a>Met behulp van SQL</span><span class="sxs-lookup"><span data-stu-id="0a908-115"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="0a908-116">Deze sectie beschrijft de verschillende methoden met SQL voor het uitvoeren van eenvoudige willekeurige steekproef op basis van de gegevens in de database.</span><span class="sxs-lookup"><span data-stu-id="0a908-116">This section describes several methods using SQL to perform simple random sampling against the data in the database.</span></span> <span data-ttu-id="0a908-117">Kies een methode op basis van de gegevensgrootte van uw en de distributie.</span><span class="sxs-lookup"><span data-stu-id="0a908-117">Please choose a method based on your data size and its distribution.</span></span>

<span data-ttu-id="0a908-118">De volgende twee items laten zien hoe newid in SQL Server gebruikt de steekproeven uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0a908-118">The two items below show how to use newid in SQL Server to perform the sampling.</span></span> <span data-ttu-id="0a908-119">Welke methode u kiest is afhankelijk van hoe willekeurige u wilt dat de steekproef worden (pk_id in de volgende voorbeeldcode wordt ervan uitgegaan dat een automatisch gegenereerde primaire sleutel).</span><span class="sxs-lookup"><span data-stu-id="0a908-119">The method you choose depends on how random you want the sample to be (pk_id in the sample code below is assumed to be an auto-generated primary key).</span></span>

1. <span data-ttu-id="0a908-120">Minder strikte steekproef</span><span class="sxs-lookup"><span data-stu-id="0a908-120">Less strict random sample</span></span>
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. <span data-ttu-id="0a908-121">Meer steekproef</span><span class="sxs-lookup"><span data-stu-id="0a908-121">More random sample</span></span> 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

<span data-ttu-id="0a908-122">Component TABLESAMPLE kan worden gebruikt voor steekproeven evenals gedemonstreerd hieronder.</span><span class="sxs-lookup"><span data-stu-id="0a908-122">Tablesample can be used for sampling as well as demonstrated below.</span></span> <span data-ttu-id="0a908-123">Dit kan een betere benadering zijn als de gegevensgrootte van uw groot is (ervan uitgaande dat de gegevens op verschillende pagina's worden niet gecorreleerd) en voor de query uit te voeren in een redelijke tijd.</span><span class="sxs-lookup"><span data-stu-id="0a908-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for the query to complete in a reasonable time.</span></span>

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> <span data-ttu-id="0a908-124">U kunt verkennen en functies van deze steekproefgegevens genereren door op te slaan in een nieuwe tabel</span><span class="sxs-lookup"><span data-stu-id="0a908-124">You can explore and generate features from this sampled data by storing it in a new table</span></span>
> 
> 

### <span data-ttu-id="0a908-125"><a name="sql-aml"></a>Verbinding maken met Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0a908-125"><a name="sql-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="0a908-126">U kunt rechtstreeks de voorbeeldquery's boven in de Azure Machine Learning [importgegevens] [ import-data] module die u wilt de gegevens onderweg down-voorbeeld en brengt u het in een Azure Machine Learning-experiment.</span><span class="sxs-lookup"><span data-stu-id="0a908-126">You can directly  use the sample queries above in the Azure Machine Learning [Import Data][import-data] module to down-sample the data on the fly and bring it into an Azure Machine Learning experiment.</span></span> <span data-ttu-id="0a908-127">Een schermafbeelding van de module reader gebruikt om te lezen van de steekproefgegevens wordt hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="0a908-127">A screen shot of using the reader module to read the sampled data is shown below:</span></span>

![lezer sql][1]

## <span data-ttu-id="0a908-129"><a name="python"></a>Met behulp van de programmeertaal Python</span><span class="sxs-lookup"><span data-stu-id="0a908-129"><a name="python"></a>Using the Python programming language</span></span>
<span data-ttu-id="0a908-130">Deze sectie wordt gedemonstreerd met behulp van de [pyodbc bibliotheek](https://code.google.com/p/pyodbc/) tot stand brengen van een ODBC verbinding maken met een SQL server-database in Python.</span><span class="sxs-lookup"><span data-stu-id="0a908-130">This section demonstrates using the [pyodbc library](https://code.google.com/p/pyodbc/) to establish an ODBC connect to a SQL server database in Python.</span></span> <span data-ttu-id="0a908-131">De tekenreeks voor databaseverbinding is als volgt: (vervangen servername, dbname, username en password door uw configuratie):</span><span class="sxs-lookup"><span data-stu-id="0a908-131">The database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="0a908-132">De [Pandas](http://pandas.pydata.org/) in Python-bibliotheek biedt een uitgebreide set gegevensstructuren en hulpprogramma's voor gegevensanalyse voor gegevensmanipulatie voor het programmeren van Python.</span><span class="sxs-lookup"><span data-stu-id="0a908-132">The [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="0a908-133">De onderstaande code leest een steekproef 0,1% van de gegevens uit een tabel in Azure SQL-database in een Pandas-gegevens:</span><span class="sxs-lookup"><span data-stu-id="0a908-133">The code below reads a 0.1% sample of the data from a table in Azure SQL database into a Pandas data :</span></span>

    import pandas as pd

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

<span data-ttu-id="0a908-134">Nu kunt u werken met de steekproefgegevens in het kader van de gegevens Pandas.</span><span class="sxs-lookup"><span data-stu-id="0a908-134">You can now work with the sampled data in the Pandas data frame.</span></span> 

### <span data-ttu-id="0a908-135"><a name="python-aml"></a>Verbinding maken met Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0a908-135"><a name="python-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="0a908-136">U kunt de volgende voorbeeldcode omlaag actieve gegevens naar een bestand opslaan en upload dit naar een Azure-blob.</span><span class="sxs-lookup"><span data-stu-id="0a908-136">You can use the following sample code to save the down-sampled data to a file and upload it to an Azure blob.</span></span> <span data-ttu-id="0a908-137">De gegevens in de blob rechtstreeks kunnen worden gelezen in een Azure Machine Learning-Experiment met behulp van de [importgegevens] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="0a908-137">The data in the blob can be directly read into an Azure Machine Learning Experiment using the [Import Data][import-data] module.</span></span> <span data-ttu-id="0a908-138">De stappen zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="0a908-138">The steps are as follows:</span></span> 

1. <span data-ttu-id="0a908-139">Het frame pandas-gegevens schrijven naar een lokaal bestand</span><span class="sxs-lookup"><span data-stu-id="0a908-139">Write the pandas data frame to a local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="0a908-140">Lokaal bestand uploaden naar Azure blob</span><span class="sxs-lookup"><span data-stu-id="0a908-140">Upload local file to Azure blob</span></span>
   
        from azure.storage import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading blob:"+BLOBNAME)
3. <span data-ttu-id="0a908-141">Gegevens lezen uit Azure blob met Azure Machine Learning [importgegevens] [ import-data] module, zoals wordt weergegeven in het scherm schermafbeelding hieronder:</span><span class="sxs-lookup"><span data-stu-id="0a908-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in the screen grab below:</span></span>

![lezer blob][2]

## <a name="the-team-data-science-process-in-action-example"></a><span data-ttu-id="0a908-143">De procedure van wetenschappelijke gegevens Team in actie voorbeeld</span><span class="sxs-lookup"><span data-stu-id="0a908-143">The Team Data Science Process in Action example</span></span>
<span data-ttu-id="0a908-144">Zie voor een overzicht van de end-to-end voorbeeld van het Team gegevens wetenschap proces een met een openbare gegevensset [Team gegevens wetenschappelijke processen in actie: SQL-Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="0a908-144">For an end-to-end walkthrough example of the Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
