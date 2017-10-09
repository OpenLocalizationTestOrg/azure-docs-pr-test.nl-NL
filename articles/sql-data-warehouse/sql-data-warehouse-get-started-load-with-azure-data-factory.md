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
# <a name="load-data-with-azure-data-factory"></a>Gegevens laden met Azure Data Factory
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)  
> 
> 

Deze zelfstudie leert u hoe toocreate een pijplijn in Azure Data Factory toomove gegevens uit Azure Storage-Blob tooAzure SQL Data Warehouse. U gaat Hello stappen te volgen:

* U stelt voorbeeldgegevens in een Azure Storage-blob in.
* Verbinding maken met resources tooAzure Data Factory.
* Een pijplijn toomove gegevens van de Storage-Blobs tooSQL Data Warehouse maken.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a>Voordat u begint
toofamiliarize uzelf met Azure Data Factory, Zie [inleiding tooAzure Data Factory][Introduction tooAzure Data Factory].

### <a name="create-or-identify-resources"></a>Resources maken of identificeren
Voordat u deze zelfstudie begint, moet u toohave Hallo resources te volgen:

* **Azure Storage-Blob**: deze zelfstudie wordt Azure Storage-Blob als gegevensbron Hallo voor hello Azure Data Factory-pijplijn en dus moet u toohave één beschikbaar toostore Hallo voorbeeldgegevens. Als u niet al hebt, meer te weten hoe te[een opslagaccount maken][Create a storage account].
* **SQL Data Warehouse**: met deze zelfstudie verplaatst Hallo-gegevens uit Azure Storage-Blob te SQL Data Warehouse en kan dus moeten toohave een datawarehouse online zijn waarin van Hallo voorbeeldgegevens van AdventureWorksDW zijn geladen. Als u nog geen datawarehouse, meer te weten hoe te[inrichten][Create a SQL Data Warehouse]. Als u wel een datawarehouse hebt, maar nog niet hebt ingericht met voorbeeldgegevens hello, kunt u [handmatig laden][Load sample data into SQL Data Warehouse].
* **Azure Data Factory**: Azure Data Factory Hallo daadwerkelijke laadbewerking wordt voltooid en dus moet u toohave een waarmee u toobuild Hallo data movement pijplijn kunt. Als u niet al hebt, Ontdek hoe toocreate een in stap 1 van [aan de slag met Azure Data Factory (Data Factory-Editor)][Get started with Azure Data Factory (Data Factory Editor)].
* **AZCopy**: moet u voorbeeldgegevens van AZCopy toocopy Hallo van uw lokale client tooyour Azure Storage-Blob. Zie voor installatie-instructies Hallo [documentatie van AZCopy][AZCopy documentation].

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a>Stap 1: Voorbeeld gegevens tooAzure Storage-Blob kopiëren
Zodra u alle Hallo stukken gereed hebt, bent u klaar toocopy sample data tooyour Azure Storage-Blob.

1. [Voorbeeldgegevens downloaden][Download sample data]. Deze gegevens wordt een andere drie jaar aan verkoopgegevens tooyour voorbeeldgegevens van AdventureWorksDW toegevoegd.
2. Gebruik deze AZCopy-opdracht toocopy Hallo drie jaar aan gegevens tooyour Azure Storage-Blob.
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-tooazure-data-factory"></a>Stap 2: Verbinding maken met resources tooAzure Data Factory
Nu sprake is van Hallo gegevens we kunt maken hello Azure Data Factory-pijplijn toomove Hallo gegevens uit Azure blob storage in SQL Data Warehouse.

tooget gestart, open Hallo [Azure-portal] [ Azure portal] en selecteer uw gegevensfactory in Hallo links menu.

### <a name="step-21-create-linked-service"></a>Stap 2.1: gekoppelde service maken
Koppel uw Azure-opslagaccount en SQL Data Warehouse tooyour data factory.  

1. Eerst Hallo registratieproces beginnen door te klikken op Hallo 'Gekoppelde Services' gedeelte van uw gegevensfactory en klik op 'Nieuw gegevensarchief'. Kies een tooregister de naam van uw azure-opslag, selecteer Azure Storage als type en voer uw accountnaam en Accountsleutel.
2. tooregister SQL Data Warehouse gaat u de sectie 'Maken en implementeren' toohello, selecteert u 'Nieuw gegevensarchief' en 'Azure SQL Data Warehouse'. Kopieer en plak deze sjabloon erin, en vul vervolgens uw specifieke gegevens in.
   
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

### <a name="step-22-define-hello-dataset"></a>Step 2.2: Hallo gegevensset definiëren
Nadat het maken van Hallo gekoppelde services, moeten we toodefine Hallo gegevenssets.  Dit betekent hier Hallo structuur van Hallo-gegevens die worden verplaatst van uw opslag tooyour datawarehouse definiëren.  U kunt meer lezen over het aanmaakproces

1. Start dit proces door te navigeren toohello ' sectie maken en implementeren' van uw gegevensfactory.
2. Klik op 'Nieuwe gegevensset' Azure Blob-opslag toolink uw opslag tooyour data factory.  U kunt Hallo hieronder script toodefine uw gegevens in Azure Blob-opslag:
   
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
3. Vervolgens definieert u de gegevensset voor SQL Data Warehouse. U begint op Hallo dezelfde manier, door te klikken op 'Nieuwe gegevensset' en 'Azure SQL Data Warehouse'.
   
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

## <a name="step-3-create-and-run-your-pipeline"></a>Stap 3: een pijplijn maken en uitvoeren
Ten slotte we instellen en Hallo pijplijn in Azure Data Factory uitgevoerd.  Dit is Hallo bewerking waarmee de daadwerkelijke gegevensverplaatsing hello wordt voltooid.  U vindt een volledig overzicht van Hallo-bewerkingen die u met SQL Data Warehouse en Azure Data Factory uitvoeren kunt [hier][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].

In de sectie 'Maken en implementeren' hello, klik op 'Meer opdrachten' 'Nieuwe pijplijn'.  Nadat u Hallo pijplijn gemaakt, kunt u Hallo hieronder de code tootransfer hello tooyour gegevens datawarehouse:

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

## <a name="next-steps"></a>Volgende stappen
toolearn starten, weer te geven:

* [Leertraject voor Azure Data Factory][Azure Data Factory learning path].
* [Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector]. Dit is Hallo belangrijkste naslagonderwerp voor het gebruik van Azure Data Factory met Azure SQL Data Warehouse.

Deze onderwerpen bevatten gedetailleerde informatie over Azure Data Factory. Informatie over Azure SQL Database of HDInsight, maar Hallo-informatie is ook van toepassing tooAzure SQL Data Warehouse.

* [Zelfstudie: Aan de slag met Azure Data Factory] [ Tutorial: Get started with Azure Data Factory] dit Hallo belangrijkste zelfstudie voor het verwerken van gegevens met Azure Data Factory is. In deze zelfstudie maakt u uw eerste pijplijn die gebruikmaakt van HDInsight tootransform bouwt en analyseren van weblogboeken op maandelijkse basis. Opmerking: deze zelfstudie omvat geen kopieeractiviteit.
* [Zelfstudie: Gegevens kopiëren van Azure Storage-Blob tooAzure SQL-Database][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]. In deze zelfstudie maakt u een pijplijn in Azure Data Factory toocopy gegevens uit Azure Storage-Blob tooAzure SQL-Database.

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
