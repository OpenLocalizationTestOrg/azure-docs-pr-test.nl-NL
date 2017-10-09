---
title: aaaMove gegevens tooand van SQL Server | Microsoft Docs
description: Meer informatie over hoe toomove gegevens van/naar SQL Server-database die lokaal of in een virtuele machine in Azure met Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a>Verplaatsen van gegevens tooand van SQL Server on-premises of op IaaS (Azure VM) met behulp van Azure Data Factory
Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit een on-premises SQL Server database. Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft. 

## <a name="supported-scenarios"></a>Ondersteunde scenario 's
U kunt gegevens kopiëren **uit een SQL Server-database** toohello gegevensarchieven te volgen:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Gegevens kunnen worden gekopieerd van de volgende gegevensarchieven Hallo **tooa SQL Server-database**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a>Ondersteunde versies van SQL Server
Deze ondersteuning van SQL Server-connector kopiëren van gegevens uit / toohello volgende versies van gehost exemplaar lokaal of in Azure IaaS met behulp van zowel de SQL-verificatie en de Windows-verificatie: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005

## <a name="enabling-connectivity"></a>Connectiviteit inschakelen
Hallo-concepten en de stappen die nodig zijn om verbinding te maken met SQL Server die wordt gehost on-premises of in Azure IaaS (Infrastructure-as-a-Service) virtuele machines zijn Hallo dezelfde. In beide gevallen moet u toouse Data Management Gateway voor connectiviteit.

Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn artikel over Data Management Gateway en stapsgewijze instructies over het instellen van Hallo-gateway. Instellen van een gatewayexemplaar is een vereiste voor het verbinden met SQL Server.

Tijdens de installatie van gateway op Hallo dezelfde lokale machine of de cloud VM-instantie als Hallo van SQL Server voor betere prestaties, raden we u deze installeren op afzonderlijke computers. Hallo-gateway en SQL Server met op afzonderlijke computers, worden bronconflicten beperkt.

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een on-premises SQL Server database verplaatst met behulp van verschillende hulpprogramma's voor API's.

Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.

U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit. 

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren: 

