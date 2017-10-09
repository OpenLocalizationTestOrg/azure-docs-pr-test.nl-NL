---
title: aaaCreate functies voor Azure blob storage-gegevens met behulp van Panda | Microsoft Docs
description: Hoe toocreate functies voor gegevens die zijn opgeslagen in Azure blob-container met Hallo Panda Python-pakket.
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
ms.openlocfilehash: 8594046c5d76a36ad87fc77e407752489d30afcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a>Met Panda functies maken voor Azure Blok-opslaggegevens
Dit document ziet u hoe toocreate functies voor gegevens die zijn opgeslagen in Azure blob-container met Hallo [Pandas](http://pandas.pydata.org/) Python-pakket. Na hoe tooload Hallo gegevens in een kader Panda-gegevens, wordt een melding weergegeven waarin wordt beschreven hoe toogenerate categorische functies met indicatorwaarden Python-scripts en functies met binning.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Dit **menu** koppelingen tootopics waarin wordt beschreven hoe toocreate functies voor gegevens in verschillende omgevingen. Deze taak is een stap in Hallo [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u een Azure blob storage-account hebt gemaakt en er in uw gegevens hebt opgeslagen. Als u instructies tooset van een account nodig hebt, raadpleegt u [een Azure Storage-account maken](../storage/common/storage-create-storage-account.md#create-a-storage-account)

## <a name="load-hello-data-into-a-pandas-data-frame"></a>Hallo gegevens laden in een frame Pandas-gegevens
In de volgorde toodo verkennen en manipuleren van een gegevensset, deze moet worden gedownload uit Hallo blob tooa lokale bronbestand die vervolgens kan worden geladen in een Pandas gegevensframe. Hier volgen Hallo stappen toofollow voor deze procedure:

1. Hallo gegevens downloaden vanaf Azure blob met Hallo Python voorbeeldcode met behulp van blob-service te volgen. Hallo-variabele in het Hallo-code hieronder vervangen door uw eigen specifieke waarden:
   
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
2. Hallo-gegevens lezen in een Pandas gegevens tijdskader van Hallo gedownload bestand.
   
        #LOCALFILE is hello file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

Nu u bent gereed tooexplore Hallo gegevens en genereren van de functies voor deze gegevensset.

## <a name="blob-featuregen"></a>Functie generatie
de volgende twee secties Hallo laten zien hoe toogenerate categorische functies met indicatorwaarden en binning functies met behulp van Python-scripts.

### <a name="blob-countfeature"></a>Indicatorwaarde op basis van functie generatie
Categorische functies kunnen als volgt worden gemaakt:

1. Hallo-verdeling van Hallo categorische kolom controleren:
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. Indicatorwaarden voor elk van de kolomwaarden Hallo genereren
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. Hallo indicatorkolom met de oorspronkelijke gegevensframe Hallo koppelen
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. Hallo oorspronkelijke variabele zelf verwijderen:
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <a name="blob-binningfeature"></a>Met binning functie generatie
Voor het genereren van binned functies gaan we als volgt:

1. Een reeks van kolommen toobin een numerieke kolom toevoegen
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. Met binning tooa reeks Boole-variabelen converteren
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. Ten slotte back Join Hallo dummy-variabelen-toohello oorspronkelijke gegevensframe
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <a name="sql-featuregen"></a>Het schrijven van gegevens back-tooAzure blob en gebruiken in Azure Machine Learning
Nadat u hebt Hallo gegevens verkend en Hallo benodigde onderdelen gemaakt, kunt u Hallo gegevens uploaden (actieve of featurized) tooan Azure blob- en deze wordt gebruikt in Azure Machine Learning met Hallo stappen te volgen: Houd er rekening mee dat extra functies kunnen worden gemaakt in Hallo Azure Machine Learning Studio ook.

1. Hallo gegevens frame toolocal-bestand schrijven
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. Hallo gegevens tooAzure blob als volgt uploaden:
   
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
3. Nu Hallo gegevens kunnen worden gelezen vanuit Hallo blob met Azure Machine Learning Hallo [importgegevens](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module, zoals wordt weergegeven in het welkomstscherm hieronder:

![lezer blob](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

