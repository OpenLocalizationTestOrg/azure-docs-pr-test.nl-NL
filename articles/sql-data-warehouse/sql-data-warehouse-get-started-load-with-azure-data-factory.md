---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: Gegevens laden met Azure Data Factory | Microsoft Docs
description: Informatie over het laden van gegevens met Azure Data Factory
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
ms.openlocfilehash: 0b01c77c916b616974545fc3da442e72e5336399
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-with-azure-data-factory"></a><span data-ttu-id="bdec8-103">Gegevens laden met Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="bdec8-103">Load Data with Azure Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bdec8-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="bdec8-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="bdec8-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="bdec8-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="bdec8-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="bdec8-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="bdec8-107">BCP</span><span class="sxs-lookup"><span data-stu-id="bdec8-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)  
> 
> 

<span data-ttu-id="bdec8-108">In deze zelfstudie ziet u hoe u een pijplijn maakt in Azure Data Factory om gegevens te verplaatsen van een Azure Storage-blob naar Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bdec8-108">This tutorial shows you how to create a pipeline in Azure Data Factory to move data from Azure Storage Blob to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="bdec8-109">Met deze stappen bewerkstelligt u het volgende:</span><span class="sxs-lookup"><span data-stu-id="bdec8-109">With the following steps you will:</span></span>

