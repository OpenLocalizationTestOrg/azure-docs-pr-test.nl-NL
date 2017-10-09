---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: aaaLoad gegevens met Azure Data Factory | Microsoft Docs
description: Meer informatie over tooload gegevens met Azure Data Factory
services: sql-data-warehouse
documentationcenter: NA
author: twounder
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: ac7ddaa7-a3a5-4e15-b3cf-c696d2d105df
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 10/31/2016
ms.author: mausher;barbkess
ms.custom: loading
ms.openlocfilehash: 4186bd88d14be33f90130a41e8df06ce1d7cbab2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-azure-data-factory"></a><span data-ttu-id="74103-103">Gegevens laden met Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="74103-103">Load Data with Azure Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="74103-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="74103-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="74103-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="74103-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="74103-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="74103-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="74103-107">BCP</span><span class="sxs-lookup"><span data-stu-id="74103-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)  
> 
> 

<span data-ttu-id="74103-108">Deze zelfstudie leert u hoe toocreate een pijplijn in Azure Data Factory toomove gegevens uit Azure Storage-Blob tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="74103-108">This tutorial shows you how toocreate a pipeline in Azure Data Factory toomove data from Azure Storage Blob tooAzure SQL Data Warehouse.</span></span> <span data-ttu-id="74103-109">U gaat Hello stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="74103-109">With hello following steps you will:</span></span>

