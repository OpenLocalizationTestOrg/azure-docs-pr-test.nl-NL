---
title: aaaExplore gegevens in SQL Server virtuele Machine in Azure | Microsoft Docs
description: Hoe tooexplore gegevens die zijn opgeslagen in een virtuele SQL Server-machine in Azure.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ccbb3085-af9e-4ec2-9df2-15dcab261d05
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: fcc449fc0d0e49be9b673cfb2de347cf44804017
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a>Gegevens in virtuele SQL Server-machine verkennen in Azure
Dit document bevat informatie over hoe tooexplore gegevens die zijn opgeslagen in een virtuele SQL Server-machine in Azure. Dit kan worden gedaan door gegevens worsteling met SQL of via een programmeertaal zoals Python.

Hallo volgende **menu** tootopics waarin wordt beschreven hoe toouse hulpprogramma's voor tooexplore gegevens uit verschillende omgevingen voor opslag is gekoppeld. Deze taak is een stap in Hallo Cortana Analytics proces (CAP).

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> Hallo voorbeeld SQL-instructies in dit document wordt ervan uitgegaan dat gegevens in SQL Server worden. Dit niet het geval is, raadpleegt u toohello cloud gegevens wetenschap proces kaart toolearn hoe toomove uw gegevens tooSQL Server.
> 
> 

## <a name="sql-dataexploration"></a>SQL-gegevens met SQL-scripts verkennen
Hier volgen enkele voorbeelden SQL-scripts die gebruikt tooexplore gegevensarchieven SQL Server worden kunnen.

1. Hallo-telling van metingen per dag
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. Hallo niveaus in een categorische kolom ophalen
   
    `select  distinct <column_name> from <databasename>`
3. Hallo aantal niveaus in de combinatie van twee categorische kolommen ophalen 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. Hallo-distributie voor numerieke kolommen ophalen
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> Voor een voorbeeld, kunt u Hallo [NYC Taxi gegevensset](http://www.andresmh.com/nyctaxitrips/) Raadpleeg toohello IPNB met de titel en [IPython laptop- en SQL Server met de gegevens van de NYC worsteling](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) voor een end-to-end-procedure.
> 
> 

## <a name="python"></a>SQL-gegevens met behulp van Python verkennen
Met behulp van Python tooexplore gegevens en het genereren van functies als Hallo gegevens in SQL Server is vergelijkbaar tooprocessing gegevens in Azure blob met behulp van Python, zoals beschreven in [proces Azure Blob-gegevens in uw omgeving van de wetenschappelijke gegevens](machine-learning-data-science-process-data-blob.md). Hallo gegevens moet toobe uit Hallo-database in een pandas DataFrame geladen en vervolgens verder kan worden verwerkt. We Documenteer Hallo proces van het verbinden van toohello database en het Hallo-gegevens in Hallo DataFrame in deze sectie te laden.

Hallo na indeling verbindingsreeks kan gebruikte tooconnect tooa SQL Server-database met Python met pyodbc (vervang servername, dbname, gebruikersnaam en wachtwoord op uw specifieke waarden) zijn:

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Hallo [Pandas bibliotheek](http://pandas.pydata.org/) in Python voorziet in een uitgebreide set van gegevensstructuren en hulpprogramma's voor gegevensanalyse voor gegevensmanipulatie voor het programmeren van Python. Hallo leest volgende code Hallo resultaten geretourneerd uit een SQL Server-database in een kader Pandas-gegevens:

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

Nu u met de Hallo Pandas DataFrame werken kunt zoals besproken in Hallo onderwerp [proces Azure Blob-gegevens in uw omgeving van de wetenschappelijke gegevens](machine-learning-data-science-process-data-blob.md).

## <a name="cortana-analytics-process-in-action-example"></a>Cortana-Analytics-proces in de actie voorbeeld
Zie voor een voorbeeld van de end-to-end-overzicht van Hallo Cortana-Analytics proces met behulp van een openbare gegevensset, [Hallo Team gegevens wetenschappelijke processen in actie: met behulp van SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

