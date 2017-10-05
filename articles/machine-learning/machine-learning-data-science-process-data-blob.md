---
title: Verwerken van Azure blob-gegevens met geavanceerde analyses | Microsoft Docs
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
ms.openlocfilehash: 36d950fd81029af82d9f2f652b2f01dba5fc8cc9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="729ae-103"><a name="heading"></a>Azure blob-gegevens met geavanceerde analyses verwerken</span><span class="sxs-lookup"><span data-stu-id="729ae-103"><a name="heading"></a>Process Azure blob data with advanced analytics</span></span>
<span data-ttu-id="729ae-104">Dit document bevat informatie over gegevens verkennen en genereren van de functies van de gegevens die zijn opgeslagen in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="729ae-104">This document covers exploring data and generating features from data stored in Azure Blob storage.</span></span> 

## <a name="load-the-data-into-a-pandas-data-frame"></a><span data-ttu-id="729ae-105">De gegevens in een frame Pandas-gegevens laden</span><span class="sxs-lookup"><span data-stu-id="729ae-105">Load the data into a Pandas data frame</span></span>
<span data-ttu-id="729ae-106">Om te verkennen en het bewerken van een gegevensset, moet deze worden gedownload van de bron van de blob naar een lokaal bestand die vervolgens kan worden geladen in een Pandas gegevensframe.</span><span class="sxs-lookup"><span data-stu-id="729ae-106">In order to explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="729ae-107">Hier volgen de stappen voor deze procedure:</span><span class="sxs-lookup"><span data-stu-id="729ae-107">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="729ae-108">Download de gegevens van Azure-blob met de volgende voorbeeldcode Python met behulp van blob-service.</span><span class="sxs-lookup"><span data-stu-id="729ae-108">Download the data from Azure blob with the following sample Python code using blob service.</span></span> <span data-ttu-id="729ae-109">De variabele in de volgende code vervangen door uw eigen specifieke waarden:</span><span class="sxs-lookup"><span data-stu-id="729ae-109">Replace the variable in the code below with your specific values:</span></span> 
   
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
2. <span data-ttu-id="729ae-110">De gegevens in een Pandas gegevens tijdskader uit het gedownloade bestand gelezen.</span><span class="sxs-lookup"><span data-stu-id="729ae-110">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="729ae-111">U bent nu klaar voor de gegevens verkennen en het genereren van functies op deze dataset.</span><span class="sxs-lookup"><span data-stu-id="729ae-111">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="729ae-112"><a name="blob-dataexploration"></a>Gegevensverkenning</span><span class="sxs-lookup"><span data-stu-id="729ae-112"><a name="blob-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="729ae-113">Hier volgen enkele voorbeelden van methoden voor het verkennen van gegevens met behulp van Pandas:</span><span class="sxs-lookup"><span data-stu-id="729ae-113">Here are a few examples of ways to explore data using Pandas:</span></span>

