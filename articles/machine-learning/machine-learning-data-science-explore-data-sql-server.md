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
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a><span data-ttu-id="99ffc-103">Gegevens in virtuele SQL Server-machine verkennen in Azure</span><span class="sxs-lookup"><span data-stu-id="99ffc-103">Explore data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="99ffc-104">Dit document bevat informatie over hoe tooexplore gegevens die zijn opgeslagen in een virtuele SQL Server-machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="99ffc-104">This document covers how tooexplore data that is stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="99ffc-105">Dit kan worden gedaan door gegevens worsteling met SQL of via een programmeertaal zoals Python.</span><span class="sxs-lookup"><span data-stu-id="99ffc-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

<span data-ttu-id="99ffc-106">Hallo volgende **menu** tootopics waarin wordt beschreven hoe toouse hulpprogramma's voor tooexplore gegevens uit verschillende omgevingen voor opslag is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="99ffc-106">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="99ffc-107">Deze taak is een stap in Hallo Cortana Analytics proces (CAP).</span><span class="sxs-lookup"><span data-stu-id="99ffc-107">This task is a step in hello Cortana Analytics Process (CAP).</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> <span data-ttu-id="99ffc-108">Hallo voorbeeld SQL-instructies in dit document wordt ervan uitgegaan dat gegevens in SQL Server worden.</span><span class="sxs-lookup"><span data-stu-id="99ffc-108">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="99ffc-109">Dit niet het geval is, raadpleegt u toohello cloud gegevens wetenschap proces kaart toolearn hoe toomove uw gegevens tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="99ffc-109">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="99ffc-110"><a name="sql-dataexploration"></a>SQL-gegevens met SQL-scripts verkennen</span><span class="sxs-lookup"><span data-stu-id="99ffc-110"><a name="sql-dataexploration"></a>Explore SQL data with SQL scripts</span></span>
<span data-ttu-id="99ffc-111">Hier volgen enkele voorbeelden SQL-scripts die gebruikt tooexplore gegevensarchieven SQL Server worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="99ffc-111">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

1. <span data-ttu-id="99ffc-112">Hallo-telling van metingen per dag</span><span class="sxs-lookup"><span data-stu-id="99ffc-112">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="99ffc-113">Hallo niveaus in een categorische kolom ophalen</span><span class="sxs-lookup"><span data-stu-id="99ffc-113">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="99ffc-114">Hallo aantal niveaus in de combinatie van twee categorische kolommen ophalen</span><span class="sxs-lookup"><span data-stu-id="99ffc-114">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="99ffc-115">Hallo-distributie voor numerieke kolommen ophalen</span><span class="sxs-lookup"><span data-stu-id="99ffc-115">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> <span data-ttu-id="99ffc-116">Voor een voorbeeld, kunt u Hallo [NYC Taxi gegevensset](http://www.andresmh.com/nyctaxitrips/) Raadpleeg toohello IPNB met de titel en [IPython laptop- en SQL Server met de gegevens van de NYC worsteling](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) voor een end-to-end-procedure.</span><span class="sxs-lookup"><span data-stu-id="99ffc-116">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <span data-ttu-id="99ffc-117"><a name="python"></a>SQL-gegevens met behulp van Python verkennen</span><span class="sxs-lookup"><span data-stu-id="99ffc-117"><a name="python"></a>Explore SQL data with Python</span></span>
<span data-ttu-id="99ffc-118">Met behulp van Python tooexplore gegevens en het genereren van functies als Hallo gegevens in SQL Server is vergelijkbaar tooprocessing gegevens in Azure blob met behulp van Python, zoals beschreven in [proces Azure Blob-gegevens in uw omgeving van de wetenschappelijke gegevens](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="99ffc-118">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="99ffc-119">Hallo gegevens moet toobe uit Hallo-database in een pandas DataFrame geladen en vervolgens verder kan worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="99ffc-119">hello data needs toobe loaded from hello database into a pandas DataFrame and then can be processed further.</span></span> <span data-ttu-id="99ffc-120">We Documenteer Hallo proces van het verbinden van toohello database en het Hallo-gegevens in Hallo DataFrame in deze sectie te laden.</span><span class="sxs-lookup"><span data-stu-id="99ffc-120">We document hello process of connecting toohello database and loading hello data into hello DataFrame in this section.</span></span>

<span data-ttu-id="99ffc-121">Hallo na indeling verbindingsreeks kan gebruikte tooconnect tooa SQL Server-database met Python met pyodbc (vervang servername, dbname, gebruikersnaam en wachtwoord op uw specifieke waarden) zijn:</span><span class="sxs-lookup"><span data-stu-id="99ffc-121">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="99ffc-122">Hallo [Pandas bibliotheek](http://pandas.pydata.org/) in Python voorziet in een uitgebreide set van gegevensstructuren en hulpprogramma's voor gegevensanalyse voor gegevensmanipulatie voor het programmeren van Python.</span><span class="sxs-lookup"><span data-stu-id="99ffc-122">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="99ffc-123">Hallo leest volgende code Hallo resultaten geretourneerd uit een SQL Server-database in een kader Pandas-gegevens:</span><span class="sxs-lookup"><span data-stu-id="99ffc-123">hello following code reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="99ffc-124">Nu u met de Hallo Pandas DataFrame werken kunt zoals besproken in Hallo onderwerp [proces Azure Blob-gegevens in uw omgeving van de wetenschappelijke gegevens](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="99ffc-124">Now you can work with hello Pandas DataFrame as covered in hello topic [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="cortana-analytics-process-in-action-example"></a><span data-ttu-id="99ffc-125">Cortana-Analytics-proces in de actie voorbeeld</span><span class="sxs-lookup"><span data-stu-id="99ffc-125">Cortana Analytics Process in Action Example</span></span>
<span data-ttu-id="99ffc-126">Zie voor een voorbeeld van de end-to-end-overzicht van Hallo Cortana-Analytics proces met behulp van een openbare gegevensset, [Hallo Team gegevens wetenschappelijke processen in actie: met behulp van SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="99ffc-126">For an end-to-end walkthrough example of hello Cortana Analytics Process using a public dataset, see [hello Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

