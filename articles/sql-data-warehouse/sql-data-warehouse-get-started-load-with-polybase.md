---
title: aaaPolyBase in SQL Data Warehouse-zelfstudie | Microsoft Docs
description: Meer informatie over wat PolyBase is en hoe toouse voor datawarehousescenario's.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 0a0103b4-ddd6-4d1e-87be-4965d6e99f3f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/01/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 3e680ec407c1d920dd59ea922b82c9208b5e9a84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a>Gegevens laden met PolyBase in SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

Deze zelfstudie laat zien hoe tooload gegevens in SQL Data Warehouse met AzCopy en PolyBase. Aan het einde kunt u:

* AzCopy toocopy gegevens tooAzure blob storage gebruiken
* Maken van databaseobjecten toodefine Hallo gegevens
* Uitvoeren van een T-SQL-query tooload Hallo gegevens

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>Vereisten
toostep voor deze zelfstudie, moet u

* Een SQL Data Warehouse-database.
* Een Azure-opslagaccount van het type standaard lokaal redundante opslag (Standard Locally Redundant Storage (Standard-LRS)), standaard geografisch redundante opslag (Standard Geo-Redundant Storage (Standard-GRS)) of standaard geografisch redundante opslag met leestoegang (Standard Read-Access Geo-Redundant Storage (Standard-RAGRS)).
* AzCopy-opdrachtregelprogramma. Download en installeer Hallo [meest recente versie van AzCopy] [ latest version of AzCopy] die is geïnstalleerd met Hallo hulpprogramma's voor Microsoft Azure Storage.
  
    ![Hulpprogramma's van Azure Storage](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a>Stap 1: Voorbeeld gegevens tooAzure blob-opslag toevoegen
Volgorde tooload gegevens moeten we tooput voorbeeldgegevens in een Azure blob storage. In deze stap vult u een Azure Storage Blob met voorbeeldgegevens. Later, we gebruiken PolyBase tooload deze voorbeeldgegevens in uw SQL Data Warehouse-database.

### <a name="a-prepare-a-sample-text-file"></a>A. Een voorbeeldtekstbestand voorbereiden
een voorbeeldtekstbestand tooprepare:

1. Open Kladblok en kopieer Hallo regels met gegevens in een nieuw bestand te volgen. Sla dit tooyour lokale tijdelijke map op als % temp%\DimDate2.txt.

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="b-find-your-blob-service-endpoint"></a>B. Het eindpunt van de blob-service zoeken
toofind uw blobeindpunt-service:

1. Selecteer in Azure Portal Hallo **Bladeren** > **Opslagaccounts**.
2. Klik op Hallo gewenste toouse storage-account.
3. Klik in de blade Opslagaccount Hallo op Blobs.
   
    ![Klik op Blobs.](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. Sla de URL van het eindpunt van de blob-service op voor later gebruik.
   
    ![Eindpunt van blob-service](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a>C. Uw Azure-opslagsleutel zoeken
toofind uw Azure-opslagsleutel:

1. Selecteer in Azure Portal Hallo, **Bladeren** > **Opslagaccounts**.
2. Klik op de gewenste toouse Hallo-opslagaccount.
3. Selecteer **Alle instellingen** > **Toegangssleutels**.
4. Klik op Hallo kopie vak toocopy een van uw toegang tot sleutels toohello Klembord.
   
    ![Azure-opslagsleutel kopiëren](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a>D. Hallo voorbeeld bestand tooAzure blob-opslag kopiëren
toocopy de tooAzure blob-opslag van gegevens:

1. Open een opdrachtprompt en wijzig de mappen toohello AzCopy-installatiemap. Deze opdracht wijzigt toohello standaardinstallatiemap op een 64-bits Windows-client.
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. Hallo opdrachtbestand tooupload Hallo volgende worden uitgevoerd. Geef de URL van het eindpunt van de blob-service op voor <blob service endpoint URL> en de Azure-toegangssleutel voor <azure_storage_account_key>.
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

Zie ook [aan de slag met het AzCopy-opdrachtregelprogramma Hallo][Getting Started with hello AzCopy Command-Line Utility].

### <a name="e-explore-your-blob-storage-container"></a>E. De Blob Storage-container verkennen
geüploade tooblob opslag toosee Hallo-bestand:

1. Ga terug blade tooyour Blob-service.
2. Dubbelklik onder Containers op **datacontainer**.
3. tooexplore hello pad tooyour gegevens, klikt u op Hallo map **datedimension** en ziet u het geüploade bestand **DimDate2.txt**.
4. tooview eigenschappen, klikt u op **DimDate2.txt**.
5. Houd er rekening mee dat in Hallo blade blobeigenschappen kunt u downloaden of Hallo bestand verwijderen.
   
    ![Azure Storage-blob weergeven](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a>Stap 2: Een externe tabel voor Hallo voorbeeldgegevens maken
In deze sectie maken we een externe tabel waarin de voorbeeldgegevens Hallo.

PolyBase gebruikt externe tabellen tooaccess gegevens in Azure blob-opslag. Aangezien het Hallo-gegevens worden niet opgeslagen in SQL Data Warehouse, verwerkt PolyBase externe verificatiegegevens toohello met behulp van een database-scoped referentie.

Hallo-voorbeeld in deze stap maakt gebruik van deze Transact-SQL-instructies toocreate een externe tabel.

* [Maken van Master Key (Transact-SQL)] [ Create Master Key (Transact-SQL)] tooencrypt Hallo geheim van de database-scoped referentie.
* [Create Database Scoped Credential (Transact-SQL)] [ Create Database Scoped Credential (Transact-SQL)] toospecify verificatie-informatie voor uw Azure storage-account.
* [Create External Data Source (Transact-SQL)] [ Create External Data Source (Transact-SQL)] toospecify Hallo locatie van uw Azure-blobopslag.
* [Create External File Format (Transact-SQL)] [ Create External File Format (Transact-SQL)] toospecify Hallo indeling van uw gegevens.
* [Create External Table (Transact-SQL)] [ Create External Table (Transact-SQL)] toospecify Hallo tabeldefinitie en locatie van gegevens Hallo.

Voer deze query uit voor uw SQL Data Warehouse-database. Een externe tabel DimDate2External met de naam in Hallo dbo-schema dat toohello voorbeeldgegevens in DimDate2.txt in hello Azure blob-opslag wijst wordt gemaakt.

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication tooAzure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);


-- D: Create an external file format
-- FORMAT_TYPE: Type of file format in Azure storage (supported: DELIMITEDTEXT, RCFILE, ORC, PARQUET).
-- FORMAT_OPTIONS: Specify field terminator, string delimiter, date format etc. for delimited text files.
-- Specify DATA_COMPRESSION method if data is compressed.

CREATE EXTERNAL FILE FORMAT TextFile
WITH (
    FORMAT_TYPE = DelimitedText,
    FORMAT_OPTIONS (FIELD_TERMINATOR = ',')
);


-- E: Create hello external table
-- Specify column names and data types. This needs toomatch hello data in hello sample file.
-- LOCATION: Specify path toofile or directory that contains hello data (relative toohello blob container).
-- toopoint tooall files under hello blob container, use LOCATION='.'

CREATE EXTERNAL TABLE dbo.DimDate2External (
    DateId INT NOT NULL,
    CalendarQuarter TINYINT NOT NULL,
    FiscalQuarter TINYINT NOT NULL
)
WITH (
    LOCATION='/datedimension/',
    DATA_SOURCE=AzureStorage,
    FILE_FORMAT=TextFile
);


-- Run a query on hello external table

SELECT count(*) FROM dbo.DimDate2External;

```


In SQL Server-Objectverkenner in Visual Studio ziet u Hallo externe bestandsindeling, externe gegevensbron en Hallo DimDate2External tabel.

![Externe tabel weergeven](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a>Stap 3: gegevens laden in SQL Data Warehouse
Zodra Hallo externe tabel is gemaakt, kunt u Hallo gegevens in een nieuwe tabel laden of in een bestaande tabel invoegen.

* tooload hello gegevens in een nieuwe tabel, Voer Hallo [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instructie. Hallo nieuwe tabel hebben met de naam in de query Hallo Hallo-kolommen. de gegevenstypen Hallo van Hallo kolommen komt overeen met de Hallo-gegevenstypen in de definitie van de externe tabel Hallo.
* tooload hello gegevens in een bestaande tabel, gebruikt u Hallo [INSERT... SELECT (Transact-SQL)] [ INSERT...SELECT (Transact-SQL)] instructie.

```sql
-- Load hello data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE dbo.DimDate2
WITH
(   
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT * FROM [dbo].[DimDate2External];
```

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>Stap 4: statistieken maken voor uw zojuist geladen gegevens
SQL Data Warehouse bevat geen functionaliteit voor het automatisch maken of bijwerken van statistieken. Daarom tooachieve hoge queryprestaties, het is belangrijk toocreate statistieken op elke kolom in elke tabel na Hallo eerst laden. Het is ook belangrijk tooupdate statistieken na Hallo gegevens substantieel zijn gewijzigd.

In dit voorbeeld maakt statistieken voor één kolom op Hallo nieuwe tabel dimdate2.

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

toolearn meer, Zie [statistieken][Statistics].  

## <a name="next-steps"></a>Volgende stappen
Zie Hallo [PolyBase-handleiding] [ PolyBase guide] voor meer informatie over het ontwikkelen van een oplossing die gebruikmaakt van PolyBase.

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
[Getting Started with hello AzCopy Command-Line Utility]:../storage/common/storage-use-azcopy.md
[latest version of AzCopy]:../storage/common/storage-use-azcopy.md

<!--External references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx


[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]:https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189450.aspx
