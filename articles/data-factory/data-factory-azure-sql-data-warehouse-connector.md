---
title: aaaCopy gegevens van/naar Azure SQL Data Warehouse | Microsoft Docs
description: Meer informatie over hoe toocopy gegevens van/naar Azure SQL Data Warehouse met behulp van Azure Data Factory
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a>Tooand gegevens kopiëren van Azure SQL Data Warehouse met behulp van Azure Data Factory
Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens van Azure SQL Data Warehouse. Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.  

> [!TIP]
> tooachieve optimaal, gebruikt u PolyBase tooload gegevens in Azure SQL Data Warehouse. Hallo [gebruik PolyBase tooload gegevens in Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) sectie bevat informatie. Zie voor een overzicht met een gebruiksvoorbeeld [1 TB laden in Azure SQL Data Warehouse onder 15 minuten met Azure Data Factory](data-factory-load-sql-data-warehouse.md).

## <a name="supported-scenarios"></a>Ondersteunde scenario 's
U kunt gegevens kopiëren **van Azure SQL Data Warehouse** toohello gegevensarchieven te volgen:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Gegevens kunnen worden gekopieerd van de volgende gegevensarchieven Hallo **tooAzure SQL Data Warehouse**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> Bij het kopiëren van gegevens uit SQL Server of Azure SQL Database tooAzure kunt SQL Data Warehouse, als Hallo tabel niet in het doelarchief hello, Data Factory bestaat automatisch Hallo tabel maken in SQL Data Warehouse met behulp van schema van tabel Hallo Hallo in Hallo bron gegevensopslag. Zie [automatisch maken van de tabel](#auto-table-creation) voor meer informatie.

## <a name="supported-authentication-type"></a>Ondersteund verificatietype
Azure SQL Data Warehouse connector ondersteuning voor basisverificatie.

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens worden verplaatst van een Azure SQL Data Warehouse met behulp van verschillende hulpprogramma's voor API's.

Hallo gemakkelijkste manier toocreate een pijplijn waarmee gegevens van Azure SQL Data Warehouse worden gekopieerd is wizard toouse Hallo kopiëren-gegevens. Zie [zelfstudie: gegevens laden in SQL Data Warehouse met Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.

U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:

1. Maak een **gegevensfactory**. Een gegevensfactory kan één of meer pijplijnen bevatten. 
2. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory. Bijvoorbeeld, als u gegevens uit een Azure blob storage tooan Azure SQL datawarehouse kopiëren wilt, u twee gekoppelde services toolink uw Azure storage-account en Azure SQL datawarehouse tooyour data factory. Zie voor de gekoppelde service-eigenschappen die specifiek tooAzure SQL Data Warehouse, [gekoppelde service-eigenschappen](#linked-service-properties) sectie. 
3. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking. In vermeld in de laatste stap Hallo Hallo voorbeeld maakt u een gegevensset toospecify Hallo blob-container en map met invoergegevens Hallo. En u een andere dataset toospecify Hallo tabel maken in hello Azure SQL datawarehouse die Hallo gegevens gekopieerd van de blob-opslag Hallo bevat. Zie voor eigenschappen van gegevensset die specifieke tooAzure SQL Data Warehouse, [eigenschappen van gegevensset](#dataset-properties) sectie.
4. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer. In Hallo voorbeeld eerder vermeld, gebruikt u BlobSource als een bron- en SqlDWSink als een sink voor de kopieeractiviteit Hallo. Op dezelfde manier als u van Azure SQL Data Warehouse tooAzure Blob Storage kopiëren wilt, gebruikt u SqlDWSource en BlobSink in Hallo kopieeractiviteit. Zie voor activiteitseigenschappen kopiëren die specifieke tooAzure SQL Data Warehouse, [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie. Voor informatie over hoe toouse een gegevensarchief als een bron of een sink, klikt u op Hallo-koppeling in de vorige sectie Hallo voor de gegevensopslag.

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.  Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van/naar een Azure SQL Data Warehouse zijn, [JSON voorbeelden](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) sectie van dit artikel.

Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooAzure SQL Data Warehouse zijn:

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Hallo volgende tabel bevat een beschrijving voor JSON-elementen specifieke tooAzure SQL Data Warehouse gekoppelde service.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |Hallo type eigenschap moet worden ingesteld op: **AzureSqlDW** |Ja |
| connectionString |Geef informatie tooconnect toohello Azure SQL Data Warehouse-exemplaar voor de eigenschap connectionString Hallo nodig. Alleen basisverificatie wordt ondersteund. |Ja |

> [!IMPORTANT]
> Configureer [Azure SQL Database-Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) en database-server te Hallo[Azure Services tooaccess Hallo server toestaan](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). Bovendien configureren als u gegevens tooAzure SQL Data Warehouse kopiëren wilt uit buiten Azure met inbegrip van on-premises gegevensbronnen met data factory-gateway, de juiste IP-adresbereik voor Hallo-machine dat gegevens tooAzure SQL Data Warehouse verzendt.

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).

Hallo typeProperties sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo. Hallo **typeProperties** sectie voor Hallo gegevensset van het type **AzureSqlDWTable** heeft Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |De naam van het Hallo-tabel of weergave in hello Azure SQL Data Warehouse-database die Hallo gekoppelde service verwijst. |Ja |

## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.

> [!NOTE]
> Hallo Kopieeractiviteit slechts één invoer en slechts één uitvoer produceert.

Terwijl de eigenschappen die beschikbaar zijn in Hallo typeProperties gedeelte van de activiteit Hallo variëren met elk activiteitstype. Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.

### <a name="sqldwsource"></a>SqlDWSource
Wanneer de bron is van het type **SqlDWSource**, Hallo volgende eigenschappen beschikbaar zijn in **typeProperties** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| sqlReaderQuery |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-query-tekenreeks. Bijvoorbeeld: Selecteer * from MijnTabel. |Nee |
| sqlReaderStoredProcedureName |Naam van Hallo opgeslagen procedure die gegevens uit Hallo brontabel leest. |Naam van Hallo opgeslagen procedure. Hallo laatste SQL-instructie moet een SELECT-instructie in Hallo opgeslagen procedure. |Nee |
| storedProcedureParameters |Parameters voor Hallo opgeslagen procedure. |Naam/waarde-paren. Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters. |Nee |

Als hello **sqlReaderQuery** is opgegeven voor Hallo SqlDWSource, hello Kopieeractiviteit deze query wordt uitgevoerd tegen Hallo tooget Azure SQL Data Warehouse-Hallo brongegevens.

U kunt ook een opgeslagen procedure opgeven door te geven Hallo **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als hello opgeslagen procedure parameters zijn vereist).

Als u geen sqlReaderQuery of sqlReaderStoredProcedureName opgeeft, zijn Hallo kolommen gedefinieerd in de sectie Hallo structuur van Hallo gegevensset JSON gebruikte toobuild een query toorun tegen hello Azure SQL Data Warehouse. Voorbeeld: `select column1, column2 from mytable`. Als de definitie van de gegevensset Hallo geen Hallo structuur, worden alle kolommen uit Hallo tabel geselecteerd.

#### <a name="sqldwsource-example"></a>Voorbeeld van SqlDWSource

```JSON
"source": {
    "type": "SqlDWSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```
**Hallo opgeslagen proceduredefinitie:**

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqldwsink"></a>SqlDWSink
**SqlDWSink** ondersteunt Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |Geef een query voor de Kopieeractiviteit tooexecute zodat de gegevens van een bepaald segment wordt opgeschoond. Zie voor meer informatie [herhaalbaarheid sectie](#repeatability-during-copy). |Een query-instructie. |Nee |
| allowPolyBase |Hiermee wordt aangegeven of toouse PolyBase (indien van toepassing) in plaats van BULKINSERT mechanisme. <br/><br/> **Met PolyBase is Hallo aanbevolen manier tooload gegevens in SQL Data Warehouse.** Zie [gebruik PolyBase tooload gegevens in Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) sectie voor beperkingen en meer informatie. |True <br/>False (standaard) |Nee |
| polyBaseSettings |Een groep met eigenschappen die kunnen worden opgegeven wanneer hello **allowPolybase** eigenschap is ingesteld, te**true**. |&nbsp; |Nee |
| rejectValue |Hiermee geeft u op Hallo getal of het percentage van de rijen die kunnen worden afgewezen voordat het Hallo-query is mislukt. <br/><br/>Meer informatie over Hallo PolyBase van opties in Hallo afwijzen **argumenten** sectie van [maken EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) onderwerp. |0 (standaard), 1, 2... |Nee |
| rejectType |Hiermee geeft u op of Hallo rejectValue optie is opgegeven als een letterlijke waarde of een percentage. |In waarde (standaard), Percentage |Nee |
| rejectSampleValue |Bepaalt het aantal rijen tooretrieve Hallo voordat Hallo PolyBase Hallo percentage geweigerde rijen opnieuw berekend. |1, 2, … |Ja, als **rejectType** is **percentage** |
| useTypeDefault |Hiermee geeft u op hoe toohandle ontbreken waarden in tekstbestanden gescheiden wanneer PolyBase gegevens uit Hallo tekstbestand ophaalt.<br/><br/>Meer informatie over deze eigenschap in Hallo argumenten sectie [maken EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx). |True, False (standaard) |Nee |
| writeBatchSize |Voegt de gegevens in SQL-tabel Hallo wanneer Hallo buffergrootte writeBatchSize bereikt |Geheel getal (aantal rijen) |Nee (standaard: 10000) |
| writeBatchTimeout |Wachttijd voor Hallo batch insert-bewerking toocomplete voordat een time-out optreedt. |TimeSpan<br/><br/> Voorbeeld: "00: 30:00 ' (30 minuten). |Nee |

#### <a name="sqldwsink-example"></a>Voorbeeld van SqlDWSink

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a>PolyBase tooload gegevens in Azure SQL Data Warehouse gebruiken
Met behulp van  **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)**  is een efficiënte manier van het laden van grote hoeveelheid gegevens in Azure SQL Data Warehouse met hoge doorvoer. U kunt een grote toename in doorvoer Hallo zien door met PolyBase in plaats van Hallo BULKINSERT standaardmechanisme. Zie [prestaties referentienummer kopiëren](data-factory-copy-activity-performance.md#performance-reference) met gedetailleerde vergelijking. Zie voor een overzicht met een gebruiksvoorbeeld [1 TB laden in Azure SQL Data Warehouse onder 15 minuten met Azure Data Factory](data-factory-load-sql-data-warehouse.md).

* Als de brongegevens **Azure Blob- of Azure Data Lake Store**, en Hallo-indeling is compatibel met PolyBase, kunt u rechtstreeks tooAzure SQL Data Warehouse met PolyBase kopiëren. Zie  **[Direct kopiëren met PolyBase](#direct-copy-using-polybase)**  met details.
* Als uw brongegevensarchief en de indeling wordt oorspronkelijk niet ondersteund door PolyBase, kunt u Hallo  **[gefaseerde kopiëren met PolyBase](#staged-copy-using-polybase)**  in plaats daarvan functie. Dit biedt u ook betere doorvoer door automatisch converteren van Hallo gegevens naar de PolyBase-compatibele indeling en Hallo gegevens opslaan in Azure Blob-opslag. Vervolgens worden gegevens geladen in SQL Data Warehouse.

Set Hallo `allowPolyBase` eigenschap te**true** zoals weergegeven in het volgende voorbeeld voor Azure Data Factory toouse PolyBase toocopy gegevens in Azure SQL Data Warehouse Hallo. Als u allowPolyBase tootrue instelt, kunt u PolyBase specifieke eigenschappen met Hallo `polyBaseSettings` eigenschappengroep. Zie Hallo [SqlDWSink](#SqlDWSink) sectie voor meer informatie over de eigenschappen die u met polyBaseSettings gebruiken kunt.

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a>Directe kopiëren met PolyBase
SQL Data Warehouse PolyBase ondersteuning rechtstreeks voor Azure-Blob en Azure Data Lake Store (met behulp van de service-principal) als bron en met vereisten voor een specifieke indeling. Als de brongegevens voldoet aan Hallo criteria in deze sectie beschreven, kunt u rechtstreeks kopiëren van bron data store tooAzure die SQL Data Warehouse met PolyBase. Anders kunt u [gefaseerde kopiëren met PolyBase](#staged-copy-using-polybase).

> [!TIP]
> toocopy gegevens van Data Lake Store tooSQL Data Warehouse efficiënt, meer wilt weten van [Azure Data Factory maakt het eenvoudiger en handige toouncover inzicht in gegevens, zelfs als u Data Lake Store met SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).

Als Hallo vereisten niet wordt voldaan, wordt Azure Data Factory Hallo instellingen controleert en automatisch terugvalt toohello BULKINSERT mechanisme voor gegevensverplaatsing Hallo.

1. **Bron gekoppelde service** is van het type: **AzureStorage** of **AzureDataLakeStore met verificatie van de service-principal**.  
2. Hallo **invoergegevensset** is van het type: **AzureBlob** of **AzureDataLakeStore**, en hello, indelingstype onder `type` eigenschappen is **OrcFormat** , of **TextFormat** Hello volgende configuraties:

   1. `rowDelimiter`moet  **\n** .
   2. `nullValue`te is ingesteld,**lege tekenreeks** (""), of `treatEmptyAsNull` te is ingesteld,**true**.
   3. `encodingName`te is ingesteld,**utf-8**, namelijk **standaard** waarde.
   4. `escapeChar`, `quoteChar`, `firstRowAsHeader`, en `skipLineCount` zijn niet opgegeven.
   5. `compression`kan **geen compressie**, **GZip**, of **Deflate**.

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. Er is geen `skipHeaderLineCount` onder **BlobSource** of **AzureDataLakeStore** voor Hallo kopieeractiviteit in Hallo pijplijn.
4. Er is geen `sliceIdentifierColumnName` onder **SqlDWSink** voor Hallo kopieeractiviteit in Hallo pijplijn. (PolyBase zorgt ervoor dat alle gegevens worden bijgewerkt of niet in een enkel uitvoering bijgewerkt wordt. tooachieve **herhaalbaarheid**, kunt u `sqlWriterCleanupScript`).
5. Er is geen `columnMapping` in Hallo gekoppeld in de kopieerbewerking wordt gebruikt.

### <a name="staged-copy-using-polybase"></a>Gefaseerde kopiëren met PolyBase
Als de brongegevens niet voldoet aan de Hallo criteria die zijn geïntroduceerd in de vorige sectie hello, kunt u kopiëren van gegevens via een tussentijdse staging Azure Blob Storage (kan niet voor Premium-opslag) inschakelen. In dit geval Azure Data Factory automatisch voert transformaties op Hallo toomeet gegevens indeling vereisten van gegevens en gebruik PolyBase tooload gegevens vervolgens PolyBase in SQL Data Warehouse en ten minste opschonen uw tijdelijke gegevens uit Hallo Blob storage. Zie [kopie gefaseerde](data-factory-copy-activity-performance.md#staged-copy) voor meer informatie over de werking kopiëren van gegevens via een gefaseerde installatie Azure-Blob in het algemeen.

> [!NOTE]
> Bij het kopiëren van gegevens uit een on-premises gegevens opslaan in Azure SQL Data Warehouse met PolyBase en fasering, als uw Data Management Gateway-versie lager dan 2.4 is Java Runtime Environment (Java Runtime Environment) is vereist op de gateway van de computer die is gebruikt tootransform de brongegevens in de juiste notatie. Stelt dat u uw gateway toohello nieuwste tooavoid deze afhankelijkheid upgraden.
>

toouse die deze functie, maakt een [gekoppelde Azure Storage-service](data-factory-azure-blob-connector.md#azure-storage-linked-service) die toohello Azure Storage-Account met Hallo tussentijdse blob storage verwijst, geeft u Hallo `enableStaging` en `stagingSettings` eigenschappen voor Hallo kopieerbewerking zoals u in de volgende code Hallo:

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a>Aanbevolen procedures voor met PolyBase
Hallo volgende secties bevatten aanvullende best practices toohello die worden vermeld in [aanbevolen procedures voor Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).

### <a name="required-database-permission"></a>Vereiste databasemachtiging
toouse PolyBase, hiervoor Hallo gebruiker worden gegevens in SQL Data Warehouse gebruikte tooload heeft Hallo [machtiging "Beheer"](https://msdn.microsoft.com/library/ms191291.aspx) op Hallo doeldatabase. Eenzijdige tooachieve die tooadd die gebruiker als lid van de rol 'db_owner'. Meer informatie over hoe toodo die door de volgende [in deze sectie](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).

### <a name="row-size-and-data-type-limitation"></a>Typ de beperking rijgrootte en gegevens
Polybase-belastingen zijn beperkt tooloading rijen beide kleiner is dan **1 MB** en kan niet worden geladen tooVARCHR(MAX), NVARCHAR(MAX) of VARBINARY(MAX). Raadpleeg te[hier](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).

Als u de brongegevens met rijen van de omvang is groter dan 1 MB hebt, kunt u toosplit Hallo brontabellen verticaal in verschillende kleine netwerken waar Hallo grootste rijgrootte van elk van deze Hallo limiet niet overschrijdt. Hallo kleinere tabellen kunnen vervolgens worden geladen met PolyBase en samengevoegd in Azure SQL Data Warehouse.

### <a name="sql-data-warehouse-resource-class"></a>De bronklasse SQL Data Warehouse
tooachieve best mogelijke doorvoer, overweeg tooassign groter resource klasse toohello gebruiker wordt tooload gegevens in SQL Data Warehouse met PolyBase gebruikt. Meer informatie over hoe toodo die door de volgende [wijzigen van een voorbeeld van een gebruiker resource klasse](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).

### <a name="tablename-in-azure-sql-data-warehouse"></a>tableName in Azure SQL Data Warehouse
Hallo volgende tabel bevat voorbeelden van hoe toospecify hello **tableName** eigenschap in de gegevensset JSON voor verschillende combinaties van schema en de tabelnaam.

| DB Schema | De tabelnaam van de | JSON-eigenschap tableName |
| --- | --- | --- |
| dbo |MyTable |MyTable of dbo. MyTable of [dbo]. [MijnTabel] |
| dbo1 |MyTable |dbo1. MyTable of [dbo1]. [MijnTabel] |
| dbo |My.Table |[My.Table] of [dbo]. [My.Table] |
| dbo1 |My.Table |[dbo1]. [My.Table] |

Als u de volgende fout Hallo ziet, is het mogelijk een probleem met het Hallo-waarde die u hebt opgegeven voor de eigenschap tableName Hallo. Zie de tabel Hallo voor Hallo juiste manier toospecify waarden voor de bijbehorende eigenschap tableName JSON Hallo.  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a>Kolommen met standaardwaarden
Op dit moment PolyBase-functie in de Data Factory accepteert alleen hetzelfde aantal kolommen in de doeltabel Hallo Hallo. Stel, u hebt een tabel met vier kolommen en een ervan is gedefinieerd met een standaardwaarde. Hallo invoergegevens moet nog steeds vier kolommen bevatten. Een invoergegevensset 3 kolommen bieden zou resulteert in een fout vergelijkbare toohello volgende bericht:

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
NULL-waarde is een speciale vorm van de standaardwaarde. Als Hallo kolom waarvoor null is toegestaan, kan het invoergegevens hello (in blob) voor de kolom leeg zijn (kan niet aanwezig zijn op Hallo invoergegevensset). PolyBase voegt NULL zijn voor deze in hello Azure SQL Data Warehouse.  

## <a name="auto-table-creation"></a>Maken van de tabel automatisch
Als u gegevens van de Wizard kopiëren toocopy van SQL Server gebruikt of Azure SQL Database tooAzure SQL Data Warehouse en Hallo tabel die overeenkomt met de brontabel toohello niet in het doelarchief hello bestaat, maken Data Factory automatisch Hallo-tabel in Hallo het datawarehouse met behulp van de bron-tabelschema Hallo.

Data Factory maakt Hallo tabel in het doelarchief Hallo Hello dezelfde naam in Hallo brongegevensarchief tabel. Hallo-gegevenstypen voor kolommen worden gekozen op basis van Hallo toewijzing van het type te volgen. Indien nodig, voert het type conversies toofix incompatibiliteitsproblemen tussen bron- en doelserver stores. Round Robin tabeldistributie worden ook gebruikt.

| Type gegevensbron SQL Database-kolom | Doel-SQL DW-kolomtype (de maximale grootte) |
| --- | --- |
| int | int |
| BigInt | BigInt |
| SmallInt | SmallInt |
| TinyInt | TinyInt |
| bits | bits |
| Decimale | Decimale |
| numerieke | Decimale |
| Float | Float |
| Money | Money |
| Real | Real |
| SmallMoney | SmallMoney |
| Binaire | Binaire |
| varbinary | Varbinary (omhoog too8000) |
| Date | Date |
| Datum/tijd | Datum/tijd |
| DateTime2 | DateTime2 |
| Time | Time |
| DateTimeOffset | DateTimeOffset |
| SmallDateTime | SmallDateTime |
| Tekst | Varchar (omhoog too8000) |
| NText | NVarChar (omhoog too4000) |
| Installatiekopie | VarBinary (omhoog too8000) |
| UniqueIdentifier | UniqueIdentifier |
| CHAR | CHAR |
| NChar | NChar |
| VarChar | VarChar (omhoog too8000) |
| NVarChar | NVarChar (omhoog too4000) |
| XML | Varchar (omhoog too8000) |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a>Toewijzing van het type voor Azure SQL Data Warehouse
Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello 2 stap benadering te volgen:

1. Systeemeigen bron typen too.NET type converteren
2. Converteren van .NET-type toonative sink-type

Bij het verplaatsen van gegevens te & van Azure SQL Data Warehouse worden hello volgende toewijzingen gebruikt vanuit SQL type too.NET type en vice versa.

Hallo-toewijzing is hetzelfde als Hallo [SQL Server gegevenstypetoewijzing voor ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).

| SQL Server Database Engine-type | .NET framework-type |
| --- | --- |
| bigint |Int64 |
| Binaire |Byte] |
| bits |Booleaanse waarde |
| CHAR |Tekenreeks, Char] |
| Datum |Datum/tijd |
| Datum/tijd |Datum/tijd |
| datetime2 |Datum/tijd |
| DateTimeOffset |DateTimeOffset |
| Decimale |Decimale |
| FILESTREAM-kenmerk (varbinary(max)) |Byte] |
| Float |dubbele |
| Afbeelding |Byte] |
| int |Int32 |
| Money |Decimale |
| nchar |Tekenreeks, Char] |
| ntext |Tekenreeks, Char] |
| numerieke |Decimale |
| nvarchar |Tekenreeks, Char] |
| echte |Één |
| ROWVERSION |Byte] |
| smalldatetime |Datum/tijd |
| smallint |Int16 |
| smallmoney |Decimale |
| sql_variant |Object * |
| Tekst |Tekenreeks, Char] |
| tijd |TimeSpan |
| tijdstempel |Byte] |
| tinyint |Byte |
| uniqueidentifier |GUID |
| varbinary |Byte] |
| varchar |Tekenreeks, Char] |
| xml |XML |

