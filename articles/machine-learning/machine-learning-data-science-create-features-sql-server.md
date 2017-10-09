---
title: aaaCreate functies voor gegevens in SQL Server met behulp van SQL en Python | Microsoft Docs
description: Gegevens over het installatieproces van SQL Azure
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: 
ms.assetid: bf1f4a6c-7711-4456-beb7-35fdccd46a44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;fashah;garye
ms.openlocfilehash: 223352edb0377a159333e7528ad03c43902e6f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-sql-server-using-sql-and-python"></a>Met SQL en Python functies maken voor gegevens in SQL Server
Dit document ziet u hoe toogenerate functies voor opgeslagen gegevens in een SQL Server VM op Azure waarmee algoritmen efficiënter leren van Hallo-gegevens. Dit kan worden gedaan met behulp van SQL of met behulp van een programmeertaal zoals Python, die hier worden uitgelegd.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Dit **menu** koppelingen tootopics waarin wordt beschreven hoe toocreate functies voor gegevens in verschillende omgevingen. Deze taak is een stap in Hallo [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

> [!NOTE]
> Voor een voorbeeld, kunt u raadplegen Hallo [NYC Taxi gegevensset](http://www.andresmh.com/nyctaxitrips/) Raadpleeg toohello IPNB met de titel en [IPython laptop- en SQL Server met de gegevens van de NYC worsteling](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) voor een end-to-end-procedure.
> 
> 

## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u hebt:

* Een Azure storage-account gemaakt. Als u instructies nodig hebt, raadpleegt u [een Azure Storage-account maken](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Uw gegevens opgeslagen in SQL Server. Als u niet hebt, raadpleegt u [verplaatsen van gegevens tooan Azure SQL Database voor Azure Machine Learning](machine-learning-data-science-move-sql-azure.md) voor instructies over hoe toomove Hallo er gegevens.

## <a name="sql-featuregen"></a>Functie genereren met behulp van SQL
In deze sectie beschrijven we manieren voor het genereren van functies met behulp van SQL:  

1. [Aantal op basis van functie generatie](#sql-countfeature)
2. [Met binning functie generatie](#sql-binningfeature)
3. [Hallo-functies rolt uit één kolom](#sql-featurerollout)

> [!NOTE]
> Als u extra functies genereert, kunt u toe te voegen als kolommen toohello bestaande tabel of een nieuwe tabel maken met de Hallo extra functies en primaire sleutel, die kan worden samengevoegd met de oorspronkelijke tabel Hallo.
> 
> 

### <a name="sql-countfeature"></a>Aantal op basis van functie generatie
Dit document wordt gedemonstreerd op twee manieren voor het genereren van het aantal functies. Hallo eerste methode Voorwaardelijke som gebruikt en de tweede methode gebruikt Hallo Hallo 'where-clausule. Deze kunnen vervolgens worden samengevoegd met de Hallo oorspronkelijke (met behulp van de primaire-sleutelkolommen) toohave aantal tabelfuncties naast Hallo oorspronkelijke gegevens.

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3>

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename>
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2>

### <a name="sql-binningfeature"></a>Met binning functie generatie
Hallo volgende voorbeeld laat zien hoe toogenerate binned functies met binning (met behulp van 5 opslaglocaties) een numerieke kolom die kan worden gebruikt als een functie in plaats daarvan:

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <a name="sql-featurerollout"></a>Hallo-functies rolt uit één kolom
In deze sectie ziet u hoe tooroll-out één kolom in een tabel toogenerate extra onderdelen. Hallo-voorbeeld wordt ervan uitgegaan dat er een kolom breedtegraad of lengtegraad in Hallo tabel waaruit u toogenerate functies probeert.

Hier volgt een korte primer op breedtegraad/lengtegraad locatiegegevens (resources voorzien van stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`). Dit is nuttig toounderstand voordat featurizing Hallo locatieveld:

* Hallo aanmelding weten ons of er zijn ten noorden of Zuid, Oost of west op Hallo wereld.
* Een andere waarde dan nul honderden cijfer vertellen we maken gebruik van WL, niet NB!
* Hallo tientallen cijfer biedt een tooabout positie 1000 kilometers. Dit biedt ons nuttige informatie over welke continent of Oceaan we worden op.
* Hallo eenheden cijfer (één decimale graad) biedt een positie omhoog too111 kilometers (60 zeemijl, ongeveer 69 mijl). Deze kunt ons ongeveer welke grote rechtsgebied die we in zijn.
* de eerste decimaal Hallo too11.1 km is waard: het Hallo-positie van een grote plaats van een aangrenzende grote stad kunt onderscheiden.
* de tweede decimaal Hallo too1.1 km is waard: het kunt één village scheiden van Hallo naast.
* de derde decimaal Hallo is waard too110 m: dat deze grote de veld of institutionele bereik kunt identificeren.
* de vierde decimaal Hallo is waard too11 m: dat deze een pakket van de grond kunt identificeren. Het is gemiddelde nauwkeurigheid van een niet-gecorrigeerde GPS-eenheid zonder storing vergelijkbare toohello.
* Hallo vijfde decimaal is waard too1.1 m: deze structuren van elkaar te onderscheiden. Nauwkeurigheid toothis niveau met commerciële GPS-eenheden kan alleen worden verkregen met differentiële gecorrigeerd.
* Hallo zesde decimaal is waard too0.11 m: die u deze gebruiken kunt voor het indelen van structuren met details voor het ontwerpen van landschappen, wegen bouwen. Moet meer dan goed genoeg voor het bijhouden van verkeer van glaciers en rivieren zijn. Dit kan worden bereikt door middel van hele maatregelen met GPS zoals differentially gecorrigeerde GPS.

Hallo locatiegegevens kunt mag featurized als volgt scheiden van de regio, locatie en plaats. Let op: één keer kunt ook aanroepen een REST-eindpunt zoals Bing kaarten-API beschikbaar op `https://msdn.microsoft.com/library/ff701710.aspx` tooget Hallo regio/regionale informatie.

    select
        <location_columnname>
        ,round(<location_columnname>,0) as l1        
        ,l2=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 1 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),1,1) else '0' end     
        ,l3=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 2 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),2,1) else '0' end     
        ,l4=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 3 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),3,1) else '0' end     
        ,l5=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 4 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),4,1) else '0' end     
        ,l6=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 5 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),5,1) else '0' end     
        ,l7=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 6 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),6,1) else '0' end     
    from <tablename>