* <span data-ttu-id="74103-110">U stelt voorbeeldgegevens in een Azure Storage-blob in.</span><span class="sxs-lookup"><span data-stu-id="74103-110">Set up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="74103-111">Verbinding maken met resources tooAzure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="74103-111">Connect resources tooAzure Data Factory.</span></span>
* <span data-ttu-id="74103-112">Een pijplijn toomove gegevens van de Storage-Blobs tooSQL Data Warehouse maken.</span><span class="sxs-lookup"><span data-stu-id="74103-112">Create a pipeline toomove data from Storage Blobs tooSQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="74103-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="74103-113">Before you begin</span></span>
<span data-ttu-id="74103-114">toofamiliarize uzelf met Azure Data Factory, Zie [inleiding tooAzure Data Factory][Introduction tooAzure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="74103-114">toofamiliarize yourself with Azure Data Factory, see [Introduction tooAzure Data Factory][Introduction tooAzure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="74103-115">Resources maken of identificeren</span><span class="sxs-lookup"><span data-stu-id="74103-115">Create or identify resources</span></span>
<span data-ttu-id="74103-116">Voordat u deze zelfstudie begint, moet u toohave Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="74103-116">Before starting this tutorial, you need toohave hello following resources:</span></span>

* <span data-ttu-id="74103-117">**Azure Storage-Blob**: deze zelfstudie wordt Azure Storage-Blob als gegevensbron Hallo voor hello Azure Data Factory-pijplijn en dus moet u toohave één beschikbaar toostore Hallo voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="74103-117">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as hello data source for hello Azure Data Factory pipeline, and so you need toohave one available toostore hello sample data.</span></span> <span data-ttu-id="74103-118">Als u niet al hebt, meer te weten hoe te[een opslagaccount maken][Create a storage account].</span><span class="sxs-lookup"><span data-stu-id="74103-118">If you don't have one already, learn how too[Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="74103-119">**SQL Data Warehouse**: met deze zelfstudie verplaatst Hallo-gegevens uit Azure Storage-Blob te SQL Data Warehouse en kan dus moeten toohave een datawarehouse online zijn waarin van Hallo voorbeeldgegevens van AdventureWorksDW zijn geladen.</span><span class="sxs-lookup"><span data-stu-id="74103-119">**SQL Data Warehouse**: This tutorial moves hello data from Azure Storage Blob too SQL Data Warehouse and so need toohave a data warehouse online that is loaded with hello AdventureWorksDW sample data.</span></span> <span data-ttu-id="74103-120">Als u nog geen datawarehouse, meer te weten hoe te[inrichten][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="74103-120">If you do not already have a data warehouse, learn how too[provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="74103-121">Als u wel een datawarehouse hebt, maar nog niet hebt ingericht met voorbeeldgegevens hello, kunt u [handmatig laden][Load sample data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="74103-121">If you have a data warehouse but didn't provision it with hello sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="74103-122">**Azure Data Factory**: Azure Data Factory Hallo daadwerkelijke laadbewerking wordt voltooid en dus moet u toohave een waarmee u toobuild Hallo data movement pijplijn kunt.</span><span class="sxs-lookup"><span data-stu-id="74103-122">**Azure Data Factory**: Azure Data Factory completes hello actual load and so you need toohave one that you can use toobuild hello data movement pipeline.</span></span> <span data-ttu-id="74103-123">Als u niet al hebt, Ontdek hoe toocreate een in stap 1 van [aan de slag met Azure Data Factory (Data Factory-Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span><span class="sxs-lookup"><span data-stu-id="74103-123">If you don't have one already, learn how toocreate one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="74103-124">**AZCopy**: moet u voorbeeldgegevens van AZCopy toocopy Hallo van uw lokale client tooyour Azure Storage-Blob.</span><span class="sxs-lookup"><span data-stu-id="74103-124">**AZCopy**: You need AZCopy toocopy hello sample data from your local client tooyour Azure Storage Blob.</span></span> <span data-ttu-id="74103-125">Zie voor installatie-instructies Hallo [documentatie van AZCopy][AZCopy documentation].</span><span class="sxs-lookup"><span data-stu-id="74103-125">For install instructions, see hello [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a><span data-ttu-id="74103-126">Stap 1: Voorbeeld gegevens tooAzure Storage-Blob kopiëren</span><span class="sxs-lookup"><span data-stu-id="74103-126">Step 1: Copy sample data tooAzure Storage Blob</span></span>
<span data-ttu-id="74103-127">Zodra u alle Hallo stukken gereed hebt, bent u klaar toocopy sample data tooyour Azure Storage-Blob.</span><span class="sxs-lookup"><span data-stu-id="74103-127">Once you have all hello pieces ready, you are ready toocopy sample data tooyour Azure Storage Blob.</span></span>

1. <span data-ttu-id="74103-128">[Voorbeeldgegevens downloaden][Download sample data].</span><span class="sxs-lookup"><span data-stu-id="74103-128">[Download sample data][Download sample data].</span></span> <span data-ttu-id="74103-129">Deze gegevens wordt een andere drie jaar aan verkoopgegevens tooyour voorbeeldgegevens van AdventureWorksDW toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="74103-129">This data adds another three years of sales data tooyour AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="74103-130">Gebruik deze AZCopy-opdracht toocopy Hallo drie jaar aan gegevens tooyour Azure Storage-Blob.</span><span class="sxs-lookup"><span data-stu-id="74103-130">Use this AZCopy command toocopy hello three years of data tooyour Azure Storage Blob.</span></span>
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-tooazure-data-factory"></a><span data-ttu-id="74103-131">Stap 2: Verbinding maken met resources tooAzure Data Factory</span><span class="sxs-lookup"><span data-stu-id="74103-131">Step 2: Connect resources tooAzure Data Factory</span></span>
<span data-ttu-id="74103-132">Nu sprake is van Hallo gegevens we kunt maken hello Azure Data Factory-pijplijn toomove Hallo gegevens uit Azure blob storage in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="74103-132">Now that hello data is in place we can create hello Azure Data Factory pipeline toomove hello data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="74103-133">tooget gestart, open Hallo [Azure-portal] [ Azure portal] en selecteer uw gegevensfactory in Hallo links menu.</span><span class="sxs-lookup"><span data-stu-id="74103-133">tooget started, open hello [Azure portal][Azure portal] and select your data factory from hello left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="74103-134">Stap 2.1: gekoppelde service maken</span><span class="sxs-lookup"><span data-stu-id="74103-134">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="74103-135">Koppel uw Azure-opslagaccount en SQL Data Warehouse tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="74103-135">Link your Azure storage account and SQL Data Warehouse tooyour data factory.</span></span>  

1. <span data-ttu-id="74103-136">Eerst Hallo registratieproces beginnen door te klikken op Hallo 'Gekoppelde Services' gedeelte van uw gegevensfactory en klik op 'Nieuw gegevensarchief'.</span><span class="sxs-lookup"><span data-stu-id="74103-136">First, begin hello registration process by clicking hello 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="74103-137">Kies een tooregister de naam van uw azure-opslag, selecteer Azure Storage als type en voer uw accountnaam en Accountsleutel.</span><span class="sxs-lookup"><span data-stu-id="74103-137">Choose a name tooregister your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="74103-138">tooregister SQL Data Warehouse gaat u de sectie 'Maken en implementeren' toohello, selecteert u 'Nieuw gegevensarchief' en 'Azure SQL Data Warehouse'.</span><span class="sxs-lookup"><span data-stu-id="74103-138">tooregister SQL Data Warehouse navigate toohello 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="74103-139">Kopieer en plak deze sjabloon erin, en vul vervolgens uw specifieke gegevens in.</span><span class="sxs-lookup"><span data-stu-id="74103-139">Copy and paste in this template, and then fill in your specific information.</span></span>
   
    ```JSON
    {
        "name": "<Linked Service Name>",
        "properties": {
            "description": "",
            "type": "AzureSqlDW",
            "typeProperties": {
                 "connectionString": "Data Source=tcp:<server name>.database.windows.net,1433;Initial Catalog=<server name>;Integrated Security=False;User ID=<user>@<servername>;Password=<password>;Connect Timeout=30;Encrypt=True"
             }
        }
    }
    ```

### <a name="step-22-define-hello-dataset"></a><span data-ttu-id="74103-140">Step 2.2: Hallo gegevensset definiëren</span><span class="sxs-lookup"><span data-stu-id="74103-140">Step 2.2: Define hello dataset</span></span>
<span data-ttu-id="74103-141">Nadat het maken van Hallo gekoppelde services, moeten we toodefine Hallo gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="74103-141">After creating hello linked services, we will have toodefine hello data sets.</span></span>  <span data-ttu-id="74103-142">Dit betekent hier Hallo structuur van Hallo-gegevens die worden verplaatst van uw opslag tooyour datawarehouse definiëren.</span><span class="sxs-lookup"><span data-stu-id="74103-142">Here this means defining hello structure of hello data that is being moved from your storage tooyour data warehouse.</span></span>  <span data-ttu-id="74103-143">U kunt meer lezen over het aanmaakproces</span><span class="sxs-lookup"><span data-stu-id="74103-143">You can read more about creating</span></span>

1. <span data-ttu-id="74103-144">Start dit proces door te navigeren toohello ' sectie maken en implementeren' van uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="74103-144">Start this process by navigating toohello 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="74103-145">Klik op 'Nieuwe gegevensset' Azure Blob-opslag toolink uw opslag tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="74103-145">Click 'New dataset' and then 'Azure Blob storage' toolink your storage tooyour data factory.</span></span>  <span data-ttu-id="74103-146">U kunt Hallo hieronder script toodefine uw gegevens in Azure Blob-opslag:</span><span class="sxs-lookup"><span data-stu-id="74103-146">You can use hello below script toodefine your data in Azure Blob storage:</span></span>
   
    ```JSON
    {
        "name": "<Dataset Name>",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "<linked storage name>",
            "typeProperties": {
                "folderPath": "<containter name>",
                "fileName": "FactInternetSales.csv",
                "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
                }
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }
    ```
3. <span data-ttu-id="74103-147">Vervolgens definieert u de gegevensset voor SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="74103-147">Now we define our dataset for SQL Data Warehouse.</span></span> <span data-ttu-id="74103-148">U begint op Hallo dezelfde manier, door te klikken op 'Nieuwe gegevensset' en 'Azure SQL Data Warehouse'.</span><span class="sxs-lookup"><span data-stu-id="74103-148">We start in hello same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>
   
    ```JSON
    {
        "name": "DWDataset",
        "properties": {
            "type": "AzureSqlDWTable",
            "linkedServiceName": "AzureSqlDWLinkedService",
            "typeProperties": {
                "tableName": "FactInternetSales"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="74103-149">Stap 3: een pijplijn maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="74103-149">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="74103-150">Ten slotte we instellen en Hallo pijplijn in Azure Data Factory uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="74103-150">Finally, we set up and run hello pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="74103-151">Dit is Hallo bewerking waarmee de daadwerkelijke gegevensverplaatsing hello wordt voltooid.</span><span class="sxs-lookup"><span data-stu-id="74103-151">This is hello operation that completes hello actual data movement.</span></span>  <span data-ttu-id="74103-152">U vindt een volledig overzicht van Hallo-bewerkingen die u met SQL Data Warehouse en Azure Data Factory uitvoeren kunt [hier][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="74103-152">You can find a full view of hello operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="74103-153">In de sectie 'Maken en implementeren' hello, klik op 'Meer opdrachten' 'Nieuwe pijplijn'.</span><span class="sxs-lookup"><span data-stu-id="74103-153">In hello 'Author and Deploy' section, click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="74103-154">Nadat u Hallo pijplijn gemaakt, kunt u Hallo hieronder de code tootransfer hello tooyour gegevens datawarehouse:</span><span class="sxs-lookup"><span data-stu-id="74103-154">After you create hello pipeline, you can use hello below code tootransfer hello data tooyour data warehouse:</span></span>

```JSON
{
    "name": "<Pipeline Name>",
    "properties": {
        "description": "<Description>",
        "activities": [
          {
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "skipHeaderLineCount": 1
                },
                "sink": {
                    "type": "SqlDWSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:10"
                }
            },
            "inputs": [
              {
                "name": "<Storage Dataset>"
              }
            ],
            "outputs": [
              {
                "name": "<Data Warehouse Dataset>"
              }
            ],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Sample Copy",
            "description": "Copy Activity"
          }
        ],
        "start": "<Date YYYY-MM-DD>",
        "end": "<Date YYYY-MM-DD>",
        "isPaused": false
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="74103-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="74103-155">Next steps</span></span>
<span data-ttu-id="74103-156">toolearn starten, weer te geven:</span><span class="sxs-lookup"><span data-stu-id="74103-156">toolearn more, start by viewing:</span></span>

* <span data-ttu-id="74103-157">[Leertraject voor Azure Data Factory][Azure Data Factory learning path].</span><span class="sxs-lookup"><span data-stu-id="74103-157">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="74103-158">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span><span class="sxs-lookup"><span data-stu-id="74103-158">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="74103-159">Dit is Hallo belangrijkste naslagonderwerp voor het gebruik van Azure Data Factory met Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="74103-159">This is hello core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="74103-160">Deze onderwerpen bevatten gedetailleerde informatie over Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="74103-160">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="74103-161">Informatie over Azure SQL Database of HDInsight, maar Hallo-informatie is ook van toepassing tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="74103-161">They discuss Azure SQL Database or HDInsight, but hello information also applies tooAzure SQL Data Warehouse.</span></span>

* <span data-ttu-id="74103-162">[Zelfstudie: Aan de slag met Azure Data Factory] [ Tutorial: Get started with Azure Data Factory] dit Hallo belangrijkste zelfstudie voor het verwerken van gegevens met Azure Data Factory is.</span><span class="sxs-lookup"><span data-stu-id="74103-162">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is hello core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="74103-163">In deze zelfstudie maakt u uw eerste pijplijn die gebruikmaakt van HDInsight tootransform bouwt en analyseren van weblogboeken op maandelijkse basis.</span><span class="sxs-lookup"><span data-stu-id="74103-163">In this tutorial, you will build your first pipeline that uses HDInsight tootransform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="74103-164">Opmerking: deze zelfstudie omvat geen kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="74103-164">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="74103-165">[Zelfstudie: Gegevens kopiëren van Azure Storage-Blob tooAzure SQL-Database][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span><span class="sxs-lookup"><span data-stu-id="74103-165">[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span></span> <span data-ttu-id="74103-166">In deze zelfstudie maakt u een pijplijn in Azure Data Factory toocopy gegevens uit Azure Storage-Blob tooAzure SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="74103-166">In this tutorial, you create a pipeline in Azure Data Factory toocopy data from Azure Storage Blob tooAzure SQL Database.</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction tooAzure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
