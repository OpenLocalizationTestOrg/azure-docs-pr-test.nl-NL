---
title: aaaMove gegevens van de lokale HDFS | Microsoft Docs
description: Meer informatie over hoe toomove gegevens van de lokale HDFS met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a>Gegevens verplaatsen van de lokale HDFS met behulp van Azure Data Factory
Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit een lokale HDFS. Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.

U kunt gegevens uit HDFS tooany ondersteund sink gegevensarchief kopiëren. Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel. Data factory ondersteunt momenteel alleen zwevend gegevens uit een gegevensarchieven lokale HDFS tooother, maar niet voor het verplaatsen van gegevens van andere gegevens winkels tooan lokale HDFS.

> [!NOTE]
> Kopieeractiviteit worden Hallo-bronbestand niet verwijderd nadat het is gekopieerde toohello bestemming. Als u toodelete Hallo-bronbestand na een geslaagde kopie moet, maakt u een aangepaste activiteit toodelete Hallo-bestand en Hallo activiteit in de pijplijn hello gebruiken. 

## <a name="enabling-connectivity"></a>Connectiviteit inschakelen
Data Factory-service ondersteunt verbindende tooon lokale HDFS met Hallo Data Management Gateway. Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn artikel over Data Management Gateway en stapsgewijze instructies over het instellen van Hallo-gateway. Gebruik Hallo gateway tooconnect tooHDFS zelfs als deze is opgenomen in een Azure IaaS VM.

> [!NOTE]
> Zorg ervoor dat Hallo Data Management Gateway toegankelijk te**alle** Hallo [naam van knooppunt server]: [name knooppunt poort] en [knooppunt gegevensservers]: [knooppunt gegevenspoort] van Hallo Hadoop-cluster. Standaard [naam van knooppunt poort] is 50070 en standaard [knooppunt gegevenspoort] 50075 is.

Terwijl u kunt de gateway installeren op Hallo dezelfde lokale machine of hello Azure VM als HDFS hello, is het raadzaam dat u Hallo-gateway installeert op een afzonderlijke computer/Azure IaaS VM. Met gateway op een afzonderlijke computer bronconflicten vermindert en verbetert de prestaties. Wanneer u Hallo-gateway op een afzonderlijke computer installeert, is het Hallo-machine moeten kunnen tooaccess Hallo machine Hello HDFS.

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens van een HDFS-bron verplaatst met behulp van verschillende hulpprogramma's voor API's.

Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.

U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:

1. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.
2. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.
3. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.  Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van een gegevensarchief HDFS zijn [JSON-voorbeeld: gegevens kopiëren van lokale HDFS tooAzure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) sectie van dit artikel.

Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooHDFS zijn:

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Een gekoppelde service een gegevensfactory store tooa gegevens gekoppeld. Maken van een gekoppelde service van het type **Hdfs** toolink een lokale HDFS tooyour data factory. Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooHDFS gekoppelde service.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |Hallo type eigenschap moet worden ingesteld op: **Hdfs** |Ja |
| URL |URL toohello HDFS |Ja |
| authenticationType |Anoniem, of Windows. <br><br> toouse **Kerberos-verificatie** voor HDFS-connector te verwijzen[in deze sectie](#use-kerberos-authentication-for-hdfs-connector) tooset van uw on-premises omgeving dienovereenkomstig. |Ja |
| Gebruikersnaam |Gebruikersnaam voor Windows-verificatie. |Ja (voor Windows-verificatie) |
| wachtwoord |Wachtwoord voor Windows-verificatie. |Ja (voor Windows-verificatie) |
| gatewayName |Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello HDFS gebruiken. |Ja |
| encryptedCredential |[Nieuwe AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) uitvoer van de referentie voor Hallo-toegang. |Nee |

### <a name="using-anonymous-authentication"></a>Anonieme verificatie

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a>Met behulp van Windows-verificatie

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a>Eigenschappen van gegevensset
Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).

Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo. Hallo typeProperties sectie voor de gegevensset van het type **FileShare** (inclusief HDFS gegevensset) heeft Hallo volgende eigenschappen

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| folderPath |Pad toohello map. Voorbeeld:`myfolder`<br/><br/>Gebruik van escape-teken ' \ ' voor speciale tekens in Hallo-tekenreeks. Bijvoorbeeld: map opgeven voor folder\subfolder,\\\\submap en geef voor d:\samplefolder, d:\\\\Voorbeeldmap.<br/><br/>U kunt deze eigenschap combineren met **partitionBy** toohave mappaden op basis van het segment beginnen of eindigen-datums en tijden. |Ja |
| fileName |Hallo-naam van Hallo-bestand opgeven in Hallo **folderPath** als u wilt dat Hallo tabel toorefer tooa specifiek bestand in map Hallo. Als u geen waarde voor deze eigenschap niet opgeeft, wijst Hallo tabel tooall bestanden in de map Hallo.<br/><br/>Wanneer fileName niet voor een uitvoergegevensset opgegeven is, zou Hallo van Hallo gegenereerd bestand in worden Hallo volgt deze indeling: <br/><br/>Gegevens. <Guid>.txt (voorbeeld:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Nee |
| partitionedBy |partitionedBy mag gebruikte toospecify een dynamische folderPath bestandsnaam op van de reeksgegevens. Voorbeeld: folderPath geparametriseerde voor elk uur van gegevens. |Nee |
| Indeling | Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set Hallo **type** eigenschap onder indeling tooone van deze waarden. Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties. <br><br> Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan. |Nee |
| Compressie | Hallo-type en compressieniveau voor Hallo gegevens opgeven. Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**. Ondersteunde niveaus: **optimale** en **snelst**. Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Nee |

> [!NOTE]
> bestandsnaam en fileFilter worden niet gelijktijdig gebruikt.

### <a name="using-partionedby-property"></a>Gebruik de eigenschap partionedBy
Zoals vermeld in de vorige sectie hello, kunt u een dynamische folderPath en de bestandsnaam voor de reeks tijdgegevens Hello **partitionedBy** -eigenschap [Data Factory-functies en Hallo systeemvariabelen](data-factory-functions-variables.md).

toolearn meer informatie over het time series gegevenssets, planning en segmenten, Zie [gegevenssets maken](data-factory-create-datasets.md), [planning en uitvoering](data-factory-scheduling-and-execution.md), en [pijplijnen maken](data-factory-create-pipelines.md) artikelen.

#### <a name="sample-1"></a>Voorbeeld 1:

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
In dit voorbeeld {segment} is vervangen door de waarde van de Hallo van Data Factory systeemvariabele SliceStart Hallo-indeling (YYYYMMDDHH) opgegeven. Hallo SliceStart verwijst toostart tijd van Hallo segment. Hallo folderPath verschilt voor elk segment. Bijvoorbeeld: wikidatagateway/wikisampledataout/2014100103 of wikidatagateway/wikisampledataout/2014100104.

#### <a name="sample-2"></a>Voorbeeld 2:

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
In dit voorbeeld worden jaar, maand, dag en tijd van de SliceStart uitgepakt in verschillende variabelen die worden gebruikt door de eigenschappen voor folderPath en de bestandsnaam.

## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en beleidsregels zijn beschikbaar voor alle typen activiteiten.

Terwijl de eigenschappen die beschikbaar zijn in Hallo typeProperties gedeelte van de activiteit Hallo variëren met elk activiteitstype. Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.

Voor de Kopieeractiviteit, wanneer de bron van het type **FileSystemSource** Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:

**FileSystemSource** ondersteunt Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| Recursieve |Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo. |True, False (standaard) |Nee |

## <a name="supported-file-and-compression-formats"></a>Ondersteunde indelingen voor bestands- en compressie
Zie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artikel voor meer informatie.

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a>JSON-voorbeeld: gegevens kopiëren van lokale HDFS tooAzure Blob
In dit voorbeeld laat zien hoe toocopy gegevens uit een lokale HDFS tooAzure Blob Storage. Echter, de gegevens kunnen worden gekopieerd **rechtstreeks** tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.  

Hallo-voorbeeld bevat JSON-definities voor Hallo Data Factory-entiteiten te volgen. U kunt deze definities toocreate een pijplijn toocopy gegevens uit HDFS tooAzure Blob Storage gebruiken met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).

