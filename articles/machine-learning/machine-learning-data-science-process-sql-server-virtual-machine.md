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
# <span data-ttu-id="28348-103"><a name="heading"></a>Procesgegevens in de virtuele Machine van SQL Server op Azure</span><span class="sxs-lookup"><span data-stu-id="28348-103"><a name="heading"></a>Process Data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="28348-104">Dit document bevat informatie over hoe tooexplore gegevens en het genereren van de functies voor gegevens die zijn opgeslagen in een virtuele SQL Server-machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="28348-104">This document covers how tooexplore data and generate features for data stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="28348-105">Dit kan worden gedaan door gegevens worsteling met SQL of via een programmeertaal zoals Python.</span><span class="sxs-lookup"><span data-stu-id="28348-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

> [!NOTE]
> <span data-ttu-id="28348-106">Hallo voorbeeld SQL-instructies in dit document wordt ervan uitgegaan dat gegevens in SQL Server worden.</span><span class="sxs-lookup"><span data-stu-id="28348-106">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="28348-107">Dit niet het geval is, raadpleegt u toohello cloud gegevens wetenschap proces kaart toolearn hoe toomove uw gegevens tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="28348-107">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="28348-108"><a name="SQL"></a>Met behulp van SQL</span><span class="sxs-lookup"><span data-stu-id="28348-108"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="28348-109">We beschrijven Hallo gegevens worsteling taken in deze sectie met behulp van SQL te volgen:</span><span class="sxs-lookup"><span data-stu-id="28348-109">We describe hello following data wrangling tasks in this section using SQL:</span></span>

