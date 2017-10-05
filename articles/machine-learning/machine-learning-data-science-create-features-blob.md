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
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a>Met Panda functies maken voor Azure Blok-opslaggegevens
Dit document wordt beschreven hoe maakt functies voor gegevens die zijn opgeslagen in Azure blob-container gebruiken de [Pandas](http://pandas.pydata.org/) Python-pakket. Na het waarin wordt beschreven hoe u de gegevens in een frame Panda-gegevens laden, er wordt weergegeven hoe categorische functies met indicatorwaarden Python-scripts en functies met binning genereren.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Dit **menu** koppelingen naar onderwerpen waarin wordt beschreven hoe u functies voor gegevens in verschillende omgevingen maken. Deze taak is een stap in de [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u een Azure blob storage-account hebt gemaakt en er in uw gegevens hebt opgeslagen. Als u instructies voor het instellen van een account nodig hebt, raadpleegt u [een Azure Storage-account maken](../storage/common/storage-create-storage-account.md#create-a-storage-account)

## <a name="load-the-data-into-a-pandas-data-frame"></a>De gegevens in een frame Pandas-gegevens laden
Om te verkennen en manipuleren van een gegevensset, moet deze worden gedownload van de bron van de blob naar een lokaal bestand die vervolgens kan worden geladen in een Pandas gegevensframe. Hier volgen de stappen voor deze procedure:

1. Download de gegevens van Azure-blob met de volgende voorbeeldcode Python met behulp van blob-service. De variabele in de volgende code vervangen door uw eigen specifieke waarden:
   
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
2. De gegevens in een Pandas gegevens tijdskader uit het gedownloade bestand gelezen.
   
        #LOCALFILE is the file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

U bent nu klaar voor de gegevens verkennen en het genereren van functies op deze dataset.

## <a name="blob-featuregen"></a>Functie generatie
De volgende twee secties laten zien hoe categorische waarvan de indicatorwaarde en binning functies met behulp van Python-scripts genereren.

### <a name="blob-countfeature"></a>Indicatorwaarde op basis van functie generatie
Categorische functies kunnen als volgt worden gemaakt:

1. Inspecteer de distributie van de kolom categorische:
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. Indicatorwaarden voor elk van de kolomwaarden genereren
   
        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. Lid worden van de indicatorkolom met de oorspronkelijke gegevensframe
   
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. De oorspronkelijke variabele zelf verwijderen:
   
        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <a name="blob-binningfeature"></a>Met binning functie generatie
Voor het genereren van binned functies gaan we als volgt:

1. Een reeks van kolommen die u wilt een numerieke kolom bin toevoegen
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. Converteren naar een reeks Boole-variabelen met binning
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. Ten slotte de dummy variabelen Join terug naar de oorspronkelijke gegevensframe
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <a name="sql-featuregen"></a>Schrijven van gegevens terug naar Azure blob en gebruiken in Azure Machine Learning
Nadat u de gegevens hebt verkend en de benodigde onderdelen hebt gemaakt, kunt u de gegevens uploaden (actieve of featurized) naar een Azure blob- en deze wordt gebruikt in Azure Machine Learning met behulp van de volgende stappen uit: Houd er rekening mee dat extra functies kunnen worden gemaakt in de Azure-Machine Ook Learning Studio.

1. Het gegevensframe schrijven naar een lokaal bestand
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. Uploaden van de gegevens naar Azure blob als volgt:
   
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
3. Nu de gegevens kunnen worden gelezen vanaf de blob met de Azure Machine Learning [importgegevens](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module, zoals wordt weergegeven in het scherm hieronder:

![lezer blob](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

