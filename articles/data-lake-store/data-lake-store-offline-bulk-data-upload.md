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
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a>Hello Azure Import/Export-service voor offline-exemplaar van data Lake Store voor tooData gebruiken
In dit artikel leert u hoe toocopy grote gegevenssets (> 200 GB) in een Azure Data Lake Store met behulp van methoden van offline-exemplaar, zoals Hallo [Azure Import/Export-service](../storage/common/storage-import-export-service.md). Hallo bestand dat wordt gebruikt als voorbeeld in dit artikel is bijzonder 339,420,860,416 bytes of ongeveer 319 GB op schijf. Laten we dit bestand 319GB.tsv aanroepen.

Hello Azure Import/Export-service kunt u grote hoeveelheden gegevens meer veilig tooAzure Blob-opslag door back-ups van harde schijf tooan Azure-datacenter stations tootransfer.

## <a name="prerequisites"></a>Vereisten
Voordat u begint, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Een Azure storage-account**.
* **Een Azure Data Lake Store-account**. Voor instructies over het toocreate één, Zie [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md)

## <a name="preparing-hello-data"></a>Hallo gegevens voorbereiden
Voordat u Hallo Import/Export-service, einde Hallo gegevens bestand toobe overgedragen **in kopieën die kleiner zijn dan 200 GB zijn** in grootte. hulpprogramma voor het importeren van Hallo werkt niet met bestanden die groter zijn dan 200 GB. In deze zelfstudie Splits we Hallo-bestand in segmenten van 100 GB. U kunt dit doen met behulp van [Cygwin](https://cygwin.com/install.html). Cygwin biedt ondersteuning voor Linux-opdrachten. In dit geval gebruiken Hallo volgende opdracht:

    split -b 100m 319GB.tsv

Hallo split-bewerking maakt bestanden Hello namen te volgen.

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a>Bereid u voor schijven met gegevens
Volg de instructies in Hallo [hello Azure Import/Export-service met](../storage/common/storage-import-export-service.md) (onder Hallo **voorbereiden van uw schijven** sectie) tooprepare uw harde schijven. Hier volgt Hallo algemene volgorde:

1. Schaft u een harde schijf die voldoet aan Hallo vereiste toobe gebruikt voor hello Azure Import/Export-service.
2. Identificeer een Azure storage-account waarnaar de Hallo gegevens worden gekopieerd, nadat deze verzonden toohello Azure-datacenter is.
3. Gebruik Hallo [Azure-hulpprogramma voor importeren/exporteren](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), een opdrachtregelprogramma. Hier volgt een voorbeeld-fragment dat toont hoe toouse Hallo hulpprogramma.

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    Zie [hello Azure Import/Export-service met](../storage/common/storage-import-export-service.md) voor meer voorbeelden codefragmenten.
4. Hallo voorgaande opdracht maakt een journaal-bestand op Hallo opgegeven locatie. Gebruik dit logboek bestand toocreate een import-taak uit Hallo [klassieke Azure-portal](https://manage.windowsazure.com).

## <a name="create-an-import-job"></a>Een importtaak maken
U kunt nu een import-taak maken met behulp van instructies Hallo in [hello Azure Import/Export-service met](../storage/common/storage-import-export-service.md) (onder Hallo **Hallo Import-taak maken** sectie). Voor deze taak importeren met andere details, bieden ook Hallo journal-bestand is gemaakt tijdens het voorbereiden van Hallo harde schijven.

## <a name="physically-ship-hello-disks"></a>Hallo schijven fysiek verzenden
U kunt nu fysiek Hallo schijven tooan Azure-datacenter verzenden. Daar Hallo gegevens gekopieerd via toohello Azure Storage blobs die u hebt opgegeven tijdens het maken van Hallo import-taak. Ook bij het maken van de taak Hallo kunt als u hebt gekozen tooprovide hello later traceringsgegevens u nu teruggaan tooyour import-taak en update Hallo volgnummer.

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a>Gegevens kopiëren van Azure Storage blobs tooAzure Data Lake Store
Na het Hallo-status van Hallo ziet import-taak u dat deze voltooid, kunt u controleren of Hallo gegevens zijn beschikbaar in hello Azure Storage blobs die had opgegeven. Vervolgens kunt u een aantal methoden toomove dat gegevens van Hallo blobs tooAzure Data Lake Store. Zie voor alle beschikbare opties voor het uploaden van gegevens hello, [ophalen van gegevens in Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).

In deze sectie bieden we u Hallo JSON definities dat u een Azure Data Factory-pijplijn toocreate gebruiken kunt voor het kopiëren van gegevens. U kunt deze JSON-definities van Hallo [Azure-portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), of [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), of [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).

### <a name="source-linked-service-azure-storage-blob"></a>Bron gekoppelde service (Azure Storage-blob)
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

### <a name="target-linked-service-azure-data-lake-store"></a>Doel van de gekoppelde service (Azure Data Lake Store)
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
### <a name="input-data-set"></a>Invoer gegevensset
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
### <a name="output-data-set"></a>Gegevensset voor uitvoer
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
### <a name="pipeline-copy-activity"></a>Pijplijn (kopieeractiviteit)
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
Zie voor meer informatie [verplaatsen van gegevens van Azure Storage-blob tooAzure Data Lake Store met Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a>Hallo-gegevensbestanden in Azure Data Lake Store Reconstrueer
We met een bestand dat is 319 GB en moest worden deze in kleinere bestanden zodat deze kan worden overgedragen met behulp van hello Azure Import/Export-service is gestart. Nu dat Hallo gegevens zich in Azure Data Lake Store, kunnen we Hallo tooits oorspronkelijke bestandsgrootte opnieuw opgebouwd. U kunt hello Azure PowerShell cmldts toodo dus volgen.

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

## <a name="next-steps"></a>Volgende stappen
* [Gegevens in Data Lake Store beveiligen](data-lake-store-secure-data.md)
* [Azure Data Lake Analytics gebruiken met Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight gebruiken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
