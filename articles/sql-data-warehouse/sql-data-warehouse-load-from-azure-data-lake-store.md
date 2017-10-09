---
title: aaaLoad - Azure Data Lake Store tooSQL Data Warehouse | Microsoft Docs
description: Meer informatie over hoe toouse PolyBase externe tooload gegevens van Azure Data Lake Store tabellen in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 01/25/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 50ef23b3eba5f58bc9974095f84140dc5c11fa4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a>Gegevens uit Azure Data Lake Store laden in SQL Data Warehouse
Dit document biedt u alle stappen die u moet tooload uw eigen gegevens van Azure Data Lake Store (ADLS) in SQL Data Warehouse met PolyBase.
Terwijl u kunnen toorun ad-hoc-query's over Hallo-gegevens die zijn opgeslagen in met behulp van de externe tabellen Hallo ADLS bent, als best practice raadzaam Hallo gegevens importeren in SQL Data Warehouse Hallo.
Schatting van de tijd: 10 minuten, ervan uitgaande dat er Hallo vereisten moet toocomplete.
In deze zelfstudie leert u hoe:

1. Externe Database objecten tooload van Azure Data Lake Store maken.
2. Verbinding maken met Azure Data Lake Store Directory tooan.
3. Gegevens laden in Azure SQL Data Warehouse.

## <a name="before-you-begin"></a>Voordat u begint
toorun deze zelfstudie hebt u nodig:

* Azure Active Directory-toepassing toouse voor verificatie van de Service-naar-Service. toocreate, volg [Active directory-verificatie](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)

>[!NOTE] 
> U moet Hallo client-ID en sleutel OAuth2.0 Token Endpoint-waarde van uw Active Directory-toepassing tooconnect tooyour Azure Data Lake van SQL Data Warehouse. Details voor hoe tooget deze waarden in de bovenstaande Hallo-koppeling worden.
>Opmerking voor registratie in Azure Active Directory-App Hallo toepassings-ID gebruiken als Hallo Client-ID.

* SQL Server Management Studio of SQL Server Data Tools, toodownload SSMS en verbinding maken met Zie [Query SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)

* Een Azure SQL Data Warehouse toocreate één Volg: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision

* Een Azure Data Lake Store, met of zonder versleuteling ingeschakeld. een Volg toocreate: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal




## <a name="configure-hello-data-source"></a>Hallo-gegevensbron configureren
PolyBase gebruikt T-SQL externe objecten toodefine Hallo locatie en kenmerken van Hallo externe gegevens. Hallo externe objecten worden opgeslagen in SQL Data Warehouse en verwijzing Hallo gegevens th is die extern zijn opgeslagen.