1. <span data-ttu-id="729ae-114">Het aantal rijen en kolommen controleren</span><span class="sxs-lookup"><span data-stu-id="729ae-114">Inspect the number of rows and columns</span></span> 
   
        print 'the size of the data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="729ae-115">Inspecteer de eerste of laatste paar rijen in de gegevensset zoals hieronder:</span><span class="sxs-lookup"><span data-stu-id="729ae-115">Inspect the first or last few rows in the dataset as below:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="729ae-116">Controleer het gegevenstype dat elke kolom is geïmporteerd als het gebruik van de volgende voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="729ae-116">Check the data type each column was imported as using the following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="729ae-117">De algemene statistieken voor de kolommen in de gegevensset als volgt controleren</span><span class="sxs-lookup"><span data-stu-id="729ae-117">Check the basic stats for the columns in the data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="729ae-118">Het aantal items voor elke waarde in de kolom als volgt bekijken</span><span class="sxs-lookup"><span data-stu-id="729ae-118">Look at the number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="729ae-119">Ontbrekende waarden ten opzichte van het werkelijke aantal vermeldingen in elke kolom met de volgende voorbeeldcode tellen</span><span class="sxs-lookup"><span data-stu-id="729ae-119">Count missing values versus the actual number of entries in each column using the following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="729ae-120">Als u ontbrekende waarden voor een specifieke kolom in de gegevens hebt, kunt u ze als volgt verwijderen:</span><span class="sxs-lookup"><span data-stu-id="729ae-120">If you have missing values for a specific column in the data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="729ae-121">dataframe_blobdata_noNA dataframe_blobdata.dropna() dataframe_blobdata_noNA.shape =</span><span class="sxs-lookup"><span data-stu-id="729ae-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="729ae-122">Ontbrekende waarden te vervangen op een andere manier is met de modusfunctie:</span><span class="sxs-lookup"><span data-stu-id="729ae-122">Another way to replace missing values is with the mode function:</span></span>
   
     <span data-ttu-id="729ae-123">dataframe_blobdata_mode dataframe_blobdata.fillna = ({< column_name >: .mode()[0]}) dataframe_blobdata ['< column_name >"]</span><span class="sxs-lookup"><span data-stu-id="729ae-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="729ae-124">Histogram tekent variabele aantal opslaglocaties gebruiken om te tekenen van de distributie van een variabele maken</span><span class="sxs-lookup"><span data-stu-id="729ae-124">Create a histogram plot using variable number of bins to plot the distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="729ae-125">Bekijk correlatie tussen variabelen met behulp van een scatterplot of via de ingebouwde correlatiefunctie</span><span class="sxs-lookup"><span data-stu-id="729ae-125">Look at correlations between variables using a scatterplot or using the built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <span data-ttu-id="729ae-126"><a name="blob-featuregen"></a>Functie generatie</span><span class="sxs-lookup"><span data-stu-id="729ae-126"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="729ae-127">Functies met behulp van Python als volgt kan worden gegenereerd:</span><span class="sxs-lookup"><span data-stu-id="729ae-127">We can generate features using Python as follows:</span></span>

### <span data-ttu-id="729ae-128"><a name="blob-countfeature"></a>Indicatorwaarde op basis van functie generatie</span><span class="sxs-lookup"><span data-stu-id="729ae-128"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="729ae-129">Categorische functies kunnen als volgt worden gemaakt:</span><span class="sxs-lookup"><span data-stu-id="729ae-129">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="729ae-130">Inspecteer de distributie van de kolom categorische:</span><span class="sxs-lookup"><span data-stu-id="729ae-130">Inspect the distribution of the categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="729ae-131">Indicatorwaarden voor elk van de kolomwaarden genereren</span><span class="sxs-lookup"><span data-stu-id="729ae-131">Generate indicator values for each of the column values</span></span>
   
        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="729ae-132">Lid worden van de indicatorkolom met de oorspronkelijke gegevensframe</span><span class="sxs-lookup"><span data-stu-id="729ae-132">Join the indicator column with the original data frame</span></span> 
   
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="729ae-133">De oorspronkelijke variabele zelf verwijderen:</span><span class="sxs-lookup"><span data-stu-id="729ae-133">Remove the original variable itself:</span></span>
   
        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="729ae-134"><a name="blob-binningfeature"></a>Met binning functie generatie</span><span class="sxs-lookup"><span data-stu-id="729ae-134"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="729ae-135">Voor het genereren van binned functies gaan we als volgt:</span><span class="sxs-lookup"><span data-stu-id="729ae-135">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="729ae-136">Een reeks van kolommen die u wilt een numerieke kolom bin toevoegen</span><span class="sxs-lookup"><span data-stu-id="729ae-136">Add a sequence of columns to bin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="729ae-137">Converteren naar een reeks Boole-variabelen met binning</span><span class="sxs-lookup"><span data-stu-id="729ae-137">Convert binning to a sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="729ae-138">Ten slotte de dummy variabelen Join terug naar de oorspronkelijke gegevensframe</span><span class="sxs-lookup"><span data-stu-id="729ae-138">Finally, Join the dummy variables back to the original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <span data-ttu-id="729ae-139"><a name="sql-featuregen"></a>Schrijven van gegevens terug naar Azure blob en gebruiken in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="729ae-139"><a name="sql-featuregen"></a>Writing data back to Azure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="729ae-140">Nadat u de gegevens hebt verkend en de benodigde onderdelen hebt gemaakt, kunt u de gegevens uploaden (actieve of featurized) naar een Azure blob- en deze wordt gebruikt in Azure Machine Learning met behulp van de volgende stappen uit: Houd er rekening mee dat extra functies kunnen worden gemaakt in de Azure-Machine Ook Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="729ae-140">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span></span> 

1. <span data-ttu-id="729ae-141">Het gegevensframe schrijven naar een lokaal bestand</span><span class="sxs-lookup"><span data-stu-id="729ae-141">Write the data frame to local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="729ae-142">Uploaden van de gegevens naar Azure blob als volgt:</span><span class="sxs-lookup"><span data-stu-id="729ae-142">Upload the data to Azure blob as follows:</span></span>
   
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
3. <span data-ttu-id="729ae-143">Nu de gegevens kunnen worden gelezen vanaf de blob met de Azure Machine Learning [importgegevens] [ import-data] module, zoals wordt weergegeven in het scherm hieronder:</span><span class="sxs-lookup"><span data-stu-id="729ae-143">Now the data can be read from the blob using the Azure Machine Learning [Import Data][import-data] module as shown in the screen below:</span></span>

![lezer blob][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

