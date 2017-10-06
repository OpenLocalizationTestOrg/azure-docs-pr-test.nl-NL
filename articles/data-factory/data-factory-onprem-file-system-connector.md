---
title: aaaCopy gegevens van/naar een bestandssysteem met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over hoe toocopy gegevens tooand uit een on-premises bestandssysteem met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a>Tooand gegevens kopiëren van een on-premises bestandssysteem met behulp van Azure Data Factory
Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toocopy gegevens uit een on-premises bestandssysteem. Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.

## <a name="supported-scenarios"></a>Ondersteunde scenario 's
U kunt gegevens kopiëren **uit een on-premises bestandssysteem** toohello gegevensarchieven te volgen:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Gegevens kunnen worden gekopieerd van de volgende gegevensarchieven Hallo **tooan lokaal bestandssysteem**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Kopieeractiviteit worden Hallo-bronbestand niet verwijderd nadat het is gekopieerde toohello bestemming. Als u toodelete Hallo-bronbestand na een geslaagde kopie moet, maakt u een aangepaste activiteit toodelete Hallo-bestand en Hallo activiteit in de pijplijn hello gebruiken. 

## <a name="enabling-connectivity"></a>Connectiviteit inschakelen
Data Factory ondersteunt verbindende tooand uit een on-premises bestandssysteem via **Data Management Gateway**. U moet Hallo Data Management Gateway installeren in uw on-premises omgeving voor Hallo Data Factory-service tooconnect tooany ondersteunde on-premises gegevensopslag met inbegrip van bestandssysteem. toolearn over Data Management Gateway en voor stapsgewijze instructies over het instellen van Hallo-gateway, Zie [gegevens verplaatsen tussen lokale bronnen en Hallo cloud met Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md). Naast Data Management Gateway moeten geen binaire bestanden geïnstalleerd toobe toocommunicate tooand uit een on-premises bestandssysteem. U moet installeren en gebruiken van Hallo Data Management Gateway, zelfs als het bestandssysteem Hallo in Azure IaaS VM. Zie voor gedetailleerde informatie over gateway-Hallo [Data Management Gateway](data-factory-data-management-gateway.md).

