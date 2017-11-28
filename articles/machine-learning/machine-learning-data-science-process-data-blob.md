---
title: aaaProcess Azure blob-gegevens met geavanceerde analyses | Microsoft Docs
description: Procesgegevens in Azure Blob-opslag.
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8a59078-91d3-4440-b85c-430363c3f4d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5911d4211c4135680555a8cdd99e745499a24215
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="c6d39-103"><a name="heading"></a>Azure blob-gegevens met geavanceerde analyses verwerken</span><span class="sxs-lookup"><span data-stu-id="c6d39-103"><a name="heading"></a>Process Azure blob data with advanced analytics</span></span>
<span data-ttu-id="c6d39-104">Dit document bevat informatie over gegevens verkennen en genereren van de functies van de gegevens die zijn opgeslagen in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="c6d39-104">This document covers exploring data and generating features from data stored in Azure Blob storage.</span></span> 

## <a name="load-hello-data-into-a-pandas-data-frame"></a><span data-ttu-id="c6d39-105">Hallo gegevens laden in een frame Pandas-gegevens</span><span class="sxs-lookup"><span data-stu-id="c6d39-105">Load hello data into a Pandas data frame</span></span>
<span data-ttu-id="c6d39-106">In de volgorde tooexplore en manipuleren van een gegevensset, deze moet worden gedownload uit Hallo blob tooa lokale bronbestand die vervolgens kan worden geladen in een Pandas gegevensframe.</span><span class="sxs-lookup"><span data-stu-id="c6d39-106">In order tooexplore and manipulate a dataset, it must be downloaded from hello blob source tooa local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="c6d39-107">Hier volgen Hallo stappen toofollow voor deze procedure:</span><span class="sxs-lookup"><span data-stu-id="c6d39-107">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="c6d39-108">Hallo gegevens downloaden vanaf Azure blob met Hallo Python voorbeeldcode met behulp van blob-service te volgen.</span><span class="sxs-lookup"><span data-stu-id="c6d39-108">Download hello data from Azure blob with hello following sample Python code using blob service.</span></span> <span data-ttu-id="c6d39-109">Hallo-variabele in het Hallo-code hieronder vervangen door uw eigen specifieke waarden:</span><span class="sxs-lookup"><span data-stu-id="c6d39-109">Replace hello variable in hello code below with your specific values:</span></span> 
   
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
2. <span data-ttu-id="c6d39-110">Hallo-gegevens lezen in een Pandas gegevens tijdskader van Hallo gedownload bestand.</span><span class="sxs-lookup"><span data-stu-id="c6d39-110">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="c6d39-111">Nu u bent gereed tooexplore Hallo gegevens en genereren van de functies voor deze gegevensset.</span><span class="sxs-lookup"><span data-stu-id="c6d39-111">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="c6d39-112"><a name="blob-dataexploration"></a>Gegevensverkenning</span><span class="sxs-lookup"><span data-stu-id="c6d39-112"><a name="blob-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="c6d39-113">Hier volgen enkele voorbeelden van de manieren tooexplore-gegevens met behulp van Pandas:</span><span class="sxs-lookup"><span data-stu-id="c6d39-113">Here are a few examples of ways tooexplore data using Pandas:</span></span>

