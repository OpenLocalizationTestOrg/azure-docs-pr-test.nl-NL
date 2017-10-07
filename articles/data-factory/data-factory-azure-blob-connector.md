---
title: aaaCopy gegevens van/naar Azure Blob Storage | Microsoft Docs
description: 'Meer informatie over hoe toocopy blob-gegevens in Azure Data Factory. Gebruik onze voorbeeld: hoe toocopy gegevens tooand uit Azure Blob Storage en Azure SQL Database.'
keywords: "BLOB-gegevens, azure-blob kopiëren"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a>Kopiëren van gegevens tooor uit Azure Blob Storage met Azure Data Factory
Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toocopy gegevens tooand uit Azure Blob Storage. Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.

## <a name="overview"></a>Overzicht
U kunt gegevens kopiëren van een ondersteunde bron gegevens opslaan tooAzure Blob Storage of Azure Blob-opslag ondersteund tooany sink gegevens opslaan. Hello volgende tabel geeft een lijst van gegevensarchieven ondersteund als bronnen of sinks door Hallo kopieeractiviteit. U kunt bijvoorbeeld gegevens verplaatsen **van** een SQL Server-database of een Azure SQL database **naar** Azure blob storage. En u kunt gegevens kopiëren **van** Azure blob-opslag **naar** een Azure SQL Data Warehouse of een verzameling Azure Cosmos DB. 

## <a name="supported-scenarios"></a>Ondersteunde scenario 's
U kunt gegevens kopiëren **uit Azure Blob Storage** toohello gegevensarchieven te volgen:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Gegevens kunnen worden gekopieerd van de volgende gegevensarchieven Hallo **tooAzure Blob Storage**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> Kopieeractiviteit ondersteunt kopiëren van gegevens van / tooboth voor algemene doeleinden Azure Storage-accounts en Hot/Cool storage-Blob. Hallo-activiteit ondersteunt **lezen van het blok, toevoegen of pagina-blobs**, maar ondersteunt **tooonly blok-blobs schrijven**. Azure Premium-opslag wordt niet ondersteund als een sink omdat het wordt ondersteund door de pagina-blobs.
> 
> Kopieeractiviteit verwijdert geen gegevens van de bron Hallo nadat Hallo gegevens correct zijn gekopieerd toohello bestemming. Als u brongegevens toodelete na een geslaagde kopie moet, maakt u een [aangepaste activiteit](data-factory-use-custom-activities.md) toodelete Hallo van gegevens en Hallo activiteit in de pijplijn hello gebruiken. Zie voor een voorbeeld Hallo [verwijderen blob of de map voorbeeld op GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity). 

## <a name="get-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een Azure Blob-opslag verplaatst met behulp van verschillende hulpprogramma's voor API's.

Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Dit artikel bevat een [scenario](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) voor het maken van een pijplijn toocopy gegevens van een Azure Blob Storage locatie tooanother Azure Blob Storage-locatie. Zie voor een zelfstudie over het maken van een pijplijn toocopy gegevens van een Azure Blob Storage tooAzure SQL-Database, [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md).

U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:

