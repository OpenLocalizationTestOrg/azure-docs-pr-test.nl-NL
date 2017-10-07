---
title: aaaMove gegevens van Cassandra gebruik Data Factory | Microsoft Docs
description: Meer informatie over hoe toomove gegevens uit een Cassandra lokale database met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a>Verplaatsen van gegevens uit een on-premises Cassandra-database met behulp van Azure Data Factory
Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit een on-premises Cassandra-database. Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.

U kunt gegevens uit een on-premises Cassandra gegevens store tooany ondersteund sink gegevensopslag kopiëren. Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel. Data factory ondersteunt momenteel alleen verplaatsen van gegevens uit een data Cassandra tooother gegevensarchieven opslaan, maar niet voor het verplaatsen van gegevens uit andere winkels tooa Cassandra gegevens gegevensopslag. 

## <a name="supported-versions"></a>Ondersteunde versies
Hallo Cassandra connector ondersteunt Hallo volgende versies van Cassandra: 2.X.

## <a name="prerequisites"></a>Vereisten
Voor hello Azure Data Factory-service toobe kunnen tooconnect tooyour lokale Cassandra-database, moet u een Data Management Gateway installeren op Hallo dezelfde die hosts Hallo-database van de computer of op een afzonderlijke computer tooavoid concurreren voor bronnen met Hallo de database. Data Management Gateway is een onderdeel dat lokale gegevensbronnen toocloud services in een veilige en beheerde manier verbindt. Zie [Data Management Gateway](data-factory-data-management-gateway.md) voor meer informatie over Data Management Gateway. Zie [verplaatsen van gegevens uit de lokale toocloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies over het instellen van Hallo gateway een data pipeline toomove gegevens.

Zelfs als het Hallo-database wordt gehost in Hallo cloud, bijvoorbeeld op een virtuele machine van Azure IaaS, moet u Hallo gateway tooconnect tooa Cassandra database gebruiken. Y u Hallo-gateway kan hebben op dezelfde virtuele machine die hosts Hallo database Hallo of op een afzonderlijke virtuele machine zo lang Hallo gateway kunt verbinding maken met toohello database.  

Wanneer u Hallo-gateway installeert, installeert deze automatisch een Microsoft Cassandra ODBC-stuurprogramma gebruikt tooconnect tooCassandra database. Dus u hoeft niet toomanually stuurprogramma installeren op de gatewaycomputer Hallo bij het kopiëren van gegevens uit Hallo Cassandra database. 

> [!NOTE]
> Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises Cassandra-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's. 

- Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren. 
- U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit. 

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:

1. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.
2. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking. 
3. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer. 

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.  Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens uit een on-premises Cassandra-gegevensopslag zijn [JSON-voorbeeld: gegevens kopiëren van Cassandra tooAzure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) sectie van dit artikel. 

Hallo volgende secties vindt u informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooa Cassandra gegevensarchief zijn:

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooCassandra gekoppelde service.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |Hallo type eigenschap moet worden ingesteld op: **OnPremisesCassandra** |Ja |
| host |Een of meer IP-adressen of hostnamen van Cassandra servers.<br/><br/>Geef een door komma's gescheiden lijst met IP-adressen of namen tooconnect tooall hostservers gelijktijdig. |Ja |
| poort |toolisten Hello TCP-poort die Hallo Cassandra server gebruikt voor clientverbindingen. |Nee, de standaardwaarde: 9042 |
| authenticationType |Basic- of anonieme |Ja |
| gebruikersnaam |Geef de gebruikersnaam voor Hallo-gebruikersaccount. |Ja, als authenticationType tooBasic is ingesteld. |
| wachtwoord |Wachtwoord voor gebruikersaccount Hallo opgeven. |Ja, als authenticationType tooBasic is ingesteld. |
| gatewayName |Hallo-naam van Hallo-gateway die is gebruikt tooconnect toohello lokale Cassandra-database. |Ja |
| encryptedCredential |Referentie versleuteld door Hallo-gateway. |Nee |

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).

Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo. Hallo typeProperties sectie voor de gegevensset van het type **CassandraTable** heeft de volgende eigenschappen Hallo

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| met keyspace |Naam van Hallo keyspace of het schema in Cassandra-database. |Ja (als **query** voor **CassandraSource** is niet gedefinieerd). |
| tableName |Naam van de tabel Hallo in Cassandra-database. |Ja (als **query** voor **CassandraSource** is niet gedefinieerd). |

## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.

