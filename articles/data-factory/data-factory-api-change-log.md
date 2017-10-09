---
title: aaaData Factory - logbestand voor .NET API | Microsoft Docs
description: Beschrijft de grote wijzigingen, functie toevoegingen, oplossingen voor problemen enzovoort... in een specifieke versie van .NET API voor hello Azure Data Factory.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8208271b-7f4c-4214-b665-d2ff503c4470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: spelluru
ms.openlocfilehash: 1d44b45c3dc8f9d483d1f1cef7068edacc610932
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---net-api-change-log"></a>Azure Data Factory - logbestand voor .NET API
In dit artikel bevat informatie over wijzigingen tooAzure Data Factory SDK in een specifieke versie. U vindt de nieuwste NuGet-pakket Hallo voor Azure Data Factory [hier](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories)

## <a name="version-4110"></a>Versie 4.11.0
Functie toevoegingen:

* Hallo zijn volgende gekoppelde servicetypen toegevoegd:
  * [OnPremisesMongoDbLinkedService](https://msdn.microsoft.com/library/mt765129.aspx)
  * [AmazonRedshiftLinkedService](https://msdn.microsoft.com/library/mt765121.aspx)
  * [AwsAccessKeyLinkedService](https://msdn.microsoft.com/library/mt765144.aspx)
* Hallo volgende gegevensset typen zijn toegevoegd:
  * [MongoDbCollectionDataset](https://msdn.microsoft.com/library/mt765145.aspx)
  * [AmazonS3Dataset](https://msdn.microsoft.com/library/mt765112.aspx)
* Hallo volgende kopiëren bron typen zijn toegevoegd:
  * [MongoDbSource](https://msdn.microsoft.com/library/mt765123.aspx)

## <a name="version-4100"></a>Versie 4.10.0
* Hallo volgende optionele eigenschappen zijn tooTextFormat toegevoegd:
  * [SkipLineCount](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.skiplinecount.aspx)
  * [FirstRowAsHeader](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.firstrowasheader.aspx)
  * [TreatEmptyAsNull](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.treatemptyasnull.aspx)
* Hallo zijn volgende gekoppelde servicetypen toegevoegd:
  * [OnPremisesCassandraLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandralinkedservice.aspx)
  * [SalesforceLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.salesforcelinkedservice.aspx)
* Hallo volgende gegevensset typen zijn toegevoegd:
  * [OnPremisesCassandraTableDataset](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandratabledataset.aspx)
* Hallo volgende kopiëren bron typen zijn toegevoegd:
  * [CassandraSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.cassandrasource.aspx)
* Voeg [WebServiceInputs](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azuremlbatchexecutionactivity.webserviceinputs.aspx) eigenschap tooAzureMLBatchExecutionActivity
  * Meerdere web service invoer doorgegeven tooan Azure Machine Learning-experiment inschakelen

## <a name="version-491"></a>Versie 4.9.1
### <a name="bug-fix"></a>Fout-oplossing
* Afschaffen WebApi-verificatie voor [WebLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.weblinkedservice.authenticationtype.aspx).

## <a name="version-490"></a>Versie 4.9.0
### <a name="feature-additions"></a>Functie-toevoegingen
* Voeg [EnableStaging](https://msdn.microsoft.com/library/mt767916.aspx) en [StagingSettings](https://msdn.microsoft.com/library/mt767918.aspx) tooCopyActivity eigenschappen. Zie [kopie gefaseerde](data-factory-copy-activity-performance.md#staged-copy) voor meer informatie over het Hallo-functie.

### <a name="bug-fix"></a>Fout-oplossing
* Introduceert een overload van [ActivityWindowOperationExtensions.List](https://msdn.microsoft.com/library/mt767915.aspx) methode waarbij een [ActivityWindowsByActivityListParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.activitywindowsbyactivitylistparameters.aspx) exemplaar.
* Markeer [WriteBatchSize](https://msdn.microsoft.com/library/dn884293.aspx) en [WriteBatchTimeout](https://msdn.microsoft.com/library/dn884245.aspx) als optioneel in CopySink.

## <a name="version-480"></a>Versie 4.8.0
### <a name="feature-additions"></a>Functie-toevoegingen
* Hallo volgende optionele eigenschappen zijn toegevoegd tooCopy activiteit tooenable afstemming van de prestaties van de kopie van type:
  * [ParallelCopies](https://msdn.microsoft.com/library/mt767910.aspx)
  * [CloudDataMovementUnits](https://msdn.microsoft.com/library/mt767912.aspx)

## <a name="version-470"></a>Versie 4.7.0
### <a name="feature-additions"></a>Functie-toevoegingen
* Nieuwe StorageFormat type toegevoegd [OrcFormat](https://msdn.microsoft.com/library/mt723391.aspx) toocopy bestanden typt in geoptimaliseerde rij kolomindeling (ORC).
* Voeg [AllowPolyBase](https://msdn.microsoft.com/library/mt723396.aspx) en PolyBaseSettings eigenschappen tooSqlDWSink.
  * Hallo-gebruik van PolyBase toocopy gegevens ingeschakeld in SQL Data Warehouse.

## <a name="version-461"></a>Versie 4.6.1
### <a name="bug-fixes"></a>Oplossingen voor problemen
* HTTP-aanvraag voor het aanbieden van activiteit windows corrigeert.
  * Verwijdert Hallo Resourcegroepnaam en Hallo data factory-naam van de aanvraaglading Hallo.

## <a name="version-460"></a>Versie 4.6.0
### <a name="feature-additions"></a>Functie-toevoegingen
* Hallo volgende eigenschappen zijn toegevoegd te[PipelineProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties_properties.aspx):
  * [PipelineMode](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.pipelinemode.aspx)
  * [ExpirationTime](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.expirationtime.aspx)
  * [Gegevenssets](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.datasets.aspx)
* Hallo volgende eigenschappen zijn toegevoegd te[PipelineRuntimeInfo](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.aspx):
  * [PipelineState](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.pipelinestate.aspx)
* Nieuw toegevoegd [StorageFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.storageformat.aspx) type [JsonFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.jsonformat.aspx) toodefine gegevenssets waarvan de gegevens in JSON-indeling is type.

## <a name="version-450"></a>Versie 4.5.0
### <a name="feature-additions"></a>Functie-toevoegingen
* Toegevoegd [bewerkingen voor activiteitvenster](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.activitywindowoperationsextensions.aspx).
  * Methoden tooretrieve activiteit windows toegevoegd met filters op basis van Hallo Entiteitstypen (dat wil zeggen, data Factory, gegevenssets, pijplijnen en activiteiten).
* Hallo zijn volgende gekoppelde servicetypen toegevoegd:
  * [ODataLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odatalinkedservice.aspx), [WebLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.weblinkedservice.aspx)
* Hallo volgende gegevensset typen zijn toegevoegd:
  * [ODataResourceDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odataresourcedataset.aspx), [WebTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.webtabledataset.aspx)
* Hallo volgende kopiëren bron typen zijn toegevoegd:     
  * [WebSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.websource.aspx)

## <a name="version-440"></a>Versie 4.4.0
### <a name="feature-additions"></a>Functie-toevoegingen
* Hallo volgende gekoppelde-servicetype is toegevoegd als gegevensbronnen en de sinks voor de activiteiten kopiëren:
  * [AzureStorageSasLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azurestoragesaslinkedservice.aspx). Zie [Azure Storage Linked Service SAS](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) voor conceptuele informatie en voorbeelden.

## <a name="version-430"></a>Versie 4.3.0
### <a name="feature-additions"></a>Functie-toevoegingen
* na de gekoppelde service typen haven Hallo zijn toegevoegd als gegevensbronnen voor de activiteiten kopiëren:
  * [HdfsLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.hdfslinkedservice.aspx). Zie [verplaatsen van gegevens uit HDFS gebruik Data Factory](data-factory-hdfs-connector.md) voor conceptuele informatie en voorbeelden.
  * [OnPremisesOdbcLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisesodbclinkedservice.aspx). Zie [verplaatsen van gegevens van ODBC-gegevensarchieven met behulp van Azure Data Factory](data-factory-odbc-connector.md) voor conceptuele informatie en voorbeelden.

## <a name="version-420"></a>Versie 4.2.0
### <a name="feature-additions"></a>Functie-toevoegingen
* Hallo nieuw activiteitstype volgen is toegevoegd: [AzureMLUpdateResourceActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremlupdateresourceactivity.aspx). Zie voor meer informatie over de activiteit Hallo [modellen van Azure ML bijwerken met behulp van Hallo Update Resourceactiviteit](data-factory-azure-ml-batch-execution-activity.md).
* Een nieuwe optionele eigenschap [updateResourceEndpoint](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.updateresourceendpoint.aspx) toohello is toegevoegd [AzureMLLinkedService klasse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.aspx).
* [LongRunningOperationInitialTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationinitialtimeout.aspx) en [LongRunningOperationRetryTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationretrytimeout.aspx) eigenschappen toegevoegd toohello [DataFactoryManagementClient](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.aspx) klasse.
* Configuratie van Hallo time-outs voor client-aanroepen toohello Data Factory-service toestaan.

## <a name="version-410"></a>Versie 4.1.0
### <a name="feature-additions"></a>Functie-toevoegingen
* Hallo zijn volgende gekoppelde servicetypen toegevoegd:
  * [AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx)
  * [AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx)
* Hallo volgende activiteitstypen zijn toegevoegd:
  * [DataLakeAnalyticsUSQLActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datalakeanalyticsusqlactivity.aspx)
* Hallo volgende gegevensset typen zijn toegevoegd:
  * [AzureDataLakeStoreDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoredataset.aspx)
* Hallo zijn volgende bron- en sink-typen voor de Kopieeractiviteit toegevoegd:
  * [AzureDataLakeStoreSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresource.aspx)
  * [AzureDataLakeStoreSink](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresink.aspx)

## <a name="version-401"></a>Versie 4.0.1
### <a name="breaking-changes"></a>Wijzigingen op te splitsen
Hallo volgende klassen hebben gekregen. Hallo nieuwe namen zijn oorspronkelijke namen van klassen Hallo voordat 4.0.0 loslaat.

| Naam in 4.0.0 | Naam in 4.0.1 |
|:--- |:--- |
| AzureSqlDataWarehouseDataset |[AzureSqlDataWarehouseTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuresqldatawarehousetabledataset.aspx) |
| AzureSqlDataset |[AzureSqlTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuresqltabledataset.aspx) |
| AzureDataset |[AzureTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuretabledataset.aspx) |
| OracleDataset |[OracleTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.oracletabledataset.aspx) |
| RelationalDataset |[RelationalTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.relationaltabledataset.aspx) |
| SqlServerDataset |[SqlServerTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.sqlservertabledataset.aspx) |

## <a name="version-400"></a>Versie 4.0.0
### <a name="breaking-changes"></a>Wijzigingen op te splitsen
* Hallo na klassen/interfaces zijn gewijzigd.

| Oude naam | Nieuwe naam |
|:--- |:--- |
| ITableOperations |[IDatasetOperations](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.idatasetoperations.aspx) |
| Tabel |[Gegevensset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.dataset.aspx) |
| TableProperties |[DatasetProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetproperties.aspx) |
| TableTypeProprerties |[DatasetTypeProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasettypeproperties.aspx) |
| TableCreateOrUpdateParameters |[DatasetCreateOrUpdateParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdateparameters.aspx) |
| TableCreateOrUpdateResponse |[DatasetCreateOrUpdateResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdateresponse.aspx) |
| TableGetResponse |[DatasetGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetgetresponse.aspx) |
| TableListResponse |[DatasetListResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetlistresponse.aspx) |
| CreateOrUpdateWithRawJsonContentParameters |[DatasetCreateOrUpdateWithRawJsonContentParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdatewithrawjsoncontentparameters.aspx) |

* Hallo **lijst** methoden nu wisselbare resultaten geretourneerd. Als antwoord Hallo een niet-lege bevat **NextLink** eigenschap, client-toepassing hello moet toocontinue ophalen Hallo volgende pagina totdat alle pagina's zijn geretourneerd.  Hier volgt een voorbeeld:

    ```csharp
    PipelineListResponse response = client.Pipelines.List("ResourceGroupName", "DataFactoryName");
    var pipelines = new List<Pipeline>(response.Pipelines);

    string nextLink = response.NextLink;
    while (!string.IsNullOrEmpty(nextLink))
    {
        PipelineListResponse nextResponse = client.Pipelines.ListNext(nextLink);
        pipelines.AddRange(nextResponse.Pipelines);

        nextLink = nextResponse.NextLink;
    }
    ```
* **Lijst** pijplijn API retourneert alleen Hallo samenvatting van een pijplijn in plaats van de volledige gegevens. Activiteiten in een pijplijn samenvatting bevatten bijvoorbeeld alleen naam en type.

### <a name="feature-additions"></a>Functie-toevoegingen
* Hallo [SqlDWSink](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsink.aspx) klasse ondersteunt twee nieuwe eigenschappen **SliceIdentifierColumnName** en **SqlWriterCleanupScript**, toosupport idempotent kopie tooAzure SQL-gegevens Het magazijn. Zie Hallo [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md) artikel voor meer informatie over deze eigenschappen.
* We bieden nu ondersteuning opgeslagen procedure gegevensbronnen voor Azure SQL Database en Azure SQL Data Warehouse uitgevoerd als onderdeel van Hallo Kopieeractiviteit. Hallo [SqlSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqlsource.aspx) en [SqlDWSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsource.aspx) klassen Hallo volgende eigenschappen hebben: **SqlReaderStoredProcedureName** en **StoredProcedureParameters** . Zie Hallo [Azure SQL Database](data-factory-azure-sql-connector.md#sqlsource) en [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#sqldwsource) artikelen op Azure.com voor meer informatie over deze eigenschappen.  
