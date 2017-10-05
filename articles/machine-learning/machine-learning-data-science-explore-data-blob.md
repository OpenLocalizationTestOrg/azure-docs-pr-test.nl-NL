---
title: Gegevens in Azure blob storage met Pandas | Microsoft Docs
description: Hoe gegevens die zijn opgeslagen in Azure blob-container met Pandas verkennen.
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: feaa9e54-01e0-48c8-a917-1eba0f9d9ec7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: e1b33b17270122a38228484a56c8324c5b4505a0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a><span data-ttu-id="4796f-103">Met Pandas gegevens verkennen in Azure Blok-opslag</span><span class="sxs-lookup"><span data-stu-id="4796f-103">Explore data in Azure blob storage with Pandas</span></span>
<span data-ttu-id="4796f-104">Dit document wordt beschreven hoe gegevens die zijn opgeslagen in het gebruik van Azure blob-container verkennen [Pandas](http://pandas.pydata.org/) Python-pakket.</span><span class="sxs-lookup"><span data-stu-id="4796f-104">This document covers how to explore data that is stored in Azure blob container using [Pandas](http://pandas.pydata.org/) Python package.</span></span>

<span data-ttu-id="4796f-105">De volgende **menu** koppelingen naar onderwerpen waarin wordt beschreven hoe u gegevens uit verschillende omgevingen met opslag verkennen met behulp van hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="4796f-105">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span> <span data-ttu-id="4796f-106">Deze taak is een stap in de [gegevens wetenschap proces]().</span><span class="sxs-lookup"><span data-stu-id="4796f-106">This task is a step in the [Data Science Process]().</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="4796f-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4796f-107">Prerequisites</span></span>
<span data-ttu-id="4796f-108">In dit artikel wordt ervan uitgegaan dat u hebt:</span><span class="sxs-lookup"><span data-stu-id="4796f-108">This article assumes that you have:</span></span>

* <span data-ttu-id="4796f-109">Een Azure storage-account gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4796f-109">Created an Azure storage account.</span></span> <span data-ttu-id="4796f-110">Als u instructies nodig hebt, raadpleegt u [een Azure Storage-account maken](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="4796f-110">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="4796f-111">Uw gegevens opgeslagen in een Azure blob storage-account.</span><span class="sxs-lookup"><span data-stu-id="4796f-111">Stored your data in an Azure blob storage account.</span></span> <span data-ttu-id="4796f-112">Als u instructies nodig hebt, raadpleegt u [verplaatsen van gegevens naar en van Azure Storage](../storage/common/storage-moving-data.md)</span><span class="sxs-lookup"><span data-stu-id="4796f-112">If you need instructions, see [Moving data to and from Azure Storage](../storage/common/storage-moving-data.md)</span></span>

## <a name="load-the-data-into-a-pandas-dataframe"></a><span data-ttu-id="4796f-113">De gegevens in een DataFrame Pandas laden</span><span class="sxs-lookup"><span data-stu-id="4796f-113">Load the data into a Pandas DataFrame</span></span>
<span data-ttu-id="4796f-114">Om te verkennen en het bewerken van een gegevensset, moet deze eerst worden gedownload van de bron van de blob naar een lokaal bestand, die vervolgens kan worden geladen in een DataFrame Pandas.</span><span class="sxs-lookup"><span data-stu-id="4796f-114">To explore and manipulate a dataset, it must first be downloaded from the blob source to a local file, which can then be loaded in a Pandas DataFrame.</span></span> <span data-ttu-id="4796f-115">Hier volgen de stappen voor deze procedure:</span><span class="sxs-lookup"><span data-stu-id="4796f-115">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="4796f-116">Download de gegevens van Azure-blob met de volgende Python-codevoorbeeld met behulp van blob-service.</span><span class="sxs-lookup"><span data-stu-id="4796f-116">Download the data from Azure blob with the following Python code sample using blob service.</span></span> <span data-ttu-id="4796f-117">De variabele in de volgende code vervangen door uw eigen specifieke waarden:</span><span class="sxs-lookup"><span data-stu-id="4796f-117">Replace the variable in the following code with your specific values:</span></span> 
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        LOCALFILENAME= <local_file_name>        
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        #download from blob
        t1=time.time()
        blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
        blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILENAME)
        t2=time.time()
        print(("It takes %s seconds to download "+blobname) % (t2 - t1))
