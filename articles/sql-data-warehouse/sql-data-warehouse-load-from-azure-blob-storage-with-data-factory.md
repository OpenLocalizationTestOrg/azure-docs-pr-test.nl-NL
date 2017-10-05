---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: Gegevens uit Azure blob-opslag laden in Azure SQL Data Warehouse (Azure Data Factory) | Microsoft Docs
description: Informatie over het laden van gegevens met Azure Data Factory
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 689fb02e-eb98-4f7c-81e6-6c1d22d53901
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: barbkess
ms.custom: loading
ms.openlocfilehash: ca8bdfc21582253e8709a33eb624547fed4461d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-azure-blob-storage-into-azure-sql-data-warehouse-azure-data-factory"></a><span data-ttu-id="deaa0-103">Gegevens uit Azure Blob-opslag laden in Azure SQL Data Warehouse (Azure Data Factory)</span><span class="sxs-lookup"><span data-stu-id="deaa0-103">Load data from Azure blob storage into Azure SQL Data Warehouse (Azure Data Factory)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="deaa0-104">Data Factory</span><span class="sxs-lookup"><span data-stu-id="deaa0-104">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="deaa0-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="deaa0-105">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

 <span data-ttu-id="deaa0-106">In deze zelfstudie ziet u hoe u een pijplijn maakt in Azure Data Factory om gegevens te verplaatsen van een Azure Storage-blob naar SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="deaa0-106">This tutorial shows you how to create a pipeline in Azure Data Factory to move data from Azure Storage Blob to SQL Data Warehouse.</span></span> <span data-ttu-id="deaa0-107">Met deze stappen bewerkstelligt u het volgende:</span><span class="sxs-lookup"><span data-stu-id="deaa0-107">With the following steps you will:</span></span>

