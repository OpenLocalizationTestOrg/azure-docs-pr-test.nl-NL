---
title: Voorbeeldgegevens in Azure blob storage | Microsoft Docs
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
ms.openlocfilehash: aa9ab454706429682a393c3d5758cebe20790e19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="fbbbc-103"><a name="heading"></a>Voorbeeldgegevens in Azure blob-opslag</span><span class="sxs-lookup"><span data-stu-id="fbbbc-103"><a name="heading"></a>Sample data in Azure blob storage</span></span>
<span data-ttu-id="fbbbc-104">Dit document bevat informatie over steekproeven opgeslagen gegevens in Azure blob-opslag door programmatisch downloaden en vervolgens wordt met behulp van de procedures die zijn geschreven in Python.</span><span class="sxs-lookup"><span data-stu-id="fbbbc-104">This document covers sampling data stored in Azure blob storage by downloading it programmatically and then sampling it using procedures written in Python.</span></span>

<span data-ttu-id="fbbbc-105">De volgende **menu** koppelingen naar onderwerpen waarin wordt beschreven hoe u voorbeeldgegevens uit verschillende omgevingen voor opslag.</span><span class="sxs-lookup"><span data-stu-id="fbbbc-105">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="fbbbc-106">**Waarom een steekproef nemen uit uw gegevens?**</span><span class="sxs-lookup"><span data-stu-id="fbbbc-106">**Why sample your data?**</span></span>
<span data-ttu-id="fbbbc-107">Als de gegevensset die u wilt analyseren groot is, is het meestal een goed idee om de gegevens om deze aan de grootte van een kleinere maar representatief en gemakkelijker down-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="fbbbc-107">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="fbbbc-108">Dit vereenvoudigt het begrip van de gegevens, exploratie en functie-engineering.</span><span class="sxs-lookup"><span data-stu-id="fbbbc-108">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="fbbbc-109">De rol in de Cortana-Analytics-proces is om in te schakelen snel maken van een prototype van de functies voor het verwerken van gegevens en machine learning-modellen.</span><span class="sxs-lookup"><span data-stu-id="fbbbc-109">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="fbbbc-110">Deze taak steekproeven is een stap in de [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="fbbbc-110">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="download-and-down-sample-data"></a><span data-ttu-id="fbbbc-111">De download- en omlaag voorbeeldgegevens</span><span class="sxs-lookup"><span data-stu-id="fbbbc-111">Download and down-sample data</span></span>
1. <span data-ttu-id="fbbbc-112">De gegevens uit Azure blob storage met behulp van de blob-service van de volgende voorbeeldcode voor Python downloaden:</span><span class="sxs-lookup"><span data-stu-id="fbbbc-112">Download the data from Azure blob storage using the blob service from the following sample Python code:</span></span> 
   
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

2. <span data-ttu-id="fbbbc-113">Gegevens lezen in een Pandas gegevens tijdskader uit het bestand gedownload hierboven.</span><span class="sxs-lookup"><span data-stu-id="fbbbc-113">Read data into a Pandas data-frame from the file downloaded above.</span></span>
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. <span data-ttu-id="fbbbc-114">Omlaag-voorbeeld de gegevens met behulp van de `numpy`van `random.choice` als volgt:</span><span class="sxs-lookup"><span data-stu-id="fbbbc-114">Down-sample the data using the `numpy`'s `random.choice` as follows:</span></span>
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

<span data-ttu-id="fbbbc-115">Nu kunt u werken met de bovenstaande gegevensframe met het voorbeeld 1 procent voor verdere verkenning en functie generatie.</span><span class="sxs-lookup"><span data-stu-id="fbbbc-115">Now you can work with the above data frame with the 1 Percent sample for further exploration and feature generation.</span></span>

## <span data-ttu-id="fbbbc-116"><a name="heading"></a>Gegevens uploaden en lezen in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="fbbbc-116"><a name="heading"></a>Upload data and read it into Azure Machine Learning</span></span>
<span data-ttu-id="fbbbc-117">U kunt de volgende voorbeeldcode down-voorbeeld de gegevens en deze rechtstreeks in Azure Machine Learning gebruiken:</span><span class="sxs-lookup"><span data-stu-id="fbbbc-117">You can use the following sample code to down-sample the data and use it directly in Azure Machine Learning:</span></span>

1. <span data-ttu-id="fbbbc-118">Het gegevensframe schrijven naar een lokaal bestand</span><span class="sxs-lookup"><span data-stu-id="fbbbc-118">Write the data frame to a local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. <span data-ttu-id="fbbbc-119">Het lokale bestand uploaden naar een Azure-blob met behulp van de volgende voorbeeldcode:</span><span class="sxs-lookup"><span data-stu-id="fbbbc-119">Upload the local file to an Azure blob using the following sample code:</span></span>
   
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
            print ("Something went wrong with uploading to the blob:"+ BLOBNAME)

3. <span data-ttu-id="fbbbc-120">De gegevens lezen van de blob van Azure met Azure Machine Learning [importgegevens](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) zoals weergegeven in de onderstaande afbeelding:</span><span class="sxs-lookup"><span data-stu-id="fbbbc-120">Read the data from the Azure blob using Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) as shown in the image below:</span></span>

![lezer blob](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