* <span data-ttu-id="bdec8-110">U stelt voorbeeldgegevens in een Azure Storage-blob in.</span><span class="sxs-lookup"><span data-stu-id="bdec8-110">Set up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="bdec8-111">U verbindt resources met Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="bdec8-111">Connect resources to Azure Data Factory.</span></span>
* <span data-ttu-id="bdec8-112">U maakt een pijplijn om gegevens te verplaatsen van opslag-blobs naar SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bdec8-112">Create a pipeline to move data from Storage Blobs to SQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="bdec8-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="bdec8-113">Before you begin</span></span>
<span data-ttu-id="bdec8-114">Zie [Inleiding tot Azure Data Factory][Introduction to Azure Data Factory] om vertrouwd te raken met Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="bdec8-114">To familiarize yourself with Azure Data Factory, see [Introduction to Azure Data Factory][Introduction to Azure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="bdec8-115">Resources maken of identificeren</span><span class="sxs-lookup"><span data-stu-id="bdec8-115">Create or identify resources</span></span>
<span data-ttu-id="bdec8-116">Voordat u met deze zelfstudie begint, moet u beschikken over de volgende resources:</span><span class="sxs-lookup"><span data-stu-id="bdec8-116">Before starting this tutorial, you need to have the following resources:</span></span>

* <span data-ttu-id="bdec8-117">**Azure Storage-blob**: in deze zelfstudie wordt een Azure Storage-blob gebruikt als gegevensbron voor de Azure Data Factory-pijplijn, dus u hebt er een nodig om de voorbeeldgegevens in op te slaan.</span><span class="sxs-lookup"><span data-stu-id="bdec8-117">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as the data source for the Azure Data Factory pipeline, and so you need to have one available to store the sample data.</span></span> <span data-ttu-id="bdec8-118">Als u nog geen opslagaccount hebt, raadpleegt u [Een opslagaccount maken][Create a storage account].</span><span class="sxs-lookup"><span data-stu-id="bdec8-118">If you don't have one already, learn how to [Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="bdec8-119">**SQL Data Warehouse**: in deze zelfstudie worden de gegevens uit een Azure Storage-blob verplaatst naar SQL Data Warehouse. Hiervoor moet een datawarehouse online zijn waarin de voorbeeldgegevens van AdventureWorksDW zijn geladen.</span><span class="sxs-lookup"><span data-stu-id="bdec8-119">**SQL Data Warehouse**: This tutorial moves the data from Azure Storage Blob to  SQL Data Warehouse and so need to have a data warehouse online that is loaded with the AdventureWorksDW sample data.</span></span> <span data-ttu-id="bdec8-120">Als u nog geen datawarehouse hebt, kunt u [er een inrichten][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="bdec8-120">If you do not already have a data warehouse, learn how to [provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="bdec8-121">Als u wel een datawarehouse hebt, maar u dit nog niet hebt ingericht met de voorbeeldgegevens, kunt u [het handmatig laden][Load sample data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="bdec8-121">If you have a data warehouse but didn't provision it with the sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="bdec8-122">**Azure Data Factory**: Azure Data Factory voltooit de werkelijke belasting. U hebt er dus een nodig die u kunt gebruiken voor het bouwen van de pijplijn voor het verplaatsen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="bdec8-122">**Azure Data Factory**: Azure Data Factory completes the actual load and so you need to have one that you can use to build the data movement pipeline.</span></span> <span data-ttu-id="bdec8-123">Als u er nog geen hebt, krijgt u informatie om er een te maken in Stap 1 van [Aan de slag met Azure Data Factory (Data Factory-editor)][Get started with Azure Data Factory (Data Factory Editor)].</span><span class="sxs-lookup"><span data-stu-id="bdec8-123">If you don't have one already, learn how to create one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="bdec8-124">**AZCopy**: u hebt AZCopy nodig om de voorbeeldgegevens van de lokale client te kopiëren naar uw Azure Storage-blob.</span><span class="sxs-lookup"><span data-stu-id="bdec8-124">**AZCopy**: You need AZCopy to copy the sample data from your local client to your Azure Storage Blob.</span></span> <span data-ttu-id="bdec8-125">Zie de [documentatie van AZCopy][AZCopy documentation] voor installatie-instructies.</span><span class="sxs-lookup"><span data-stu-id="bdec8-125">For install instructions, see the [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-to-azure-storage-blob"></a><span data-ttu-id="bdec8-126">Stap 1: Voorbeeldgegevens kopiëren naar Azure Storage-blob</span><span class="sxs-lookup"><span data-stu-id="bdec8-126">Step 1: Copy sample data to Azure Storage Blob</span></span>
<span data-ttu-id="bdec8-127">Als u beschikt over alle benodigde onderdelen, bent u klaar om de voorbeeldgegevens te kopiëren naar uw Azure Storage-blob.</span><span class="sxs-lookup"><span data-stu-id="bdec8-127">Once you have all the pieces ready, you are ready to copy sample data to your Azure Storage Blob.</span></span>

1. <span data-ttu-id="bdec8-128">[Voorbeeldgegevens downloaden][Download sample data].</span><span class="sxs-lookup"><span data-stu-id="bdec8-128">[Download sample data][Download sample data].</span></span> <span data-ttu-id="bdec8-129">Hiermee worden nog eens drie jaar aan verkoopgegevens toegevoegd aan de voorbeeldgegevens van AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="bdec8-129">This data adds another three years of sales data to your AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="bdec8-130">Gebruik deze AZCopy-opdracht om de drie jaar aan gegevens naar uw Azure Storage-blob te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="bdec8-130">Use this AZCopy command to copy the three years of data to your Azure Storage Blob.</span></span>
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-to-azure-data-factory"></a><span data-ttu-id="bdec8-131">Stap 2: resources verbinden met Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="bdec8-131">Step 2: Connect resources to Azure Data Factory</span></span>
<span data-ttu-id="bdec8-132">Nu de gegevens zijn opgeslagen, kunt u de Azure Data Factory-pijplijn maken om de gegevens te kunnen verplaatsen van de Azure Blob-opslag naar SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bdec8-132">Now that the data is in place we can create the Azure Data Factory pipeline to move the data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="bdec8-133">Open [Azure Portal][Azure portal] en selecteer uw gegevensfactory in het menu aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="bdec8-133">To get started, open the [Azure portal][Azure portal] and select your data factory from the left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="bdec8-134">Stap 2.1: gekoppelde service maken</span><span class="sxs-lookup"><span data-stu-id="bdec8-134">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="bdec8-135">Koppel uw Azure-opslagaccount en SQL Data Warehouse aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="bdec8-135">Link your Azure storage account and SQL Data Warehouse to your data factory.</span></span>  

1. <span data-ttu-id="bdec8-136">Start het registratieproces door te klikken op de sectie Gekoppelde services van uw gegevensfactory en klik op Nieuwe gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="bdec8-136">First, begin the registration process by clicking the 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="bdec8-137">Geef een naam op voor uw Azure-opslag, selecteer Azure Storage als type en voer uw accountnaam en accountsleutel in.</span><span class="sxs-lookup"><span data-stu-id="bdec8-137">Choose a name to register your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="bdec8-138">Registreer SQL Data Warehouse door te navigeren naar de sectie Maken en implementeren, selecteer Nieuwe gegevensopslag en selecteer vervolgens Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bdec8-138">To register SQL Data Warehouse navigate to the 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="bdec8-139">Kopieer en plak deze sjabloon erin, en vul vervolgens uw specifieke gegevens in.</span><span class="sxs-lookup"><span data-stu-id="bdec8-139">Copy and paste in this template, and then fill in your specific information.</span></span>
   
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

### <a name="step-22-define-the-dataset"></a><span data-ttu-id="bdec8-140">Step 2.2: de gegevensset definiëren</span><span class="sxs-lookup"><span data-stu-id="bdec8-140">Step 2.2: Define the dataset</span></span>
<span data-ttu-id="bdec8-141">Na het maken van de gekoppelde services moet u de gegevenssets definiëren.</span><span class="sxs-lookup"><span data-stu-id="bdec8-141">After creating the linked services, we will have to define the data sets.</span></span>  <span data-ttu-id="bdec8-142">Dat houdt in dat u de structuur moet definiëren van de gegevens die worden verplaatst van de opslag naar het datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="bdec8-142">Here this means defining the structure of the data that is being moved from your storage to your data warehouse.</span></span>  <span data-ttu-id="bdec8-143">U kunt meer lezen over het aanmaakproces</span><span class="sxs-lookup"><span data-stu-id="bdec8-143">You can read more about creating</span></span>

1. <span data-ttu-id="bdec8-144">Start dit proces door te navigeren naar de sectie Maken en implementeren van uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="bdec8-144">Start this process by navigating to the 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="bdec8-145">Klik achtereenvolgens op Nieuwe gegevensset en Azure Blob-opslag om uw opslag te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="bdec8-145">Click 'New dataset' and then 'Azure Blob storage' to link your storage to your data factory.</span></span>  <span data-ttu-id="bdec8-146">Met onderstaand script kunt u uw gegevens definiëren in Azure Blob-opslag:</span><span class="sxs-lookup"><span data-stu-id="bdec8-146">You can use the below script to define your data in Azure Blob storage:</span></span>
   
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
3. <span data-ttu-id="bdec8-147">Vervolgens definieert u de gegevensset voor SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bdec8-147">Now we define our dataset for SQL Data Warehouse.</span></span> <span data-ttu-id="bdec8-148">U begint op dezelfde manier, door te klikken op Nieuwe gegevensset. Klik vervolgens op Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bdec8-148">We start in the same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>
   
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

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="bdec8-149">Stap 3: een pijplijn maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="bdec8-149">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="bdec8-150">Tot slot moet u een pijplijn in Azure Data Factory instellen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="bdec8-150">Finally, we set up and run the pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="bdec8-151">Dit is de bewerking waarmee de daadwerkelijke gegevensverplaatsing wordt voltooid.</span><span class="sxs-lookup"><span data-stu-id="bdec8-151">This is the operation that completes the actual data movement.</span></span>  <span data-ttu-id="bdec8-152">Een volledig overzicht van de bewerkingen die u met SQL Data Warehouse en Azure Data Factory kunt uitvoeren, vindt u [hier][Move data to and from Azure SQL Data Warehouse using Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="bdec8-152">You can find a full view of the operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data to and from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="bdec8-153">Klik nu in de sectie Maken en implementeren op Meer opdrachten en vervolgens op Nieuwe pijplijn.</span><span class="sxs-lookup"><span data-stu-id="bdec8-153">In the 'Author and Deploy' section, click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="bdec8-154">Nadat u de pijplijn hebt gemaakt, kunt u onderstaande code gebruiken voor de gegevensoverdracht naar uw datawarehouse:</span><span class="sxs-lookup"><span data-stu-id="bdec8-154">After you create the pipeline, you can use the below code to transfer the data to your data warehouse:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="bdec8-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bdec8-155">Next steps</span></span>
<span data-ttu-id="bdec8-156">Bekijk de volgende onderwerpen voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="bdec8-156">To learn more, start by viewing:</span></span>

* <span data-ttu-id="bdec8-157">[Leertraject voor Azure Data Factory][Azure Data Factory learning path].</span><span class="sxs-lookup"><span data-stu-id="bdec8-157">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="bdec8-158">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span><span class="sxs-lookup"><span data-stu-id="bdec8-158">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="bdec8-159">Dit is het belangrijkste naslagonderwerp voor het gebruik van Azure Data Factory met Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bdec8-159">This is the core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="bdec8-160">Deze onderwerpen bevatten gedetailleerde informatie over Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="bdec8-160">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="bdec8-161">De informatie gaat over Azure SQL Database of HDInsight, maar is ook van toepassing op Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bdec8-161">They discuss Azure SQL Database or HDInsight, but the information also applies to Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="bdec8-162">[Zelfstudie: aan de slag met Azure Data Factory][Tutorial: Get started with Azure Data Factory] Dit is de belangrijkste zelfstudie voor het verwerken van gegevens met Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="bdec8-162">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is the core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="bdec8-163">In deze zelfstudie maakt u uw eerste pijplijn voor het maandelijks transformeren en analyseren van weblogboeken met behulp van HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bdec8-163">In this tutorial, you will build your first pipeline that uses HDInsight to transform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="bdec8-164">Opmerking: deze zelfstudie omvat geen kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="bdec8-164">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="bdec8-165">[Zelfstudie: gegevens kopiëren van Azure Storage-blob naar Azure SQL Database][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database].</span><span class="sxs-lookup"><span data-stu-id="bdec8-165">[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database].</span></span> <span data-ttu-id="bdec8-166">In deze zelfstudie maakt u een pijplijn in Azure Data Factory om gegevens te kopiëren van een Azure Storage-blob naar SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bdec8-166">In this tutorial, you create a pipeline in Azure Data Factory to copy data from Azure Storage Blob to Azure SQL Database.</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction to Azure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data to and from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
