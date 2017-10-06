---
title: gegevens uit gegevensarchieven ODBC aaaMove | Microsoft Docs
description: Meer informatie over hoe toomove gegevens van ODBC-gegevens worden opgeslagen met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a>Verplaatsen van gegevens van ODBC-gegevensarchieven met behulp van Azure Data Factory
Dit artikel wordt uitgelegd hoe toouse hello Kopieeractiviteit in Azure Data Factory toomove gegevens uit een on-premises ODBC gegevens opslaan. Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.

U kunt gegevens kopiëren van een ODBC data store tooany ondersteund sink-gegevensarchief. Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel. Data factory ondersteunt momenteel alleen verplaatsen van gegevens van een ODBC-gegevensbron tooother gegevensarchieven opslaan, maar niet voor het verplaatsen van gegevens uit andere gegevens winkels tooan ODBC data store. 

## <a name="enabling-connectivity"></a>Connectiviteit inschakelen
Data Factory-service ondersteunt verbindende tooon lokale ODBC-bronnen met behulp van Hallo Data Management Gateway. Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn artikel over Data Management Gateway en stapsgewijze instructies over het instellen van Hallo-gateway. Hallo gateway tooconnect tooan-ODBC-gegevensarchief gebruiken, zelfs als deze is opgenomen in een Azure IaaS VM.

U kunt Hallo gateway installeren op Hallo dezelfde on-premises machine of virtuele machine van Azure als gegevensopslag voor ODBC-Hallo Hallo. We raden u echter aan dat u Hallo-gateway op een afzonderlijke computer/Azure IaaS VM installeert tooavoid bronconflicten en voor betere prestaties. Wanneer u Hallo-gateway op een afzonderlijke computer installeert, is het Hallo-machine moeten kunnen tooaccess Hallo machine met Hallo ODBC data store.

Naast Hallo Data Management Gateway moet u ook tooinstall Hallo ODBC-stuurprogramma voor de gegevensopslag Hallo op Hallo gateway-apparaat.

> [!NOTE]
> Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een ODBC data store verplaatst met behulp van verschillende hulpprogramma's voor API's.

Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.

U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit. 

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren: 

1. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.
2. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking. 
3. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer. 

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.  Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens uit een ODBC data store zijn [JSON-voorbeeld: gegevens kopiëren van ODBC-gegevens opslaan tooAzure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) sectie van dit artikel. 

Hallo volgende secties bieden informatie over de JSON-eigenschappen die specifiek tooODBC gegevensopslag voor gebruikte toodefine Data Factory-entiteiten zijn:

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooODBC gekoppelde service.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |Hallo type eigenschap moet worden ingesteld op: **OnPremisesOdbc** |Ja |
| connectionString |Hallo niet access credential gedeelte van het Hallo-verbindingsreeks en een optionele versleuteld referentie. Zie de voorbeelden in Hallo uit te voeren. |Ja |
| referentie |Hallo toegang referentie gedeelte van het Hallo-verbindingsreeks die is opgegeven in de indeling van de eigenschapswaarde specifieke stuurprogramma's. Voorbeeld: "Uid =<user ID>; Pwd =<password>; RefreshToken =<secret refresh token>; '. |Nee |
| authenticationType |Type verificatie gebruikt tooconnect toohello ODBC-gegevensarchief. Mogelijke waarden zijn: anonieme en Basic. |Ja |
| gebruikersnaam |Geef de gebruikersnaam als u basisverificatie gebruikt. |Nee |
| wachtwoord |Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven. |Nee |
| gatewayName |Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello ODBC-gegevensarchief gebruiken. |Ja |

### <a name="using-basic-authentication"></a>Met behulp van basisverificatie

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a>Met behulp van basisverificatie met versleutelde referenties
U kunt versleutelen Hallo-referenties met een Hallo [nieuw AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) cmdlet (versie 1.0 van Azure PowerShell) of [nieuw AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 of een eerdere versie van Hallo Azure PowerShell).  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a>Anonieme verificatie

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a>Eigenschappen van gegevensset
Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).

Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo. Hallo typeProperties sectie voor de gegevensset van het type **RelationalTable** (waaronder ODBC gegevensset) heeft Hallo volgende eigenschappen

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| tableName |Naam van de tabel Hallo in Hallo ODBC-gegevensarchief. |Ja |

## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en beleidsregels zijn beschikbaar voor alle typen activiteiten.

Eigenschappen die beschikbaar zijn in Hallo **typeProperties** sectie Hallo-activiteit op Hallo daarentegen variëren met elk activiteitstype. Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.

