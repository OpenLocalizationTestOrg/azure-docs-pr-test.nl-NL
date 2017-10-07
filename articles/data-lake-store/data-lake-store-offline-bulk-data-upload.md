---
title: grote hoeveelheden gegevens in Data Lake Store met behulp van offline methoden aaaUpload | Microsoft Docs
description: Gebruik Hallo AdlCopy hulpprogramma toocopy gegevens uit Azure Storage blobs tooData Lake Store
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 45321f6a-179f-4ee4-b8aa-efa7745b8eb6
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 42ef75142a26ebfab05d89614782a54c244c4bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a><span data-ttu-id="6c42e-103">Hello Azure Import/Export-service voor offline-exemplaar van data Lake Store voor tooData gebruiken</span><span class="sxs-lookup"><span data-stu-id="6c42e-103">Use hello Azure Import/Export service for offline copy of data tooData Lake Store</span></span>
<span data-ttu-id="6c42e-104">In dit artikel leert u hoe toocopy grote gegevenssets (> 200 GB) in een Azure Data Lake Store met behulp van methoden van offline-exemplaar, zoals Hallo [Azure Import/Export-service](../storage/common/storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="6c42e-104">In this article, you'll learn how toocopy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like hello [Azure Import/Export service](../storage/common/storage-import-export-service.md).</span></span> <span data-ttu-id="6c42e-105">Hallo bestand dat wordt gebruikt als voorbeeld in dit artikel is bijzonder 339,420,860,416 bytes of ongeveer 319 GB op schijf.</span><span class="sxs-lookup"><span data-stu-id="6c42e-105">Specifically, hello file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span></span> <span data-ttu-id="6c42e-106">Laten we dit bestand 319GB.tsv aanroepen.</span><span class="sxs-lookup"><span data-stu-id="6c42e-106">Let's call this file 319GB.tsv.</span></span>

<span data-ttu-id="6c42e-107">Hello Azure Import/Export-service kunt u grote hoeveelheden gegevens meer veilig tooAzure Blob-opslag door back-ups van harde schijf tooan Azure-datacenter stations tootransfer.</span><span class="sxs-lookup"><span data-stu-id="6c42e-107">hello Azure Import/Export service helps you tootransfer large amounts of data more securely tooAzure Blob storage by shipping hard disk drives tooan Azure datacenter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c42e-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6c42e-108">Prerequisites</span></span>
<span data-ttu-id="6c42e-109">Voordat u begint, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="6c42e-109">Before you begin, you must have hello following:</span></span>

* <span data-ttu-id="6c42e-110">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="6c42e-110">**An Azure subscription**.</span></span> <span data-ttu-id="6c42e-111">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6c42e-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6c42e-112">**Een Azure storage-account**.</span><span class="sxs-lookup"><span data-stu-id="6c42e-112">**An Azure storage account**.</span></span>
* <span data-ttu-id="6c42e-113">**Een Azure Data Lake Store-account**.</span><span class="sxs-lookup"><span data-stu-id="6c42e-113">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="6c42e-114">Voor instructies over het toocreate één, Zie [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="6c42e-114">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="preparing-hello-data"></a><span data-ttu-id="6c42e-115">Hallo gegevens voorbereiden</span><span class="sxs-lookup"><span data-stu-id="6c42e-115">Preparing hello data</span></span>
<span data-ttu-id="6c42e-116">Voordat u Hallo Import/Export-service, einde Hallo gegevens bestand toobe overgedragen **in kopieën die kleiner zijn dan 200 GB zijn** in grootte.</span><span class="sxs-lookup"><span data-stu-id="6c42e-116">Before using hello Import/Export service, break hello data file toobe transferred **into copies that are less than 200 GB** in size.</span></span> <span data-ttu-id="6c42e-117">hulpprogramma voor het importeren van Hallo werkt niet met bestanden die groter zijn dan 200 GB.</span><span class="sxs-lookup"><span data-stu-id="6c42e-117">hello import tool does not work with files greater than 200 GB.</span></span> <span data-ttu-id="6c42e-118">In deze zelfstudie Splits we Hallo-bestand in segmenten van 100 GB.</span><span class="sxs-lookup"><span data-stu-id="6c42e-118">In this tutorial, we split hello file into chunks of 100 GB each.</span></span> <span data-ttu-id="6c42e-119">U kunt dit doen met behulp van [Cygwin](https://cygwin.com/install.html).</span><span class="sxs-lookup"><span data-stu-id="6c42e-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span></span> <span data-ttu-id="6c42e-120">Cygwin biedt ondersteuning voor Linux-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="6c42e-120">Cygwin supports Linux commands.</span></span> <span data-ttu-id="6c42e-121">In dit geval gebruiken Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6c42e-121">In this case, use hello following command:</span></span>

    split -b 100m 319GB.tsv

<span data-ttu-id="6c42e-122">Hallo split-bewerking maakt bestanden Hello namen te volgen.</span><span class="sxs-lookup"><span data-stu-id="6c42e-122">hello split operation creates files with hello following names.</span></span>

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a><span data-ttu-id="6c42e-123">Bereid u voor schijven met gegevens</span><span class="sxs-lookup"><span data-stu-id="6c42e-123">Get disks ready with data</span></span>
<span data-ttu-id="6c42e-124">Volg de instructies in Hallo [hello Azure Import/Export-service met](../storage/common/storage-import-export-service.md) (onder Hallo **voorbereiden van uw schijven** sectie) tooprepare uw harde schijven.</span><span class="sxs-lookup"><span data-stu-id="6c42e-124">Follow hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Prepare your drives** section) tooprepare your hard drives.</span></span> <span data-ttu-id="6c42e-125">Hier volgt Hallo algemene volgorde:</span><span class="sxs-lookup"><span data-stu-id="6c42e-125">Here's hello overall sequence:</span></span>

1. <span data-ttu-id="6c42e-126">Schaft u een harde schijf die voldoet aan Hallo vereiste toobe gebruikt voor hello Azure Import/Export-service.</span><span class="sxs-lookup"><span data-stu-id="6c42e-126">Procure a hard disk that meets hello requirement toobe used for hello Azure Import/Export service.</span></span>
2. <span data-ttu-id="6c42e-127">Identificeer een Azure storage-account waarnaar de Hallo gegevens worden gekopieerd, nadat deze verzonden toohello Azure-datacenter is.</span><span class="sxs-lookup"><span data-stu-id="6c42e-127">Identify an Azure storage account where hello data will be copied after it is shipped toohello Azure datacenter.</span></span>
3. <span data-ttu-id="6c42e-128">Gebruik Hallo [Azure-hulpprogramma voor importeren/exporteren](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), een opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="6c42e-128">Use hello [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span></span> <span data-ttu-id="6c42e-129">Hier volgt een voorbeeld-fragment dat toont hoe toouse Hallo hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="6c42e-129">Here's a sample snippet that shows how toouse hello tool.</span></span>

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    <span data-ttu-id="6c42e-130">Zie [hello Azure Import/Export-service met](../storage/common/storage-import-export-service.md) voor meer voorbeelden codefragmenten.</span><span class="sxs-lookup"><span data-stu-id="6c42e-130">See [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) for more sample snippets.</span></span>
4. <span data-ttu-id="6c42e-131">Hallo voorgaande opdracht maakt een journaal-bestand op Hallo opgegeven locatie.</span><span class="sxs-lookup"><span data-stu-id="6c42e-131">hello preceding command creates a journal file at hello specified location.</span></span> <span data-ttu-id="6c42e-132">Gebruik dit logboek bestand toocreate een import-taak uit Hallo [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="6c42e-132">Use this journal file toocreate an import job from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="create-an-import-job"></a><span data-ttu-id="6c42e-133">Een importtaak maken</span><span class="sxs-lookup"><span data-stu-id="6c42e-133">Create an import job</span></span>
<span data-ttu-id="6c42e-134">U kunt nu een import-taak maken met behulp van instructies Hallo in [hello Azure Import/Export-service met](../storage/common/storage-import-export-service.md) (onder Hallo **Hallo Import-taak maken** sectie).</span><span class="sxs-lookup"><span data-stu-id="6c42e-134">You can now create an import job by using hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Create hello Import job** section).</span></span> <span data-ttu-id="6c42e-135">Voor deze taak importeren met andere details, bieden ook Hallo journal-bestand is gemaakt tijdens het voorbereiden van Hallo harde schijven.</span><span class="sxs-lookup"><span data-stu-id="6c42e-135">For this import job, with other details, also provide hello journal file created while preparing hello disk drives.</span></span>

## <a name="physically-ship-hello-disks"></a><span data-ttu-id="6c42e-136">Hallo schijven fysiek verzenden</span><span class="sxs-lookup"><span data-stu-id="6c42e-136">Physically ship hello disks</span></span>
<span data-ttu-id="6c42e-137">U kunt nu fysiek Hallo schijven tooan Azure-datacenter verzenden.</span><span class="sxs-lookup"><span data-stu-id="6c42e-137">You can now physically ship hello disks tooan Azure datacenter.</span></span> <span data-ttu-id="6c42e-138">Daar Hallo gegevens gekopieerd via toohello Azure Storage blobs die u hebt opgegeven tijdens het maken van Hallo import-taak.</span><span class="sxs-lookup"><span data-stu-id="6c42e-138">There, hello data is copied over toohello Azure Storage blobs you provided while creating hello import job.</span></span> <span data-ttu-id="6c42e-139">Ook bij het maken van de taak Hallo kunt als u hebt gekozen tooprovide hello later traceringsgegevens u nu teruggaan tooyour import-taak en update Hallo volgnummer.</span><span class="sxs-lookup"><span data-stu-id="6c42e-139">Also, while creating hello job, if you opted tooprovide hello tracking information later, you can now go back tooyour import job and update hello tracking number.</span></span>

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a><span data-ttu-id="6c42e-140">Gegevens kopiëren van Azure Storage blobs tooAzure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="6c42e-140">Copy data from Azure Storage blobs tooAzure Data Lake Store</span></span>
<span data-ttu-id="6c42e-141">Na het Hallo-status van Hallo ziet import-taak u dat deze voltooid, kunt u controleren of Hallo gegevens zijn beschikbaar in hello Azure Storage blobs die had opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6c42e-141">After hello status of hello import job shows that it's completed, you can verify whether hello data is available in hello Azure Storage blobs you had specified.</span></span> <span data-ttu-id="6c42e-142">Vervolgens kunt u een aantal methoden toomove dat gegevens van Hallo blobs tooAzure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="6c42e-142">You can then use a variety of methods toomove that data from hello blobs tooAzure Data Lake Store.</span></span> <span data-ttu-id="6c42e-143">Zie voor alle beschikbare opties voor het uploaden van gegevens hello, [ophalen van gegevens in Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="6c42e-143">For all hello available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span></span>

<span data-ttu-id="6c42e-144">In deze sectie bieden we u Hallo JSON definities dat u een Azure Data Factory-pijplijn toocreate gebruiken kunt voor het kopiëren van gegevens.</span><span class="sxs-lookup"><span data-stu-id="6c42e-144">In this section, we provide you with hello JSON definitions that you can use toocreate an Azure Data Factory pipeline for copying data.</span></span> <span data-ttu-id="6c42e-145">U kunt deze JSON-definities van Hallo [Azure-portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), of [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), of [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6c42e-145">You can use these JSON definitions from hello [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

### <a name="source-linked-service-azure-storage-blob"></a><span data-ttu-id="6c42e-146">Bron gekoppelde service (Azure Storage-blob)</span><span class="sxs-lookup"><span data-stu-id="6c42e-146">Source linked service (Azure Storage blob)</span></span>
````
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
````

### <a name="target-linked-service-azure-data-lake-store"></a><span data-ttu-id="6c42e-147">Doel van de gekoppelde service (Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="6c42e-147">Target linked service (Azure Data Lake Store)</span></span>
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' tooallow this data factory and hello activities it runs tooaccess this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from hello OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a><span data-ttu-id="6c42e-148">Invoer gegevensset</span><span class="sxs-lookup"><span data-stu-id="6c42e-148">Input data set</span></span>
````
{
    "name": "InputDataSet",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "importcontainer/vf1/"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
````
### <a name="output-data-set"></a><span data-ttu-id="6c42e-149">Gegevensset voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="6c42e-149">Output data set</span></span>
````
{
"name": "OutputDataSet",
"properties": {
  "published": false,
  "type": "AzureDataLakeStore",
  "linkedServiceName": "AzureDataLakeStoreLinkedService",
  "typeProperties": {
    "folderPath": "/importeddatafeb8job/"
    },
  "availability": {
    "frequency": "Hour",
    "interval": 1
    }
  }
}
````
### <a name="pipeline-copy-activity"></a><span data-ttu-id="6c42e-150">Pijplijn (kopieeractiviteit)</span><span class="sxs-lookup"><span data-stu-id="6c42e-150">Pipeline (copy activity)</span></span>
````
{
    "name": "CopyImportedData",
    "properties": {
        "description": "Pipeline with copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "AzureDataLakeStoreSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataSet"
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
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity"
            }
        ],
        "start": "2016-02-08T22:00:00Z",
        "end": "2016-02-08T23:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
````
<span data-ttu-id="6c42e-151">Zie voor meer informatie [verplaatsen van gegevens van Azure Storage-blob tooAzure Data Lake Store met Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span><span class="sxs-lookup"><span data-stu-id="6c42e-151">For more information, see [Move data from Azure Storage blob tooAzure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span>

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a><span data-ttu-id="6c42e-152">Hallo-gegevensbestanden in Azure Data Lake Store Reconstrueer</span><span class="sxs-lookup"><span data-stu-id="6c42e-152">Reconstruct hello data files in Azure Data Lake Store</span></span>
<span data-ttu-id="6c42e-153">We met een bestand dat is 319 GB en moest worden deze in kleinere bestanden zodat deze kan worden overgedragen met behulp van hello Azure Import/Export-service is gestart.</span><span class="sxs-lookup"><span data-stu-id="6c42e-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using hello Azure Import/Export service.</span></span> <span data-ttu-id="6c42e-154">Nu dat Hallo gegevens zich in Azure Data Lake Store, kunnen we Hallo tooits oorspronkelijke bestandsgrootte opnieuw opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="6c42e-154">Now that hello data is in Azure Data Lake Store, we can reconstruct hello file tooits original size.</span></span> <span data-ttu-id="6c42e-155">U kunt hello Azure PowerShell cmldts toodo dus volgen.</span><span class="sxs-lookup"><span data-stu-id="6c42e-155">You can use hello following Azure PowerShell cmldts toodo so.</span></span>

````
# Login tooour account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch toohello subscription you want toowork with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  hello files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a><span data-ttu-id="6c42e-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6c42e-156">Next steps</span></span>
* [<span data-ttu-id="6c42e-157">Gegevens in Data Lake Store beveiligen</span><span class="sxs-lookup"><span data-stu-id="6c42e-157">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="6c42e-158">Azure Data Lake Analytics gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="6c42e-158">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="6c42e-159">Azure HDInsight gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="6c42e-159">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
