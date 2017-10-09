---
title: aaaFile en compressie-notaties in Azure Data Factory | Microsoft Docs
description: Meer informatie over bestandsindelingen hello wordt ondersteund door Azure Data Factory.
keywords: "BLOB-gegevens, azure-blob kopiëren"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9d40517b059fc533776bcc088db8c531ee5b003d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a>Bestands- en compressie indelingen die worden ondersteund door Azure Data Factory
*Dit onderwerp geldt toohello connectors te volgen: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [bestandssysteem](data-factory-onprem-file-system-connector.md), [ FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), en [SFTP](data-factory-sftp-connector.md).*

Azure Data Factory ondersteunt Hallo typen bestandsindelingen te volgen:

* [Tekstopmaak](#text-format)
* [JSON-indeling](#json-format)
* [Avro-indeling](#avro-format)
* [ORC-indeling](#orc-format)
* [Parketvloeren-indeling](#parquet-format)

## <a name="text-format"></a>Tekstopmaak
Als u tooread uit een tekstbestand of tooa tekstbestand schrijven, stelt u Hallo `type` eigenschap in Hallo `format` sectie van het Hallo-gegevensset te**TextFormat**. U kunt ook opgeven Hallo volgende **optionele** eigenschappen in Hallo `format` sectie. Zie [TextFormat voorbeeld](#textformat-example) sectie over het tooconfigure.

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| columnDelimiter |Hallo teken tooseparate kolommen in een bestand gebruikt. U kunt toouse een zeldzame niet-afdrukbaar teken die waarschijnlijk niet bestaat in uw gegevens. Geef bijvoorbeeld '\u0001', waarmee de Start van kop (SOH). |Er is slechts één teken toegestaan. Hallo **standaard** waarde is **met door komma's (',')**. <br/><br/>toouse Unicode-teken te verwijzen[Unicode-tekens](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello overeenkomstige code voor deze. |Nee |
| rowDelimiter |Hallo teken tooseparate rijen in een bestand gebruikt. |Er is slechts één teken toegestaan. Hallo **standaard** waarde is een van de volgende waarden op lezen Hallo: **['\r\n', '\r', '\n']** en **'\r\n'** op schrijven. |Nee |
| escapeChar |Hallo speciaal teken tooescape een kolomscheidingsteken in inhoud van invoerbestand Hallo gebruikt. <br/><br/>Het is niet mogelijk om zowel escapeChar als quoteChar voor een tabel op te geven. |Er is slechts één teken toegestaan. Er is geen standaardwaarde. <br/><br/>Voorbeeld: als er een door komma's (', ') als scheidingsteken voor Hallo kolommen, maar u toohave hello kommateken in de tekst hello wilt (voorbeeld: "Hallo, wereld"), kunt u definiëren '$' als Hallo escape-teken en gebruiken van de tekenreeks "$Hallo, wereld" in de Hallo bron. |Nee |
| quoteChar |Hallo teken gebruikt tooquote een string-waarde. Hallo kolom en rij scheidingstekens binnen de aanhalingstekens Hallo zou worden beschouwd als onderdeel van Hallo string-waarde. Deze eigenschap is van toepassing tooboth invoer- en uitvoergegevenssets.<br/><br/>Het is niet mogelijk om zowel escapeChar als quoteChar voor een tabel op te geven. |Er is slechts één teken toegestaan. Er is geen standaardwaarde. <br/><br/>Bijvoorbeeld, als er een door komma's (', ') als scheidingsteken voor Hallo kolommen, maar u toohave kommateken in de tekst hello wilt (voorbeeld: < Hallo, wereld >), kunt u definiëren ' (dubbel aanhalingsteken) als Hallo aanhalingsteken en gebruiken van Hallo tekenreeks "Hallo, wereld" in hello bron. |Nee |
| nullValue |Een of meer tekens gebruikt toorepresent een null-waarde. |Een of meer tekens. Hallo **standaard** waarden zijn **'\N' en 'NULL'** bij lezen en **'\N'** op schrijven. |Nee |
| encodingName |Hallo coderingsnaam opgeven. |Een geldige coderingsnaam. Zie [De eigenschap Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx). Voorbeeld: windows 1250 of shift_jis. Hallo **standaard** waarde is **UTF-8**. |Nee |
| firstRowAsHeader |Hiermee geeft u op of tooconsider Hallo eerste rij als een koptekst. Bij een gegevensset voor invoer leest Data Factory de eerste rij als een header. Bij een gegevensset voor uitvoer schrijft Data Factory de eerste rij als een header. <br/><br/>Zie [Gebruiksscenario's`firstRowAsHeader` en `skipLineCount` ](#scenarios-for-using-firstrowasheader-and-skiplinecount) voor voorbeeldscenario's. |True<br/><b>False (standaard)</b> |Nee |
| skipLineCount |Geeft het aantal rijen tooskip Hallo bij het lezen van gegevens uit invoerbestanden. Als zowel skipLineCount en firstRowAsHeader zijn opgegeven, Hallo regels eerst worden overgeslagen en wordt Hallo koptekstgegevens gelezen uit het invoerbestand Hallo. <br/><br/>Zie [Gebruiksscenario's`firstRowAsHeader` en `skipLineCount` ](#scenarios-for-using-firstrowasheader-and-skiplinecount) voor voorbeeldscenario's. |Geheel getal |Nee |
| treatEmptyAsNull |Hiermee geeft u op of tootreat null of lege tekenreeks als een null-waarde wanneer lezen van gegevens uit een bestand voor invoer. |**True (standaard)**<br/>False |Nee |

### <a name="textformat-example"></a>Voorbeeld van TextFormat
In Hallo JSON-definitie voor een gegevensset te volgen, worden enkele van de optionele eigenschappen Hallo opgegeven.

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

toouse een `escapeChar` in plaats van `quoteChar`, vervang Hallo regel met `quoteChar` Hello escapeChar te volgen:

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a>Scenario's voor het gebruik van firstRowAsHeader en skipLineCount
* U kopieert uit een tekstbestand voor niet-bestandsbron tooa en tooadd een kopregel die Hallo schemametagegevens bevatten (bijvoorbeeld: SQL-schema). Geef `firstRowAsHeader` als waar zijn in de uitvoergegevensset Hallo voor dit scenario.
* U kopieert uit een tekstbestand met een header regel tooa niet bestand sink en wilt toodrop die regel. Geef `firstRowAsHeader` echte in Hallo invoergegevensset.
* U kopieert uit een tekstbestand en tooskip een paar regels aan begin Hallo die geen gegevens of header-gegevens bevatten. Geef `skipLineCount` tooindicate Hallo aantal regels toobe overgeslagen. Als Hallo rest van Hallo-bestand een kopregel bevat, u kunt ook opgeven `firstRowAsHeader`. Als beide `skipLineCount` en `firstRowAsHeader` zijn opgegeven, Hallo regels eerst worden overgeslagen en wordt Hallo koptekstgegevens gelezen uit het invoerbestand Hallo

## <a name="json-format"></a>JSON-indeling
te**importeren/exporteren als een JSON-bestand-is naar/van Azure DB die Cosmos**, Hallo Zie [voor importeren/exporteren JSON-documenten](data-factory-azure-documentdb-connector.md#importexport-json-documents) in sectie [gegevens verplaatsen naar/van Azure DB die Cosmos](data-factory-azure-documentdb-connector.md) artikel.

Als u wilt dat tooparse Hallo JSON-bestanden of Hallo-gegevens in JSON-indeling schrijven, stel Hallo `type` eigenschap in Hallo `format` te sectie**JsonFormat**. U kunt ook opgeven Hallo volgende **optionele** eigenschappen in Hallo `format` sectie. Zie [JsonFormat voorbeeld](#jsonformat-example) sectie over het tooconfigure.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| filePattern |Hallo-patroon van de gegevens die zijn opgeslagen in elk JSON-bestand aangeven. Toegestane waarden zijn **setOfObjects** en **arrayOfObjects**. Hallo **standaard** waarde is **setOfObjects**. Zie het gedeelte [JSON-bestandpatronen](#json-file-patterns) voor meer informatie over deze patronen. |Nee |
| jsonNodeReference | Als u tooiterate wilt en gegevens uit het Hallo-objecten in een matrix ophalen veld Hello hetzelfde patroon, geeft u Hallo JSON-pad van de matrix. Deze eigenschap wordt alleen ondersteund bij het kopiëren van gegevens uit JSON-bestanden. | Nee |
| jsonPathDefinition | Hallo JSON-pad-expressie voor elke kolomtoewijzing met een aangepaste kolomnaam (start met kleine) opgeven. Deze eigenschap wordt alleen ondersteund bij het kopiëren van gegevens uit JSON-bestanden. U kunt gegevens ophalen uit het object of een matrix. <br/><br/> Voor velden onder hoofdobject beginnen met hoofdmap $; voor velden binnen het Hallo-matrix door gekozen `jsonNodeReference` begin vanaf matrixelement Hallo-eigenschap. Zie [JsonFormat voorbeeld](#jsonformat-example) sectie over het tooconfigure. | Nee |
| encodingName |Hallo coderingsnaam opgeven. Zie voor Hallo lijst met geldige namen voor codering: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) eigenschap. Bijvoorbeeld: windows 1250 of shift_jis. Hallo **standaard** waarde is: **UTF-8**. |Nee |
| nestingSeparator |Teken gebruikte tooseparate aantal geneste niveaus. Hallo-standaardwaarde is '.' (punt). |Nee |

### <a name="json-file-patterns"></a>JSON-bestandpatronen

Kopieeractiviteit kan parseren Hallo patronen van JSON-bestanden te volgen:

- **Type I: setOfObjects**

    Elk bestand bevat één object of meerdere door regels gescheiden/samengevoegde objecten. Wanneer deze optie is geselecteerd in een uitvoergegevensset, produceert de kopieerbewerking een enkel JSON-bestand met één object per regel (door regels gescheiden).

    * **voorbeeld van JSON-bestand met één object**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * **voorbeeld van JSON-bestand dat door regels is gescheiden**

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * **voorbeeld van JSON-bestand met samengevoegde objecten**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- **Type II: arrayOfObjects**

    Elk bestand bevat een matrix met objecten.

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

### <a name="jsonformat-example"></a>Voorbeeld van JsonFormat

**Voorbeeld 1: gegevens uit JSON-bestanden kopiëren**

Zie Hallo twee steekproeven te volgen bij het kopiëren van gegevens van JSON-bestanden. Hallo algemene punten toonote:

**Voorbeeld 1: gegevens ophalen uit object en matrix**

In dit voorbeeld verwacht u dat een hoofdmap JSON-object toegewezen toosingle record in tabelvorm resultatenset. Als u een JSON-bestand Hello volgende inhoud hebt:  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```
en u wilt dat deze naar een Azure SQL-tabel in de volgende Hallo-indeling, door het extraheren van gegevens uit zowel objecten als matrix toocopy:

| id | deviceType | targetResourceType | resourceManagmentProcessRunId | occurrenceTime |
| --- | --- | --- | --- | --- |
| ed0e4960-d9c5-11e6-85dc-d7996816aad3 | Pc | Microsoft.Compute/virtualMachines | 827f8aaa-ab72-437c-ba48-d8917a7336a3 | 13/1/2017 11:24:37 uur |

Hallo invoergegevensset met **JsonFormat** type is als volgt gedefinieerd: (gedeeltelijke definitie met alleen relevante Hallo delen). Met name:

- `structure`sectie definieert Hallo aangepast kolomnamen en het bijbehorende gegevenstype Hallo tijdens het converteren van tootabular gegevens. Deze sectie is **optionele** tenzij u de kolomtoewijzing toodo hoeft. Zie [toewijzen gegevensset kolommen toodestination gegevensset bronkolommen](data-factory-map-columns.md) sectie voor meer informatie.
- `jsonPathDefinition`Hiermee geeft u Hallo JSON-pad voor elke kolom waarmee wordt aangegeven waar tooextract Hallo gegevens uit. toocopy gegevens van een matrix, kunt u **matrix [x] .property** tooextract waarde Hallo gegeven eigenschap Hallo x objecten of u kunt gebruiken  **matrix [*] .property** toofind Hallo-waarde van een object met deze eigenschap.

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}      
        }
    }
}
```

**Voorbeeld 2: toepassing kruislingse meerdere objecten met dezelfde patroon van een matrix Hallo**

In dit voorbeeld kunt u één hoofdmap JSON-object tootransform in meerdere records in tabelvorm resultaat verwacht. Als u een JSON-bestand Hello volgende inhoud hebt:  

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```
en u wilt dat deze naar een Azure SQL-tabel in de volgende Hallo-indeling, door het Hallo-gegevens binnen de matrix Hallo afvlakken toocopy cross join met Hallo algemene hoofdmap gegevens:

| ordernumber | orderdate | order_pd | order_price | city |
| --- | --- | --- | --- | --- |
| 01 | 20170122 | P1 | 23 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P2 | 13 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P3 | 231 | [{"sanmateo":"No 1"}] |

Hallo invoergegevensset met **JsonFormat** type is als volgt gedefinieerd: (gedeeltelijke definitie met alleen relevante Hallo delen). Met name:

- `structure`sectie definieert Hallo aangepast kolomnamen en het bijbehorende gegevenstype Hallo tijdens het converteren van tootabular gegevens. Deze sectie is **optionele** tenzij u de kolomtoewijzing toodo hoeft. Zie [toewijzen gegevensset kolommen toodestination gegevensset bronkolommen](data-factory-map-columns.md) sectie voor meer informatie.
- `jsonNodeReference`Hiermee wordt aangegeven tooiterate en gegevens te extraheren uit het Hallo-objecten met dezelfde patroon onder Hallo **matrix** orderlines.
- `jsonPathDefinition`Hiermee geeft u Hallo JSON-pad voor elke kolom waarmee wordt aangegeven waar tooextract Hallo gegevens uit. In dit voorbeeld zijn 'ordernumber', 'orderdate' en 'plaats' onder hoofdobject met JSON-pad beginnen met "$.", terwijl 'order_pd' en 'order_price' worden gedefinieerd met het pad dat is afgeleid van een matrixelement Hallo zonder "$"..

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}         
        }
    }
}
```

**Houd er rekening mee Hallo volgende punten:**

* Als hello `structure` en `jsonPathDefinition` zijn niet gedefinieerd in de Data Factory-gegevensset hello, hello Kopieeractiviteit detecteert schema van de eerste object Hallo Hallo en plat Hallo gehele object.
* Als Hallo JSON-invoer een matrix heeft, standaard zet Hallo Kopieeractiviteit Hallo volledige Matrixwaarde in een tekenreeks. U kunt tooextract gegevens met behulp van `jsonNodeReference` en/of `jsonPathDefinition`, of door op te geven niet in overslaan `jsonPathDefinition`.
* Als er dubbele namen op hetzelfde niveau hello, Hallo Kopieeractiviteit uitgelicht Hallo laatste.
* Eigenschapnamen zijn hoofdlettergevoelig. Twee eigenschappen met dezelfde naam maar met een verschil in hoofdletters en kleine letters worden behandeld als twee afzonderlijke eigenschappen.

**Voorbeeld 2: Schrijven tooJSON gegevensbestand**

Als u Hallo tabel in SQL-Database hebt:

| id | order_date | order_price | order_by |
| --- | --- | --- | --- |
| 1 | 20170119 | 2000 | David |
| 2 | 20170120 | 3500 | Patrick |
| 3 | 20170121 | 4000 | Jason |

en u voor elke record in de volgende indeling Hallo toowrite tooa JSON-object verwacht:
```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

Hallo uitvoergegevensset met **JsonFormat** type is als volgt gedefinieerd: (gedeeltelijke definitie met alleen relevante Hallo delen). Meer specifiek, `structure` sectie Hallo aangepast eigenschapnamen worden gedefinieerd in doelbestand, `nestingSeparator` (standaardwaarde is ".") gebruikte tooidentify Hallo nest laag uit Hallo naam zijn. Deze sectie is **optionele** tenzij u wilt vergelijken met de naam van bronkolom Hallo-eigenschapsnaam voor toochange of sommige Hallo-eigenschappen worden genest.

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

## <a name="avro-format"></a>AVRO-indeling
Als u wilt dat tooparse hello Avro bestanden of Hallo-gegevens in de Avro-indeling schrijven, ingesteld Hallo `format` `type` eigenschap te**AvroFormat**. U hoeft geen eigenschappen in Hallo indeling sectie binnen Hallo typeProperties sectie niet toospecify. Voorbeeld:

```json
"format":
{
    "type": "AvroFormat",
}
```

toouse Avro-indeling in een Hive-tabel, kunt u verwijzen te[van Apache Hive zelfstudie](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).

Houd er rekening mee Hallo volgende punten:  

* [Complexe gegevenstypen](http://avro.apache.org/docs/current/spec.html#schema_complex) worden niet ondersteund (registreert enums, matrices, kaarten, samenvoegingen, en vaste).

## <a name="orc-format"></a>ORC-indeling
Als u wilt dat tooparse hello ORC-bestanden of Hallo-gegevens in ORC-indeling schrijven, ingesteld Hallo `format` `type` eigenschap te**OrcFormat**. U hoeft geen eigenschappen in Hallo indeling sectie binnen Hallo typeProperties sectie niet toospecify. Voorbeeld:

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> Als u geen ORC-bestanden kopieert **als-is** tussen on-premises en cloud gegevensarchieven, moet u tooinstall Hallo JRE 8 (Java Runtime Environment) op uw computer met de gateway. Een 64-bits-gateway vereist 64-bits JRE en 32-bits JRE is vereist voor een 32-bits-gateway. U vindt beide versies [hier](http://go.microsoft.com/fwlink/?LinkId=808605). Hallo juiste wachtwoord kiezen.
>
>

Houd er rekening mee Hallo volgende punten:

* Complexe gegevenstypen worden niet ondersteund (STRUCT, MAP, LIST, UNION)
* Een ORC-bestand heeft drie [opties voor compressie](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY. Data Factory ondersteunt het lezen van gegevens uit ORC-bestanden in een van deze gecomprimeerde indelingen. Hierbij Hallo compressie codec bevindt zich in Hallo metagegevens tooread Hallo gegevens. Echter, bij het schrijven van tooan ORC bestand Data Factory kiest ZLIB, dit is de standaardoptie Hallo voor ORC. Er is momenteel geen optie toooverride dit gedrag.

## <a name="parquet-format"></a>Parketvloeren-indeling
Als u tooparse Hallo parketvloeren bestanden wilt of Hallo-gegevens in de indeling parketvloeren schrijven, ingesteld Hallo `format` `type` eigenschap te**ParquetFormat**. U hoeft geen eigenschappen in Hallo indeling sectie binnen Hallo typeProperties sectie niet toospecify. Voorbeeld:

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> Als u geen parketvloeren bestanden kopieert **als-is** tussen on-premises en cloud gegevensarchieven, moet u tooinstall Hallo JRE 8 (Java Runtime Environment) op uw computer met de gateway. Een 64-bits-gateway vereist 64-bits JRE en 32-bits JRE is vereist voor een 32-bits-gateway. U vindt beide versies [hier](http://go.microsoft.com/fwlink/?LinkId=808605). Hallo juiste wachtwoord kiezen.
>
>

Houd er rekening mee Hallo volgende punten:

* Complexe gegevenstypen worden niet ondersteund (MAP, LIST)
* Parketvloeren bestand heeft Hallo volgend opties voor compressie: NONE, SNAPPY GZIP en LZO. Data Factory ondersteunt het lezen van gegevens uit ORC-bestanden in een van deze gecomprimeerde indelingen. Hallo compressiecodec wordt gebruikt in Hallo metagegevens tooread Hallo gegevens. Echter bij het schrijven van tooa parketvloeren bestand kiest Data Factory SNAPPY, dit is de standaardoptie Hallo voor parketvloeren-indeling. Er is momenteel geen optie toooverride dit gedrag.

## <a name="compression-support"></a>Compressieondersteuning
Verwerking van grote gegevenssets kan leiden tot i/o en netwerk knelpunten. Daarom kunt gecomprimeerde gegevens via stores niet alleen gegevensoverdracht via Hallo netwerk versnellen en schijfruimte te besparen, maar ook brengen aanzienlijke prestatieverbeteringen bij het verwerken van big data. Compressie wordt momenteel ondersteund voor de opgeslagen gegevens op basis van bestanden zoals Azure Blob- of On-premises bestandssysteem.  

toospecify compressie voor een gegevensset, gebruik Hallo **compressie** eigenschap in Hallo gegevensset JSON zoals Hallo volgt in:   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```

Stel Hallo voorbeeldgegevensset wordt gebruikt als uitvoer van een kopieeractiviteit hello, uitvoergegevens met GZIP codec met optimale verhouding Hallo kopie activiteit gecomprimeerd hello- en vervolgens Hallo gecomprimeerde gegevens schrijven naar een bestand met de naam pagecounts.csv.gz in hello Azure Blob Storage.

> [!NOTE]
> Compressie-instellingen worden niet ondersteund voor gegevens in Hallo **AvroFormat**, **OrcFormat**, of **ParquetFormat**. Bij het lezen van bestanden in de volgende indelingen worden Data Factory detecteert en Hallo-compressiecodec in Hallo-metagegevens gebruikt. Bij het schrijven van toofiles in de volgende indelingen, kiest Data Factory Hallo standaard compressiecodec voor die indeling. Bijvoorbeeld, ZLIB voor OrcFormat en SNAPPY voor ParquetFormat.   

Hallo **compressie** sectie heeft twee eigenschappen:  

* **Type:** Hallo compressiecodec, wat kan **GZIP**, **Deflate**, **BZIP2**, of **ZipDeflate**.  
* **Niveau:** Hallo compressieverhouding, wat kan **optimale** of **snelst**.

  * **Snelste:** Hallo compressie bewerking zo snel mogelijk, moet uitvoeren, zelfs als het resulterende bestand Hallo niet optimaal is gecomprimeerd.
  * **Optimale**: Hallo compressie bewerking moet worden optimaal gecomprimeerd, zelfs als Hallo bewerking een langere tijd toocomplete duurt.

    Zie voor meer informatie [compressieniveau](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) onderwerp.

Wanneer u opgeeft `compression` eigenschap in een invoergegevensset JSON Hallo pijplijn gecomprimeerde gegevens van Hallo source; kan lezen en wanneer u de eigenschap Hallo in een uitvoergegevensset JSON opgeeft, Hallo kopieeractiviteit gecomprimeerde gegevens toohello bestemming kunt schrijven. Hier volgen enkele voorbeeldscenario's:

* GZIP gecomprimeerde gegevens lezen uit een Azure-blob en decomprimeren van het resultaat gegevens tooan Azure SQL-database te schrijven. U definieert hello Azure Blob invoergegevensset Hello `compression` `type` JSON eigenschap GZIP.
* Gegevens lezen uit een tekstbestand van on-premises bestandssysteem, comprimeren met behulp van GZip-indeling en schrijf Hallo gecomprimeerde gegevens tooan Azure-blob. U definieert een uitvoer-Azure Blob-gegevensset Hello `compression` `type` JSON eigenschap GZip.
* ZIP-bestand lezen van FTP-server decomprimeren tooget Hallo bestanden binnen en de bestanden neerzetten in Azure Data Lake Store. Definieert u een FTP-invoergegevensset Hello `compression` `type` JSON eigenschap ZipDeflate.
* Een GZIP-gecomprimeerde gegevens lezen uit een Azure-blob, decomprimeren, comprimeren met behulp van BZIP2 en resultaat gegevens tooan Azure blob schrijven. U definieert Hallo invoer Azure Blob-gegevensset met `compression` `type` tooGZIP ingesteld en Hallo uitvoergegevensset met `compression` `type` tooBZIP2 in dit geval ingesteld.   


## <a name="next-steps"></a>Volgende stappen
Zie de volgende artikelen voor bestandsgebaseerde gegevensarchieven ondersteund door Azure Data Factory Hallo:

- [Azure Blob Storage](data-factory-azure-blob-connector.md)
- [Azure Data Lake Store](data-factory-azure-datalake-connector.md)
- [FTP](data-factory-ftp-connector.md)
- [HDFS](data-factory-hdfs-connector.md)
- [Bestandssysteem](data-factory-onprem-file-system-connector.md)
- [Amazon S3](data-factory-amazon-simple-storage-service-connector.md)