###  <a name="create-a-credential"></a>Een referentie maken
tooaccess uw Azure Data Lake opslaan, moet u een databasehoofdsleutel tooencrypt toocreate uw geheime referentie is gebruikt in de volgende stap Hallo.
Vervolgens maakt u een scoped databasereferentie die Hallo principal Servicereferenties ingesteld in AAD opslaat. Syntaxis verschilt voor mensen die u hebt gebruikt PolyBase tooconnect tooWindows Azure Storage-Blobs, houd er rekening mee dat Hallo-referentie.
tooconnect tooAzure Data Lake Store, moet u **eerste** een Azure Active Directory-toepassing maken, maakt u een toegangssleutel en Hallo toegang toohello Azure Data Lake toepassingsbron verlenen. Instrucitons tooperform deze stappen zijn gevonden [hier](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass hello client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
-- SECRET: Provide your AAD Application Service Principal key.
-- For more information on Create Database Scoped Credential: https://msdn.microsoft.com/en-us/library/mt270260.aspx

CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '<client_id>@<OAuth_2.0_Token_EndPoint>',
    SECRET = '<key>'
;

-- It should look something like this:
CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '536540b4-4239-45fe-b9a3-629f97591c0c@https://login.microsoftonline.com/42f988bf-85f1-41af-91ab-2d2cd011da47/oauth2/token',
    SECRET = 'BjdIlmtKp4Fpyh9hIvr8HJlUida/seM5kQ3EpLAmeDI='
;
```


### <a name="create-hello-external-data-source"></a>De externe gegevensbron Hallo maken
Gebruik deze [externe gegevensbron maken] [ CREATE EXTERNAL DATA SOURCE] opdracht toostore Hallo locatie van het Hallo-gegevens en Hallo type gegevens.
U vindt Hallo ADL URI in hello Azure-portal en www.portal.azure.com.

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a>Indeling van gegevens configureren
tooimport hello gegevens uit ADLS, moet u toospecify Hallo externe bestandsindeling. Deze opdracht heeft indeling-specifieke opties toodescribe uw gegevens.
Hieronder volgt een voorbeeld van een veelgebruikte bestandsindeling die een pipe gescheiden tekstbestand is.
Bekijk onze T-SQL-documentatie voor een volledige lijst met [EXTERNAL FILE FORMAT maken][CREATE EXTERNAL FILE FORMAT]

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks hello end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies hello field terminator for data of type string in hello text-delimited file.
-- DATE_FORMAT: Specifies a custom format for all date and time data that might appear in a delimited text file.
-- Use_Type_Default: Store all Missing values as NULL

CREATE EXTERNAL FILE FORMAT TextFileFormat
WITH
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE
                    )
);
```

## <a name="create-hello-external-tables"></a>Hallo externe tabellen maken
Nu u Hallo bron- en gegevensindeling hebt opgegeven, bent u klaar toocreate Hallo externe tabellen. Externe tabellen zijn interactie met externe gegevens. PolyBase gebruikt recursieve directory traversal tooread alle bestanden in alle submappen van de opgegeven in de parameter locatie Hallo Hallo-map. Hallo volgende voorbeeld toont ook hoe toocreate Hallo object. U moet toocustomize Hallo instructie toowork met Hallo gegevens hebt u in ADLS.

```sql
-- D: Create an External Table
-- LOCATION: Folder under hello ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object toouse.
-- FILE_FORMAT: Specifies which File Format Object toouse
-- REJECT_TYPE: Specifies how you want toodeal with rejected rows. Either Value or percentage of hello total
-- REJECT_VALUE: Sets hello Reject value based on hello reject type.

-- DimProduct
CREATE EXTERNAL TABLE [dbo].[DimProduct_external] (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL
)
WITH
(
    LOCATION='/DimProduct/'
,   DATA_SOURCE = AzureDataLakeStore
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

```

## <a name="external-table-considerations"></a>Externe tabel overwegingen
Het maken van een externe tabel is eenvoudig, maar er zijn enkele nuances waarvoor toobe besproken.

Laden van gegevens met PolyBase is sterk getypeerd. Dit betekent dat elke rij Hallo gegevens wordt ingenomen Hallo tabelschemadefinitie moet voldoen.
Als een bepaalde rij komt niet overeen met de schemadefinitie hello, wordt Hallo rij afgewezen op Hallo laden.

Hallo REJECT_TYPE en REJECT_VALUE opties kunt u toodefine hoeveel rijen of welk percentage van Hallo gegevens moet aanwezig zijn in de laatste tabel Hallo.
Tijdens het laden, als Hallo afwijzen waarde is bereikt, mislukt Hallo laden. meest voorkomende oorzaak van de Hallo van geweigerde rijen is een niet-overeenkomend schema definitie.
Als een kolom onjuist voor Hallo-schema van int opgegeven is het Hallo-gegevens in Hallo-bestand een tekenreeks is, wordt elke rij tooload mislukken.

Hallo locatie geeft Hallo bovenste map die u wilt dat tooread gegevens uit.
Als er zou submappen onder /DimProduct/ PolyBase in dit geval alle Hallo gegevens binnen Hallo submappen importeren.

## <a name="load-hello-data"></a>Hallo gegevens laden
tooload gegevens van Azure Data Lake Store gebruiken Hallo [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instructie. Laden met CTAS gebruikt Hallo sterk hebt getypt, externe tabel die u hebt gemaakt.

CTAS wordt een nieuwe tabel gemaakt en gevuld met Hallo resultaten van een select-instructie. CTAS definieert Hallo nieuwe tabel toohave Hallo dezelfde kolommen en gegevenstypen hebben als Hallo resultaten van Hallo-instructie SELECT. Als u alle Hallo kolommen uit een externe tabel selecteert, is Hallo nieuwe tabel een replica van Hallo kolommen en gegevenstypen in Hallo externe tabel.

In dit voorbeeld maakt er een hash-tabel gedistribueerde DimProduct aangeroepen vanuit de externe tabel DimProduct_external.

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a>Compressie columnstore optimaliseren
Standaard worden in SQL Data Warehouse Hallo tabel opgeslagen als een geclusterde columnstore-index. Nadat een belasting is voltooid, zijn aantal rijen met Hallo gegevens niet gecomprimeerd in Hallo columnstore.  Er is een aantal redenen waarom dit kan gebeuren. toolearn meer, Zie [columnstore-indexen beheren][manage columnstore indexes].

queryprestaties toooptimize en de compressie columnstore na een load opnieuw worden opgebouwd Hallo tabel tooforce hello columnstore-index toocompress alle Hallo rijen.

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

Zie voor meer informatie over het onderhouden van de columnstore-indexen Hallo [columnstore-indexen beheren] [ manage columnstore indexes] artikel.

## <a name="optimize-statistics"></a>Statistieken optimaliseren
Het is beste toocreate-statistieken voor één kolom onmiddellijk na een belasting. Er zijn enkele mogelijkheden voor statistieken. Bijvoorbeeld, als u één kolom statistieken voor elke kolom maken duurt het mogelijk een lange tijd toorebuild alle Hallo statistieken. Als u weet dat bepaalde kolommen niet toobe in query predicaten gaat, kunt u statistieken maken voor deze kolommen overslaan.

Als u toocreate statistieken voor één kolom voor elke kolom van elke tabel besluit, kunt u Hallo opgeslagen procedure-codevoorbeeld `prc_sqldw_create_stats` in Hallo [statistieken] [ statistics] artikel.

Hallo volgende voorbeeld is een goed uitgangspunt voor het maken van statistieken. Statistieken voor één kolom wordt gemaakt op elke kolom in de dimensietabel Hallo en op elke gekoppelde kolom in Hallo feitentabellen. U kunt één of meerdere kolommen statistieken tooother feit tabelkolommen altijd later op toevoegen.


## <a name="achievement-unlocked"></a>Bereiken ontgrendeld!
U hebt gegevens geladen in Azure SQL Data Warehouse. Taak geweldig!

##<a name="next-steps"></a>Volgende stappen
Laden van gegevens is Hallo eerste stap toodeveloping een datawarehouse-oplossing met behulp van SQL Data Warehouse. Bekijk onze ontwikkeling bronnen op [tabellen](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) en [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).


<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Load data into SQL Data Warehouse]: sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[manage columnstore indexes]: sql-data-warehouse-tables-index.md
[Statistics]: sql-data-warehouse-tables-statistics.md
[CTAS]: sql-data-warehouse-develop-ctas.md
[label]: sql-data-warehouse-develop-label.md

<!--MSDN references-->
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