2. <span data-ttu-id="4796f-118">De gegevens in een Pandas gegevens tijdskader uit het gedownloade bestand gelezen.</span><span class="sxs-lookup"><span data-stu-id="4796f-118">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="4796f-119">U bent nu klaar voor de gegevens verkennen en het genereren van functies op deze dataset.</span><span class="sxs-lookup"><span data-stu-id="4796f-119">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="4796f-120"><a name="blob-dataexploration"></a>Voorbeelden van gegevensverkenning met Pandas</span><span class="sxs-lookup"><span data-stu-id="4796f-120"><a name="blob-dataexploration"></a>Examples of data exploration using Pandas</span></span>
<span data-ttu-id="4796f-121">Hier volgen enkele voorbeelden van methoden voor het verkennen van gegevens met behulp van Pandas:</span><span class="sxs-lookup"><span data-stu-id="4796f-121">Here are a few examples of ways to explore data using Pandas:</span></span>

1. <span data-ttu-id="4796f-122">Inspecteer de **aantal rijen en kolommen**</span><span class="sxs-lookup"><span data-stu-id="4796f-122">Inspect the **number of rows and columns**</span></span> 
   
        print 'the size of the data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="4796f-123">**Inspecteer** enkele van de eerste of laatste **rijen** in de volgende gegevensset:</span><span class="sxs-lookup"><span data-stu-id="4796f-123">**Inspect** the first or last few **rows** in the following dataset:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="4796f-124">Controleer de **gegevenstype** elke kolom is geïmporteerd als het gebruik van de volgende voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="4796f-124">Check the **data type** each column was imported as using the following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="4796f-125">Controleer de **elementaire statistieken** voor de kolommen in de gegevens als volgt instellen</span><span class="sxs-lookup"><span data-stu-id="4796f-125">Check the **basic stats** for the columns in the data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="4796f-126">Het aantal items voor elke waarde in de kolom als volgt bekijken</span><span class="sxs-lookup"><span data-stu-id="4796f-126">Look at the number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="4796f-127">**Ontbrekende waarden tellen** ten opzichte van het werkelijke aantal vermeldingen in elke kolom met de volgende voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="4796f-127">**Count missing values** versus the actual number of entries in each column using the following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="4796f-128">Als u hebt **ontbrekende waarden** voor een specifieke kolom in de gegevens verwijderen ze als volgt:</span><span class="sxs-lookup"><span data-stu-id="4796f-128">If you have **missing values** for a specific column in the data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="4796f-129">dataframe_blobdata_noNA dataframe_blobdata.dropna() dataframe_blobdata_noNA.shape =</span><span class="sxs-lookup"><span data-stu-id="4796f-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="4796f-130">Ontbrekende waarden te vervangen op een andere manier is met de modusfunctie:</span><span class="sxs-lookup"><span data-stu-id="4796f-130">Another way to replace missing values is with the mode function:</span></span>
   
     <span data-ttu-id="4796f-131">dataframe_blobdata_mode dataframe_blobdata.fillna = ({< column_name >: .mode()[0]}) dataframe_blobdata ['< column_name >"]</span><span class="sxs-lookup"><span data-stu-id="4796f-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="4796f-132">Maak een **histogram** getekend met een variabele aantal opslaglocaties uitzetten van de distributie van een variabele</span><span class="sxs-lookup"><span data-stu-id="4796f-132">Create a **histogram** plot using variable number of bins to plot the distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="4796f-133">Bekijk **correlaties** tussen variabelen met behulp van een scatterplot of via de ingebouwde correlatiefunctie</span><span class="sxs-lookup"><span data-stu-id="4796f-133">Look at **correlations** between variables using a scatterplot or using the built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

