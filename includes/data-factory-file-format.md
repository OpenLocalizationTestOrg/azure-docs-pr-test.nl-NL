## <a name="specifying-formats"></a>Indelingen opgeven
Azure Data Factory ondersteunt Hallo indelingstypen te volgen:

* [Tekstindeling](#specifying-textformat)
* [JSON-indeling](#specifying-jsonformat)
* [Avro-indeling](#specifying-avroformat)
* [ORC-indeling](#specifying-orcformat)
* [Parquet-indeling](#specifying-parquetformat)

### <a name="specifying-textformat"></a>TextFormat opgeven
Als u wilt dat tooparse Hallo tekstbestanden of Hallo-gegevens in tekstindeling schrijven, ingesteld Hallo `format` `type` eigenschap te**TextFormat**. U kunt ook opgeven Hallo volgende **optionele** eigenschappen in Hallo `format` sectie. Zie [TextFormat voorbeeld](#textformat-example) sectie over het tooconfigure.

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| columnDelimiter |Hallo teken tooseparate kolommen in een bestand gebruikt. Kunt u overwegen toouse een zeldzame niet-afdrukbaar teken die waarschijnlijk niet voorkomt in uw gegevens: bijvoorbeeld '\u0001' waarmee de Start van kop (SOH) opgeven. |Er is slechts één teken toegestaan. Hallo **standaard** waarde is **met door komma's (',')**. <br/><br/>toouse een Unicode-teken te verwijzen[Unicode-tekens](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello overeenkomstige code voor deze. |Nee |
| rowDelimiter |Hallo teken tooseparate rijen in een bestand gebruikt. |Er is slechts één teken toegestaan. Hallo **standaard** waarde is een van de volgende waarden op lezen Hallo: **['\r\n', '\r', '\n']** en **'\r\n'** op schrijven. |Nee |
| escapeChar |Hallo speciaal teken tooescape een kolomscheidingsteken in inhoud van invoerbestand Hallo gebruikt. <br/><br/>Het is niet mogelijk om zowel escapeChar als quoteChar voor een tabel op te geven. |Er is slechts één teken toegestaan. Er is geen standaardwaarde. <br/><br/>Voorbeeld: als er een door komma's (', ') als scheidingsteken voor Hallo kolommen, maar u toohave hello kommateken in de tekst hello wilt (voorbeeld: "Hallo, wereld"), kunt u definiëren '$' als Hallo escape-teken en gebruiken van de tekenreeks "$Hallo, wereld" in de Hallo bron. |Nee |
| quoteChar |Hallo teken gebruikt tooquote een string-waarde. Hallo kolom en rij scheidingstekens binnen de aanhalingstekens Hallo zou worden beschouwd als onderdeel van Hallo string-waarde. Deze eigenschap is van toepassing tooboth invoer- en uitvoergegevenssets.<br/><br/>Het is niet mogelijk om zowel escapeChar als quoteChar voor een tabel op te geven. |Er is slechts één teken toegestaan. Er is geen standaardwaarde. <br/><br/>Bijvoorbeeld, als er een door komma's (', ') als scheidingsteken voor Hallo kolommen, maar u toohave kommateken in de tekst hello wilt (voorbeeld: < Hallo, wereld >), kunt u definiëren ' (dubbel aanhalingsteken) als Hallo aanhalingsteken en gebruiken van Hallo tekenreeks "Hallo, wereld" in hello bron. |Nee |
| nullValue |Een of meer tekens gebruikt toorepresent een null-waarde. |Een of meer tekens. Hallo **standaard** waarden zijn **'\N' en 'NULL'** bij lezen en **'\N'** op schrijven. |Nee |
| encodingName |Hallo coderingsnaam opgeven. |Een geldige coderingsnaam. Zie [De eigenschap Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx). Voorbeeld: windows 1250 of shift_jis. Hallo **standaard** waarde is **UTF-8**. |Nee |
| firstRowAsHeader |Hiermee geeft u op of tooconsider Hallo eerste rij als een koptekst. Bij een gegevensset voor invoer leest Data Factory de eerste rij als een header. Bij een gegevensset voor uitvoer schrijft Data Factory de eerste rij als een header. <br/><br/>Zie [Gebruiksscenario's`firstRowAsHeader` en `skipLineCount` ](#scenarios-for-using-firstrowasheader-and-skiplinecount) voor voorbeeldscenario's. |True<br/>**False (standaard)** |Nee |
| skipLineCount |Geeft het aantal rijen tooskip Hallo bij het lezen van gegevens uit invoerbestanden. Als zowel skipLineCount en firstRowAsHeader zijn opgegeven, Hallo regels eerst worden overgeslagen en wordt Hallo koptekstgegevens gelezen uit het invoerbestand Hallo. <br/><br/>Zie [Gebruiksscenario's`firstRowAsHeader` en `skipLineCount` ](#scenarios-for-using-firstrowasheader-and-skiplinecount) voor voorbeeldscenario's. |Geheel getal |Nee |
| treatEmptyAsNull |Hiermee geeft u op of tootreat null of lege tekenreeks als een null-waarde wanneer lezen van gegevens uit een bestand voor invoer. |**True (standaard)**<br/>False |Nee |

#### <a name="textformat-example"></a>Voorbeeld van TextFormat
Hallo volgende voorbeeld ziet u enkele eigenschappen Hallo voor TextFormat.

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

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a>Scenario's voor het gebruik van firstRowAsHeader en skipLineCount
* U kopieert uit een tekstbestand voor niet-bestandsbron tooa en tooadd een kopregel die Hallo schemametagegevens bevatten (bijvoorbeeld: SQL-schema). Geef `firstRowAsHeader` als waar zijn in de uitvoergegevensset Hallo voor dit scenario.
* U kopieert uit een tekstbestand met een header regel tooa niet bestand sink en wilt toodrop die regel. Geef `firstRowAsHeader` echte in Hallo invoergegevensset.
* U kopieert uit een tekstbestand en tooskip een paar regels aan begin Hallo die geen gegevens of header-gegevens bevatten. Geef `skipLineCount` tooindicate Hallo aantal regels toobe overgeslagen. Als Hallo rest van Hallo-bestand een kopregel bevat, u kunt ook opgeven `firstRowAsHeader`. Als beide `skipLineCount` en `firstRowAsHeader` zijn opgegeven, Hallo regels eerst worden overgeslagen en wordt Hallo koptekstgegevens gelezen uit het invoerbestand Hallo

### <a name="specifying-jsonformat"></a>JsonFormat opgeven
te**als JSON-bestanden voor importeren/exporteren-is naar/van Azure DB die Cosmos**, Zie [voor importeren/exporteren JSON-documenten](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) sectie in hello Azure Cosmos DB connector met details.

Als u wilt dat tooparse Hallo JSON-bestanden of Hallo-gegevens in JSON-indeling schrijven, stel Hallo `format` `type` eigenschap te**JsonFormat**. U kunt ook opgeven Hallo volgende **optionele** eigenschappen in Hallo `format` sectie. Zie [JsonFormat voorbeeld](#jsonformat-example) sectie over het tooconfigure.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| filePattern |Hallo-patroon van de gegevens die zijn opgeslagen in elk JSON-bestand aangeven. Toegestane waarden zijn **setOfObjects** en **arrayOfObjects**. Hallo **standaard** waarde is **setOfObjects**. Zie het gedeelte [JSON-bestandpatronen](#json-file-patterns) voor meer informatie over deze patronen. |Nee |
| jsonNodeReference | Als u tooiterate wilt en gegevens uit het Hallo-objecten in een matrix ophalen veld Hello hetzelfde patroon, geeft u Hallo JSON-pad van de matrix. Deze eigenschap wordt alleen ondersteund bij het kopiëren van gegevens uit JSON-bestanden. | Nee |
| jsonPathDefinition | Hallo JSON-pad-expressie voor elke kolomtoewijzing met een aangepaste kolomnaam (start met kleine) opgeven. Deze eigenschap wordt alleen ondersteund bij het kopiëren van gegevens uit JSON-bestanden. U kunt gegevens ophalen uit het object of een matrix. <br/><br/> Voor velden onder hoofdobject beginnen met hoofdmap $; voor velden binnen het Hallo-matrix door gekozen `jsonNodeReference` begin vanaf matrixelement Hallo-eigenschap. Zie [JsonFormat voorbeeld](#jsonformat-example) sectie over het tooconfigure. | Nee |
| encodingName |Hallo coderingsnaam opgeven. Zie voor Hallo lijst met geldige namen voor codering: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) eigenschap. Bijvoorbeeld: windows 1250 of shift_jis. Hallo **standaard** waarde is: **UTF-8**. |Nee |
| nestingSeparator |Teken gebruikte tooseparate aantal geneste niveaus. Hallo-standaardwaarde is '.' (punt). |Nee |

#### <a name="json-file-patterns"></a>JSON-bestandpatronen

Kopieerbewerkingen kunnen onderstaande patronen van JSON-bestanden parseren:

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

#### <a name="jsonformat-example"></a>Voorbeeld van JsonFormat

**Voorbeeld 1: gegevens uit JSON-bestanden kopiëren**

Hieronder twee soorten voorbeelden vindt u bij het kopiëren van gegevens van JSON-bestanden en algemene punten toonote Hallo:

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

- `structure`sectie definieert Hallo aangepast kolomnamen en het bijbehorende gegevenstype Hallo tijdens het converteren van tootabular gegevens. Deze sectie is **optionele** tenzij u de kolomtoewijzing toodo hoeft. Zie het gedeelte [Een structuurdefinitie opgeven voor rechthoekige gegevenssets](#specifying-structure-definition-for-rectangular-datasets) voor meer informatie.
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

- `structure`sectie definieert Hallo aangepast kolomnamen en het bijbehorende gegevenstype Hallo tijdens het converteren van tootabular gegevens. Deze sectie is **optionele** tenzij u de kolomtoewijzing toodo hoeft. Zie het gedeelte [Een structuurdefinitie opgeven voor rechthoekige gegevenssets](#specifying-structure-definition-for-rectangular-datasets) voor meer informatie.
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

Als u de onderstaande tabel hebt in SQL-Database:

| id | order_date | order_price | order_by |
| --- | --- | --- | --- |
| 1 | 20170119 | 2000 | David |
| 2 | 20170120 | 3500 | Patrick |
| 3 | 20170121 | 4000 | Jason |

en voor elke record verwacht toowrite tooa JSON-object in de onderstaande indeling:
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

Hallo uitvoergegevensset met **JsonFormat** type is als volgt gedefinieerd: (gedeeltelijke definitie met alleen relevante Hallo delen). Meer specifiek, `structure` sectie Hallo aangepast eigenschapnamen worden gedefinieerd in doelbestand, `nestingSeparator` (standaardwaarde is '. ') worden gebruikte tooidentify Hallo nest laag uit Hallo-naam. Deze sectie is **optionele** tenzij u wilt vergelijken met de naam van bronkolom Hallo-eigenschapsnaam voor toochange of sommige Hallo-eigenschappen worden genest.

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

### <a name="specifying-avroformat"></a>AvroFormat opgeven
Als u wilt dat tooparse hello Avro bestanden of Hallo-gegevens in de Avro-indeling schrijven, ingesteld Hallo `format` `type` eigenschap te**AvroFormat**. U hoeft geen eigenschappen in Hallo indeling sectie binnen Hallo typeProperties sectie niet toospecify. Voorbeeld:

```json
"format":
{
    "type": "AvroFormat",
}
```

toouse Avro-indeling in een Hive-tabel, kunt u verwijzen te[van Apache Hive zelfstudie](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).

Houd er rekening mee Hallo volgende punten:  

* [Complexe gegevenstypen](http://avro.apache.org/docs/current/spec.html#schema_complex) worden niet ondersteund (records, enums, matrices, kaarten, samenvoegingen en vaste bestanden).

### <a name="specifying-orcformat"></a>OrcFormat opgeven
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

### <a name="specifying-parquetformat"></a>ParquetFormat opgeven
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