1. Maak een **gegevensfactory**. Een gegevensfactory kan één of meer pijplijnen bevatten. 
2. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory. Bijvoorbeeld, als u gegevens uit een SQL Server-database tooan Azure blob-opslag kopiëren wilt, u twee gekoppelde services toolink uw SQL Server-database en de Azure storage-account tooyour data factory. Zie voor de gekoppelde service-eigenschappen die specifiek tooSQL Server-database, [gekoppelde service-eigenschappen](#linked-service-properties) sectie. 
3. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking. In voorbeeld Hallo vermeld in de laatste stap Hallo kunt u een gegevensset toospecify Hallo SQL-tabel maken in uw SQL Server-database waarin de invoergegevens Hallo. Maken van een andere dataset toospecify Hallo blob-container en Hallo map Hallo gegevens gekopieerd van Hallo SQL Server-database. Zie voor eigenschappen van gegevensset die specifieke tooSQL Server-database, [eigenschappen van gegevensset](#dataset-properties) sectie.
4. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer. In Hallo voorbeeld eerder vermeld, gebruikt u SqlSource als een bron- en BlobSink als een sink voor de kopieeractiviteit Hallo. Op dezelfde manier als u uit Azure Blob Storage tooSQL Server-Database kopiëren wilt, gebruikt u BlobSource en SqlSink in Hallo kopieeractiviteit. Zie voor activiteitseigenschappen kopiëren die specifieke tooSQL Server-Database, [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie. Voor informatie over hoe toouse een gegevensarchief als een bron of een sink, klikt u op Hallo-koppeling in de vorige sectie Hallo voor de gegevensopslag. 

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.  Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van/naar een lokale SQL Server-database zijn, [JSON voorbeelden](#json-examples-for-copying-data-from-and-to-sql-server) sectie van dit artikel. 

Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooSQL Server zijn: 

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Maken van een gekoppelde service van het type **OnPremisesSqlServer** toolink een lokale SQL Server-database tooa data factory. Hallo volgende tabel biedt een beschrijving voor de service voor JSON-elementen specifieke tooon-premises SQL Server gekoppeld.

Hallo volgende tabel bevat een beschrijving voor JSON-elementen specifieke tooSQL gekoppelde Server-service.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |Hallo type eigenschap moet worden ingesteld op: **OnPremisesSqlServer**. |Ja |
| connectionString |Geef connectionString informatie nodig tooconnect toohello lokale SQL Server-database met behulp van de SQL-verificatie of de Windows-verificatie. |Ja |
| gatewayName |Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale SQL Server-database gebruiken. |Ja |
| gebruikersnaam |Geef de gebruikersnaam als u Windows-verificatie gebruikt. Voorbeeld: **domainname\\gebruikersnaam**. |Nee |
| wachtwoord |Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven. |Nee |

U kunt referenties met een Hallo versleutelen **nieuw AzureRmDataFactoryEncryptValue** cmdlet en in de verbindingsreeks hello gebruiken, zoals wordt weergegeven in het volgende voorbeeld Hallo (**EncryptedCredential** eigenschap):  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a>Voorbeelden
**JSON voor het gebruik van SQL-verificatie**

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
**JSON voor het gebruik van Windows-verificatie**

Data Management Gateway imiteert Hallo opgegeven gebruiker account tooconnect toohello lokale SQL Server-database. 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
In Hallo voorbeelden, hebt u een gegevensset van het type gebruikt **SqlServerTable** toorepresent een tabel in een SQL Server-database.  

Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (SQL Server, Azure blob-, Azure-tabel, enz.).

Hallo typeProperties sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo. Hallo **typeProperties** sectie voor Hallo gegevensset van het type **SqlServerTable** heeft Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |De naam van het Hallo-tabel of weergave in Hallo SQL Server Database-instantie waarnaar de gekoppelde service verwijst. |Ja |

## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Als u gegevens uit een SQL Server-database verplaatst, u Hallo brontype instellen in de kopieerbewerking Hallo te**SqlSource**. Als u gegevens tooa SQL Server-database verplaatst, u stelt Hallo sink-type in de kopieerbewerking Hallo te**SqlSink**. Deze sectie bevat een lijst met eigenschappen die worden ondersteund door SqlSource en SqlSink.

Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en beleidsregels zijn beschikbaar voor alle typen activiteiten.

> [!NOTE]
> Hallo Kopieeractiviteit slechts één invoer en slechts één uitvoer produceert.

Terwijl de eigenschappen die beschikbaar zijn in Hallo typeProperties gedeelte van de activiteit Hallo variëren met elk activiteitstype. Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.

### <a name="sqlsource"></a>SqlSource
Wanneer u de gegevensbron in een kopieeractiviteit is van het type **SqlSource**, Hallo volgende eigenschappen beschikbaar zijn in **typeProperties** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| sqlReaderQuery |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-query-tekenreeks. Bijvoorbeeld: Selecteer * from MijnTabel. Kan naar meerdere tabellen uit Hallo database waarnaar wordt verwezen door de invoergegevensset Hallo verwijzen. Als niet wordt opgegeven, Hallo SQL-instructie die is uitgevoerd: Selecteer een van de MyTable. |Nee |
| sqlReaderStoredProcedureName |Naam van Hallo opgeslagen procedure die gegevens uit Hallo brontabel leest. |Naam van Hallo opgeslagen procedure. Hallo laatste SQL-instructie moet een SELECT-instructie in Hallo opgeslagen procedure. |Nee |
| storedProcedureParameters |Parameters voor Hallo opgeslagen procedure. |Naam/waarde-paren. Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters. |Nee |

Als hello **sqlReaderQuery** is opgegeven voor Hallo SqlSource, hello Kopieeractiviteit deze query wordt uitgevoerd tegen Hallo SQL Server-Database tooget Hallo brongegevens.

U kunt ook een opgeslagen procedure opgeven door te geven Hallo **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als hello opgeslagen procedure parameters zijn vereist).

Als u geen sqlReaderQuery of sqlReaderStoredProcedureName opgeeft, zijn gedefinieerd in de sectie structuur Hallo Hallo-kolommen gebruikte toobuild een toorun selectiequery tegen Hallo SQL Server-Database. Als de definitie van de gegevensset Hallo geen Hallo structuur, worden alle kolommen uit Hallo tabel geselecteerd.

> [!NOTE]
> Als u werkt met **sqlReaderStoredProcedureName**, moet u nog steeds toospecify een waarde voor Hallo **tableName** eigenschap in de gegevensset Hallo JSON. Er zijn geen controles uitgevoerd voor deze tabel al.

### <a name="sqlsink"></a>SqlSink
**SqlSink** ondersteunt Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| writeBatchTimeout |Wachttijd voor Hallo batch insert-bewerking toocomplete voordat een time-out optreedt. |TimeSpan<br/><br/> Voorbeeld: "00: 30:00 ' (30 minuten). |Nee |
| writeBatchSize |Voegt de gegevens in SQL-tabel Hallo wanneer Hallo buffergrootte writeBatchSize bereikt. |Geheel getal (aantal rijen) |Nee (standaard: 10000) |
| sqlWriterCleanupScript |Query voor de Kopieeractiviteit tooexecute opgeven zodat de gegevens van een bepaald segment wordt opgeschoond. Zie voor meer informatie [herhaalbare kopiëren](#repeatable-copy) sectie. |Een query-instructie. |Nee |
| sliceIdentifierColumnName |Geef kolomnaam voor Kopieeractiviteit toofill met segment-ID automatisch gegenereerd en die is gebruikt tooclean van gegevens van een bepaald segment wanneer opnieuw uitgevoerd. Zie voor meer informatie [herhaalbare kopiëren](#repeatable-copy) sectie. |De naam van de kolom van een kolom met gegevenstype binary(32). |Nee |
| sqlWriterStoredProcedureName |Naam van Hallo opgeslagen procedure die upserts (updates/INSERT) gegevens in de doeltabel Hallo. |Naam van Hallo opgeslagen procedure. |Nee |
| storedProcedureParameters |Parameters voor Hallo opgeslagen procedure. |Naam/waarde-paren. Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters. |Nee |
| sqlWriterTableType |Geef tabel type naam toobe in Hallo opgeslagen procedure gebruikt. Kopieeractiviteit beschikbaar Hallo-gegevens worden verplaatst in een tijdelijke tabel met dit tabeltype. Opgeslagen procedurecode kunt Hallo gegevens wordt gekopieerd met de bestaande gegevens vervolgens samenvoegen. |Een typenaam van de tabel. |Nee |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a>JSON-voorbeelden voor het kopiëren van gegevens van en tooSQL Server
Hallo volgende voorbeelden geven voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Hallo van de volgende voorbeelden tonen hoe toocopy gegevens tooand van SQL Server en Azure Blob Storage. Echter gegevens kunnen worden gekopieerd **rechtstreeks** uit een van de bronnen tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a>Voorbeeld: Gegevens uit SQL Server-tooAzure Blob kopiëren
Hallo volgende ziet:

1. Een gekoppelde service van het type [OnPremisesSqlServer](#linked-service-properties).
2. Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [SqlServerTable](#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Hallo [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [SqlSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Hallo voorbeeld opgehaald-timeseries-gegevens uit een SQL Server-tabel tooan Azure blob elk uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

Instellen als eerste stap Hallo data management gateway. Hallo-instructies vindt u in Hallo [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.

**SQL Server gekoppeld-service**
```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
**Azure Blob-opslag gekoppelde service**

```json
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
**SQL Server-invoergegevensset**

Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in SQL Server en deze bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens. U kunt een query over meerdere tabellen in dezelfde database met behulp van een één gegevensset, maar één tabel moet worden gebruikt voor een van deze dataset Hallo tableName typeProperty Hallo.

Instelling 'extern': 'true' informeert Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.

```json
{
  "name": "SqlServerInput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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
**Azure Blob-uitvoergegevensset**

Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1). pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.

```json
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
**Pijplijn met de kopieeractiviteit**

Hallo pijplijn bevat een Kopieeractiviteit die is geconfigureerd toouse deze invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**SqlSource** en **sink** type is ingesteld, te**BlobSink**. Hallo SQL-query is opgegeven voor Hallo **SqlReaderQuery** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
In dit voorbeeld **sqlReaderQuery** voor Hallo SqlSource is opgegeven. Deze query Hallo Kopieeractiviteit uitgevoerd tegen Hallo tooget SQL Server-Database-Hallo brongegevens. U kunt ook een opgeslagen procedure opgeven door te geven Hallo **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als hello opgeslagen procedure parameters zijn vereist). Hallo sqlReaderQuery kunt verwijzen naar meerdere tabellen in Hallo database waarnaar wordt verwezen door Hallo invoergegevensset. Het is niet beperkt tooonly Hallo tabel van deze dataset tableName typeProperty Hallo ingesteld.

Als u geen sqlReaderQuery of sqlReaderStoredProcedureName opgeeft, zijn gedefinieerd in de sectie structuur Hallo Hallo-kolommen gebruikte toobuild een toorun selectiequery tegen Hallo SQL Server-Database. Als de definitie van de gegevensset Hallo geen Hallo structuur, worden alle kolommen uit Hallo tabel geselecteerd.

Zie Hallo [Sql-bron](#sqlsource) sectie en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) voor Hallo lijst met eigenschappen die ondersteund worden door SqlSource en BlobSink.

## <a name="example-copy-data-from-azure-blob-toosql-server"></a>Voorbeeld: Gegevens kopiëren van Azure Blob-tooSQL Server
Hallo volgende ziet:

1. Hallo gekoppelde service van het type [OnPremisesSqlServer](#linked-service-properties).
2. Hallo gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).
5. Hallo [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) en [SqlSink](#sql-server-copy-activity-type-properties).

Hallo voorbeeld opgehaald-timeseries-gegevens uit een Azure-blobopslag tooa SQL Server-tabel om het uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

**SQL Server gekoppeld-service**

```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
**Azure Blob-opslag gekoppelde service**

```json
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
**Azure Blob-invoergegevensset**

Gegevens wordt opgehaald uit een nieuwe blob elk uur (frequentie: uur, interval: 1). Hallo map pad en de naam voor de blob Hallo worden dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. Hallo mappad jaar, maand en dag deel uit van de begintijd Hallo en bestandsnaam gebruikt Hallo uur deel uit van de begintijd Hallo. "extern": "true" instelling informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.

```json
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
**Gegevensset voor SQL Server-uitvoer**

Hallo voorbeeld kopieert gegevens tooa tabel "MijnTabel" in SQL Server. Hallo-tabel maken in SQL-Server met hetzelfde aantal kolommen Hallo zoals Hallo Blob CSV-bestand toocontain verwacht. Nieuwe rijen worden toohello tabel toegevoegd om het uur.

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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
**Pijplijn met de kopieeractiviteit**

Hallo pijplijn bevat een Kopieeractiviteit die is geconfigureerd toouse deze invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**BlobSource** en **sink** type is ingesteld, te**SqlSink**.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": " SqlServerOutput "
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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

## <a name="troubleshooting-connection-issues"></a>Verbindingsproblemen oplossen
1. Configureer uw SQL Server tooaccept externe verbindingen. Start **SQL Server Management Studio**, met de rechtermuisknop op **server**, en klik op **eigenschappen**. Selecteer **verbindingen** van Hallo lijst en controle **toestaan externe verbindingen toohello server**.

    ![Externe verbindingen inschakelen](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    Zie [Hallo remote access Server Configuration Option configureert](https://msdn.microsoft.com/library/ms191464.aspx) voor gedetailleerde stappen.
2. Start **SQL Server Configuration Manager**. Vouw **SQL Server-netwerkconfiguratie** voor Hallo exemplaar u wilt en selecteer **protocollen voor MSSQLSERVER**. U ziet protocollen in Hallo rechterdeelvenster. TCP/IP inschakelen met de rechtermuisknop op **TCP/IP** en te klikken op **inschakelen**.

    ![TCP/IP inschakelen](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    Zie [in- of uitschakelen van een Server netwerkprotocol](https://msdn.microsoft.com/library/ms191294.aspx) voor meer informatie en alternatieve manieren TCP/IP-protocol in te schakelen.
3. In hetzelfde venster Hallo, dubbelklikt u op **TCP/IP** toolaunch **TCP/IP-eigenschappen** venster.
4. Overschakelen van toohello **IP-adressen** tabblad. Schuif omlaag toosee **IPAll** sectie. Noteer Hallo ** TCP-poort ** (standaardwaarde is **1433**).
5. Maak een **regel voor Windows Firewall Hallo** op Hallo machine tooallow binnenkomend verkeer via deze poort.  
6. **Verbinding controleren**: tooconnect toohello SQL Server met behulp van volledig gekwalificeerde naam SQL Server Management Studio gebruiken vanaf een andere computer. Bijvoorbeeld: '<machine>.<domain>. Corp.<company>.com, 1433. "

   > [!IMPORTANT]

   > Zie [gegevens verplaatsen tussen lokale bronnen en Hallo cloud met Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) voor gedetailleerde informatie.
   >
   > Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.
   >
   >


## <a name="identity-columns-in-hello-target-database"></a>Id-kolommen in de doeldatabase Hallo
Deze sectie bevat een voorbeeld waarin gegevens worden gekopieerd van een brontabel met geen doeltabel identiteit kolom tooa met een identiteitskolom.

**Brontabel:**

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**Doeltabel:**

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

U ziet dat doeltabel Hallo heeft een identiteitskolom.

**Bron gegevensset JSON-definitie**

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
**Doel-dataset JSON-definitie**

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

Merk op dat als de bron en doel-tabel verschillende schema's zijn (doel heeft een extra kolom met de identiteit). In dit scenario moet u toospecify **structuur** eigenschap in Hallo doel gegevenssetdefinitie, waaronder Hallo identiteitskolom niet.

## <a name="invoke-stored-procedure-from-sql-sink"></a>Aanroepen van opgeslagen procedure uit SQL-sink
Zie [opgeslagen procedure voor SQL-sink aanroepen in de kopieerbewerking](data-factory-invoke-stored-procedure-from-copy-activity.md) artikel voor een voorbeeld van een opgeslagen procedure van SQL-sink in een kopieeractiviteit van een pijplijn wordt aangeroepen.

## <a name="type-mapping-for-sql-server"></a>Toewijzing van het type voor SQL server
Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel Hallo kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello 2 stap benadering te volgen:

1. Systeemeigen bron typen too.NET type converteren
2. Converteren van .NET-type toonative sink-type

Als zwevend gegevens te & van SQL server, Hallo gebruikt volgende toewijzingen van de SQL-type too.NET type en vice versa.

Hallo-toewijzing is hetzelfde als SQL Server gegevenstypetoewijzing voor ADO.NET Hallo.

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

## <a name="mapping-source-toosink-columns"></a>Toewijzing toosink bronkolommen
toomap kolommen uit de bron gegevensset toocolumns uit sink gegevensset, Zie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-copy"></a>Herhaalbare kopiëren
Bij het kopiëren van gegevens tooSQL Server-Database, voegt Hallo kopieeractiviteit gegevenstabel toohello sink standaard. een UPSERT tooperform in plaats daarvan Zie [herhaalbare schrijven tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artikel. 

Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten. In Azure Data Factory, kunt u een segment handmatig opnieuw. U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt. Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd. Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Prestaties en het afstemmen
Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.
