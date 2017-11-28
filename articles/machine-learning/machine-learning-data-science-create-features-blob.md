---
title: Maken van de functies voor Azure blob storage-gegevens met behulp van Panda | Microsoft Docs
description: Het maken van de functies voor gegevens die zijn opgeslagen in Azure blob-container met het Panda Python-pakket.
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 676b5fb0-4c89-4516-b3a8-e78ae3ca078d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: 2ef2acfea2372ac7fd52d099a2b4203ee2242d81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a><span data-ttu-id="69fb2-103">Met Panda functies maken voor Azure Blok-opslaggegevens</span><span class="sxs-lookup"><span data-stu-id="69fb2-103">Create features for Azure blob storage data using Panda</span></span>
<span data-ttu-id="69fb2-104">Dit document wordt beschreven hoe maakt functies voor gegevens die zijn opgeslagen in Azure blob-container gebruiken de [Pandas](http://pandas.pydata.org/) Python-pakket.</span><span class="sxs-lookup"><span data-stu-id="69fb2-104">This document shows how to create features for data that is stored in Azure blob container using the [Pandas](http://pandas.pydata.org/) Python package.</span></span> <span data-ttu-id="69fb2-105">Na het waarin wordt beschreven hoe u de gegevens in een frame Panda-gegevens laden, er wordt weergegeven hoe categorische functies met indicatorwaarden Python-scripts en functies met binning genereren.</span><span class="sxs-lookup"><span data-stu-id="69fb2-105">After outlining how to load the data into a Panda data frame, it shows how to generate categorical features using Python scripts with indicator values and binning features.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="69fb2-106">Dit **menu** koppelingen naar onderwerpen waarin wordt beschreven hoe u functies voor gegevens in verschillende omgevingen maken.</span><span class="sxs-lookup"><span data-stu-id="69fb2-106">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="69fb2-107">Deze taak is een stap in de [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="69fb2-107">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69fb2-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="69fb2-108">Prerequisites</span></span>
<span data-ttu-id="69fb2-109">In dit artikel wordt ervan uitgegaan dat u een Azure blob storage-account hebt gemaakt en er in uw gegevens hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="69fb2-109">This article assumes that you have created an Azure blob storage account and have stored your data there.</span></span> <span data-ttu-id="69fb2-110">Als u instructies voor het instellen van een account nodig hebt, raadpleegt u [een Azure Storage-account maken](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="69fb2-110">If you need instructions to set up an account, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>

## <a name="load-the-data-into-a-pandas-data-frame"></a><span data-ttu-id="69fb2-111">De gegevens in een frame Pandas-gegevens laden</span><span class="sxs-lookup"><span data-stu-id="69fb2-111">Load the data into a Pandas data frame</span></span>
<span data-ttu-id="69fb2-112">Om te verkennen en manipuleren van een gegevensset, moet deze worden gedownload van de bron van de blob naar een lokaal bestand die vervolgens kan worden geladen in een Pandas gegevensframe.</span><span class="sxs-lookup"><span data-stu-id="69fb2-112">In order to do explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="69fb2-113">Hier volgen de stappen voor deze procedure:</span><span class="sxs-lookup"><span data-stu-id="69fb2-113">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="69fb2-114">Download de gegevens van Azure-blob met de volgende voorbeeldcode Python met behulp van blob-service.</span><span class="sxs-lookup"><span data-stu-id="69fb2-114">Download the data from Azure blob with the following sample Python code using blob service.</span></span> <span data-ttu-id="69fb2-115">De variabele in de volgende code vervangen door uw eigen specifieke waarden:</span><span class="sxs-lookup"><span data-stu-id="69fb2-115">Replace the variable in the code below with your specific values:</span></span>
   
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
2. <span data-ttu-id="69fb2-116">De gegevens in een Pandas gegevens tijdskader uit het gedownloade bestand gelezen.</span><span class="sxs-lookup"><span data-stu-id="69fb2-116">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="69fb2-117">U bent nu klaar voor de gegevens verkennen en het genereren van functies op deze dataset.</span><span class="sxs-lookup"><span data-stu-id="69fb2-117">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="69fb2-118"><a name="blob-featuregen"></a>Functie generatie</span><span class="sxs-lookup"><span data-stu-id="69fb2-118"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="69fb2-119">De volgende twee secties laten zien hoe categorische waarvan de indicatorwaarde en binning functies met behulp van Python-scripts genereren.</span><span class="sxs-lookup"><span data-stu-id="69fb2-119">The next two sections show how to generate categorical features with indicator values and binning features using Python scripts.</span></span>

### <span data-ttu-id="69fb2-120"><a name="blob-countfeature"></a>Indicatorwaarde op basis van functie generatie</span><span class="sxs-lookup"><span data-stu-id="69fb2-120"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="69fb2-121">Categorische functies kunnen als volgt worden gemaakt:</span><span class="sxs-lookup"><span data-stu-id="69fb2-121">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="69fb2-122">Inspecteer de distributie van de kolom categorische:</span><span class="sxs-lookup"><span data-stu-id="69fb2-122">Inspect the distribution of the categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="69fb2-123">Indicatorwaarden voor elk van de kolomwaarden genereren</span><span class="sxs-lookup"><span data-stu-id="69fb2-123">Generate indicator values for each of the column values</span></span>
   
        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="69fb2-124">Lid worden van de indicatorkolom met de oorspronkelijke gegevensframe</span><span class="sxs-lookup"><span data-stu-id="69fb2-124">Join the indicator column with the original data frame</span></span>
   
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="69fb2-125">De oorspronkelijke variabele zelf verwijderen:</span><span class="sxs-lookup"><span data-stu-id="69fb2-125">Remove the original variable itself:</span></span>
   
        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="69fb2-126"><a name="blob-binningfeature"></a>Met binning functie generatie</span><span class="sxs-lookup"><span data-stu-id="69fb2-126"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="69fb2-127">Voor het genereren van binned functies gaan we als volgt:</span><span class="sxs-lookup"><span data-stu-id="69fb2-127">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="69fb2-128">Een reeks van kolommen die u wilt een numerieke kolom bin toevoegen</span><span class="sxs-lookup"><span data-stu-id="69fb2-128">Add a sequence of columns to bin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="69fb2-129">Converteren naar een reeks Boole-variabelen met binning</span><span class="sxs-lookup"><span data-stu-id="69fb2-129">Convert binning to a sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="69fb2-130">Ten slotte de dummy variabelen Join terug naar de oorspronkelijke gegevensframe</span><span class="sxs-lookup"><span data-stu-id="69fb2-130">Finally, Join the dummy variables back to the original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <span data-ttu-id="69fb2-131"><a name="sql-featuregen"></a>Schrijven van gegevens terug naar Azure blob en gebruiken in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="69fb2-131"><a name="sql-featuregen"></a>Writing data back to Azure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="69fb2-132">Nadat u de gegevens hebt verkend en de benodigde onderdelen hebt gemaakt, kunt u de gegevens uploaden (actieve of featurized) naar een Azure blob- en deze wordt gebruikt in Azure Machine Learning met behulp van de volgende stappen uit: Houd er rekening mee dat extra functies kunnen worden gemaakt in de Azure-Machine Ook Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="69fb2-132">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span></span>

1. <span data-ttu-id="69fb2-133">Het gegevensframe schrijven naar een lokaal bestand</span><span class="sxs-lookup"><span data-stu-id="69fb2-133">Write the data frame to local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="69fb2-134">Uploaden van de gegevens naar Azure blob als volgt:</span><span class="sxs-lookup"><span data-stu-id="69fb2-134">Upload the data to Azure blob as follows:</span></span>
   
        from azure.storage.blob import BlobService
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
3. <span data-ttu-id="69fb2-135">Nu de gegevens kunnen worden gelezen vanaf de blob met de Azure Machine Learning [importgegevens](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module, zoals wordt weergegeven in het scherm hieronder:</span><span class="sxs-lookup"><span data-stu-id="69fb2-135">Now the data can be read from the blob using the Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module as shown in the screen below:</span></span>

![lezer blob](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

