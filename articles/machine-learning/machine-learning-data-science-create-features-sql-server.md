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
# <a name="create-features-for-data-in-sql-server-using-sql-and-python"></a><span data-ttu-id="5f250-103">Met SQL en Python functies maken voor gegevens in SQL Server</span><span class="sxs-lookup"><span data-stu-id="5f250-103">Create features for data in SQL Server using SQL and Python</span></span>
<span data-ttu-id="5f250-104">Dit document ziet u hoe toogenerate functies voor opgeslagen gegevens in een SQL Server VM op Azure waarmee algoritmen efficiënter leren van Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="5f250-104">This document shows how toogenerate features for data stored in a SQL Server VM on Azure that help algorithms learn more efficiently from hello data.</span></span> <span data-ttu-id="5f250-105">Dit kan worden gedaan met behulp van SQL of met behulp van een programmeertaal zoals Python, die hier worden uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="5f250-105">This can be done by using SQL or by using a programming language like Python, both of which are demonstrated here.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="5f250-106">Dit **menu** koppelingen tootopics waarin wordt beschreven hoe toocreate functies voor gegevens in verschillende omgevingen.</span><span class="sxs-lookup"><span data-stu-id="5f250-106">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="5f250-107">Deze taak is een stap in Hallo [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="5f250-107">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

> [!NOTE]
> <span data-ttu-id="5f250-108">Voor een voorbeeld, kunt u raadplegen Hallo [NYC Taxi gegevensset](http://www.andresmh.com/nyctaxitrips/) Raadpleeg toohello IPNB met de titel en [IPython laptop- en SQL Server met de gegevens van de NYC worsteling](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) voor een end-to-end-procedure.</span><span class="sxs-lookup"><span data-stu-id="5f250-108">For a practical example, you can consult hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="5f250-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5f250-109">Prerequisites</span></span>
<span data-ttu-id="5f250-110">In dit artikel wordt ervan uitgegaan dat u hebt:</span><span class="sxs-lookup"><span data-stu-id="5f250-110">This article assumes that you have:</span></span>

* <span data-ttu-id="5f250-111">Een Azure storage-account gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f250-111">Created an Azure storage account.</span></span> <span data-ttu-id="5f250-112">Als u instructies nodig hebt, raadpleegt u [een Azure Storage-account maken](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="5f250-112">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="5f250-113">Uw gegevens opgeslagen in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5f250-113">Stored your data in SQL Server.</span></span> <span data-ttu-id="5f250-114">Als u niet hebt, raadpleegt u [verplaatsen van gegevens tooan Azure SQL Database voor Azure Machine Learning](machine-learning-data-science-move-sql-azure.md) voor instructies over hoe toomove Hallo er gegevens.</span><span class="sxs-lookup"><span data-stu-id="5f250-114">If you have not, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md) for instructions on how toomove hello data there.</span></span>

## <span data-ttu-id="5f250-115"><a name="sql-featuregen"></a>Functie genereren met behulp van SQL</span><span class="sxs-lookup"><span data-stu-id="5f250-115"><a name="sql-featuregen"></a>Feature Generation with SQL</span></span>
<span data-ttu-id="5f250-116">In deze sectie beschrijven we manieren voor het genereren van functies met behulp van SQL:</span><span class="sxs-lookup"><span data-stu-id="5f250-116">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="5f250-117">Aantal op basis van functie generatie</span><span class="sxs-lookup"><span data-stu-id="5f250-117">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="5f250-118">Met binning functie generatie</span><span class="sxs-lookup"><span data-stu-id="5f250-118">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="5f250-119">Hallo-functies rolt uit één kolom</span><span class="sxs-lookup"><span data-stu-id="5f250-119">Rolling out hello features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="5f250-120">Als u extra functies genereert, kunt u toe te voegen als kolommen toohello bestaande tabel of een nieuwe tabel maken met de Hallo extra functies en primaire sleutel, die kan worden samengevoegd met de oorspronkelijke tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f250-120">Once you generate additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, that can be joined with hello original table.</span></span>
> 
> 

### <span data-ttu-id="5f250-121"><a name="sql-countfeature"></a>Aantal op basis van functie generatie</span><span class="sxs-lookup"><span data-stu-id="5f250-121"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="5f250-122">Dit document wordt gedemonstreerd op twee manieren voor het genereren van het aantal functies.</span><span class="sxs-lookup"><span data-stu-id="5f250-122">This document demonstrates two ways of generating count features.</span></span> <span data-ttu-id="5f250-123">Hallo eerste methode Voorwaardelijke som gebruikt en de tweede methode gebruikt Hallo Hallo 'where-clausule.</span><span class="sxs-lookup"><span data-stu-id="5f250-123">hello first method uses conditional sum and hello second method uses hello 'where\` clause.</span></span> <span data-ttu-id="5f250-124">Deze kunnen vervolgens worden samengevoegd met de Hallo oorspronkelijke (met behulp van de primaire-sleutelkolommen) toohave aantal tabelfuncties naast Hallo oorspronkelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="5f250-124">These can then be joined with hello original table (using primary key columns) toohave count features alongside hello original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3>

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename>
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2>

### <span data-ttu-id="5f250-125"><a name="sql-binningfeature"></a>Met binning functie generatie</span><span class="sxs-lookup"><span data-stu-id="5f250-125"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="5f250-126">Hallo volgende voorbeeld laat zien hoe toogenerate binned functies met binning (met behulp van 5 opslaglocaties) een numerieke kolom die kan worden gebruikt als een functie in plaats daarvan:</span><span class="sxs-lookup"><span data-stu-id="5f250-126">hello following example shows how toogenerate binned features by binning (using 5 bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="5f250-127"><a name="sql-featurerollout"></a>Hallo-functies rolt uit één kolom</span><span class="sxs-lookup"><span data-stu-id="5f250-127"><a name="sql-featurerollout"></a>Rolling out hello features from a single column</span></span>
<span data-ttu-id="5f250-128">In deze sectie ziet u hoe tooroll-out één kolom in een tabel toogenerate extra onderdelen.</span><span class="sxs-lookup"><span data-stu-id="5f250-128">In this section, we demonstrate how tooroll-out a single column in a table toogenerate additional features.</span></span> <span data-ttu-id="5f250-129">Hallo-voorbeeld wordt ervan uitgegaan dat er een kolom breedtegraad of lengtegraad in Hallo tabel waaruit u toogenerate functies probeert.</span><span class="sxs-lookup"><span data-stu-id="5f250-129">hello example assumes that there is a latitude or longitude column in hello table from which you are trying toogenerate features.</span></span>

<span data-ttu-id="5f250-130">Hier volgt een korte primer op breedtegraad/lengtegraad locatiegegevens (resources voorzien van stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span><span class="sxs-lookup"><span data-stu-id="5f250-130">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span></span> <span data-ttu-id="5f250-131">Dit is nuttig toounderstand voordat featurizing Hallo locatieveld:</span><span class="sxs-lookup"><span data-stu-id="5f250-131">This is useful toounderstand before featurizing hello location field:</span></span>

* <span data-ttu-id="5f250-132">Hallo aanmelding weten ons of er zijn ten noorden of Zuid, Oost of west op Hallo wereld.</span><span class="sxs-lookup"><span data-stu-id="5f250-132">hello sign tells us whether we are north or south, east or west on hello globe.</span></span>
* <span data-ttu-id="5f250-133">Een andere waarde dan nul honderden cijfer vertellen we maken gebruik van WL, niet NB!</span><span class="sxs-lookup"><span data-stu-id="5f250-133">A nonzero hundreds digit tells us we're using longitude, not latitude!</span></span>
* <span data-ttu-id="5f250-134">Hallo tientallen cijfer biedt een tooabout positie 1000 kilometers.</span><span class="sxs-lookup"><span data-stu-id="5f250-134">hello tens digit gives a position tooabout 1,000 kilometers.</span></span> <span data-ttu-id="5f250-135">Dit biedt ons nuttige informatie over welke continent of Oceaan we worden op.</span><span class="sxs-lookup"><span data-stu-id="5f250-135">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="5f250-136">Hallo eenheden cijfer (één decimale graad) biedt een positie omhoog too111 kilometers (60 zeemijl, ongeveer 69 mijl).</span><span class="sxs-lookup"><span data-stu-id="5f250-136">hello units digit (one decimal degree) gives a position up too111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="5f250-137">Deze kunt ons ongeveer welke grote rechtsgebied die we in zijn.</span><span class="sxs-lookup"><span data-stu-id="5f250-137">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="5f250-138">de eerste decimaal Hallo too11.1 km is waard: het Hallo-positie van een grote plaats van een aangrenzende grote stad kunt onderscheiden.</span><span class="sxs-lookup"><span data-stu-id="5f250-138">hello first decimal place is worth up too11.1 km: it can distinguish hello position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="5f250-139">de tweede decimaal Hallo too1.1 km is waard: het kunt één village scheiden van Hallo naast.</span><span class="sxs-lookup"><span data-stu-id="5f250-139">hello second decimal place is worth up too1.1 km: it can separate one village from hello next.</span></span>
* <span data-ttu-id="5f250-140">de derde decimaal Hallo is waard too110 m: dat deze grote de veld of institutionele bereik kunt identificeren.</span><span class="sxs-lookup"><span data-stu-id="5f250-140">hello third decimal place is worth up too110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="5f250-141">de vierde decimaal Hallo is waard too11 m: dat deze een pakket van de grond kunt identificeren.</span><span class="sxs-lookup"><span data-stu-id="5f250-141">hello fourth decimal place is worth up too11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="5f250-142">Het is gemiddelde nauwkeurigheid van een niet-gecorrigeerde GPS-eenheid zonder storing vergelijkbare toohello.</span><span class="sxs-lookup"><span data-stu-id="5f250-142">It is comparable toohello typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="5f250-143">Hallo vijfde decimaal is waard too1.1 m: deze structuren van elkaar te onderscheiden.</span><span class="sxs-lookup"><span data-stu-id="5f250-143">hello fifth decimal place is worth up too1.1 m: it distinguish trees from each other.</span></span> <span data-ttu-id="5f250-144">Nauwkeurigheid toothis niveau met commerciële GPS-eenheden kan alleen worden verkregen met differentiële gecorrigeerd.</span><span class="sxs-lookup"><span data-stu-id="5f250-144">Accuracy toothis level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="5f250-145">Hallo zesde decimaal is waard too0.11 m: die u deze gebruiken kunt voor het indelen van structuren met details voor het ontwerpen van landschappen, wegen bouwen.</span><span class="sxs-lookup"><span data-stu-id="5f250-145">hello sixth decimal place is worth up too0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="5f250-146">Moet meer dan goed genoeg voor het bijhouden van verkeer van glaciers en rivieren zijn.</span><span class="sxs-lookup"><span data-stu-id="5f250-146">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="5f250-147">Dit kan worden bereikt door middel van hele maatregelen met GPS zoals differentially gecorrigeerde GPS.</span><span class="sxs-lookup"><span data-stu-id="5f250-147">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="5f250-148">Hallo locatiegegevens kunt mag featurized als volgt scheiden van de regio, locatie en plaats.</span><span class="sxs-lookup"><span data-stu-id="5f250-148">hello location information can can be featurized as follows, separating out region, location and city information.</span></span> <span data-ttu-id="5f250-149">Let op: één keer kunt ook aanroepen een REST-eindpunt zoals Bing kaarten-API beschikbaar op `https://msdn.microsoft.com/library/ff701710.aspx` tooget Hallo regio/regionale informatie.</span><span class="sxs-lookup"><span data-stu-id="5f250-149">Note that once can also call a REST end point such as Bing Maps API available at `https://msdn.microsoft.com/library/ff701710.aspx` tooget hello region/district information.</span></span>

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

<span data-ttu-id="5f250-150">Hallo bovenstaande locatie op basis van de functies verder kunnen worden gebruikt toogenerate aantal aanvullende functies, zoals eerder beschreven.</span><span class="sxs-lookup"><span data-stu-id="5f250-150">hello above location based features can be further used toogenerate additional count features as described earlier.</span></span>

> [!TIP]
> <span data-ttu-id="5f250-151">U kunt programmatisch Hallo registreert met behulp van de taal van keuze invoegen.</span><span class="sxs-lookup"><span data-stu-id="5f250-151">You can programmatically insert hello records using your language of choice.</span></span> <span data-ttu-id="5f250-152">Mogelijk moet u tooinsert Hallo gegevens in reeksen tooimprove schrijven efficiëntie [uitchecken Hallo voorbeeld van hoe u toodo deze met pyodbc hier](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span><span class="sxs-lookup"><span data-stu-id="5f250-152">You may need tooinsert hello data in chunks tooimprove write efficiency [Check out hello example of how toodo this using pyodbc here](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span></span>
> <span data-ttu-id="5f250-153">Een ander alternatief is tooinsert gegevens in het Hallo-database met [hulpprogramma BCP](https://msdn.microsoft.com/library/ms162802.aspx)</span><span class="sxs-lookup"><span data-stu-id="5f250-153">Another alternative is tooinsert data in hello database using [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx)</span></span>
> 
> 

### <span data-ttu-id="5f250-154"><a name="sql-aml"></a>Verbinding maken met tooAzure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5f250-154"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="5f250-155">Hallo zojuist gegenereerde functie worden toegevoegd als een bestaande tabel met kolom tooan of opgeslagen in een nieuwe tabel en samengevoegd met de oorspronkelijke tabel Hallo voor machine learning.</span><span class="sxs-lookup"><span data-stu-id="5f250-155">hello newly generated feature can be added as a column tooan existing table or stored in a new table and joined with hello original table for machine learning.</span></span> <span data-ttu-id="5f250-156">Functies kunnen worden gegenereerd of toegankelijk is als al hebt gemaakt, met Hallo [importgegevens](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) -module in de Azure ML zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5f250-156">Features can be generated or accessed if already created, using hello [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module in Azure ML as shown below:</span></span>

![azureml lezers](./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png)

## <span data-ttu-id="5f250-158"><a name="python"></a>Gebruik een programmeertaal zoals Python</span><span class="sxs-lookup"><span data-stu-id="5f250-158"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="5f250-159">Soortgelijke tooprocessing gegevens met behulp van Python toogenerate functies wanneer Hallo gegevens in SQL Server is in Azure blob met behulp van Python, zoals beschreven in [proces Azure Blob-gegevens in u gegevens wetenschappelijke omgeving](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="5f250-159">Using Python toogenerate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python as documented in [Process Azure Blob data in you data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="5f250-160">Hallo gegevens moet toobe uit Hallo-database in een pandas gegevensframe geladen en vervolgens verder kan worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="5f250-160">hello data needs toobe loaded from hello database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="5f250-161">We Documenteer Hallo proces van het verbinden van toohello database en het Hallo-gegevens in Hallo gegevensframe in deze sectie te laden.</span><span class="sxs-lookup"><span data-stu-id="5f250-161">We document hello process of connecting toohello database and loading hello data into hello data frame in this section.</span></span>

<span data-ttu-id="5f250-162">Hallo na indeling verbindingsreeks kan gebruikte tooconnect tooa SQL Server-database met Python met pyodbc (vervang servername, dbname, gebruikersnaam en wachtwoord met uw specifieke waarden) zijn:</span><span class="sxs-lookup"><span data-stu-id="5f250-162">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="5f250-163">Hallo [Pandas bibliotheek](http://pandas.pydata.org/) in Python voorziet in een uitgebreide set van gegevensstructuren en hulpprogramma's voor gegevensanalyse voor gegevensmanipulatie voor het programmeren van Python.</span><span class="sxs-lookup"><span data-stu-id="5f250-163">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="5f250-164">Hallo-code hieronder gelezen Hallo resultaten geretourneerd uit een SQL Server-database in een kader Pandas-gegevens:</span><span class="sxs-lookup"><span data-stu-id="5f250-164">hello code below reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="5f250-165">Nu u met de Hallo Pandas gegevensframe werken kunt zoals beschreven in de onderwerpen [maken van de functies voor Azure blob storage-gegevens met behulp van Panda](machine-learning-data-science-create-features-blob.md).</span><span class="sxs-lookup"><span data-stu-id="5f250-165">Now you can work with hello Pandas data frame as covered in topics [Create features for Azure blob storage data using Panda](machine-learning-data-science-create-features-blob.md).</span></span>