installeren van een bestandsshare Linux toouse [Samba](https://www.samba.org/) op uw Linux-server en de Data Management Gateway installeren op een WindowsServer. Data Management Gateway installeren op een Linux-server wordt niet ondersteund.

## <a name="getting-started"></a>Aan de slag
U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens van een bestandssysteem wordt verplaatst met behulp van verschillende hulpprogramma's voor API's.

Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**. Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.

U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**. Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.

Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:

1. Maak een **gegevensfactory**. Een gegevensfactory kan één of meer pijplijnen bevatten. 
2. Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory. Bijvoorbeeld, als u gegevens uit een Azure blob storage tooan lokale bestandssysteem kopiëren wilt, u twee gekoppelde services toolink uw on-premises bestandssysteem en de Azure storage-account tooyour data factory. Zie voor de gekoppelde service-eigenschappen die specifiek tooan on-premises bestandssysteem, [gekoppelde service-eigenschappen](#linked-service-properties) sectie.
3. Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking. In vermeld in de laatste stap Hallo Hallo voorbeeld maakt u een gegevensset toospecify Hallo blob-container en map met invoergegevens Hallo. En u een andere dataset toospecify Hallo map- en -naam (optioneel) in het bestandssysteem maken. Zie voor de eigenschappen van de gegevensset die specifieke tooon lokaal bestandssysteem, [eigenschappen van gegevensset](#dataset-properties) sectie.
4. Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer. In Hallo voorbeeld eerder vermeld, gebruikt u BlobSource als een bron- en FileSystemSink als een sink voor de kopieeractiviteit Hallo. Op dezelfde manier als u uit het lokale bestand system tooAzure Blob Storage kopiëren wilt, gebruikt u FileSystemSource en BlobSink in Hallo kopieeractiviteit. Zie voor de activiteitseigenschappen kopiëren die specifieke tooon lokaal bestandssysteem, [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie. Voor informatie over hoe toouse een gegevensarchief als een bron of een sink, klikt u op Hallo-koppeling in de vorige sectie Hallo voor de gegevensopslag.

Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt. Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.  Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van/naar een bestandssysteem zijn, [JSON voorbeelden](#json-examples-for-copying-data-to-and-from-file-system) sectie van dit artikel.

Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke toofile system zijn:

## <a name="linked-service-properties"></a>Eigenschappen van de gekoppelde service
U kunt een lokaal bestand system tooan Azure data factory Hello koppelen **On-Premises bestandsserver** gekoppelde service. Hallo volgende tabel bevat beschrijvingen van JSON-elementen die specifiek toohello bestandsserver On-Premises gekoppelde service.

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| type |Zorg ervoor dat de eigenschap type hello te is ingesteld**OnPremisesFileServer**. |Ja |
| host |Hiermee geeft u het hoofdpad Hallo van Hallo map die u toocopy wilt. Gebruik Hallo escape-teken ' \ ' voor speciale tekens in Hallo-tekenreeks. Zie [voorbeeld gekoppelde service en gegevensset definities](#sample-linked-service-and-dataset-definitions) voor voorbeelden. |Ja |
| gebruikers-id |Hallo-ID van het Hallo-gebruiker met toegang toohello server opgeven. |Nee (als u ervoor encryptedCredential kiest) |
| wachtwoord |Hallo-wachtwoord voor gebruiker hello (gebruikersnaam) opgeven. |Nee (als u encryptedCredential kiezen |
| encryptedCredential |Geef referenties op Hallo versleuteld die u door de cmdlet New-AzureRmDataFactoryEncryptValue Hallo kunt ophalen. |Nee (als u toospecify gebruikersnaam en wachtwoord als tekst zonder opmaak kiezen) |
| gatewayName |Geeft de naam Hallo van Hallo gateway dat Data Factory tooconnect toohello lokale bestandsserver moeten gebruiken. |Ja |


### <a name="sample-linked-service-and-dataset-definitions"></a>Voorbeeld van de gekoppelde service en de definities van de gegevensset
| Scenario | In de definitie van de gekoppelde service host | folderPath in de definitie van gegevensset |
| --- | --- | --- |
| Lokale map op de Data Management Gateway-apparaat: <br/><br/>Voorbeelden: D:\\ \* of D:\folder\subfolder\\* |D:\\ \\ (voor Data Management Gateway 2.0 en hoger) <br/><br/> localhost (voor oudere versies dan Data Management Gateway 2.0) |. \\ \\ of de map\\\\submap (voor Data Management Gateway 2.0 en hoger) <br/><br/>D:\\ \\ of D:\\\\map\\\\submap (voor gatewayversie lager dan 2.0) |
| Externe gedeelde map: <br/><br/>Voorbeelden: \\ \\MijnServer\\delen\\ \* of \\ \\MijnServer\\delen\\map\\submap\\* |\\\\\\\\MijnServer\\\\delen |. \\ \\ of de map\\\\submap |


### <a name="example-using-username-and-password-in-plain-text"></a>Voorbeeld: Met behulp van gebruikersnaam en wachtwoord in tekst zonder opmaak

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a>Voorbeeld: Encryptedcredential gebruiken

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a>Eigenschappen van gegevensset
Zie voor een volledige lijst van de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets en secties [gegevenssets maken](data-factory-create-datasets.md). Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle typen van de gegevensset.

Hallo typeProperties sectie verschilt voor elk type dataset. Het levert informatie zoals Hallo locatie en indeling van gegevens in het gegevensarchief Hallo Hallo. Hallo typeProperties sectie voor de gegevensset Hallo van het type **FileShare** heeft Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| folderPath |Hiermee geeft u Hallo subpad toohello map. Gebruik Hallo escape-teken ' \' voor speciale tekens in Hallo-tekenreeks. Zie [voorbeeld gekoppelde service en gegevensset definities](#sample-linked-service-and-dataset-definitions) voor voorbeelden.<br/><br/>U kunt deze eigenschap combineren met **partitionBy** toohave mappaden op basis van het segment beginnen of eindigen-datums en tijden. |Ja |
| fileName |Hallo-naam van Hallo-bestand opgeven in Hallo **folderPath** als u wilt dat Hallo tabel toorefer tooa specifiek bestand in map Hallo. Als u geen waarde voor deze eigenschap niet opgeeft, wijst Hallo tabel tooall bestanden in de map Hallo.<br/><br/>Wanneer **fileName** is niet opgegeven voor een uitvoergegevensset en **preserveHierarchy** niet is opgegeven in activiteit sink Hallo-naam van Hallo gegenereerd bestand is in de volgende indeling Hallo: <br/><br/>`Data.<Guid>.txt`(Voorbeeld: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Nee |
| fileFilter |Geef dat een filter toobe tooselect gebruikt een subset van de bestanden in Hallo folderPath in plaats van alle bestanden. <br/><br/>Toegestane waarden zijn: `*` (meerdere tekens) en `?` (willekeurig teken).<br/><br/>Voorbeeld 1: 'fileFilter":" * .log '<br/>Voorbeeld 2: 'fileFilter': 2014 - 1-?. txt'<br/><br/>Houd er rekening mee dat fileFilter is van toepassing op een bestandsshare-invoergegevensset. |Nee |
| partitionedBy |U kunt partitionedBy toospecify een dynamische folderPath/bestandsnaam gebruiken voor timeseries gegevens. Een voorbeeld is folderPath geparametriseerde voor elk uur van gegevens. |Nee |
| Indeling | Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set Hallo **type** eigenschap onder indeling tooone van deze waarden. Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties. <br><br> Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan. |Nee |
| Compressie | Hallo-type en compressieniveau voor Hallo gegevens opgeven. Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**. Ondersteunde niveaus: **optimale** en **snelst**. Zie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Nee |

> [!NOTE]
> U kunt geen bestandsnaam en fileFilter gelijktijdig gebruiken.

### <a name="using-partitionedby-property"></a>Gebruik de eigenschap partitionedBy
Zoals vermeld in de vorige sectie hello, kunt u een dynamische folderPath en de bestandsnaam voor de reeks tijdgegevens Hello **partitionedBy** -eigenschap [Data Factory-functies en Hallo systeemvariabelen](data-factory-functions-variables.md).

toounderstand meer informatie over de tijdreeks gegevenssets, planning en segmenten, Zie [gegevenssets maken](data-factory-create-datasets.md), [planning en uitvoering](data-factory-scheduling-and-execution.md), en [pijplijnen maken](data-factory-create-pipelines.md).

#### <a name="sample-1"></a>Voorbeeld 1:

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

In dit voorbeeld {segment} is vervangen door Hallo-waarde van variabele system Data Factory Hallo SliceStart Hallo-indeling (YYYYMMDDHH). SliceStart verwijst toostart tijd van Hallo segment. Hallo folderPath verschilt voor elk segment. Bijvoorbeeld: wikidatagateway/wikisampledataout/2014100103 of wikidatagateway/wikisampledataout/2014100104.

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

In dit voorbeeld worden jaar, maand, dag en tijd van de SliceStart uitgepakt in verschillende variabelen die gebruikmaken van Hallo folderPath en de bestandsnaam eigenschappen.

## <a name="copy-activity-properties"></a>Eigenschappen van de activiteit kopiëren
Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel. Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer gegevenssets en beleidsregels zijn beschikbaar voor alle typen activiteiten. Dat eigenschappen beschikbaar zijn in Hallo **typeProperties** sectie van de activiteit Hallo variëren met elk activiteitstype.

Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put. Als u gegevens uit een on-premises bestandssysteem verplaatst, u Hallo brontype instellen in de kopieeractiviteit hello te**FileSystemSource**. Op dezelfde manier als u overstapt tooan gegevens op het lokale bestandssysteem, u Hallo sink-type instellen in Hallo kopieeractiviteit te**FileSystemSink**. Deze sectie bevat een lijst met eigenschappen die worden ondersteund door FileSystemSource en FileSystemSink.

**FileSystemSource** ondersteunt Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| Recursieve |Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo. |True, False (standaard) |Nee |

**FileSystemSink** ondersteunt Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| copyBehavior |Hallo kopie gedrag definieert wanneer Hallo bron BlobSource of bestandssysteem. |**PreserveHierarchy:** Hallo bestandshiërarchie in de doelmap Hallo behouden blijft. Dat wil zeggen, is relatief pad Hallo van Hallo bestand toohello bron bronmap hetzelfde als het relatieve pad van Hallo bestand toohello doel doelmap Hallo Hallo.<br/><br/>**FlattenHierarchy:** alle bestanden uit de bronmap Hallo worden gemaakt in Hallo eerste niveau van de doelmap. Hallo doelbestanden worden gemaakt met een automatisch gegenereerde naam.<br/><br/>**MergeFiles:** alle bestanden uit map Hallo-tooone bronbestand worden samengevoegd. Als Hallo bestand naam/blob-naam wordt opgegeven, is Hallo Samengevoegde bestandsnaam Hallo opgegeven naam. Anders is het een automatisch gegenereerde naam. |Nee |

### <a name="recursive-and-copybehavior-examples"></a>Voorbeelden van recursieve en copyBehavior
Deze sectie beschrijft Hallo resulterende gedrag van de kopieerbewerking Hallo voor verschillende combinaties van waarden voor Hallo recursieve en copyBehavior eigenschappen.

| recursieve waarde | copyBehavior waarde | Resulterende gedrag |
| --- | --- | --- |
| De waarde True |preserveHierarchy |Voor een bronmap Map1 Hello-structuur te volgen<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Hallo doelmap Map1 is gemaakt met dezelfde structuur, als de bron Hallo Hallo:<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 |
| De waarde True |flattenHierarchy |Voor een bronmap Map1 Hello-structuur te volgen<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Hallo doel Map1 is gemaakt met de Hallo structuur te volgen: <br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File5 |
| De waarde True |mergeFiles |Voor een bronmap Map1 Hello-structuur te volgen<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Hallo doel Map1 is gemaakt met de Hallo structuur te volgen: <br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 bestand2 + bestand3 + File4 + bestand 5 inhoud worden samengevoegd in één bestand met een automatisch gegenereerde naam. |
| ONWAAR |preserveHierarchy |Voor een bronmap Map1 Hello-structuur te volgen<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Hallo doelmap Map1 is gemaakt met de Hallo structuur te volgen:<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/><br/>Subfolder1 bestand3 File4 en File5 is niet opgenomen. |
| ONWAAR |flattenHierarchy |Voor een bronmap Map1 Hello-structuur te volgen<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Hallo doelmap Map1 is gemaakt met de Hallo structuur te volgen:<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand2<br/><br/>Subfolder1 bestand3 File4 en File5 is niet opgenomen. |
| ONWAAR |mergeFiles |Voor een bronmap Map1 Hello-structuur te volgen<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Bestand2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Hallo doelmap Map1 is gemaakt met de Hallo structuur te volgen:<br/><br/>Map1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 + bestand2 inhoud worden samengevoegd in één bestand met een automatisch gegenereerde naam.<br/>&nbsp;&nbsp;&nbsp;&nbsp;Automatisch gegenereerde naam voor File1<br/><br/>Subfolder1 bestand3 File4 en File5 is niet opgenomen. |

## <a name="supported-file-and-compression-formats"></a>Ondersteunde indelingen voor bestands- en compressie
Zie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artikel voor meer informatie.

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a>JSON-voorbeelden voor het kopiëren van gegevens tooand van bestandssysteem
Hallo volgende voorbeelden geven voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van Hallo [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Ze geven weer hoe toocopy gegevens tooand uit een on-premises bestandssysteem en de Azure-blobopslag. U kunt gegevens echter kopiëren *rechtstreeks* vanaf elke Hallo bronnen tooany van Hallo put die worden vermeld in [ondersteunde gegevensbronnen en put](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van de Kopieeractiviteit in Azure Data Factory.

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a>Voorbeeld: Gegevens kopiëren van een lokaal bestand system tooAzure Blob-opslag
In dit voorbeeld laat zien hoe toocopy gegevens van een lokaal bestand system tooAzure Blob-opslag. Hallo voorbeeld heeft Hallo Data Factory-entiteiten te volgen:

* Een gekoppelde service van het type [OnPremisesFileServer](#linked-service-properties).
* Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Invoer [gegevensset](data-factory-create-datasets.md) van het type [FileShare](#dataset-properties).
* Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [FileSystemSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Hallo voorbeeld te volgen gekopieerd timeseries gegevens van een lokaal bestand system tooAzure Blob-opslag om het uur. Hallo JSON-eigenschappen die worden gebruikt in deze voorbeelden worden beschreven in Hallo secties na Hallo voorbeelden.

Instellen als eerste stap van Data Management Gateway volgens de instructies in Hallo [gegevens verplaatsen tussen lokale bronnen en Hallo cloud met Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).

**Bestandsserver voor on-Premises gekoppelde service:**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

Aangeraden wordt Hallo **encryptedCredential** eigenschap Hallo in plaats daarvan **userid** en **wachtwoord** eigenschappen. Zie [bestandsserver gekoppelde service](#linked-service-properties) voor meer informatie over deze gekoppelde service.

**Gekoppelde Azure Storage-service:**

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

**Lokale bestandsnaam systeem invoergegevensset:**

Gegevens wordt opgehaald uit een nieuw bestand om het uur. Hallo folderPath en eigenschappen van de bestandsnaam worden bepaald op basis van Hallo begintijd van Hallo segment.  

Instelling `"external": "true"` Data Factory informeert dat gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
      ]
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

**Azure Blob storage-uitvoergegevensset:**

Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1). pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt. mappad Hallo Hallo jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Een kopieeractiviteit in een pijplijn met File System-bron en sink van Blob:**

Hallo pijplijn bevat een kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**FileSystemSource**, en **sink** type is ingesteld, te**BlobSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "FileSystemSource"
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

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a>Voorbeeld: Gegevens kopiëren van Azure SQL Database tooan on-premises-bestandssysteem
Hallo volgende ziet:

* Een gekoppelde service van het type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)
* Een gekoppelde service van het type [OnPremisesFileServer](#linked-service-properties).
* Een invoergegevensset van het type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
* Een uitvoergegevensset van het type [FileShare](#dataset-properties).
* Een pijplijn met een kopieeractiviteit die gebruikmaakt van [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) en [FileSystemSink](#copy-activity-properties).

Hallo voorbeeld opgehaald-timeseries-gegevens uit een Azure SQL tabel tooan on-premises bestandssysteem om het uur. Hallo JSON-eigenschappen die worden gebruikt in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.

**Azure SQL Database, gekoppelde service:**

```JSON
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

**Bestandsserver voor on-Premises gekoppelde service:**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

Aangeraden wordt Hallo **encryptedCredential** eigenschap in plaats van Hallo **userid** en **wachtwoord** eigenschappen. Zie [gekoppelde service van bestandssysteem](#linked-service-properties) voor meer informatie over deze gekoppelde service.

**Azure SQL invoergegevensset:**

Hallo-voorbeeld wordt ervan uitgegaan dat u een tabel 'MijnTabel' in Azure SQL gemaakt hebt en een kolom met de naam 'timestampcolumn' voor timeseries gegevens bevat.

Instelling ``“external”: ”true”`` Data Factory informeert dat gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.

```JSON
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

**Lokale bestandsnaam uitvoergegevensset systeem:**

Gegevens zijn gekopieerde tooa nieuw bestand om het uur. Hallo folderPath en de bestandsnaam voor Hallo blob zijn bepaald op basis van Hallo begintijd van Hallo segment.

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
      ]
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

**Een kopieeractiviteit in een pijplijn met de SQL-bron en sink van bestandssysteem:**

Hallo pijplijn bevat een kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur. Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**SqlSource**, en Hallo **sink** type is ingesteld, te**FileSystemSink**. Hallo SQL-query die is opgegeven voor Hallo **SqlReaderQuery** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


U kunt ook kolommen uit de bron gegevensset toocolumns uit sink gegevensset in de definitie van de activiteit kopiëren Hallo toewijzen. Zie voor meer informatie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Prestaties en afstemmen
 toolearn over sleutel factoren die gevolgen Hallo-prestaties van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize, Zie Hallo [Kopieeractiviteit prestaties en prestatieafstemming handleiding](data-factory-copy-activity-performance.md).