1. [<span data-ttu-id="28348-110">Gegevensverkenning</span><span class="sxs-lookup"><span data-stu-id="28348-110">Data Exploration</span></span>](#sql-dataexploration)
2. [<span data-ttu-id="28348-111">Functie generatie</span><span class="sxs-lookup"><span data-stu-id="28348-111">Feature Generation</span></span>](#sql-featuregen)

### <span data-ttu-id="28348-112"><a name="sql-dataexploration"></a>Gegevensverkenning</span><span class="sxs-lookup"><span data-stu-id="28348-112"><a name="sql-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="28348-113">Hier volgen enkele voorbeelden SQL-scripts die gebruikt tooexplore gegevensarchieven SQL Server worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="28348-113">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="28348-114">Voor een voorbeeld, kunt u Hallo [NYC Taxi gegevensset](http://www.andresmh.com/nyctaxitrips/) Raadpleeg toohello IPNB met de titel en [IPython laptop- en SQL Server met de gegevens van de NYC worsteling](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) voor een end-to-end-procedure.</span><span class="sxs-lookup"><span data-stu-id="28348-114">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

1. <span data-ttu-id="28348-115">Hallo-telling van metingen per dag</span><span class="sxs-lookup"><span data-stu-id="28348-115">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="28348-116">Hallo niveaus in een categorische kolom ophalen</span><span class="sxs-lookup"><span data-stu-id="28348-116">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="28348-117">Hallo aantal niveaus in de combinatie van twee categorische kolommen ophalen</span><span class="sxs-lookup"><span data-stu-id="28348-117">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="28348-118">Hallo-distributie voor numerieke kolommen ophalen</span><span class="sxs-lookup"><span data-stu-id="28348-118">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <span data-ttu-id="28348-119"><a name="sql-featuregen"></a>Functie generatie</span><span class="sxs-lookup"><span data-stu-id="28348-119"><a name="sql-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="28348-120">In deze sectie beschrijven we manieren voor het genereren van functies met behulp van SQL:</span><span class="sxs-lookup"><span data-stu-id="28348-120">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="28348-121">Aantal op basis van functie generatie</span><span class="sxs-lookup"><span data-stu-id="28348-121">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="28348-122">Met binning functie generatie</span><span class="sxs-lookup"><span data-stu-id="28348-122">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="28348-123">Hallo-functies rolt uit één kolom</span><span class="sxs-lookup"><span data-stu-id="28348-123">Rolling out hello features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="28348-124">Als u extra functies genereert, kunt u toe te voegen als kolommen toohello bestaande tabel of een nieuwe tabel maken met de Hallo extra functies en primaire sleutel, die kan worden samengevoegd met de oorspronkelijke tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="28348-124">Once you generate additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, that can be joined with hello original table.</span></span> 
> 
> 

### <span data-ttu-id="28348-125"><a name="sql-countfeature"></a>Aantal op basis van functie generatie</span><span class="sxs-lookup"><span data-stu-id="28348-125"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="28348-126">Hallo volgende voorbeelden worden twee manieren voor het genereren van het aantal functies.</span><span class="sxs-lookup"><span data-stu-id="28348-126">hello following examples demonstrate two ways of generating count features.</span></span> <span data-ttu-id="28348-127">Hallo eerste methode Voorwaardelijke som gebruikt en de tweede methode gebruikt Hallo Hallo 'where-clausule.</span><span class="sxs-lookup"><span data-stu-id="28348-127">hello first method uses conditional sum and hello second method uses hello 'where' clause.</span></span> <span data-ttu-id="28348-128">Deze kunnen vervolgens worden samengevoegd met de Hallo oorspronkelijke (met behulp van de primaire-sleutelkolommen) toohave aantal tabelfuncties naast Hallo oorspronkelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="28348-128">These can then be joined with hello original table (using primary key columns) toohave count features alongside hello original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <span data-ttu-id="28348-129"><a name="sql-binningfeature"></a>Met binning functie generatie</span><span class="sxs-lookup"><span data-stu-id="28348-129"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="28348-130">Hallo volgende voorbeeld laat zien hoe toogenerate binned functies met binning (met behulp van vijf opslaglocaties) een numerieke kolom die kan worden gebruikt als een functie in plaats daarvan:</span><span class="sxs-lookup"><span data-stu-id="28348-130">hello following example shows how toogenerate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="28348-131"><a name="sql-featurerollout"></a>Hallo-functies rolt uit één kolom</span><span class="sxs-lookup"><span data-stu-id="28348-131"><a name="sql-featurerollout"></a>Rolling out hello features from a single column</span></span>
<span data-ttu-id="28348-132">In deze sectie ziet u hoe tooroll uit één kolom in een tabel toogenerate extra onderdelen.</span><span class="sxs-lookup"><span data-stu-id="28348-132">In this section, we demonstrate how tooroll out a single column in a table toogenerate additional features.</span></span> <span data-ttu-id="28348-133">Hallo-voorbeeld wordt ervan uitgegaan dat er een kolom breedtegraad of lengtegraad in Hallo tabel waaruit u toogenerate functies probeert.</span><span class="sxs-lookup"><span data-stu-id="28348-133">hello example assumes that there is a latitude or longitude column in hello table from which you are trying toogenerate features.</span></span>

<span data-ttu-id="28348-134">Hier volgt een korte primer op breedtegraad/lengtegraad locatiegegevens (resources voorzien van stackoverflow [hoe toomeasure nauwkeurigheid van de breedtegraad en lengtegraad Hallo?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span><span class="sxs-lookup"><span data-stu-id="28348-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How toomeasure hello accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span></span> <span data-ttu-id="28348-135">Dit is nuttig toounderstand voordat featurizing Hallo locatieveld:</span><span class="sxs-lookup"><span data-stu-id="28348-135">This is useful toounderstand before featurizing hello location field:</span></span>

* <span data-ttu-id="28348-136">Hallo aanmelding weten ons of er zijn ten noorden of Zuid, Oost of west op Hallo wereld.</span><span class="sxs-lookup"><span data-stu-id="28348-136">hello sign tells us whether we are north or south, east or west on hello globe.</span></span>
* <span data-ttu-id="28348-137">Een andere waarde dan nul honderden cijfer vertelt ons dat we WL, niet NB gebruiken!</span><span class="sxs-lookup"><span data-stu-id="28348-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span></span>
* <span data-ttu-id="28348-138">Hallo tientallen cijfer biedt een tooabout positie 1000 kilometers.</span><span class="sxs-lookup"><span data-stu-id="28348-138">hello tens digit gives a position tooabout 1,000 kilometers.</span></span> <span data-ttu-id="28348-139">Dit biedt ons nuttige informatie over welke continent of Oceaan we worden op.</span><span class="sxs-lookup"><span data-stu-id="28348-139">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="28348-140">Hallo eenheden cijfer (één decimale graad) biedt een positie omhoog too111 kilometers (60 zeemijl, ongeveer 69 mijl).</span><span class="sxs-lookup"><span data-stu-id="28348-140">hello units digit (one decimal degree) gives a position up too111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="28348-141">Deze kunt ons ongeveer welke grote rechtsgebied die we in zijn.</span><span class="sxs-lookup"><span data-stu-id="28348-141">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="28348-142">de eerste decimaal Hallo too11.1 km is waard: het Hallo-positie van een grote plaats van een aangrenzende grote stad kunt onderscheiden.</span><span class="sxs-lookup"><span data-stu-id="28348-142">hello first decimal place is worth up too11.1 km: it can distinguish hello position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="28348-143">de tweede decimaal Hallo too1.1 km is waard: het kunt één village scheiden van Hallo naast.</span><span class="sxs-lookup"><span data-stu-id="28348-143">hello second decimal place is worth up too1.1 km: it can separate one village from hello next.</span></span>
* <span data-ttu-id="28348-144">de derde decimaal Hallo is waard too110 m: dat deze grote de veld of institutionele bereik kunt identificeren.</span><span class="sxs-lookup"><span data-stu-id="28348-144">hello third decimal place is worth up too110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="28348-145">de vierde decimaal Hallo is waard too11 m: dat deze een pakket van de grond kunt identificeren.</span><span class="sxs-lookup"><span data-stu-id="28348-145">hello fourth decimal place is worth up too11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="28348-146">Het is gemiddelde nauwkeurigheid van een niet-gecorrigeerde GPS-eenheid zonder storing vergelijkbare toohello.</span><span class="sxs-lookup"><span data-stu-id="28348-146">It is comparable toohello typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="28348-147">Hallo vijfde decimaal is waard too1.1 m: dat deze structuren onderscheidt van elkaar.</span><span class="sxs-lookup"><span data-stu-id="28348-147">hello fifth decimal place is worth up too1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="28348-148">Nauwkeurigheid toothis niveau met commerciële GPS-eenheden kan alleen worden verkregen met differentiële gecorrigeerd.</span><span class="sxs-lookup"><span data-stu-id="28348-148">Accuracy toothis level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="28348-149">Hallo zesde decimaal is waard too0.11 m: die u deze gebruiken kunt voor het indelen van structuren met details voor het ontwerpen van landschappen, wegen bouwen.</span><span class="sxs-lookup"><span data-stu-id="28348-149">hello sixth decimal place is worth up too0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="28348-150">Moet meer dan goed genoeg voor het bijhouden van verkeer van glaciers en rivieren zijn.</span><span class="sxs-lookup"><span data-stu-id="28348-150">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="28348-151">Dit kan worden bereikt door middel van hele maatregelen met GPS zoals differentially gecorrigeerde GPS.</span><span class="sxs-lookup"><span data-stu-id="28348-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="28348-152">Hallo locatie-informatie kan worden featurized als volgt scheiden van de regio, locatie en plaats.</span><span class="sxs-lookup"><span data-stu-id="28348-152">hello location information can be featurized as follows, separating out region, location, and city information.</span></span> <span data-ttu-id="28348-153">Houd er rekening mee dat kunt u ook een REST-eindpunt zoals Bing kaarten-API beschikbaar op aanroepen [zoeken naar een locatie met punt](https://msdn.microsoft.com/library/ff701710.aspx) tooget Hallo regio/regionale informatie.</span><span class="sxs-lookup"><span data-stu-id="28348-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) tooget hello region/district information.</span></span>

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

<span data-ttu-id="28348-154">Deze functies op basis van locatie kunnen worden verder gebruikte toogenerate aantal aanvullende functies zoals eerder beschreven.</span><span class="sxs-lookup"><span data-stu-id="28348-154">These location-based features can be further used toogenerate additional count features as described earlier.</span></span> 

> [!TIP]
> <span data-ttu-id="28348-155">U kunt programmatisch Hallo registreert met behulp van de taal van keuze invoegen.</span><span class="sxs-lookup"><span data-stu-id="28348-155">You can programmatically insert hello records using your language of choice.</span></span> <span data-ttu-id="28348-156">Mogelijk moet u tooinsert Hallo gegevens in reeksen tooimprove schrijven efficiëntie (voor een voorbeeld van hoe toodo deze pyodbc gebruikt, Zie [A HelloWorld voorbeeld tooaccess SQLServer met behulp van python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span><span class="sxs-lookup"><span data-stu-id="28348-156">You may need tooinsert hello data in chunks tooimprove write efficiency (for an example of how toodo this using pyodbc, see [A HelloWorld sample tooaccess SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span></span> <span data-ttu-id="28348-157">Een ander alternatief is tooinsert gegevens in Hallo-database met de Hallo [hulpprogramma BCP](https://msdn.microsoft.com/library/ms162802.aspx).</span><span class="sxs-lookup"><span data-stu-id="28348-157">Another alternative is tooinsert data in hello database using hello [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span></span>
> 
> 

### <span data-ttu-id="28348-158"><a name="sql-aml"></a>Verbinding maken met tooAzure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="28348-158"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="28348-159">Hallo zojuist gegenereerde functie worden toegevoegd als een bestaande tabel met kolom tooan of opgeslagen in een nieuwe tabel en samengevoegd met de oorspronkelijke tabel Hallo voor machine learning.</span><span class="sxs-lookup"><span data-stu-id="28348-159">hello newly generated feature can be added as a column tooan existing table or stored in a new table and joined with hello original table for machine learning.</span></span> <span data-ttu-id="28348-160">Functies kunnen worden gegenereerd of toegankelijk is als al hebt gemaakt, met Hallo [importgegevens] [ import-data] -module in Azure Machine Learning zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="28348-160">Features can be generated or accessed if already created, using hello [Import Data][import-data] module in Azure Machine Learning as shown below:</span></span>

![azureml lezers][1] 

## <span data-ttu-id="28348-162"><a name="python"></a>Gebruik een programmeertaal zoals Python</span><span class="sxs-lookup"><span data-stu-id="28348-162"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="28348-163">Met behulp van Python tooexplore gegevens en het genereren van functies als Hallo gegevens in SQL Server is vergelijkbaar tooprocessing gegevens in Azure blob met behulp van Python, zoals beschreven in [proces Azure Blob-gegevens in uw omgeving van de wetenschappelijke gegevens](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="28348-163">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="28348-164">Hallo gegevens moet toobe uit Hallo-database in een pandas gegevensframe geladen en vervolgens verder kan worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="28348-164">hello data needs toobe loaded from hello database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="28348-165">We Documenteer Hallo proces van het verbinden van toohello database en het Hallo-gegevens in Hallo gegevensframe in deze sectie te laden.</span><span class="sxs-lookup"><span data-stu-id="28348-165">We document hello process of connecting toohello database and loading hello data into hello data frame in this section.</span></span>

<span data-ttu-id="28348-166">Hallo na indeling verbindingsreeks kan gebruikte tooconnect tooa SQL Server-database met Python met pyodbc (vervang servername, dbname, gebruikersnaam en wachtwoord op uw specifieke waarden) zijn:</span><span class="sxs-lookup"><span data-stu-id="28348-166">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="28348-167">Hallo [Pandas bibliotheek](http://pandas.pydata.org/) in Python voorziet in een uitgebreide set van gegevensstructuren en hulpprogramma's voor gegevensanalyse voor gegevensmanipulatie voor het programmeren van Python.</span><span class="sxs-lookup"><span data-stu-id="28348-167">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="28348-168">Hallo-code hieronder gelezen Hallo resultaten geretourneerd uit een SQL Server-database in een kader Pandas-gegevens:</span><span class="sxs-lookup"><span data-stu-id="28348-168">hello code below reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="28348-169">Nu u met de Hallo Pandas gegevensframe werken kunt zoals beschreven in artikel Hallo [proces Azure Blob-gegevens in uw omgeving van de wetenschappelijke gegevens](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="28348-169">Now you can work with hello Pandas data frame as covered in hello article [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="azure-data-science-in-action-example"></a><span data-ttu-id="28348-170">Azure Gegevenswetenschap in actie voorbeeld</span><span class="sxs-lookup"><span data-stu-id="28348-170">Azure Data Science in Action Example</span></span>
<span data-ttu-id="28348-171">Zie voor een voorbeeld van de end-to-end-overzicht van hello Azure gegevens wetenschappelijke processen met behulp van een openbare gegevensset, [Azure gegevens wetenschappelijke processen in actie](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="28348-171">For an end-to-end walkthrough example of hello Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