Hallo bovenstaande locatie op basis van de functies verder kunnen worden gebruikt toogenerate aantal aanvullende functies, zoals eerder beschreven.

> [!TIP]
> U kunt programmatisch Hallo registreert met behulp van de taal van keuze invoegen. Mogelijk moet u tooinsert Hallo gegevens in reeksen tooimprove schrijven efficiëntie [uitchecken Hallo voorbeeld van hoe u toodo deze met pyodbc hier](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).
> Een ander alternatief is tooinsert gegevens in het Hallo-database met [hulpprogramma BCP](https://msdn.microsoft.com/library/ms162802.aspx)
> 
> 

### <a name="sql-aml"></a>Verbinding maken met tooAzure Machine Learning
Hallo zojuist gegenereerde functie worden toegevoegd als een bestaande tabel met kolom tooan of opgeslagen in een nieuwe tabel en samengevoegd met de oorspronkelijke tabel Hallo voor machine learning. Functies kunnen worden gegenereerd of toegankelijk is als al hebt gemaakt, met Hallo [importgegevens](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) -module in de Azure ML zoals hieronder wordt weergegeven:

![azureml lezers](./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png)

## <a name="python"></a>Gebruik een programmeertaal zoals Python
Soortgelijke tooprocessing gegevens met behulp van Python toogenerate functies wanneer Hallo gegevens in SQL Server is in Azure blob met behulp van Python, zoals beschreven in [proces Azure Blob-gegevens in u gegevens wetenschappelijke omgeving](machine-learning-data-science-process-data-blob.md). Hallo gegevens moet toobe uit Hallo-database in een pandas gegevensframe geladen en vervolgens verder kan worden verwerkt. We Documenteer Hallo proces van het verbinden van toohello database en het Hallo-gegevens in Hallo gegevensframe in deze sectie te laden.

Hallo na indeling verbindingsreeks kan gebruikte tooconnect tooa SQL Server-database met Python met pyodbc (vervang servername, dbname, gebruikersnaam en wachtwoord met uw specifieke waarden) zijn:

    #Set up hello SQL Azure connection
    import pyodbc
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Hallo [Pandas bibliotheek](http://pandas.pydata.org/) in Python voorziet in een uitgebreide set van gegevensstructuren en hulpprogramma's voor gegevensanalyse voor gegevensmanipulatie voor het programmeren van Python. Hallo-code hieronder gelezen Hallo resultaten geretourneerd uit een SQL Server-database in een kader Pandas-gegevens:

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

Nu u met de Hallo Pandas gegevensframe werken kunt zoals beschreven in de onderwerpen [maken van de functies voor Azure blob storage-gegevens met behulp van Panda](machine-learning-data-science-create-features-blob.md).

