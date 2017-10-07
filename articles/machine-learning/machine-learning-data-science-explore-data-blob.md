---
title: aaaExplore gegevens in Azure blob-opslag met Pandas | Microsoft Docs
description: Hoe tooexplore gegevens die zijn opgeslagen in Azure blob-container met behulp van Pandas.
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
ms.openlocfilehash: 28f3c0aebf2300006066c4b19dcb1f0a76a1deb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a><span data-ttu-id="e2dcb-103">Met Pandas gegevens verkennen in Azure Blok-opslag</span><span class="sxs-lookup"><span data-stu-id="e2dcb-103">Explore data in Azure blob storage with Pandas</span></span>
<span data-ttu-id="e2dcb-104">Dit document bevat informatie over hoe tooexplore gegevens die zijn opgeslagen in Azure blob-container met behulp van [Pandas](http://pandas.pydata.org/) Python-pakket.</span><span class="sxs-lookup"><span data-stu-id="e2dcb-104">This document covers how tooexplore data that is stored in Azure blob container using [Pandas](http://pandas.pydata.org/) Python package.</span></span>

<span data-ttu-id="e2dcb-105">Hallo volgende **menu** tootopics waarin wordt beschreven hoe toouse hulpprogramma's voor tooexplore gegevens uit verschillende omgevingen voor opslag is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="e2dcb-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="e2dcb-106">Deze taak is een stap in Hallo [gegevens wetenschap proces]().</span><span class="sxs-lookup"><span data-stu-id="e2dcb-106">This task is a step in hello [Data Science Process]().</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="e2dcb-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e2dcb-107">Prerequisites</span></span>
<span data-ttu-id="e2dcb-108">In dit artikel wordt ervan uitgegaan dat u hebt:</span><span class="sxs-lookup"><span data-stu-id="e2dcb-108">This article assumes that you have:</span></span>

* <span data-ttu-id="e2dcb-109">Een Azure storage-account gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e2dcb-109">Created an Azure storage account.</span></span> <span data-ttu-id="e2dcb-110">Als u instructies nodig hebt, raadpleegt u [een Azure Storage-account maken](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="e2dcb-110">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="e2dcb-111">Uw gegevens opgeslagen in een Azure blob storage-account.</span><span class="sxs-lookup"><span data-stu-id="e2dcb-111">Stored your data in an Azure blob storage account.</span></span> <span data-ttu-id="e2dcb-112">Als u instructies nodig hebt, raadpleegt u [Moving gegevens tooand uit Azure Storage](../storage/common/storage-moving-data.md)</span><span class="sxs-lookup"><span data-stu-id="e2dcb-112">If you need instructions, see [Moving data tooand from Azure Storage](../storage/common/storage-moving-data.md)</span></span>

## <a name="load-hello-data-into-a-pandas-dataframe"></a><span data-ttu-id="e2dcb-113">Hallo gegevens laden in een DataFrame Pandas</span><span class="sxs-lookup"><span data-stu-id="e2dcb-113">Load hello data into a Pandas DataFrame</span></span>
<span data-ttu-id="e2dcb-114">tooexplore en manipuleren van een gegevensset, moet eerst worden gedownload vanuit het Hallo blob bron tooa lokale bestand, die vervolgens kan worden geladen in een DataFrame Pandas.</span><span class="sxs-lookup"><span data-stu-id="e2dcb-114">tooexplore and manipulate a dataset, it must first be downloaded from hello blob source tooa local file, which can then be loaded in a Pandas DataFrame.</span></span> <span data-ttu-id="e2dcb-115">Hier volgen Hallo stappen toofollow voor deze procedure:</span><span class="sxs-lookup"><span data-stu-id="e2dcb-115">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="e2dcb-116">Hallo gegevens downloaden vanaf Azure blob met Hallo Python-codevoorbeeld met behulp van blob-service te volgen.</span><span class="sxs-lookup"><span data-stu-id="e2dcb-116">Download hello data from Azure blob with hello following Python code sample using blob service.</span></span> <span data-ttu-id="e2dcb-117">Hallo-variabele in Hallo na de code die uw specifieke waarden vervangt:</span><span class="sxs-lookup"><span data-stu-id="e2dcb-117">Replace hello variable in hello following code with your specific values:</span></span> 
   
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
        print(("It takes %s seconds toodownload "+blobname) % (t2 - t1))
2. <span data-ttu-id="e2dcb-118">Hallo-gegevens lezen in een Pandas gegevens tijdskader van Hallo gedownload bestand.</span><span class="sxs-lookup"><span data-stu-id="e2dcb-118">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="e2dcb-119">Nu u bent gereed tooexplore Hallo gegevens en genereren van de functies voor deze gegevensset.</span><span class="sxs-lookup"><span data-stu-id="e2dcb-119">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="e2dcb-120"><a name="blob-dataexploration"></a>Voorbeelden van gegevensverkenning met Pandas</span><span class="sxs-lookup"><span data-stu-id="e2dcb-120"><a name="blob-dataexploration"></a>Examples of data exploration using Pandas</span></span>
<span data-ttu-id="e2dcb-121">Hier volgen enkele voorbeelden van de manieren tooexplore-gegevens met behulp van Pandas:</span><span class="sxs-lookup"><span data-stu-id="e2dcb-121">Here are a few examples of ways tooexplore data using Pandas:</span></span>

1. <span data-ttu-id="e2dcb-122">Hallo inspecteren **aantal rijen en kolommen**</span><span class="sxs-lookup"><span data-stu-id="e2dcb-122">Inspect hello **number of rows and columns**</span></span> 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="e2dcb-123">**Inspecteer** eerste of laatste paar Hallo **rijen** in Hallo gegevensset te volgen:</span><span class="sxs-lookup"><span data-stu-id="e2dcb-123">**Inspect** hello first or last few **rows** in hello following dataset:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="e2dcb-124">Controleer de Hallo **gegevenstype** elke kolom is geïmporteerd als het gebruik van de volgende voorbeeldcode Hallo</span><span class="sxs-lookup"><span data-stu-id="e2dcb-124">Check hello **data type** each column was imported as using hello following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="e2dcb-125">Controleer de Hallo **elementaire statistieken** voor Hallo kolommen in gegevensset als volgt Hallo</span><span class="sxs-lookup"><span data-stu-id="e2dcb-125">Check hello **basic stats** for hello columns in hello data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="e2dcb-126">Bekijkt hello aantal items voor elke waarde in de kolom als volgt</span><span class="sxs-lookup"><span data-stu-id="e2dcb-126">Look at hello number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="e2dcb-127">**Ontbrekende waarden tellen** versus werkelijke aantal vermeldingen in elke kolom met de volgende voorbeeldcode Hallo Hallo</span><span class="sxs-lookup"><span data-stu-id="e2dcb-127">**Count missing values** versus hello actual number of entries in each column using hello following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="e2dcb-128">Als u hebt **ontbrekende waarden** voor een specifieke kolom in Hallo gegevens verwijderen ze als volgt:</span><span class="sxs-lookup"><span data-stu-id="e2dcb-128">If you have **missing values** for a specific column in hello data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="e2dcb-129">dataframe_blobdata_noNA dataframe_blobdata.dropna() dataframe_blobdata_noNA.shape =</span><span class="sxs-lookup"><span data-stu-id="e2dcb-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="e2dcb-130">Er is een andere manier tooreplace ontbrekende waarden met Hallo modusfunctie:</span><span class="sxs-lookup"><span data-stu-id="e2dcb-130">Another way tooreplace missing values is with hello mode function:</span></span>
   
     <span data-ttu-id="e2dcb-131">dataframe_blobdata_mode dataframe_blobdata.fillna = ({< column_name >: .mode()[0]}) dataframe_blobdata ['< column_name >"]</span><span class="sxs-lookup"><span data-stu-id="e2dcb-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="e2dcb-132">Maak een **histogram** getekend met een variabele aantal opslaglocaties tooplot Hallo distributie van een variabele</span><span class="sxs-lookup"><span data-stu-id="e2dcb-132">Create a **histogram** plot using variable number of bins tooplot hello distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="e2dcb-133">Bekijk **correlaties** tussen variabelen met een scatterplot of functie van de ingebouwde correlation Hallo</span><span class="sxs-lookup"><span data-stu-id="e2dcb-133">Look at **correlations** between variables using a scatterplot or using hello built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