1. Maak een **gegevensfactory**. Een gegevensfactory kan één of meer pijplijnen bevatten. 
2. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory. Bijvoorbeeld, als u gegevens uit een Azure blob storage tooan Azure SQL database kopiëren wilt, u twee gekoppelde services toolink uw Azure storage-account en de Azure SQL database tooyour data factory. Zie voor de gekoppelde service-eigenschappen die specifiek tooAzure Blob Storage, [gekoppelde service-eigenschappen](#linked-service-properties) sectie. 
2. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking. In vermeld in de laatste stap Hallo Hallo voorbeeld maakt u een gegevensset toospecify Hallo blob-container en map met invoergegevens Hallo. En u een andere dataset toospecify Hallo SQL-tabel maken in hello Azure SQL-database waarin Hallo-gegevens die zijn gekopieerd uit Hallo blob-opslag. Zie voor eigenschappen van gegevensset die specifieke tooAzure Blob Storage, [eigenschappen van gegevensset](#dataset-properties) sectie.
3. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer. In Hallo voorbeeld eerder vermeld, gebruikt u BlobSource als een bron- en SqlSink als een sink voor de kopieeractiviteit Hallo. Op dezelfde manier als u van Azure SQL Database tooAzure Blob Storage kopiëren wilt, gebruikt u SqlSource en BlobSink in Hallo kopieeractiviteit. Zie voor activiteitseigenschappen kopiëren die specifieke tooAzure Blob Storage, [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie. Voor informatie over hoe toouse een gegevensarchief als een bron of een sink, klikt u op Hallo-koppeling in de vorige sectie Hallo voor de gegevensopslag.  

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.  Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van/naar een Azure Blob Storage zijn, [JSON voorbeelden](#json-examples-for-copying-data-to-and-from-blob-storage  ) sectie van dit artikel.

Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooAzure Blob Storage zijn.

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
Er zijn twee typen van de gekoppelde services kunt u een Azure Storage tooan Azure data factory toolink. Ze zijn: **AzureStorage** gekoppelde service en **AzureStorageSas** gekoppelde service. Hallo gekoppelde Azure Storage-service biedt Hallo data factory met globale toegang toohello Azure Storage. Terwijl hello Azure Storage SAS (Shared Access Signature) gekoppelde biedt service Hallo gegevensfactory met de toegang beperkt/tijdsgebonden toohello Azure Storage. Er zijn geen andere verschillen tussen deze twee gekoppelde services. Kies Hallo gekoppelde service die bij uw behoeften past. Hallo vindt volgende secties u meer informatie over deze twee gekoppelde services.

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
een gegevensset toorepresent toospecify invoer- of -gegevens in een Azure Blob Storage, stelt u Hallo type-eigenschap van Hallo gegevensset: **AzureBlob**. Set Hallo **linkedServiceName** eigenschap Hallo gegevensset toohello naam van hello Azure Storage of Azure Storage SAS gekoppelde service.  Hallo-eigenschappen van gegevensset Hallo Hallo opgeven **blob-container** en Hallo **map** in Hallo blob-opslag.

Zie voor een volledige lijst van JSON-secties & eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel. Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).

Data factory ondersteunt Hallo compatibel met CLS .NET op basis van waarden voor het ontwikkelen van type-informatie in 'structuur' voor het schema op lezen gegevensbronnen zoals Azure blob te volgen: Int16, Int32, Int64, één, Double, Decimal, Byte [], Bool, String, Guid, Datetime, DateTimeOffset, Timespan. Data Factory voert automatisch typeconversies bij het verplaatsen van gegevens uit een brongegevens tooa sink data store opslaan.

Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo locatie, opmaken enz., van gegevens in het gegevensarchief Hallo Hallo. Hallo typeProperties sectie voor de gegevensset van het type **AzureBlob** dataset bevat Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| folderPath |Pad toohello container en map in Hallo blob-opslag. Voorbeeld: myblobcontainer\myblobfolder\ |Ja |
| fileName |De naam van Hallo blob. Bestandsnaam is optioneel en is hoofdlettergevoelig.<br/><br/>Als u een bestandsnaam, Hallo activiteit (inclusief kopiëren) werkt opgeeft op Hallo specifieke Blob.<br/><br/>Bestandsnaam is opgegeven, bevat kopiëren alle Blobs Hallo folderPath voor invoergegevensset.<br/><br/>Wanneer **fileName** is niet opgegeven voor een uitvoergegevensset en **preserveHierarchy** niet is opgegeven in activiteit sink Hallo-naam van Hallo gegenereerd bestand zou zijn in Hallo volgt deze indeling: Data.<Guid>. txt (bijvoorbeeld:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Nee |
| partitionedBy |partitionedBy is een optionele eigenschap. Kunt u deze toospecify een dynamische folderPath en de bestandsnaam voor de reeksgegevens. FolderPath kan bijvoorbeeld parameters worden gebruikt voor elk uur van gegevens. Zie Hallo [partitionedBy eigenschap sectie](#using-partitionedBy-property) voor meer informatie en voorbeelden. |Nee |
| Indeling | Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set Hallo **type** eigenschap onder indeling tooone van deze waarden. Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties. <br><br> Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan. |Nee |
| Compressie | Hallo-type en compressieniveau voor Hallo gegevens opgeven. Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**. Ondersteunde niveaus: **optimale** en **snelst**. Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Nee |

### <a name="using-partitionedby-property"></a>Gebruik de eigenschap partitionedBy
Zoals vermeld in de vorige sectie hello, kunt u een dynamische folderPath en de bestandsnaam voor de reeks tijdgegevens Hello **partitionedBy** -eigenschap [Data Factory-functies en Hallo systeemvariabelen](data-factory-functions-variables.md).

Zie voor meer informatie over tijd reeks gegevenssets, planning en segmenten [gegevenssets maken](data-factory-create-datasets.md) en [planning en uitvoering](data-factory-scheduling-and-execution.md) artikelen.

#### <a name="sample-1"></a>Voorbeeld 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

In dit voorbeeld {segment} is vervangen door de waarde van de Hallo van Data Factory systeemvariabele SliceStart Hallo-indeling (YYYYMMDDHH) opgegeven. Hallo SliceStart verwijst toostart tijd van Hallo segment. Hallo folderPath verschilt voor elk segment. Bijvoorbeeld: wikidatagateway/wikisampledataout/2014100103 of wikidatagateway/wikisampledataout/2014100104

#### <a name="sample-2"></a>Voorbeeld 2

```json
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
Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer gegevenssets en beleidsregels zijn beschikbaar voor alle typen activiteiten. Dat eigenschappen beschikbaar zijn in Hallo **typeProperties** sectie van de activiteit Hallo variëren met elk activiteitstype. Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put. Als u gegevens uit een Azure Blob-opslag verplaatst, u Hallo brontype instellen in de kopieeractiviteit hello te**BlobSource**. Als u gegevens tooan Azure Blob-opslag verplaatst, u stelt Hallo sink-type in de kopieerbewerking Hallo te**BlobSink**. Deze sectie bevat een lijst met eigenschappen die worden ondersteund door BlobSource en BlobSink.

**BlobSource** ondersteunt de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| Recursieve |Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo. |True (standaardwaarde), False |Nee |

**BlobSink** ondersteunt de volgende eigenschappen Hallo **typeProperties** sectie:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| copyBehavior |Hallo kopie gedrag definieert wanneer Hallo bron BlobSource of bestandssysteem. |<b>PreserveHierarchy</b>: gehandhaafd Hallo bestandshiërarchie in de doelmap Hallo. Hallo relatieve pad van de bestandsmap toosource bron is identiek toohello relatieve pad van de bestandsmap tootarget doel.<br/><br/><b>FlattenHierarchy</b>: alle bestanden uit de bronmap Hallo zijn in Hallo eerst niveau van de doelmap. Hallo doelbestanden hebben automatisch gegenereerde naam. <br/><br/><b>MergeFiles</b>: alle bestanden uit map Hallo-tooone bronbestand worden samengevoegd. Als Hallo bestand/Blob-naam wordt opgegeven, zou Hallo Samengevoegde bestandsnaam Hallo opgegeven name; zijn anders zou worden automatisch gegenereerde naam. |Nee |

**BlobSource** biedt ook ondersteuning voor deze twee eigenschappen voor achterwaartse compatibiliteit.

* **treatEmptyAsNull**: Hiermee geeft u op of tootreat null of lege tekenreeks als null-waarde.
* **skipHeaderLineCount** -geeft aan hoeveel lijnen moeten worden overgeslagen. Dit geldt alleen wanneer invoergegevensset gebruikmaakt TextFormat.

Op deze manier **BlobSink** ondersteunt Hallo na eigenschap voor achterwaartse compatibiliteit.

* **blobWriterAddHeader**: Hiermee geeft u op of een koptekst van de kolomdefinities tijdens het schrijven van tooan tooadd uitvoergegevensset.

Gegevenssets nu ondersteuning Hallo volgende eigenschappen met dezelfde functionaliteit Hallo: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.

Hallo volgende tabel bevat richtlijnen over het gebruik van Hallo nieuwe eigenschappen van gegevensset in plaats van deze eigenschappen van de bron/sink blob.

| Activiteitseigenschap kopiëren | Eigenschap DataSet |
|:--- |:--- |
| skipHeaderLineCount op BlobSource |skipLineCount en firstRowAsHeader. Regels eerst worden overgeslagen en wordt de eerste rij Hallo gelezen als een koptekst. |
| treatEmptyAsNull op BlobSource |treatEmptyAsNull op invoergegevensset |
| blobWriterAddHeader op BlobSink |firstRowAsHeader op uitvoergegevensset |

Zie [geven TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) sectie voor meer informatie over deze eigenschappen.    

### <a name="recursive-and-copybehavior-examples"></a>Voorbeelden van recursieve en copyBehavior
Deze sectie beschrijft Hallo resulterende gedrag van de kopieerbewerking Hallo voor verschillende combinaties van recursieve en copyBehavior waarden.

| Recursieve | copyBehavior | Resulterende gedrag |
| --- | --- | --- |
| De waarde True |preserveHierarchy |Voor een bronmap Map1 Hello structuur te volgen: <br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Hallo doelmap Map1 wordt gemaakt met dezelfde structuur, als de bron Hallo Hallo<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5. |
| De waarde True |flattenHierarchy |Voor een bronmap Map1 Hello structuur te volgen: <br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Hallo doel Map1 is gemaakt met de Hallo structuur te volgen: <br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File5 |
| De waarde True |mergeFiles |Voor een bronmap Map1 Hello structuur te volgen: <br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Hallo doel Map1 is gemaakt met de Hallo structuur te volgen: <br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 bestand2 + bestand3 + File4 + bestand 5 inhoud worden samengevoegd in één bestand met automatisch gegenereerde naam |
| ONWAAR |preserveHierarchy |Voor een bronmap Map1 Hello structuur te volgen: <br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Hallo doelmap Map1 wordt gemaakt met de Hallo structuur te volgen<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/><br/><br/>Subfolder1 bestand3 File4 en File5 zijn niet opgenomen. |
| ONWAAR |flattenHierarchy |Voor een bronmap Map1 Hello structuur te volgen:<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Hallo doelmap Map1 wordt gemaakt met de Hallo structuur te volgen<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand2<br/><br/><br/>Subfolder1 bestand3 File4 en File5 zijn niet opgenomen. |
| ONWAAR |mergeFiles |Voor een bronmap Map1 Hello structuur te volgen:<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Hallo doelmap Map1 wordt gemaakt met de Hallo structuur te volgen<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 + bestand2 inhoud worden samengevoegd in één bestand met automatisch gegenereerde naam. automatisch gegenereerde naam voor File1<br/><br/>Subfolder1 bestand3 File4 en File5 zijn niet opgenomen. |

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a>Overzicht: De Wizard kopiëren gebruiken toocopy gegevens van/naar Blob Storage
Bekijk hoe gegevens voor het kopiëren van tooquickly van een Azure-blobopslag. In dit overzicht bron- en doelserver gegevensopslag van het type: Azure Blob Storage. Hallo pijplijn in dit scenario kopieert gegevens van een map tooanother in Hallo dezelfde blob-container. In dit scenario is opzettelijk eenvoudige tooshow u instellingen of eigenschappen bij gebruik van Blob Storage als een bron- of sink. 

### <a name="prerequisites"></a>Vereisten
1. Maak een algemeen **Azure Storage-Account** als u nog niet hebt. U Hallo blob storage gebruiken als beide **bron** en **bestemming** gegevens opslaan in dit scenario. Als u geen Azure storage-account hebt, raadpleegt u Hallo [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) artikel voor stappen toocreate een.
2. Maak een blobcontainer met de naam **adfblobconnector** in Hallo storage-account. 
4. Maak een map met de naam **invoer** in Hallo **adfblobconnector** container.
5. Maak een bestand met de naam **emp.txt** Hello na inhoud en upload het toohello **invoer** map met hulpprogramma's zoals [Azure Opslagverkenner](https://azurestorageexplorer.codeplex.com/)
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a>Hallo een gegevensfactory maken
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op **+ nieuw** van de linkerbovenhoek hello, klikt u op **Intelligence en analyse**, en klik op **Data Factory**.
3. In Hallo **nieuwe gegevensfactory** blade:   
    1. Voer **ADFBlobConnectorDF** voor Hallo **naam**. Hallo-naam van hello Azure-gegevensfactory moet wereldwijd uniek zijn. Als u de foutmelding Hallo: `*Data factory name “ADFBlobConnectorDF” is not available`, wijzigt Hallo-naam van gegevensfactory hello (bijvoorbeeld yournameADFBlobConnectorDF) en probeert u het opnieuw. Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.
    2. Selecteer uw Azure-**abonnement**.
    3. Selecteer voor de resourcegroep **gebruik bestaande** tooselect een bestaande resource group (of) Selecteer **nieuw** tooenter een naam voor een resourcegroep.
    4. Selecteer een **locatie** voor Hallo data factory.
    5. Selecteer **pincode toodashboard** selectievakje onderaan Hallo Hallo-blade.
    6. Klik op **Create**.
3. Nadat het maken van Hallo voltooid is, ziet u Hallo **Data Factory** blade zoals weergegeven in Hallo volgende afbeelding: ![Data factory-startpagina](./media/data-factory-azure-blob-connector/data-factory-home-page.png)

### <a name="copy-wizard"></a>De wizard Kopiëren
1. Op Hallo Data Factory-startpagina, klikt u op Hallo **kopiëren van gegevens [PREVIEW]** tegel toolaunch **Data-Wizard kopiëren** op een afzonderlijke tabblad.    
    
    > [!NOTE]
    >    Als u ziet dat Hallo webbrowser is vastgelopen bij 'Autoriseren...', schakelt **blokkeren van cookies van derden en sitegegevens** instellen (of) laat dit ingeschakeld en maakt een uitzondering voor **login.microsoftonline.com**en probeer het opnieuw starten van Hallo-wizard.
2. In Hallo **eigenschappen** pagina:
    1. Voer **CopyPipeline** voor **taaknaam**. Hallo-taaknaam is Hallo-naam van Hallo pijplijn in uw gegevensfactory.
    2. Voer een **beschrijving** voor Hallo taak (optioneel).
    3. Voor **taak uitgebracht of taakschema**, Hallo houden **regelmatig wordt uitgevoerd volgens schema** optie. Als u wilt dat deze taak slechts eenmaal in plaats van meerdere keren uitgevoerd volgens een schema toorun, selecteert u **eenmaal nu uitvoeren**. Als u selecteert, **eenmaal nu uitvoeren** optie, een [eenmalige pijplijn](data-factory-create-pipelines.md#onetime-pipeline) wordt gemaakt. 
    4. Hallo-instellingen voor bewaren **terugkerend patroon**. Deze taak dagelijks wordt uitgevoerd tussen Hallo beginnen en eindigen tijd in die u in de volgende stap Hallo opgeven.
    5. Wijziging Hallo **begindatum tijd** te**21/04/2017**. 
    6. Wijziging Hallo **einddatum en-tijd** te**25/04/2017**. U kunt tootype Hallo datum in plaats van het bladeren door Hallo kalender.     
    8. Klik op **Volgende**.
      ![Hulpprogramma voor kopiëren - pagina eigenschappen](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png) 
3. Op Hallo **brongegevensarchief** pagina, klikt u op **Azure Blob Storage** tegel. U gebruikt deze pagina toospecify Hallo-brongegevensarchief voor Hallo kopieertaak. U kunt een bestaande gekoppelde service van een gegevensarchief gebruiken of een nieuw gegevensarchief opgeven. toouse een bestaande gekoppelde service, selecteert u **van bestaande gekoppelde SERVICES** en selecteer Hallo juiste gekoppelde service. 
    ![Hulpprogramma voor kopiëren - brongegevensarchief](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)
4. Op Hallo **hello Azure Blob storage-account opgeven** pagina:
   1. Hallo automatisch gegenereerde naam voor **verbindingsnaam**. Hallo verbindingsnaam heet Hallo Hallo gekoppelde service van het type: Azure Storage. 
   2. Controleer of de optie **Van Azure-abonnementen** is geselecteerd als **accountselectiemethode**.
   3. Selecteer uw Azure-abonnement of houden **Alles selecteren** voor **Azure-abonnement**.   
   4. Selecteer een **Azure storage-account** van Hallo lijst met Azure storage accounts beschikbaar in het abonnement Hallo geselecteerd. U kunt ook tooenter Opslaginstellingen account handmatig door het selecteren van **handmatig invoeren** optie voor Hallo **Accountselectiemethode**.
   5. Klik op **Volgende**. 
      ![Hulpprogramma voor kopiëren - hello Azure Blob storage-account opgeven](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)
5. Op **Kies Hallo invoerbestand of de map** pagina:
   1. Dubbelklik op **adfblobcontainer**.
   2. Selecteer **invoer**, en klik op **Kies**. In dit scenario maakt selecteren u de invoermap Hallo. U kunt ook selecteren Hallo emp.txt bestand in map Hallo in plaats daarvan. 
      ![Hulpprogramma voor kopiëren - Hallo invoerbestand of de invoermap kiezen](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)
6. Op Hallo **Kies Hallo invoerbestand of de map** pagina:
    1. Bevestig dat Hallo **bestand of map** te is ingesteld,**adfblobconnector/invoer**. Als Hallo-bestanden in submappen, bijvoorbeeld 04-01-2017, 2017/04/02 en enzovoort, en geef adfblobconnector/invoer / {year} / {month} / {day} voor bestand of map. Wanneer u op tabblad buiten het tekstvak hello, ziet u drie vervolgkeuzelijsten tooselect indelingen voor het jaar (jjjj), de maand (MM) en de dag (dd). 
    2. Stel geen **kopiëren van bestand recursief**. Selecteer deze optie toorecursively bladeren door mappen voor bestanden toobe gekopieerde toohello doel. 
    3. Niet Hallo **binaire kopiëren** optie. Selecteer deze optie tooperform een binaire kopie van de bron-bestand toohello doel. Selecteer niet voor dit scenario zodat u meer opties in de volgende pagina's Hallo kunt zien. 
    4. Bevestig dat Hallo **compressietype** te is ingesteld,**geen**. Selecteer een waarde voor deze optie als de bronbestanden in een van Hallo ondersteunde indelingen zijn gecomprimeerd. 
    5. Klik op **Volgende**.
    ![Hulpprogramma voor kopiëren - Hallo invoerbestand of de invoermap kiezen](./media/data-factory-azure-blob-connector/chose-input-file-folder.png) 
7. Op Hallo **bestandsindelingsinstellingen** pagina ziet u Hallo scheidingstekens en het Hallo-schema die automatisch worden gedetecteerd door de wizard Hallo door parseren Hallo-bestand. 
    1. Bevestig Hallo volgende opties: een. Hallo **bestandsindeling** te is ingesteld,**tekstindeling**. U kunt alle Hallo ondersteund notaties in de vervolgkeuzelijst Hallo zien. Bijvoorbeeld: JSON, Avro, ORC, parketvloeren.
        b. Hallo **kolomscheidingsteken** te is ingesteld`Comma (,)`. U kunt zien andere kolom scheidingstekens die door Data Factory worden ondersteund in de vervolgkeuzelijst Hallo Hallo. U kunt ook een aangepaste scheidingsteken opgeven.
        c. Hallo **rijscheidingsteken** te is ingesteld`Carriage Return + Line feed (\r\n)`. U kunt zien andere rij scheidingstekens die door Data Factory worden ondersteund in de vervolgkeuzelijst Hallo Hallo. U kunt ook een aangepaste scheidingsteken opgeven.
        d. Hallo **aantal regels overslaan** te is ingesteld,**0**. Als u een paar regels toobe overgeslagen Hallo boven aan het Hallo-bestand wilt, voert u hier Hallo-nummer.
        e.  Hallo **eerste gegevensrij kolomnamen bevat** is niet ingesteld. Selecteer deze optie als Hallo-bronbestanden kolomnamen in de eerste rij hello bevat.
        f. Hallo **leeg kolomwaarde behandelen als null** optie is ingesteld.
    2. Vouw **geavanceerde instellingen** toosee geavanceerde optie beschikbaar.
    3. Aan de onderkant van de Hallo van Hallo pagina, Zie Hallo **preview** van gegevens van Hallo emp.txt bestand.
    4. Klik op **SCHEMA** tabblad die wizard voor het kopiëren van Hallo afgeleid door te kijken Hallo-gegevens in het bronbestand Hallo Hallo onder toosee Hallo schema.
    5. Klik op **volgende** nadat u hello scheidingstekens bekijkt en een voorbeeld van gegevens.
    ![Hulpprogramma voor kopiëren - bestandsindelingsinstellingen](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)  
8. Op Hallo **bestemming gegevensarchief pagina**, selecteer **Azure Blob Storage**, en klik op **volgende**. Als beide Hallo bron- en doelserver gegevensarchieven in dit scenario gebruikt u hello Azure Blob Storage.    
    ![Hulpprogramma voor kopiëren - gegevensarchief van de doelserver selecteren](media/data-factory-azure-blob-connector/select-destination-data-store.png)
9. Op **hello Azure Blob storage-account opgeven** pagina:
   1. Voer **AzureStorageLinkedService** voor Hallo **verbindingsnaam** veld.
   2. Controleer of de optie **Van Azure-abonnementen** is geselecteerd als **accountselectiemethode**.
   3. Selecteer uw Azure-**abonnement**.  
   4. Selecteer uw Azure storage-account. 
   5. Klik op **Volgende**.     
10. Op Hallo **Kies Hallo bestand of map uitvoer** pagina: 
    6. Geef **mappad** als **adfblobconnector/uitvoer / {year} / {month} / {day}**. Voer **tabblad**.
    7. Voor Hallo **jaar**, selecteer **jjjj**.
    8. Voor Hallo **maand**, Controleer te ingesteld**MM**.
    9. Voor Hallo **dag**, Controleer te ingesteld**dd**.
    10. Bevestig dat Hallo **compressietype** te is ingesteld,**geen**.
    11. Bevestig dat Hallo **gedrag kopiëren** te is ingesteld,**bestanden samenvoegen**. Als Hallo uitvoerbestand met dezelfde naam al bestaat hello, is hello nieuwe inhoud toegevoegd toohello hetzelfde bestand aan Hallo einde.
    12. Klik op **Volgende**.
    ![Hulpprogramma voor kopiëren - bestand voor uitvoer of de invoermap kiezen](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)
11. Op Hallo **bestandsindelingsinstellingen** pagina, Hallo instellingen bekijken en klik op **volgende**. Een van de Hallo hier extra opties is tooadd een header toohello-uitvoerbestand. Als u deze optie selecteert, wordt een veldnamenrij toegevoegd met namen van kolommen Hallo van Hallo-schema van Hallo bron. Wanneer u bekijkt hello schema voor Hallo bron, kunt u Hallo standaardkolomnamen wijzigen. U kan bijvoorbeeld Hallo eerste kolom tooFirst naam en de tweede kolom tooLast naam wijzigen. Hallo-bestand voor uitvoer wordt vervolgens gegenereerd met een header met deze namen als kolomnamen. 
    ![Hulpprogramma voor kopiëren - bestandsindelingsinstellingen voor bestemming](media/data-factory-azure-blob-connector/file-format-destination.png)
12. Op Hallo **prestatie-instellingen** pagina, controleert u of **eenheden cloud** en **kopieën parallelle** te zijn ingesteld**automatisch**, en klik op volgende. Zie voor meer informatie over deze instellingen [activiteit prestaties en prestatieafstemming handleiding kopiëren](data-factory-copy-activity-performance.md#parallel-copy).
    ![Hulpprogramma voor kopiëren - prestatie-instellingen](media/data-factory-azure-blob-connector/copy-performance-settings.png) 
14. Op Hallo **samenvatting** pagina, controleert u alle instellingen (taakeigenschappen, instellingen voor de bron- en doelserver en instellingen) en klik op **volgende**.
    ![Hulpprogramma voor kopiëren - pagina overzicht](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)
15. Bekijk de informatie in Hallo **samenvatting** pagina en klik op **voltooien**. Hallo-wizard maakt twee gekoppelde services, twee gegevenssets (invoer en uitvoer) en één pijplijn in de gegevensfactory hello (van waaruit u Hallo Wizard kopiëren hebt gestart).
    ![Hulpprogramma voor kopiëren - pagina van de implementatie](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)

### <a name="monitor-hello-pipeline-copy-task"></a>De pijplijn bewaken hello (taak kopiëren)

1. Klik op de koppeling Hallo `Click here toomonitor copy pipeline` op Hallo **implementatie** pagina. 
2. U ziet Hallo **bewaken en beheren van de toepassing** op een afzonderlijke tabblad.  ![Bewaken en beheren van App](media/data-factory-azure-blob-connector/monitor-manage-app.png)
3. Wijziging Hallo **start** tijd Hallo boven te`04/19/2017` en **end** tijd te`04/27/2017`, en klik vervolgens op **toepassen**. 
4. Ziet u vijf activiteitsvensters in Hallo **ACTIVITEITSVENSTERS** lijst. Hallo **WindowStart** tijden moeten voldoende zijn voor alle dagen van de pijplijn start toopipeline eindtijden. 
5. Klik op **vernieuwen** knop voor Hallo **ACTIVITEITSVENSTERS** lijst een paar keer totdat er status van alle Hallo activiteit windows hello tooReady is ingesteld. 
6. Controleer nu of dat de uitvoerbestanden Hallo worden gegenereerd in de uitvoermap Hallo van adfblobconnector container. U ziet de volgende mapstructuur in de uitvoermap Hallo Hallo: 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
Zie voor gedetailleerde informatie over het controleren en beheren van gegevensfactory [bewaken en beheren van de Data Factory-pijplijn](data-factory-monitor-manage-app.md) artikel. 
 
### <a name="data-factory-entities"></a>Data Factory-entiteiten
Nu switch back toohello tabblad met Hallo Data Factory-startpagina. U ziet dat er twee gekoppelde services, twee gegevenssets en een pijplijn in uw data factory nu zijn. 

![Data Factory-startpagina met entiteiten](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

Klik op **auteur en implementeren van** toolaunch Data Factory-Editor. 

![Data Factory Editor](media/data-factory-azure-blob-connector/data-factory-editor.png)

U ziet Hallo Data Factory-entiteiten in uw data factory te volgen: 

 - Twee gekoppelde services. Een voor Hallo bron- en Hallo andere voor Hallo bestemming. Beide Hallo gekoppelde services verwijzen toohello dezelfde Azure-opslagaccount in dit scenario. 
 - Twee gegevenssets. Een invoergegevensset en een uitvoergegevensset. In dit scenario maken beide gebruik Hallo dezelfde blob-container, maar verwijzen toodifferent mappen (invoer en uitvoer).
 - Een pijplijn. Hallo pijplijn bevat een kopieeractiviteit die gebruikmaakt van een blob-bron- en een blob sink toocopy-gegevens van een Azure-blobopslag locatie tooanother Azure blob-locatie. 

Hallo bevatten volgende secties meer informatie over deze entiteiten. 

#### <a name="linked-services"></a>Gekoppelde services
Hier ziet u twee gekoppelde services. Een voor Hallo bron- en Hallo andere voor Hallo bestemming. In dit overzicht Hallo beide uiterlijk definities dezelfde behalve Hallo namen. Hallo **type** Hallo gekoppelde service te ingesteld**AzureStorage**. Belangrijkste eigenschap van de servicedefinitie Hallo gekoppeld is Hallo **connectionString**, die wordt gebruikt door de Data Factory tooconnect tooyour Azure Storage-account tijdens runtime. Hallo hubName eigenschap in de definitie van de Hallo negeren. 

##### <a name="source-blob-storage-linked-service"></a>Bron blob-opslag gekoppelde service
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a>Bestemming blob-opslag gekoppelde service

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

Zie voor meer informatie over Azure Storage gekoppelde service [gekoppelde service-eigenschappen](#linked-service-properties) sectie. 

#### <a name="datasets"></a>Gegevenssets
Er zijn twee gegevenssets: een invoergegevensset en een uitvoergegevensset. Hallo type Hallo gegevensset te is ingesteld**AzureBlob** voor beide. 

Hallo invoergegevensset verwijst toohello **invoer** map Hallo **adfblobconnector** blob-container. Hallo **externe** eigenschap is ingesteld, te**true** voor deze gegevensset als Hallo gegevens wordt niet gemaakt door Hallo pijplijn met de Hallo kopieeractiviteit waarmee deze dataset als invoer. 

Hallo output dataset punten toohello **uitvoer** map Hallo dezelfde blob-container. Hallo uitvoergegevensset gebruikt ook Hallo jaar, maand en dag Hallo **SliceStart** system variabele toodynamically Hallo pad voor het uitvoerbestand Hallo evalueren. Zie voor een lijst met functies en ondersteund door Data Factory systeemvariabelen [Data Factory-functies en systeemvariabelen](data-factory-functions-variables.md). Hallo **externe** eigenschap is ingesteld, te**false** (standaardwaarde) omdat deze gegevensset wordt geproduceerd door Hallo pijplijn. 

Zie voor meer informatie over de eigenschappen die worden ondersteund door Azure Blob-gegevensset [eigenschappen van gegevensset](#dataset-properties) sectie.

##### <a name="input-dataset"></a>Invoergegevensset

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a>Uitvoergegevensset

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a>Pijplijn
Hallo pipeline heeft slechts één activiteit. Hallo **type** Hallo activiteit te ingesteld**kopie**.  In Hallo type-eigenschappen voor Hallo activiteit zijn er twee secties, één voor de bron- en Hallo andere voor sink. type Hello te is ingesteld**BlobSource** zoals Hallo activiteit van gegevens van een blob-opslag kopiëren. Hallo sink-type is ingesteld te**BlobSink** als Hallo activiteit kopiëren van gegevens tooa blob-opslag. Hallo kopieeractiviteit Neem InputDataset z4y als Hallo invoer- en OutputDataset-z4y als Hallo uitvoer. 

Zie voor meer informatie over de eigenschappen die worden ondersteund door BlobSource en BlobSink [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie. 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a>JSON-voorbeelden voor het kopiëren van gegevens tooand van Blob-opslag  
Hallo volgende voorbeelden geven voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Ze geven weer hoe toocopy gegevens tooand uit Azure Blob Storage en Azure SQL Database. Echter gegevens kunnen worden gekopieerd **rechtstreeks** uit een van de bronnen tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a>JSON-voorbeeld: Gegevens kopiëren van Blob Storage tooSQL Database
Hallo volgende ziet:

1. Een gekoppelde service van het type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
2. Een gekoppelde service van het type [AzureStorage](#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
5. Een [pijplijn](data-factory-create-pipelines.md) met een kopieeractiviteit die gebruikmaakt van [BlobSource](#copy-activity-properties) en [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).

Hallo voorbeeld kopieert timeseries gegevens uit een Azure-blobopslag tooan Azure SQL-tabel per uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

**Azure SQL gekoppelde service:**

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Gekoppelde Azure Storage-service:**

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
Azure Data Factory ondersteunt twee soorten gekoppelde Azure Storage-services: **AzureStorage** en **AzureStorageSas**. Hallo voor eerste, u Hallo verbindingsreeks met Hallo accountsleutel opgeven en voor latere Hallo, u Hallo Shared Access Signature (SAS)-Uri opgeven. Zie [gekoppelde Services](#linked-service-properties) sectie voor meer informatie.  

**Azure Blob invoergegevensset:**

Gegevens wordt opgehaald uit een nieuwe blob elk uur (frequentie: uur, interval: 1). Hallo map pad en de naam voor de blob Hallo worden dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. Hallo mappad jaar, maand en dag deel uit van de begintijd Hallo en bestandsnaam gebruikt Hallo uur deel uit van de begintijd Hallo. "extern": "true" instelling informeert Data Factory die tabel Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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
**Azure SQL-uitvoergegevensset:**

Hallo voorbeeld kopieert gegevens tooa tabel "MijnTabel" in een Azure SQL database. Hallo-tabel maken in uw Azure SQL database met hetzelfde aantal kolommen Hallo zoals Hallo Blob CSV-bestand toocontain verwacht. Nieuwe rijen worden toohello tabel toegevoegd om het uur.

```json
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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
**Een kopieeractiviteit in een pijplijn met Blob-bron en sink SQL:**

Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**BlobSource** en **sink** type is ingesteld, te**SqlSink**.

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
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
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
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a>JSON-voorbeeld: Gegevens kopiëren van Azure SQL tooAzure Blob
Hallo volgende ziet:

1. Een gekoppelde service van het type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
2. Een gekoppelde service van het type [AzureStorage](#linked-service-properties).
3. Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
4. Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](#dataset-properties).
5. Een [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) en [BlobSink](#copy-activity-properties).

Hallo voorbeeld kopieert timeseries gegevens van een Azure SQL-tabel tooan Azure blob per uur. Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

**Azure SQL gekoppelde service:**

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Gekoppelde Azure Storage-service:**

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
Azure Data Factory ondersteunt twee soorten gekoppelde Azure Storage-services: **AzureStorage** en **AzureStorageSas**. Hallo voor eerste, u Hallo verbindingsreeks met Hallo accountsleutel opgeven en voor latere Hallo, u Hallo Shared Access Signature (SAS)-Uri opgeven. Zie [gekoppelde Services](#linked-service-properties) sectie voor meer informatie.  

**Azure SQL invoergegevensset:**

Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in Azure SQL en bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens.

Instelling 'extern': 'true' informeert Data Factory-service die tabel Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.

```json
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
      "partitionedBy": [
        {
          "name": "Year",
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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

**Een kopieeractiviteit in een pijplijn met de SQL-bron en sink van Blob:**

Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**SqlSource** en **sink** type is ingesteld, te**BlobSink**. Hallo SQL-query is opgegeven voor Hallo **SqlReaderQuery** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureSQLInput"
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

> [!NOTE]
> toomap kolommen uit de bron gegevensset toocolumns uit sink gegevensset, Zie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Prestaties en het afstemmen
Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.