1. <span data-ttu-id="c6d39-114">Hallo aantal rijen en kolommen controleren</span><span class="sxs-lookup"><span data-stu-id="c6d39-114">Inspect hello number of rows and columns</span></span> 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="c6d39-115">Hallo eerst controleren of de laatste paar rijen in dataset Hallo zoals hieronder:</span><span class="sxs-lookup"><span data-stu-id="c6d39-115">Inspect hello first or last few rows in hello dataset as below:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="c6d39-116">Hallo-gegevenstype die elke kolom is geïmporteerd als het gebruik van de volgende voorbeeldcode Hallo controleren</span><span class="sxs-lookup"><span data-stu-id="c6d39-116">Check hello data type each column was imported as using hello following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="c6d39-117">Hallo elementaire statistieken voor kolommen in gegevensset Hallo Hallo als volgt controleren</span><span class="sxs-lookup"><span data-stu-id="c6d39-117">Check hello basic stats for hello columns in hello data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="c6d39-118">Bekijkt hello aantal items voor elke waarde in de kolom als volgt</span><span class="sxs-lookup"><span data-stu-id="c6d39-118">Look at hello number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="c6d39-119">Ontbrekende waarden versus werkelijke aantal vermeldingen in elke kolom met de volgende voorbeeldcode Hallo Hallo tellen</span><span class="sxs-lookup"><span data-stu-id="c6d39-119">Count missing values versus hello actual number of entries in each column using hello following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="c6d39-120">Als u ontbrekende waarden voor een specifieke kolom in Hallo gegevens hebt, kunt u ze als volgt verwijderen:</span><span class="sxs-lookup"><span data-stu-id="c6d39-120">If you have missing values for a specific column in hello data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="c6d39-121">dataframe_blobdata_noNA dataframe_blobdata.dropna() dataframe_blobdata_noNA.shape =</span><span class="sxs-lookup"><span data-stu-id="c6d39-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="c6d39-122">Er is een andere manier tooreplace ontbrekende waarden met Hallo modusfunctie:</span><span class="sxs-lookup"><span data-stu-id="c6d39-122">Another way tooreplace missing values is with hello mode function:</span></span>
   
     <span data-ttu-id="c6d39-123">dataframe_blobdata_mode dataframe_blobdata.fillna = ({< column_name >: .mode()[0]}) dataframe_blobdata ['< column_name >"]</span><span class="sxs-lookup"><span data-stu-id="c6d39-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="c6d39-124">Histogram tekent met variabele aantal opslaglocaties tooplot Hallo distributie van een variabele maken</span><span class="sxs-lookup"><span data-stu-id="c6d39-124">Create a histogram plot using variable number of bins tooplot hello distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="c6d39-125">Bekijk correlatie tussen variabelen met een scatterplot of functie van de ingebouwde correlation Hallo</span><span class="sxs-lookup"><span data-stu-id="c6d39-125">Look at correlations between variables using a scatterplot or using hello built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <span data-ttu-id="c6d39-126"><a name="blob-featuregen"></a>Functie generatie</span><span class="sxs-lookup"><span data-stu-id="c6d39-126"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="c6d39-127">Functies met behulp van Python als volgt kan worden gegenereerd:</span><span class="sxs-lookup"><span data-stu-id="c6d39-127">We can generate features using Python as follows:</span></span>

### <span data-ttu-id="c6d39-128"><a name="blob-countfeature"></a>Indicatorwaarde op basis van functie generatie</span><span class="sxs-lookup"><span data-stu-id="c6d39-128"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="c6d39-129">Categorische functies kunnen als volgt worden gemaakt:</span><span class="sxs-lookup"><span data-stu-id="c6d39-129">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="c6d39-130">Hallo-verdeling van Hallo categorische kolom controleren:</span><span class="sxs-lookup"><span data-stu-id="c6d39-130">Inspect hello distribution of hello categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="c6d39-131">Indicatorwaarden voor elk van de kolomwaarden Hallo genereren</span><span class="sxs-lookup"><span data-stu-id="c6d39-131">Generate indicator values for each of hello column values</span></span>
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="c6d39-132">Hallo indicatorkolom met de oorspronkelijke gegevensframe Hallo koppelen</span><span class="sxs-lookup"><span data-stu-id="c6d39-132">Join hello indicator column with hello original data frame</span></span> 
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="c6d39-133">Hallo oorspronkelijke variabele zelf verwijderen:</span><span class="sxs-lookup"><span data-stu-id="c6d39-133">Remove hello original variable itself:</span></span>
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="c6d39-134"><a name="blob-binningfeature"></a>Met binning functie generatie</span><span class="sxs-lookup"><span data-stu-id="c6d39-134"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="c6d39-135">Voor het genereren van binned functies gaan we als volgt:</span><span class="sxs-lookup"><span data-stu-id="c6d39-135">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="c6d39-136">Een reeks van kolommen toobin een numerieke kolom toevoegen</span><span class="sxs-lookup"><span data-stu-id="c6d39-136">Add a sequence of columns toobin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="c6d39-137">Met binning tooa reeks Boole-variabelen converteren</span><span class="sxs-lookup"><span data-stu-id="c6d39-137">Convert binning tooa sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="c6d39-138">Ten slotte back Join Hallo dummy-variabelen-toohello oorspronkelijke gegevensframe</span><span class="sxs-lookup"><span data-stu-id="c6d39-138">Finally, Join hello dummy variables back toohello original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <span data-ttu-id="c6d39-139"><a name="sql-featuregen"></a>Het schrijven van gegevens back-tooAzure blob en gebruiken in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c6d39-139"><a name="sql-featuregen"></a>Writing data back tooAzure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="c6d39-140">Nadat u hebt Hallo gegevens verkend en Hallo benodigde onderdelen gemaakt, kunt u Hallo gegevens uploaden (actieve of featurized) tooan Azure blob- en deze wordt gebruikt in Azure Machine Learning met Hallo stappen te volgen: Houd er rekening mee dat extra functies kunnen worden gemaakt in Hallo Azure Machine Learning Studio ook.</span><span class="sxs-lookup"><span data-stu-id="c6d39-140">After you have explored hello data and created hello necessary features, you can upload hello data (sampled or featurized) tooan Azure blob and consume it in Azure Machine Learning using hello following steps: Note that additional features can be created in hello Azure Machine Learning Studio as well.</span></span> 

1. <span data-ttu-id="c6d39-141">Hallo gegevens frame toolocal-bestand schrijven</span><span class="sxs-lookup"><span data-stu-id="c6d39-141">Write hello data frame toolocal file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="c6d39-142">Hallo gegevens tooAzure blob als volgt uploaden:</span><span class="sxs-lookup"><span data-stu-id="c6d39-142">Upload hello data tooAzure blob as follows:</span></span>
   
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
3. <span data-ttu-id="c6d39-143">Nu Hallo gegevens kunnen worden gelezen vanuit Hallo blob met Azure Machine Learning Hallo [importgegevens] [ import-data] module, zoals wordt weergegeven in het welkomstscherm hieronder:</span><span class="sxs-lookup"><span data-stu-id="c6d39-143">Now hello data can be read from hello blob using hello Azure Machine Learning [Import Data][import-data] module as shown in hello screen below:</span></span>

![lezer blob][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

