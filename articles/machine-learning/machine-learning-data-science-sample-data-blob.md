---
title: aaaSample gegevens in Azure blob storage | Microsoft Docs
description: Voorbeeldgegevens in Azure Blob-opslag
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8d9ad2c-86c5-43d6-80b8-d355b5c0dccf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: cceadf1fb1fb4804fc5b5a3da55c82854651026e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Voorbeeldgegevens in Azure blob-opslag
Dit document bevat informatie over steekproeven opgeslagen gegevens in Azure blob-opslag door programmatisch downloaden en vervolgens wordt met behulp van de procedures die zijn geschreven in Python.

Hallo volgende **menu** koppelingen tootopics waarin wordt beschreven hoe toosample gegevens uit verschillende omgevingen voor opslag. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Waarom een steekproef nemen uit uw gegevens?**
Als u van plan bent tooanalyze Hallo-gegevensset te groot is, is het meestal een goed idee Hallo toodown-sample data tooreduce het tooa kleiner, maar representatief en gemakkelijker grootte. Dit vereenvoudigt het begrip van de gegevens, exploratie en functie-engineering. De rol in Hallo Cortana-Analytics-proces is tooenable snel maken van een prototype van Hallo gegevensverwerking functies en machine learning-modellen.

Deze taak steekproeven is een stap in Hallo [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="download-and-down-sample-data"></a>De download- en omlaag voorbeeldgegevens
1. Hallo gegevens uit Azure blob storage met blob-service van de volgende voorbeeldcode Python Hallo Hallo downloaden: 
   
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

2. Gegevens in een Pandas gegevens tijdskader uit gedownloade hierboven Hallo-bestand gelezen.
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. Hallo-gegevens met behulp van Hallo down-sample `numpy`van `random.choice` als volgt:
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

Nu kunt u werken met Hallo boven gegevensframe met Hallo 1 procent voorbeeld voor verdere verkenning en functie generatie.

## <a name="heading"></a>Gegevens uploaden en lezen in Azure Machine Learning
U kunt gebruiken Hallo voorbeeldgegevens code Hallo toodown voorbeeld te volgen en deze rechtstreeks in Azure Machine Learning gebruiken:

1. Hallo frame tooa lokale gegevensbestand schrijven
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. Hallo lokaal bestand tooan Azure uploaden blob met behulp van de volgende voorbeeldcode Hallo:
   
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
            print ("Something went wrong with uploading toohello blob:"+ BLOBNAME)

3. Hallo-gegevens lezen uit hello Azure blob met Azure Machine Learning [importgegevens](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) zoals weergegeven in onderstaande afbeelding voor Hallo:

![lezer blob](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