U kunt ook kolommen uit de bron gegevensset toocolumns uit sink gegevensset in de definitie van de activiteit kopiëren Hallo toewijzen. Zie voor meer informatie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a>JSON-voorbeelden voor het kopiëren van gegevens tooand van SQL Data Warehouse
Hallo volgende voorbeelden geven voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Ze geven weer hoe toocopy gegevens tooand van Azure SQL Data Warehouse en Azure Blob Storage. Echter gegevens kunnen worden gekopieerd **rechtstreeks** uit een van de bronnen tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a>Voorbeeld: Gegevens kopiëren van Azure SQL Data Warehouse tooAzure Blob
Hallo voorbeeld definieert Hallo Data Factory-entiteiten te volgen:

1. Een gekoppelde service van het type [AzureSqlDW](#linked-service-properties).
2. Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureSqlDWTable](#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [SqlDWSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Hallo voorbeeld kopieert tijdreeks (elk uur, dagelijks, enz.) gegevens uit een tabel in Azure SQL Data Warehouse-database tooa blob elk uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

**Azure SQL Data Warehouse gekoppelde service:**

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Azure Blob-opslag gekoppelde service:**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**Azure SQL Data Warehouse invoergegevensset:**

Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in Azure SQL Data Warehouse en bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens.

Instelling 'extern': 'true' informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
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
**Azure Blob-uitvoergegevensset:**

Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1). pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**De kopieeractiviteit in een pijplijn met SqlDWSource en BlobSink:**

Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**SqlDWSource** en **sink** type is ingesteld, te**BlobSink**. Hallo SQL-query is opgegeven voor Hallo **SqlReaderQuery** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```
> [!NOTE]
> In voorbeeld Hallo **sqlReaderQuery** voor Hallo SqlDWSource is opgegeven. Deze query Hallo Kopieeractiviteit uitgevoerd tegen Hallo tooget Azure SQL Data Warehouse-Hallo brongegevens.
>
> U kunt ook een opgeslagen procedure opgeven door te geven Hallo **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als hello opgeslagen procedure parameters zijn vereist).
>
> Als u geen sqlReaderQuery of sqlReaderStoredProcedureName opgeeft, Hallo kolommen die zijn gedefinieerd in de sectie Hallo structuur van Hallo gegevensset JSON gebruikte toobuild (Selecteer column1, column2 from MijnTabel) van een query zijn toorun tegen hello Azure SQL Data Warehouse. Als de definitie van de gegevensset Hallo geen Hallo structuur, worden alle kolommen uit Hallo tabel geselecteerd.
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a>Voorbeeld: Gegevens kopiëren van Azure Blob-tooAzure SQL Data Warehouse
Hallo voorbeeld definieert Hallo Data Factory-entiteiten te volgen:

1. Een gekoppelde service van het type [AzureSqlDW](#linked-service-properties).
2. Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureSqlDWTable](#dataset-properties).
5. Een [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) en [SqlDWSink](#copy-activity-properties).

Hallo voorbeeld kopieert timeseries gegevens (elk uur, dagelijks, enzovoort) uit Azure blob tooa tabel in Azure SQL Data Warehouse-database om het uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

**Azure SQL Data Warehouse gekoppelde service:**

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Azure Blob-opslag gekoppelde service:**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**Azure Blob invoergegevensset:**

Gegevens wordt opgehaald uit een nieuwe blob elk uur (frequentie: uur, interval: 1). Hallo map pad en de naam voor de blob Hallo worden dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. Hallo mappad jaar, maand en dag deel uit van de begintijd Hallo en bestandsnaam gebruikt Hallo uur deel uit van de begintijd Hallo. "extern": "true" instelling informeert Hallo Data Factory-service dat deze tabel externe toohello gegevensfactory en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
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
**Azure SQL Data Warehouse uitvoergegevensset:**

Hallo voorbeeld kopieert gegevens tooa tabel "MijnTabel" in Azure SQL Data Warehouse. Hallo-tabel maken in Azure SQL Data Warehouse met hetzelfde aantal kolommen Hallo zoals Hallo Blob CSV-bestand toocontain verwacht. Nieuwe rijen worden toohello tabel toegevoegd om het uur.

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**De kopieeractiviteit in een pijplijn met BlobSource en SqlDWSink:**

Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**BlobSource** en **sink** type is ingesteld, te**SqlDWSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
Zie voor een overzicht, Zie Hallo [1 TB laden in Azure SQL Data Warehouse onder 15 minuten met Azure Data Factory](data-factory-load-sql-data-warehouse.md) en [gegevens laden met Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) artikel in hello Azure SQL Data Warehouse documentatie.

## <a name="performance-and-tuning"></a>Prestaties en het afstemmen
Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.
