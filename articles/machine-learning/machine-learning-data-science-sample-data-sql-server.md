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
# <a name="heading"></a>Voorbeeldgegevens in SQL Server op Azure
Dit document ziet u hoe toosample gegevens opgeslagen in SQL Server op Azure met SQL of Hallo Python programmeertaal. U ziet ook hoe toomove voorbeeldgegevens in Azure Machine Learning te slaan in tooa-bestand uploaden tooan Azure blob en vervolgens te lezen in Azure Machine Learning Studio.

Hallo Python steekproeven gebruikt Hallo [pyodbc](https://code.google.com/p/pyodbc/) ODBC-bibliotheek tooconnect tooSQL Server op Azure en Hallo [Pandas](http://pandas.pydata.org/) bibliotheek toodo Hallo steekproeven.

> [!NOTE]
> Hallo voorbeeldcode SQL in dit document wordt ervan uitgegaan dat Hallo gegevens zich in een SQL-Server op Azure. Als dit niet het geval is, raadpleegt u te[verplaatsen van gegevens tooSQL Server op Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) onderwerp voor instructies over het toomove uw gegevens tooSQL Server op Azure.
> 
> 

Hallo volgende **menu** koppelingen tootopics waarin wordt beschreven hoe toosample gegevens uit verschillende omgevingen voor opslag. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Waarom een steekproef nemen uit uw gegevens?**
Als u van plan bent tooanalyze Hallo-gegevensset te groot is, is het meestal een goed idee Hallo toodown-sample data tooreduce het tooa kleiner, maar representatief en gemakkelijker grootte. Dit vereenvoudigt het begrip van de gegevens, exploratie en functie-engineering. De rol in Hallo [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is tooenable snel maken van een prototype van Hallo gegevensverwerking functies en machine learning-modellen.

Deze taak steekproeven is een stap in Hallo [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="SQL"></a>Met behulp van SQL
Deze sectie beschrijft de verschillende methoden met behulp van SQL tooperform eenvoudige steekproeven op Hallo gegevens in Hallo-database. Kies een methode op basis van de gegevensgrootte van uw en de distributie.

Hallo twee items hieronder laten zien hoe toouse newid in SQL Server-tooperform steekproeven Hallo. Hallo methode u kiest is afhankelijk van hoe willekeurige Hallo voorbeeld toobe gewenste (pk_id in Hallo voorbeeldcode hieronder wordt aangenomen dat een automatisch gegenereerde primaire sleutel toobe).

1. Minder strikte steekproef
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. Meer steekproef 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

Component TABLESAMPLE kan worden gebruikt voor steekproeven evenals gedemonstreerd hieronder. Dit kan een betere benadering zijn als de gegevensgrootte van uw groot is (ervan uitgaande dat de gegevens op verschillende pagina's worden niet gecorreleerd) en voor Hallo query toocomplete binnen een redelijke tijd.

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> U kunt verkennen en functies van deze steekproefgegevens genereren door op te slaan in een nieuwe tabel
> 
> 

### <a name="sql-aml"></a>Verbinding maken met tooAzure Machine Learning
U kunt rechtstreeks Hallo voorbeeldquery's boven in hello Azure Machine Learning [importgegevens] [ import-data] module toodown voorbeeld Hallo gegevens op Hallo vliegen en brengt u het in een Azure Machine Learning-experiment. Een schermopname van het gebruik van Hallo lezer module tooread Hallo door actieve gegevens wordt hieronder weergegeven:

![lezer sql][1]

## <a name="python"></a>Gebruik Hallo Python programmeertaal
Deze sectie wordt gedemonstreerd met behulp van Hallo [pyodbc bibliotheek](https://code.google.com/p/pyodbc/) tooestablish ODBC verbinding tooa SQL server-database in Python. Hallo databaseverbindingsreeks is als volgt: (vervangen servername, dbname, username en password door uw configuratie):

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Hallo [Pandas](http://pandas.pydata.org/) in Python-bibliotheek biedt een uitgebreide set gegevensstructuren en hulpprogramma's voor gegevensanalyse voor gegevensmanipulatie voor het programmeren van Python. Hallo-code hieronder leest een steekproef 0,1% Hallo gegevens uit een tabel in Azure SQL-database in een Pandas-gegevens:

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

Nu kunt u werken met Hallo door actieve gegevens in Hallo Pandas gegevensframe. 

### <a name="python-aml"></a>Verbinding maken met tooAzure Machine Learning
U kunt na de code toosave Hallo omlaag actieve tooa voorbeeldgegevensbestand hello gebruiken en tooan Azure-blob te uploaden. Hallo-gegevens in blob Hallo kan worden rechtstreeks gelezen in een Azure Machine Learning-Experiment met Hallo [importgegevens] [ import-data] module. Hallo stappen zijn als volgt: 

1. Hallo pandas frame tooa lokale gegevensbestand schrijven
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. Lokaal bestand tooAzure blob uploaden
   
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
3. Gegevens lezen uit Azure blob met Azure Machine Learning [importgegevens] [ import-data] module, zoals wordt weergegeven in Hallo scherm schermafbeelding hieronder:

![lezer blob][2]

## <a name="hello-team-data-science-process-in-action-example"></a>Hallo Team gegevens wetenschappelijke processen in actie voorbeeld
Zie voor een overzicht van de end-to-end voorbeeld Hallo Team gegevens wetenschappelijke processen een met een openbare gegevensset [Team gegevens wetenschappelijke processen in actie: SQL-Server](machine-learning-data-science-process-sql-walkthrough.md).

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
