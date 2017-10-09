---
title: gegevens in een virtuele machine van SQL Server op Azure aaaExplore | Microsoft Docs
description: Gegevens verkennen en genereren van functies in een virtuele machine van SQL Server op Azure
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: 
ms.assetid: 3949fb2c-ffab-49fb-908d-27d5e42f743b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 67f4b058b0f6557ee15fd42795c918d68f1a9871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Procesgegevens in de virtuele Machine van SQL Server op Azure
Dit document bevat informatie over hoe tooexplore gegevens en het genereren van de functies voor gegevens die zijn opgeslagen in een virtuele SQL Server-machine in Azure. Dit kan worden gedaan door gegevens worsteling met SQL of via een programmeertaal zoals Python.

> [!NOTE]
> Hallo voorbeeld SQL-instructies in dit document wordt ervan uitgegaan dat gegevens in SQL Server worden. Dit niet het geval is, raadpleegt u toohello cloud gegevens wetenschap proces kaart toolearn hoe toomove uw gegevens tooSQL Server.
> 
> 

## <a name="SQL"></a>Met behulp van SQL
We beschrijven Hallo gegevens worsteling taken in deze sectie met behulp van SQL te volgen:

1. [Gegevensverkenning](#sql-dataexploration)
2. [Functie generatie](#sql-featuregen)

### <a name="sql-dataexploration"></a>Gegevensverkenning
Hier volgen enkele voorbeelden SQL-scripts die gebruikt tooexplore gegevensarchieven SQL Server worden kunnen.

> [!NOTE]
> Voor een voorbeeld, kunt u Hallo [NYC Taxi gegevensset](http://www.andresmh.com/nyctaxitrips/) Raadpleeg toohello IPNB met de titel en [IPython laptop- en SQL Server met de gegevens van de NYC worsteling](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) voor een end-to-end-procedure.
> 
> 

1. Hallo-telling van metingen per dag
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. Hallo niveaus in een categorische kolom ophalen
   
    `select  distinct <column_name> from <databasename>`
3. Hallo aantal niveaus in de combinatie van twee categorische kolommen ophalen 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. Hallo-distributie voor numerieke kolommen ophalen
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <a name="sql-featuregen"></a>Functie generatie
In deze sectie beschrijven we manieren voor het genereren van functies met behulp van SQL:  

1. [Aantal op basis van functie generatie](#sql-countfeature)
2. [Met binning functie generatie](#sql-binningfeature)
3. [Hallo-functies rolt uit één kolom](#sql-featurerollout)

> [!NOTE]
> Als u extra functies genereert, kunt u toe te voegen als kolommen toohello bestaande tabel of een nieuwe tabel maken met de Hallo extra functies en primaire sleutel, die kan worden samengevoegd met de oorspronkelijke tabel Hallo. 
> 
> 

### <a name="sql-countfeature"></a>Aantal op basis van functie generatie
Hallo volgende voorbeelden worden twee manieren voor het genereren van het aantal functies. Hallo eerste methode Voorwaardelijke som gebruikt en de tweede methode gebruikt Hallo Hallo 'where-clausule. Deze kunnen vervolgens worden samengevoegd met de Hallo oorspronkelijke (met behulp van de primaire-sleutelkolommen) toohave aantal tabelfuncties naast Hallo oorspronkelijke gegevens.

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <a name="sql-binningfeature"></a>Met binning functie generatie
Hallo volgende voorbeeld laat zien hoe toogenerate binned functies met binning (met behulp van vijf opslaglocaties) een numerieke kolom die kan worden gebruikt als een functie in plaats daarvan:

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <a name="sql-featurerollout"></a>Hallo-functies rolt uit één kolom
In deze sectie ziet u hoe tooroll uit één kolom in een tabel toogenerate extra onderdelen. Hallo-voorbeeld wordt ervan uitgegaan dat er een kolom breedtegraad of lengtegraad in Hallo tabel waaruit u toogenerate functies probeert.

Hier volgt een korte primer op breedtegraad/lengtegraad locatiegegevens (resources voorzien van stackoverflow [hoe toomeasure nauwkeurigheid van de breedtegraad en lengtegraad Hallo?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)). Dit is nuttig toounderstand voordat featurizing Hallo locatieveld:

* Hallo aanmelding weten ons of er zijn ten noorden of Zuid, Oost of west op Hallo wereld.
* Een andere waarde dan nul honderden cijfer vertelt ons dat we WL, niet NB gebruiken!
* Hallo tientallen cijfer biedt een tooabout positie 1000 kilometers. Dit biedt ons nuttige informatie over welke continent of Oceaan we worden op.
* Hallo eenheden cijfer (één decimale graad) biedt een positie omhoog too111 kilometers (60 zeemijl, ongeveer 69 mijl). Deze kunt ons ongeveer welke grote rechtsgebied die we in zijn.
* de eerste decimaal Hallo too11.1 km is waard: het Hallo-positie van een grote plaats van een aangrenzende grote stad kunt onderscheiden.
* de tweede decimaal Hallo too1.1 km is waard: het kunt één village scheiden van Hallo naast.
* de derde decimaal Hallo is waard too110 m: dat deze grote de veld of institutionele bereik kunt identificeren.
* de vierde decimaal Hallo is waard too11 m: dat deze een pakket van de grond kunt identificeren. Het is gemiddelde nauwkeurigheid van een niet-gecorrigeerde GPS-eenheid zonder storing vergelijkbare toohello.
* Hallo vijfde decimaal is waard too1.1 m: dat deze structuren onderscheidt van elkaar. Nauwkeurigheid toothis niveau met commerciële GPS-eenheden kan alleen worden verkregen met differentiële gecorrigeerd.
* Hallo zesde decimaal is waard too0.11 m: die u deze gebruiken kunt voor het indelen van structuren met details voor het ontwerpen van landschappen, wegen bouwen. Moet meer dan goed genoeg voor het bijhouden van verkeer van glaciers en rivieren zijn. Dit kan worden bereikt door middel van hele maatregelen met GPS zoals differentially gecorrigeerde GPS.

Hallo locatie-informatie kan worden featurized als volgt scheiden van de regio, locatie en plaats. Houd er rekening mee dat kunt u ook een REST-eindpunt zoals Bing kaarten-API beschikbaar op aanroepen [zoeken naar een locatie met punt](https://msdn.microsoft.com/library/ff701710.aspx) tooget Hallo regio/regionale informatie.

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

Deze functies op basis van locatie kunnen worden verder gebruikte toogenerate aantal aanvullende functies zoals eerder beschreven. 

> [!TIP]
> U kunt programmatisch Hallo registreert met behulp van de taal van keuze invoegen. Mogelijk moet u tooinsert Hallo gegevens in reeksen tooimprove schrijven efficiëntie (voor een voorbeeld van hoe toodo deze pyodbc gebruikt, Zie [A HelloWorld voorbeeld tooaccess SQLServer met behulp van python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)). Een ander alternatief is tooinsert gegevens in Hallo-database met de Hallo [hulpprogramma BCP](https://msdn.microsoft.com/library/ms162802.aspx).
> 
> 

### <a name="sql-aml"></a>Verbinding maken met tooAzure Machine Learning
Hallo zojuist gegenereerde functie worden toegevoegd als een bestaande tabel met kolom tooan of opgeslagen in een nieuwe tabel en samengevoegd met de oorspronkelijke tabel Hallo voor machine learning. Functies kunnen worden gegenereerd of toegankelijk is als al hebt gemaakt, met Hallo [importgegevens] [ import-data] -module in Azure Machine Learning zoals hieronder wordt weergegeven:

![azureml lezers][1] 

## <a name="python"></a>Gebruik een programmeertaal zoals Python
Met behulp van Python tooexplore gegevens en het genereren van functies als Hallo gegevens in SQL Server is vergelijkbaar tooprocessing gegevens in Azure blob met behulp van Python, zoals beschreven in [proces Azure Blob-gegevens in uw omgeving van de wetenschappelijke gegevens](machine-learning-data-science-process-data-blob.md). Hallo gegevens moet toobe uit Hallo-database in een pandas gegevensframe geladen en vervolgens verder kan worden verwerkt. We Documenteer Hallo proces van het verbinden van toohello database en het Hallo-gegevens in Hallo gegevensframe in deze sectie te laden.

Hallo na indeling verbindingsreeks kan gebruikte tooconnect tooa SQL Server-database met Python met pyodbc (vervang servername, dbname, gebruikersnaam en wachtwoord op uw specifieke waarden) zijn:

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Hallo [Pandas bibliotheek](http://pandas.pydata.org/) in Python voorziet in een uitgebreide set van gegevensstructuren en hulpprogramma's voor gegevensanalyse voor gegevensmanipulatie voor het programmeren van Python. Hallo-code hieronder gelezen Hallo resultaten geretourneerd uit een SQL Server-database in een kader Pandas-gegevens:

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

Nu u met de Hallo Pandas gegevensframe werken kunt zoals beschreven in artikel Hallo [proces Azure Blob-gegevens in uw omgeving van de wetenschappelijke gegevens](machine-learning-data-science-process-data-blob.md).

## <a name="azure-data-science-in-action-example"></a>Azure Gegevenswetenschap in actie voorbeeld
Zie voor een voorbeeld van de end-to-end-overzicht van hello Azure gegevens wetenschappelijke processen met behulp van een openbare gegevensset, [Azure gegevens wetenschappelijke processen in actie](machine-learning-data-science-process-sql-walkthrough.md).

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