* <span data-ttu-id="deaa0-108">U stelt voorbeeldgegevens in een Azure Storage-blob in.</span><span class="sxs-lookup"><span data-stu-id="deaa0-108">Set-up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="deaa0-109">U verbindt resources met Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="deaa0-109">Connect resources to Azure Data Factory.</span></span>
* <span data-ttu-id="deaa0-110">U maakt een pijplijn om gegevens te verplaatsen van opslag-blobs naar SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="deaa0-110">Create a pipeline to move data from Storage Blobs to SQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="deaa0-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="deaa0-111">Before you begin</span></span>
<span data-ttu-id="deaa0-112">Zie [Inleiding tot Azure Data Factory][Introduction to Azure Data Factory] om vertrouwd te raken met Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="deaa0-112">To familiarize yourself with Azure Data Factory, see [Introduction to Azure Data Factory][Introduction to Azure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="deaa0-113">Resources maken of identificeren</span><span class="sxs-lookup"><span data-stu-id="deaa0-113">Create or identify resources</span></span>
<span data-ttu-id="deaa0-114">Voordat u met deze zelfstudie begint, moet u beschikken over de volgende resources.</span><span class="sxs-lookup"><span data-stu-id="deaa0-114">Before starting this tutorial, you need to have the following resources.</span></span>

* <span data-ttu-id="deaa0-115">**Azure Storage-blob**: in deze zelfstudie wordt een Azure Storage-blob gebruikt als gegevensbron voor de Azure Data Factory-pijplijn, dus u hebt er een nodig om de voorbeeldgegevens in op te slaan.</span><span class="sxs-lookup"><span data-stu-id="deaa0-115">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as the data source for the Azure Data Factory pipeline, and so you need to have one available to store the sample data.</span></span> <span data-ttu-id="deaa0-116">Als u nog geen opslagaccount hebt, raadpleegt u [Een opslagaccount maken][Create a storage account].</span><span class="sxs-lookup"><span data-stu-id="deaa0-116">If you don't have one already, learn how to [Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="deaa0-117">**SQL Data Warehouse**: in deze zelfstudie worden de gegevens uit een Azure Storage-blob verplaatst naar SQL Data Warehouse. Hiervoor moet een datawarehouse online zijn waarin de voorbeeldgegevens van AdventureWorksDW zijn geladen.</span><span class="sxs-lookup"><span data-stu-id="deaa0-117">**SQL Data Warehouse**: This tutorial moves the data from Azure Storage Blob to  SQL Data Warehouse and so need to have a data warehouse online that is loaded with the AdventureWorksDW sample data.</span></span> <span data-ttu-id="deaa0-118">Als u nog geen datawarehouse hebt, kunt u [er een inrichten][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="deaa0-118">If you do not already have a data warehouse, learn how to [provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="deaa0-119">Als u wel een datawarehouse hebt, maar u dit nog niet hebt ingericht met de voorbeeldgegevens, kunt u [het handmatig laden][Load sample data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="deaa0-119">If you have a data warehouse but didn't provision it with the sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="deaa0-120">**Azure Data Factory**: de daadwerkelijke laadbewerking wordt voltooid door Azure Data Factory en dus moet u beschikken over een die u gebruiken kunt voor het bouwen van de data movement pijplijn. Als u niet al hebt, informatie over het maken van een in stap 1 van [aan de slag met Azure Data Factory (Data Factory-Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span><span class="sxs-lookup"><span data-stu-id="deaa0-120">**Azure Data Factory**: Azure Data Factory will complete the actual load and so you need to have one that you can use to build the data movement pipeline.If you don't have one already, learn how to create one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="deaa0-121">**AZCopy**: u hebt AZCopy nodig om de voorbeeldgegevens van de lokale client te kopiëren naar uw Azure Storage-blob.</span><span class="sxs-lookup"><span data-stu-id="deaa0-121">**AZCopy**: You need AZCopy to copy the sample data from your local client to your Azure Storage Blob.</span></span> <span data-ttu-id="deaa0-122">Zie de [documentatie van AZCopy][AZCopy documentation] voor installatie-instructies.</span><span class="sxs-lookup"><span data-stu-id="deaa0-122">For install instructions, see the [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-to-azure-storage-blob"></a><span data-ttu-id="deaa0-123">Stap 1: Voorbeeldgegevens kopiëren naar Azure Storage-blob</span><span class="sxs-lookup"><span data-stu-id="deaa0-123">Step 1: Copy sample data to Azure Storage Blob</span></span>
<span data-ttu-id="deaa0-124">Als u beschikt over alle benodigde onderdelen, bent u klaar om de voorbeeldgegevens te kopiëren naar uw Azure Storage-blob.</span><span class="sxs-lookup"><span data-stu-id="deaa0-124">Once you have all of the pieces ready, you are ready to copy sample data to your Azure Storage Blob.</span></span>

1. <span data-ttu-id="deaa0-125">[Voorbeeldgegevens downloaden][Download sample data].</span><span class="sxs-lookup"><span data-stu-id="deaa0-125">[Download sample data][Download sample data].</span></span> <span data-ttu-id="deaa0-126">Hiermee worden nog eens drie jaar aan verkoopgegevens toegevoegd aan de voorbeeldgegevens van AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="deaa0-126">This data will add another three years of sales data to your AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="deaa0-127">Gebruik deze AZCopy-opdracht om de drie jaar aan gegevens naar uw Azure Storage-blob te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="deaa0-127">Use this AZCopy command to copy the three years of data to your Azure Storage Blob.</span></span>

````
AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
````


## <a name="step-2-connect-resources-to-azure-data-factory"></a><span data-ttu-id="deaa0-128">Stap 2: resources verbinden met Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="deaa0-128">Step 2: Connect resources to Azure Data Factory</span></span>
<span data-ttu-id="deaa0-129">Nu de gegevens zijn opgeslagen, kunt u de Azure Data Factory-pijplijn maken om de gegevens te kunnen verplaatsen van de Azure Blob-opslag naar SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="deaa0-129">Now that the data is in place we can create the Azure Data Factory pipeline to move the data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="deaa0-130">Open [Azure Portal][Azure portal] en selecteer uw gegevensfactory in het menu aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="deaa0-130">To get started, open the [Azure portal][Azure portal] and select your data factory from the left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="deaa0-131">Stap 2.1: gekoppelde service maken</span><span class="sxs-lookup"><span data-stu-id="deaa0-131">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="deaa0-132">Koppel uw Azure-opslagaccount en SQL Data Warehouse aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="deaa0-132">Link your Azure storage account and SQL Data Warehouse to your data factory.</span></span>  

1. <span data-ttu-id="deaa0-133">Start het registratieproces door te klikken op de sectie Gekoppelde services van uw gegevensfactory en klik op Nieuwe gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="deaa0-133">First, begin the registration process by clicking the 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="deaa0-134">Geef een naam op voor uw Azure-opslag, selecteer Azure Storage als type en voer uw accountnaam en accountsleutel in.</span><span class="sxs-lookup"><span data-stu-id="deaa0-134">Choose a name to register your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="deaa0-135">Registreer SQL Data Warehouse door te navigeren naar de sectie Maken en implementeren, selecteer Nieuwe gegevensopslag en selecteer vervolgens Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="deaa0-135">To register SQL Data Warehouse navigate to the 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="deaa0-136">Kopieer en plak deze sjabloon erin, en vul vervolgens uw specifieke gegevens in.</span><span class="sxs-lookup"><span data-stu-id="deaa0-136">Copy and paste in this template, and then fill in your specific information.</span></span>

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

### <a name="step-22-define-the-dataset"></a><span data-ttu-id="deaa0-137">Step 2.2: de gegevensset definiëren</span><span class="sxs-lookup"><span data-stu-id="deaa0-137">Step 2.2: Define the dataset</span></span>
<span data-ttu-id="deaa0-138">Na het maken van de gekoppelde services moet u de gegevenssets definiëren.</span><span class="sxs-lookup"><span data-stu-id="deaa0-138">After creating the linked services, we will have to define the data sets.</span></span>  <span data-ttu-id="deaa0-139">Dat houdt in dat u de structuur moet definiëren van de gegevens die worden verplaatst van de opslag naar het datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="deaa0-139">Here this means defining the structure of the data that is being moved from your storage to your data warehouse.</span></span>  <span data-ttu-id="deaa0-140">U kunt meer lezen over het aanmaakproces</span><span class="sxs-lookup"><span data-stu-id="deaa0-140">You can read more about creating</span></span>

1. <span data-ttu-id="deaa0-141">Start dit proces door te navigeren naar de sectie Maken en implementeren van uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="deaa0-141">Start this process by navigating to the 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="deaa0-142">Klik achtereenvolgens op Nieuwe gegevensset en Azure Blob-opslag om uw opslag te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="deaa0-142">Click 'New dataset' and then 'Azure Blob storage' to link your storage to your data factory.</span></span>  <span data-ttu-id="deaa0-143">Met onderstaand script kunt u uw gegevens definiëren in Azure Blob-opslag:</span><span class="sxs-lookup"><span data-stu-id="deaa0-143">You can use the below script to define your data in Azure Blob storage:</span></span>

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


1. <span data-ttu-id="deaa0-144">Vervolgens definieert u de gegevensset voor SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="deaa0-144">Now we will also define our dataset for SQL Data Warehouse.</span></span>  <span data-ttu-id="deaa0-145">U begint op dezelfde manier, door te klikken op Nieuwe gegevensset. Klik vervolgens op Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="deaa0-145">We start in the same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>

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

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="deaa0-146">Stap 3: een pijplijn maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="deaa0-146">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="deaa0-147">Tot slot moet u een pijplijn in Azure Data Factory instellen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="deaa0-147">Finally, we will set-up and run the pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="deaa0-148">Dit is de bewerking waarmee de daadwerkelijke gegevensverplaatsing wordt voltooid.</span><span class="sxs-lookup"><span data-stu-id="deaa0-148">This is the operation that will complete the actual data movement.</span></span>  <span data-ttu-id="deaa0-149">Een volledig overzicht van de bewerkingen die u met SQL Data Warehouse en Azure Data Factory kunt uitvoeren, vindt u [hier][Move data to and from Azure SQL Data Warehouse using Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="deaa0-149">You can find a full view of the operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data to and from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="deaa0-150">Klik nu in de sectie Maken en implementeren op Meer opdrachten en vervolgens op Nieuwe pijplijn.</span><span class="sxs-lookup"><span data-stu-id="deaa0-150">In the 'Author and Deploy' section now click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="deaa0-151">Nadat u de pijplijn hebt gemaakt, kunt u onderstaande code gebruiken voor de gegevensoverdracht naar uw datawarehouse:</span><span class="sxs-lookup"><span data-stu-id="deaa0-151">After you create the pipeline, you can use the below code to transfer the data to your data warehouse:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="deaa0-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="deaa0-152">Next steps</span></span>
<span data-ttu-id="deaa0-153">Bekijk de volgende onderwerpen voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="deaa0-153">To learn more, start by viewing:</span></span>

* <span data-ttu-id="deaa0-154">[Leertraject voor Azure Data Factory][Azure Data Factory learning path].</span><span class="sxs-lookup"><span data-stu-id="deaa0-154">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="deaa0-155">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span><span class="sxs-lookup"><span data-stu-id="deaa0-155">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="deaa0-156">Dit is het belangrijkste naslagonderwerp voor het gebruik van Azure Data Factory met Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="deaa0-156">This is the core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="deaa0-157">Deze onderwerpen bevatten gedetailleerde informatie over Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="deaa0-157">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="deaa0-158">De informatie gaat over Azure SQL Database of HDInsight, maar is ook van toepassing op Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="deaa0-158">They discuss Azure SQL Database or HDinsight, but the information also applies to Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="deaa0-159">[Zelfstudie: aan de slag met Azure Data Factory][Tutorial: Get started with Azure Data Factory] Dit is de belangrijkste zelfstudie voor het verwerken van gegevens met Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="deaa0-159">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is the core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="deaa0-160">In deze zelfstudie maakt u uw eerste pijplijn voor het maandelijks transformeren en analyseren van weblogboeken met behulp van HDInsight.</span><span class="sxs-lookup"><span data-stu-id="deaa0-160">In this tutorial you will build your first pipeline that uses HDInsight to transform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="deaa0-161">Opmerking: deze zelfstudie omvat geen kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="deaa0-161">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="deaa0-162">[Zelfstudie: gegevens kopiëren van Azure Storage-blob naar Azure SQL Database][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database].</span><span class="sxs-lookup"><span data-stu-id="deaa0-162">[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database].</span></span> <span data-ttu-id="deaa0-163">In deze zelfstudie maakt u een pijplijn in Azure Data Factory om gegevens te kopiëren van een Azure Storage-blob naar SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="deaa0-163">In this tutorial, you will create a pipeline in Azure Data Factory to copy data from Azure Storage Blob to Azure SQL Database.</span></span>

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