Terwijl de eigenschappen die beschikbaar zijn in Hallo typeProperties gedeelte van de activiteit Hallo variëren met elk activiteitstype. Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.

Wanneer de bron is van het type **CassandraSource**, Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| query |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-92 query of CQL query. Zie [CQL verwijzing](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html). <br/><br/>Wanneer u SQL-query gebruikt, geef **keyspace name.table naam** toorepresent Hallo tabel gewenste tooquery. |Nee (als tableName en keyspace op gegevensset zijn gedefinieerd). |
| consistencyLevel |Hallo consistentieniveau geeft het aantal replica's tooa leesaanvraag moet reageren voordat gegevens toohello clienttoepassing wordt geretourneerd. Cassandra controles Hallo opgegeven aantal replica's voor gegevens toosatisfy Hallo leesaanvraag. |EEN, TWEE, DRIE, QUORUM, ALL, LOCAL_QUORUM EACH_QUORUM, LOCAL_ONE. Zie [gegevensconsistentie configureren](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) voor meer informatie. |Nee. Standaardwaarde is een. |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a>JSON-voorbeeld: gegevens kopiëren van Cassandra tooAzure Blob
In dit voorbeeld voorbeeld JSON definities bevat dat u een pijplijn toocreate gebruiken met behulp van kunt [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Er wordt weergegeven hoe toocopy gegevens uit een lokale Cassandra tooan Azure Blob Storage-database. Gegevens kunnen echter wel gekopieerde tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.

> [!IMPORTANT]
> Dit voorbeeld bevat JSON-fragmenten. Dit omvat geen stapsgewijze instructies voor het maken van de gegevensfactory Hallo. Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies.

Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:

* Een gekoppelde service van het type [OnPremisesCassandra](#linked-service-properties).
* Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Invoer [gegevensset](data-factory-create-datasets.md) van het type [CassandraTable](#dataset-properties).
* Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [CassandraSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

**Cassandra gekoppelde service:**

In dit voorbeeld wordt Hallo **Cassandra** gekoppelde service. Zie [Cassandra gekoppelde service](#linked-service-properties) gedeelte voor het Hallo-eigenschappen die ondersteund worden door deze gekoppelde service.  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

**Gekoppelde Azure Storage-service:**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

**Cassandra invoergegevensset:**

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

Instelling **externe** te**true** informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.

**Azure Blob-uitvoergegevensset:**

Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**De kopieeractiviteit in een pijplijn met Cassandra bron en sink van Blob:**

Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**CassandraSource** en **sink** type is ingesteld, te**BlobSink**.

Zie [RelationalSource type-eigenschappen](#copy-activity-properties) voor Hallo lijst met eigenschappen die ondersteund worden door Hallo RelationalSource.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"

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

### <a name="type-mapping-for-cassandra"></a>Toewijzing van het type voor Cassandra
| Type Cassandra | .NET op basis van Type |
| --- | --- |
| ASCII |Tekenreeks |
| BIGINT |Int64 |
| BLOB |Byte] |
| BOOLEAANSE WAARDE |Booleaanse waarde |
| DECIMALE |Decimale |
| DOUBLE |dubbele |
| FLOAT |Één |
| INET |Tekenreeks |
| INT |Int32 |
| TEKST |Tekenreeks |
| TIJDSTEMPEL |Datum/tijd |
| TIMEUUID |GUID |
| UUID |GUID |
| VARCHAR |Tekenreeks |
| VARINT |Decimale |

> [!NOTE]
> Voor de verzameling van typen (kaart, set, lijst, enzovoort) te verwijzen[werken met Cassandra verzamelingtypen met behulp van de virtuele tabel](#work-with-collections-using-virtual-table) sectie.
>
> Gebruiker gedefinieerde typen worden niet ondersteund.
>
> Hallo-lengte van binaire kolom en String-lengte kan niet groter zijn dan 4000.
>
>

## <a name="work-with-collections-using-virtual-table"></a>Werken met behulp van de virtuele tabel verzamelingen
Azure Data Factory maakt gebruik van een ingebouwde ODBC-stuurprogramma tooconnect tooand gegevens kopiëren van de database Cassandra. Voor verzamelingtypen met inbegrip van de kaart, de verzameling en de lijst, renormalizes Hallo stuurprogramma Hallo gegevens in de bijbehorende virtuele tabellen. In het bijzonder als een tabel bevat de verzameling kolommen, genereert Hallo stuurprogramma Hallo virtuele tabellen te volgen:

* Een **basistabel**, die bevat Hallo dezelfde gegevens als Hallo echte tabel, met uitzondering Hallo verzameling kolommen. de basistabel Hallo gebruikt Hallo dezelfde naam als Hallo echte tabel die wordt vertegenwoordigd.
* Een **virtuele tabel** voor elke kolom collectie die geneste Hallo gegevens wordt uitgebreid. Hallo virtuele tabellen waarbij de verzamelingen zijn benoemde Hallo-naam van Hallo echte tabel, een scheidingsteken '*vt*' en naam van de Hallo van Hallo-kolom.

Virtuele tabellen verwijzen toohello-gegevens in de echte tabel hello, waardoor Hallo stuurprogramma tooaccess Hallo gedenormaliseerd gegevens. Zie het voorbeeld gedeelte voor meer informatie. Hallo-inhoud van Cassandra verzamelingen kunt u door het uitvoeren van query's en het toevoegen aan virtuele tabellen Hallo openen.

U kunt Hallo [Wizard kopiëren](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively weergeven Hallo lijst met tabellen in Cassandra database, inclusief Hallo virtuele tabellen en een voorbeeld van gegevens binnen Hallo. U kunt ook maakt u een query in de Wizard kopiëren Hallo en toosee Hallo resultaat valideren.

### <a name="example"></a>Voorbeeld
Hallo is volgende 'ExampleTable' bijvoorbeeld een databasetabel Cassandra die een geheel getal primaire-sleutelkolom met de naam 'pk_int', een tekstkolom benoemde waarde, een lijstkolom, een kaart kolom en een set-kolom (met de naam 'StringSet') bevat.

| pk_int | Waarde | Lijst | Kaart | StringSet |
| --- | --- | --- | --- | --- |
| 1 |'Voorbeeldwaarde 1' |["1", "2", "3"] |{"S1": "a", "S2": "b"} |{"A", "B", "C"} |
| 3 |"Voorbeeldwaarde 3" |["100", "101", "102", "105"] |{"S1": "t"} |{"A", "E"} |

Hallo stuurprogramma genereert meerdere virtuele tabellen toorepresent deze één tabel. Hallo refererende-sleutelkolommen in virtuele tabellen Hallo Hallo primaire-sleutelkolommen in Hallo echte tabel verwijzen naar en geven aan welke real tabelrij rij Hallo virtuele tabel komt overeen met.

de eerste virtuele tabel Hallo is Hallo basistabel met de naam 'ExampleTable' wordt weergegeven in de volgende tabel Hallo. de basistabel Hallo Hallo bevat dezelfde gegevens als de oorspronkelijke databasetabel hello, met uitzondering van Hallo verzamelingen, die worden weggelaten uit deze tabel en uitgevouwen in andere virtuele tabellen.

| pk_int | Waarde |
| --- | --- |
| 1 |'Voorbeeldwaarde 1' |
| 3 |"Voorbeeldwaarde 3" |

Hallo bevatten volgende tabellen Hallo virtuele tabellen die gegevens uit de lijst, toewijzing en StringSet kolommen Hallo Hallo renormalize. Hallo kolommen met namen die met '_index' of '_key eindigen' hello positie van gegevens binnen de oorspronkelijke lijst Hallo of kaart Hallo aangeven. Hallo kolommen met namen die met '_Waarde eindigen' bevatten Hallo uitgevouwen gegevens uit de verzameling Hallo.

#### <a name="table-exampletablevtlist"></a>Tabel 'ExampleTable_vt_List':
| pk_int | List_index | List_value |
| --- | --- | --- |
| 1 |0 |1 |
| 1 |1 |2 |
| 1 |2 |3 |
| 3 |0 |100 |
| 3 |1 |101 |
| 3 |2 |102 |
| 3 |3 |103 |

#### <a name="table-exampletablevtmap"></a>Tabel 'ExampleTable_vt_Map':
| pk_int | Map_key | Map_value |
| --- | --- | --- |
| 1 |S1 |A |
| 1 |S2 |B |
| 3 |S1 |T |

#### <a name="table-exampletablevtstringset"></a>Tabel 'ExampleTable_vt_StringSet':
| pk_int | StringSet_value |
| --- | --- |
| 1 |A |
| 1 |B |
| 1 |C |
| 3 |A |
| 3 |E |

## <a name="map-source-toosink-columns"></a>Bronkolommen toosink toewijzen
Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Herhaalbare leesbewerking van relationele bronnen
Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten. In Azure Data Factory, kunt u een segment handmatig opnieuw. U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt. Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd. Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Prestaties en het afstemmen
Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.