1. Een gekoppelde service van het type [OnPremisesHdfs](#linked-service-properties).
2. Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [FileShare](#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [FileSystemSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Hallo-voorbeeld worden gegevens gekopieerd van een lokale HDFS tooan Azure blob elk uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

Instellen als eerste stap Hallo data management gateway. instructies in Hallo Hallo [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.

**HDFS gekoppelde service:** in dit voorbeeld gebruikt Hallo Windows-verificatie. Zie [HDFS gekoppelde service](#linked-service-properties) sectie voor verschillende soorten verificatie die u kunt gebruiken.

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

**Gekoppelde Azure Storage-service:**

```JSON
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

**HDFS invoergegevensset:** deze gegevensset verwijst toohello HDFS map DataTransfer/UnitTest /. Hallo pijplijn kopieert alle Hallo-bestanden in deze map toohello bestemming.

Instelling 'extern': 'true' informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

**Azure Blob-uitvoergegevensset:**

Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1). pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Een kopieeractiviteit in een pijplijn met File System-bron en sink van Blob:**

Hallo pijplijn bevat een Kopieeractiviteit die is geconfigureerd toouse deze invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**FileSystemSource** en **sink** type is ingesteld, te**BlobSink**. Hallo SQL-query is opgegeven voor Hallo **query** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a>Kerberos-verificatie gebruiken voor HDFS-connector
Er zijn twee opties tooset up Hallo on-premises omgeving dus als toouse Kerberos-verificatie in HDFS-connector. U kunt kiezen Hallo een beter past bij uw aanvraag.
* Optie 1: [Join gatewaycomputer in Kerberos-realm](#kerberos-join-realm)
* Optie 2: [wederzijdse vertrouwensrelatie tussen Windows-domein en Kerberos-realm inschakelen](#kerberos-mutual-trust)

### <a name="kerberos-join-realm"></a>Optie 1: Join gatewaycomputer in Kerberos-realm

#### <a name="requirement"></a>Vereiste:

* Hallo gatewaycomputer moet toojoin Hallo Kerberos-realm en kan niet deelnemen aan een Windows-domein.

#### <a name="how-tooconfigure"></a>Hoe tooconfigure:

**Op de gatewaycomputer:**

1.  Voer Hallo **Ksetup** hulpprogramma tooconfigure Hallo Kerberos KDC-server en de standaardrealm.

    Hallo-machine moet worden geconfigureerd als lid van een werkgroep, omdat een Kerberos-realm af van een Windows-domein wijkt. Dit kan worden bereikt door Kerberos-realm Hallo instellen en als volgt een KDC-server toe te voegen. Vervang *REALM.COM* met uw eigen respectieve realm indien nodig.

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    **Opnieuw opstarten** Hallo machine na het uitvoeren van deze opdrachten 2.

2.  Controleer de configuratie Hallo met **Ksetup** opdracht. Hallo-uitvoer moet als volgt:

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

**In Azure Data Factory:**

* Configureren met behulp Hallo HDFS connector **Windows-verificatie** samen met de Kerberos-principal name en wachtwoord tooconnect toohello HDFS gegevensbron. Controleer [eigenschappen van de gekoppelde Service HDFS](#linked-service-properties) sectie over configuratie-informatie.

### <a name="kerberos-mutual-trust"></a>Optie 2: Wederzijdse vertrouwensrelatie tussen Windows-domein en Kerberos-realm inschakelen

#### <a name="requirement"></a>Vereiste:
*   Hallo gatewaycomputer moet lid worden van een Windows-domein.
*   U moet de machtiging tooupdate Hallo van de domeincontroller-instellingen.

#### <a name="how-tooconfigure"></a>Hoe tooconfigure:

> [!NOTE]
> Vervang REALM.COM en AD.COM in Hallo zelfstudie met uw eigen respectieve realm en de domeincontroller na indien nodig.

**Op de KDC-server:**

1.  Hallo KDC configuratie in bewerken **krb5.conf** bestand toolet KDC vertrouwt Windows-domein toohello na configuratiesjabloon verwijst. Standaard Hallo configuratie bevindt zich op **/etc/krb5.conf**.

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  **Opnieuw opstarten** Hallo KDC-service na de configuratie.

2.  Voorbereiden van een principal met de naam  **krbtgt/REALM.COM@AD.COM**  in de KDC-server met volgende opdracht Hallo:

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  In **hadoop.security.auth_to_local** HDFS-serviceconfiguratie bestand, het toevoegen van `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.

**Op de domeincontroller:**

1.  Voer de volgende Hallo **Ksetup** tooadd een vermelding realm-opdrachten:

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  Een vertrouwensrelatie van Windows-domein tooKerberos Realm. [wachtwoord] is Hallo wachtwoord voor Hallo principal  **krbtgt/REALM.COM@AD.COM** .

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  Selecteer de versleutelingsalgoritme die worden gebruikt in Kerberos.

    1. Ga tooServer Manager > Group Policy Management > Domain > groepsbeleidsobjecten > standaard of actieve domeinbeleid en bewerken.

    2. In Hallo **Editor voor Groepsbeleidsbeheer** pop-upvenster, Ga tooComputer Configuration > beleidsregels > Windows-instellingen > Beveiligingsinstellingen > lokaal beleid > beveiligingsopties, en configureer **netwerk beveiliging: Configureer versleutelingstypen voor Kerberos toegestaan**.

    3. Selecteer Hallo versleutelingsalgoritme gewenste toouse wanneer een verbinding tussen tooKDC. Doorgaans kunt u gewoon alle Hallo opties selecteren.

        ![Configuratie-versleutelingstypen voor Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. Gebruik **Ksetup** opdracht toospecify Hallo versleuteling algoritme toobe gebruikt op Hallo specifieke REALM.

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  Hallo-toewijzing tussen Hallo domeinaccount en Kerberos-principal in volgorde toouse Kerberos-principal in Windows-domein te maken.

    1. Hallo Systeembeheer Start > **Active Directory: gebruikers en Computers**.

    2. Geavanceerde functies configureren door te klikken op **weergave** > **geavanceerde functies**.

    3. Zoek Hallo account toowhich gewenste toocreate toewijzingen, en met de rechtermuisknop op tooview **naamstoewijzingen** > klikt u op **Kerberos-namen** tabblad.

    4. Een principal van Hallo realm toevoegen.

        ![Beveiligings-id toewijzen](media/data-factory-hdfs-connector/map-security-identity.png)

**Op de gatewaycomputer:**

* Voer de volgende Hallo **Ksetup** tooadd een vermelding realm-opdrachten.

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

**In Azure Data Factory:**

* Configureren met behulp Hallo HDFS connector **Windows-verificatie** samen met uw domeinaccount of een Kerberos-Principal tooconnect toohello HDFS-gegevensbron. Controleer [eigenschappen van de gekoppelde Service HDFS](#linked-service-properties) sectie over configuratie-informatie.

> [!NOTE]
> toomap kolommen uit de bron gegevensset toocolumns uit sink gegevensset, Zie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).


## <a name="performance-and-tuning"></a>Prestaties en het afstemmen
Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.
