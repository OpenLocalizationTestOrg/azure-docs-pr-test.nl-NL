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
# <span data-ttu-id="16077-103"><a name="heading"></a>Voorbeeldgegevens in Azure blob-opslag</span><span class="sxs-lookup"><span data-stu-id="16077-103"><a name="heading"></a>Sample data in Azure blob storage</span></span>
<span data-ttu-id="16077-104">Dit document bevat informatie over steekproeven opgeslagen gegevens in Azure blob-opslag door programmatisch downloaden en vervolgens wordt met behulp van de procedures die zijn geschreven in Python.</span><span class="sxs-lookup"><span data-stu-id="16077-104">This document covers sampling data stored in Azure blob storage by downloading it programmatically and then sampling it using procedures written in Python.</span></span>

<span data-ttu-id="16077-105">Hallo volgende **menu** koppelingen tootopics waarin wordt beschreven hoe toosample gegevens uit verschillende omgevingen voor opslag.</span><span class="sxs-lookup"><span data-stu-id="16077-105">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="16077-106">**Waarom een steekproef nemen uit uw gegevens?**</span><span class="sxs-lookup"><span data-stu-id="16077-106">**Why sample your data?**</span></span>
<span data-ttu-id="16077-107">Als u van plan bent tooanalyze Hallo-gegevensset te groot is, is het meestal een goed idee Hallo toodown-sample data tooreduce het tooa kleiner, maar representatief en gemakkelijker grootte.</span><span class="sxs-lookup"><span data-stu-id="16077-107">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="16077-108">Dit vereenvoudigt het begrip van de gegevens, exploratie en functie-engineering.</span><span class="sxs-lookup"><span data-stu-id="16077-108">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="16077-109">De rol in Hallo Cortana-Analytics-proces is tooenable snel maken van een prototype van Hallo gegevensverwerking functies en machine learning-modellen.</span><span class="sxs-lookup"><span data-stu-id="16077-109">Its role in hello Cortana Analytics Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="16077-110">Deze taak steekproeven is een stap in Hallo [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="16077-110">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="download-and-down-sample-data"></a><span data-ttu-id="16077-111">De download- en omlaag voorbeeldgegevens</span><span class="sxs-lookup"><span data-stu-id="16077-111">Download and down-sample data</span></span>
1. <span data-ttu-id="16077-112">Hallo gegevens uit Azure blob storage met blob-service van de volgende voorbeeldcode Python Hallo Hallo downloaden:</span><span class="sxs-lookup"><span data-stu-id="16077-112">Download hello data from Azure blob storage using hello blob service from hello following sample Python code:</span></span> 
   
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

2. <span data-ttu-id="16077-113">Gegevens in een Pandas gegevens tijdskader uit gedownloade hierboven Hallo-bestand gelezen.</span><span class="sxs-lookup"><span data-stu-id="16077-113">Read data into a Pandas data-frame from hello file downloaded above.</span></span>
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. <span data-ttu-id="16077-114">Hallo-gegevens met behulp van Hallo down-sample `numpy`van `random.choice` als volgt:</span><span class="sxs-lookup"><span data-stu-id="16077-114">Down-sample hello data using hello `numpy`'s `random.choice` as follows:</span></span>
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

<span data-ttu-id="16077-115">Nu kunt u werken met Hallo boven gegevensframe met Hallo 1 procent voorbeeld voor verdere verkenning en functie generatie.</span><span class="sxs-lookup"><span data-stu-id="16077-115">Now you can work with hello above data frame with hello 1 Percent sample for further exploration and feature generation.</span></span>

## <span data-ttu-id="16077-116"><a name="heading"></a>Gegevens uploaden en lezen in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="16077-116"><a name="heading"></a>Upload data and read it into Azure Machine Learning</span></span>
<span data-ttu-id="16077-117">U kunt gebruiken Hallo voorbeeldgegevens code Hallo toodown voorbeeld te volgen en deze rechtstreeks in Azure Machine Learning gebruiken:</span><span class="sxs-lookup"><span data-stu-id="16077-117">You can use hello following sample code toodown-sample hello data and use it directly in Azure Machine Learning:</span></span>

1. <span data-ttu-id="16077-118">Hallo frame tooa lokale gegevensbestand schrijven</span><span class="sxs-lookup"><span data-stu-id="16077-118">Write hello data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. <span data-ttu-id="16077-119">Hallo lokaal bestand tooan Azure uploaden blob met behulp van de volgende voorbeeldcode Hallo:</span><span class="sxs-lookup"><span data-stu-id="16077-119">Upload hello local file tooan Azure blob using hello following sample code:</span></span>
   
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

3. <span data-ttu-id="16077-120">Hallo-gegevens lezen uit hello Azure blob met Azure Machine Learning [importgegevens](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) zoals weergegeven in onderstaande afbeelding voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="16077-120">Read hello data from hello Azure blob using Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) as shown in hello image below:</span></span>

![lezer blob](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

