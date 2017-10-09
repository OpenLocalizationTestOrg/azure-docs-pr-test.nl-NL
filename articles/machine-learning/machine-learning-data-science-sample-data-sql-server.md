---
title: Gegevens in SQL Server op Azure aaaSample | Microsoft Docs
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
ms.openlocfilehash: dc7f9529c771f6deb633775557e64a04b774f5b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="aa6fc-103"><a name="heading"></a>Voorbeeldgegevens in SQL Server op Azure</span><span class="sxs-lookup"><span data-stu-id="aa6fc-103"><a name="heading"></a>Sample data in SQL Server on Azure</span></span>
<span data-ttu-id="aa6fc-104">Dit document ziet u hoe toosample gegevens opgeslagen in SQL Server op Azure met SQL of Hallo Python programmeertaal.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-104">This document shows how toosample data stored in SQL Server on Azure using either SQL or hello Python programming language.</span></span> <span data-ttu-id="aa6fc-105">U ziet ook hoe toomove voorbeeldgegevens in Azure Machine Learning te slaan in tooa-bestand uploaden tooan Azure blob en vervolgens te lezen in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-105">It also shows how toomove sampled data into Azure Machine Learning by saving it tooa file, uploading it tooan Azure blob, and then reading it into Azure Machine Learning Studio.</span></span>