In de kopieeractiviteit, wanneer de bron van het type **RelationalSource** (waaronder ODBC), Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| query |Hallo aangepaste query tooread gegevens worden gebruikt. |SQL-query-tekenreeks. Bijvoorbeeld: Selecteer * from MijnTabel. |Ja |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a>JSON-voorbeeld: gegevens kopiëren van gegevens van ODBC-tooAzure Blob opslaan
In dit voorbeeld bevat definities van de JSON die u een pijplijn toocreate gebruiken met behulp van kunt [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Er wordt weergegeven hoe toocopy van een ODBC-gegevensbron tooan Azure Blob Storage. Gegevens kunnen echter wel gekopieerde tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.

Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:

1. Een gekoppelde service van het type [OnPremisesOdbc](#linked-service-properties).
2. Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Hallo voorbeeld kopieert gegevens van de resultaten van een query in een ODBC data store tooa blob elk uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

Instellen als eerste stap Hallo data management gateway. Hallo-instructies vindt u in Hallo [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.

**ODBC gekoppelde service** in dit voorbeeld gebruikt Hallo basisverificatie. Zie [ODBC gekoppelde service](#linked-service-properties) sectie voor verschillende soorten verificatie die u kunt gebruiken.

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

**Een gekoppelde Azure Storage-service**

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

**ODBC-invoergegevensset**

Hallo-voorbeeld wordt ervan uitgegaan dat u een tabel "MijnTabel" hebt gemaakt in een ODBC-database en deze bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens.

Instelling 'extern': 'true' informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
        "typeProperties": {},
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

**Azure Blob-uitvoergegevensset**

Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1). pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


**Kopieeractiviteit in een pijplijn met ODBC-gegevensbron (RelationalSource) en Blob sink (BlobSink)**

Hallo pijplijn bevat een Kopieeractiviteit die is geconfigureerd toouse deze invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**RelationalSource** en **sink** type is ingesteld, te**BlobSink**. Hallo SQL-query is opgegeven voor Hallo **query** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
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
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a>Toewijzing van het type voor ODBC
Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello benadering in twee stappen te volgen:

1. Systeemeigen bron typen too.NET type converteren
2. Converteren van .NET-type toonative sink-type

Bij het verplaatsen van gegevens uit gegevensarchieven ODBC, ODBC-gegevenstypen zijn toegewezen too.NET typen zoals vermeld in Hallo [Gegevenstypetoewijzingen ODBC](https://msdn.microsoft.com/library/cc668763.aspx) onderwerp.

## <a name="map-source-toosink-columns"></a>Bronkolommen toosink toewijzen
Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Herhaalbare leesbewerking van relationele bronnen
Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten. In Azure Data Factory, kunt u een segment handmatig opnieuw. U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt. Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd. Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="ge-historian-store"></a>GE Historian store
Maken van een ODBC-gekoppelde service toolink een [GE Proficy Historian (nu GE Historian)](http://www.geautomation.com/products/proficy-historian) gegevensarchief tooan Azure-gegevensfactory zoals weergegeven in Hallo voorbeeld te volgen:

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

Data Management Gateway op een on-premises machine gateway installeren en registreren Hallo met Hallo-portal. Hallo-gateway is geïnstalleerd op uw lokale computer gebruikt Hallo ODBC-stuurprogramma voor GE Historian tooconnect toohello GE Historian gegevensarchief. Daarom Hallo stuurprogramma installeren als deze nog niet is geïnstalleerd op de gatewaycomputer Hallo. Zie [connectiviteit inschakelen](#enabling-connectivity) sectie voor meer informatie.

Voordat u Hallo GE Historian opslaan in een Data Factory-oplossing gebruikt, moet u controleren of Hallo gateway toohello gegevensarchief volgens de instructies in de volgende sectie Hallo verbinding kan maken.

Lees Hallo artikel vanaf Hallo voor een gedetailleerd overzicht van het gebruik van ODBC-gegevens worden opgeslagen als bron gegevensarchieven een kopieerbewerking.  

## <a name="troubleshoot-connectivity-issues"></a>Verbindingsproblemen oplossen
verbindingsproblemen tootroubleshoot, gebruik Hallo **Diagnostics** tabblad van **Data Management Gateway Configuration Manager**.

1. Start **Data Management Gateway Configuration Manager**. U kunt ofwel "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe' rechtstreeks (of) zoekopdracht uitvoeren voor **Gateway** toofind een koppeling te**Microsoft Data Management Gateway** de toepassing zoals weergegeven in Hallo installatiekopie te volgen.

    ![Gateway zoeken](./media/data-factory-odbc-connector/search-gateway.png)
2. Overschakelen van toohello **Diagnostics** tabblad.

    ![Gateway diagnostische gegevens](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. Selecteer Hallo **type** gegevens opslaan (gekoppelde service).
4. Geef **verificatie** en voer **referenties** (of) Voer **verbindingsreeks** die is gebruikt tooconnect toohello-gegevensarchief.
5. Klik op **verbinding testen** tootest Hallo verbinding toohello-gegevensarchief.

## <a name="performance-and-tuning"></a>Prestaties en het afstemmen
Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.