<span data-ttu-id="aa6fc-106">Hallo Python steekproeven gebruikt Hallo [pyodbc](https://code.google.com/p/pyodbc/) ODBC-bibliotheek tooconnect tooSQL Server op Azure en Hallo [Pandas](http://pandas.pydata.org/) bibliotheek toodo Hallo steekproeven.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-106">hello Python sampling uses hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC library tooconnect tooSQL Server on Azure and hello [Pandas](http://pandas.pydata.org/) library toodo hello sampling.</span></span>

> [!NOTE]
> <span data-ttu-id="aa6fc-107">Hallo voorbeeldcode SQL in dit document wordt ervan uitgegaan dat Hallo gegevens zich in een SQL-Server op Azure.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-107">hello sample SQL code in this document assumes that hello data is in a SQL Server on Azure.</span></span> <span data-ttu-id="aa6fc-108">Als dit niet het geval is, raadpleegt u te[verplaatsen van gegevens tooSQL Server op Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) onderwerp voor instructies over het toomove uw gegevens tooSQL Server op Azure.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-108">If it is not, please refer too[Move data tooSQL Server on Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) topic for instructions on how toomove your data tooSQL Server on Azure.</span></span>
> 
> 

<span data-ttu-id="aa6fc-109">Hallo volgende **menu** koppelingen tootopics waarin wordt beschreven hoe toosample gegevens uit verschillende omgevingen voor opslag.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="aa6fc-110">**Waarom een steekproef nemen uit uw gegevens?**</span><span class="sxs-lookup"><span data-stu-id="aa6fc-110">**Why sample your data?**</span></span>
<span data-ttu-id="aa6fc-111">Als u van plan bent tooanalyze Hallo-gegevensset te groot is, is het meestal een goed idee Hallo toodown-sample data tooreduce het tooa kleiner, maar representatief en gemakkelijker grootte.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="aa6fc-112">Dit vereenvoudigt het begrip van de gegevens, exploratie en functie-engineering.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="aa6fc-113">De rol in Hallo [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is tooenable snel maken van een prototype van Hallo gegevensverwerking functies en machine learning-modellen.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-113">Its role in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="aa6fc-114">Deze taak steekproeven is een stap in Hallo [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="aa6fc-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <span data-ttu-id="aa6fc-115"><a name="SQL"></a>Met behulp van SQL</span><span class="sxs-lookup"><span data-stu-id="aa6fc-115"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="aa6fc-116">Deze sectie beschrijft de verschillende methoden met behulp van SQL tooperform eenvoudige steekproeven op Hallo gegevens in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-116">This section describes several methods using SQL tooperform simple random sampling against hello data in hello database.</span></span> <span data-ttu-id="aa6fc-117">Kies een methode op basis van de gegevensgrootte van uw en de distributie.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-117">Please choose a method based on your data size and its distribution.</span></span>

<span data-ttu-id="aa6fc-118">Hallo twee items hieronder laten zien hoe toouse newid in SQL Server-tooperform steekproeven Hallo.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-118">hello two items below show how toouse newid in SQL Server tooperform hello sampling.</span></span> <span data-ttu-id="aa6fc-119">Hallo methode u kiest is afhankelijk van hoe willekeurige Hallo voorbeeld toobe gewenste (pk_id in Hallo voorbeeldcode hieronder wordt aangenomen dat een automatisch gegenereerde primaire sleutel toobe).</span><span class="sxs-lookup"><span data-stu-id="aa6fc-119">hello method you choose depends on how random you want hello sample toobe (pk_id in hello sample code below is assumed toobe an auto-generated primary key).</span></span>

1. <span data-ttu-id="aa6fc-120">Minder strikte steekproef</span><span class="sxs-lookup"><span data-stu-id="aa6fc-120">Less strict random sample</span></span>
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. <span data-ttu-id="aa6fc-121">Meer steekproef</span><span class="sxs-lookup"><span data-stu-id="aa6fc-121">More random sample</span></span> 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

<span data-ttu-id="aa6fc-122">Component TABLESAMPLE kan worden gebruikt voor steekproeven evenals gedemonstreerd hieronder.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-122">Tablesample can be used for sampling as well as demonstrated below.</span></span> <span data-ttu-id="aa6fc-123">Dit kan een betere benadering zijn als de gegevensgrootte van uw groot is (ervan uitgaande dat de gegevens op verschillende pagina's worden niet gecorreleerd) en voor Hallo query toocomplete binnen een redelijke tijd.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for hello query toocomplete in a reasonable time.</span></span>

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> <span data-ttu-id="aa6fc-124">U kunt verkennen en functies van deze steekproefgegevens genereren door op te slaan in een nieuwe tabel</span><span class="sxs-lookup"><span data-stu-id="aa6fc-124">You can explore and generate features from this sampled data by storing it in a new table</span></span>
> 
> 

### <span data-ttu-id="aa6fc-125"><a name="sql-aml"></a>Verbinding maken met tooAzure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="aa6fc-125"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="aa6fc-126">U kunt rechtstreeks Hallo voorbeeldquery's boven in hello Azure Machine Learning [importgegevens] [ import-data] module toodown voorbeeld Hallo gegevens op Hallo vliegen en brengt u het in een Azure Machine Learning-experiment.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-126">You can directly  use hello sample queries above in hello Azure Machine Learning [Import Data][import-data] module toodown-sample hello data on hello fly and bring it into an Azure Machine Learning experiment.</span></span> <span data-ttu-id="aa6fc-127">Een schermopname van het gebruik van Hallo lezer module tooread Hallo door actieve gegevens wordt hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="aa6fc-127">A screen shot of using hello reader module tooread hello sampled data is shown below:</span></span>

![lezer sql][1]

## <span data-ttu-id="aa6fc-129"><a name="python"></a>Gebruik Hallo Python programmeertaal</span><span class="sxs-lookup"><span data-stu-id="aa6fc-129"><a name="python"></a>Using hello Python programming language</span></span>
<span data-ttu-id="aa6fc-130">Deze sectie wordt gedemonstreerd met behulp van Hallo [pyodbc bibliotheek](https://code.google.com/p/pyodbc/) tooestablish ODBC verbinding tooa SQL server-database in Python.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-130">This section demonstrates using hello [pyodbc library](https://code.google.com/p/pyodbc/) tooestablish an ODBC connect tooa SQL server database in Python.</span></span> <span data-ttu-id="aa6fc-131">Hallo databaseverbindingsreeks is als volgt: (vervangen servername, dbname, username en password door uw configuratie):</span><span class="sxs-lookup"><span data-stu-id="aa6fc-131">hello database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="aa6fc-132">Hallo [Pandas](http://pandas.pydata.org/) in Python-bibliotheek biedt een uitgebreide set gegevensstructuren en hulpprogramma's voor gegevensanalyse voor gegevensmanipulatie voor het programmeren van Python.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-132">hello [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="aa6fc-133">Hallo-code hieronder leest een steekproef 0,1% Hallo gegevens uit een tabel in Azure SQL-database in een Pandas-gegevens:</span><span class="sxs-lookup"><span data-stu-id="aa6fc-133">hello code below reads a 0.1% sample of hello data from a table in Azure SQL database into a Pandas data :</span></span>

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

<span data-ttu-id="aa6fc-134">Nu kunt u werken met Hallo door actieve gegevens in Hallo Pandas gegevensframe.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-134">You can now work with hello sampled data in hello Pandas data frame.</span></span> 

### <span data-ttu-id="aa6fc-135"><a name="python-aml"></a>Verbinding maken met tooAzure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="aa6fc-135"><a name="python-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="aa6fc-136">U kunt na de code toosave Hallo omlaag actieve tooa voorbeeldgegevensbestand hello gebruiken en tooan Azure-blob te uploaden.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-136">You can use hello following sample code toosave hello down-sampled data tooa file and upload it tooan Azure blob.</span></span> <span data-ttu-id="aa6fc-137">Hallo-gegevens in blob Hallo kan worden rechtstreeks gelezen in een Azure Machine Learning-Experiment met Hallo [importgegevens] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="aa6fc-137">hello data in hello blob can be directly read into an Azure Machine Learning Experiment using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="aa6fc-138">Hallo stappen zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="aa6fc-138">hello steps are as follows:</span></span> 

1. <span data-ttu-id="aa6fc-139">Hallo pandas frame tooa lokale gegevensbestand schrijven</span><span class="sxs-lookup"><span data-stu-id="aa6fc-139">Write hello pandas data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="aa6fc-140">Lokaal bestand tooAzure blob uploaden</span><span class="sxs-lookup"><span data-stu-id="aa6fc-140">Upload local file tooAzure blob</span></span>
   
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
3. <span data-ttu-id="aa6fc-141">Gegevens lezen uit Azure blob met Azure Machine Learning [importgegevens] [ import-data] module, zoals wordt weergegeven in Hallo scherm schermafbeelding hieronder:</span><span class="sxs-lookup"><span data-stu-id="aa6fc-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in hello screen grab below:</span></span>

![lezer blob][2]

## <a name="hello-team-data-science-process-in-action-example"></a><span data-ttu-id="aa6fc-143">Hallo Team gegevens wetenschappelijke processen in actie voorbeeld</span><span class="sxs-lookup"><span data-stu-id="aa6fc-143">hello Team Data Science Process in Action example</span></span>
<span data-ttu-id="aa6fc-144">Zie voor een overzicht van de end-to-end voorbeeld Hallo Team gegevens wetenschappelijke processen een met een openbare gegevensset [Team gegevens wetenschappelijke processen in actie: SQL-Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="aa6fc-144">For an end-to-end walkthrough example of hello Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
