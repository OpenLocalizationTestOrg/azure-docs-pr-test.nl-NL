---
title: importtaak aaaPreparing harde schijven voor een Azure Import/Export - v1 | Microsoft Docs
description: Meer informatie over hoe tooprepare harde schijven met Hallo WAImportExport v1 hulpprogramma toocreate een import-taak voor hello Azure Import/Export-service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 3d818245-8b1b-4435-a41f-8e5ec1f194b2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 8803ac01b7c7a2ec2e3199231d7b4c04ceafd5a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>Harde schijven voorbereiden voor een importtaak
tooprepare een of meer harde schijven voor een import-taak als volgt te werk:

-   Hallo gegevens tooimport identificeren in Hallo Blob-service

-   Doel-virtuele mappen en blobs in Hallo Blob-service identificeren

-   Het aantal stations dat u moet bepalen

-   Hallo gegevens tooeach van de vaste schijven te kopiëren

 Zie voor een voorbeeldwerkstroom [voorbeeldwerkstroom tooPrepare harde schijven voor een Import-taak](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md).

## <a name="identify-hello-data-toobe-imported"></a>Hallo gegevens toobe geïmporteerd identificeren
 Hallo eerste stap toocreating een import-taak is toodetermine welke mappen en bestanden u tooimport gaat. Dit kan een lijst met mappen, een lijst met unieke bestanden of een combinatie van deze twee zijn. Wanneer een directory opgenomen is, zal alle bestanden in het Hallo-map en alle submappen onderdeel zijn van Hallo import-taak.

> [!NOTE]
>  Aangezien submappen opgenomen recursief worden wanneer een van de bovenliggende map opgenomen is, geef alleen Hallo van de bovenliggende map. Geef geen ook op een van de bijbehorende submappen.
>
>  Hallo Microsoft Azure-hulpprogramma voor importeren/exporteren heeft momenteel, Hallo volgende beperking: als een map meer gegevens bevat dan een harde schijf kan bevatten, moet Hallo directory toobe opgedeeld in kleinere mappen. Bijvoorbeeld, als een map 2,5 TB bevat van gegevens en Hallo capaciteit van de harde schijf is alleen 2TB, moet u toobreak Hallo 2,5 TB directory in kleinere mappen. Deze beperking wordt opgelost in een latere versie van Hallo-hulpprogramma.

## <a name="identify-hello-destination-locations-in-hello-blob-service"></a>De bestemmingslocatie Hallo in Hallo blob-service identificeren
 Voor elk bestand of map die worden geïmporteerd, moet u tooidentify een bestemming virtuele map of een blob in hello Azure Blob-service. U gaat deze doelen gebruiken als invoer toohello Azure-hulpprogramma voor importeren/exporteren. Houd er rekening mee dat mappen moeten worden gescheiden met Hallo slash-teken '/'.

 Hallo volgende tabel ziet u enkele voorbeelden van blob-doelen:

|Bronbestand of map|Bestemmings-blob of virtuele map|
|------------------------------|-------------------------------------------|
|H:\Video|https://mystorageaccount.BLOB.Core.Windows.NET/video|
|H:\Photo|https://mystorageaccount.BLOB.Core.Windows.NET/Photo|
|K:\Temp\FavoriteVideo.ISO|https://mystorageaccount.BLOB.Core.Windows.NET/Favorite/FavoriteVideo.ISO|
|\\\myshare\john\music|https://mystorageaccount.BLOB.Core.Windows.NET/Music|

## <a name="determine-how-many-drives-are-needed"></a>Bepalen hoeveel stations nodig zijn
 Vervolgens moet u toodetermine:

-   het aantal harde schijven Hallo nodig toostore Hallo gegevens.

-   Hallo mappen en/of zelfstandige bestanden die gekopieerd tooeach van de vaste schijf worden.

 Zorg ervoor dat u het aantal harde schijven, moet u toostore Hallo gegevens die u overdraagt Hallo.

## <a name="copy-data-tooyour-hard-drive"></a>Kopiëren van gegevens tooyour harde schijf
 Deze sectie beschrijft hoe toocall Azure-hulpprogramma voor importeren/exporteren toocopy Hallo uw gegevens tooone of meer harde schijven. Elke keer dat u hello Azure-hulpprogramma voor importeren/exporteren kunt aanroepen, maakt u een nieuw *kopiëren sessie*. U ten minste één exemplaar sessie maken voor elk station toowhich u gegevens; kopiëren in sommige gevallen moet u mogelijk meer dan één exemplaar sessie toocopy alle uw toosingle gegevensstation. Hier volgen enkele oorzaken die mogelijk moet u meerdere kopie sessies:

-   U moet voor elke schijf die u naar kopiëren een afzonderlijke kopie-sessie maken.

-   Een kopieersessie kunt kopiëren één map of een enkel blob toohello station. Als u meerdere mappen, meerdere blobs of een combinatie van beide kopieert, moet u toocreate meerdere kopie-sessies.

-   U kunt de eigenschappen en metagegevens die worden ingesteld op Hallo blobs geïmporteerd als onderdeel van een import-taak opgeven. Hallo eigenschappen of metagegevens die u voor een sessie kopiëren opgeeft tooall blobs die zijn opgegeven door die kopieersessie van toepassing. Als u andere eigenschappen toospecify of metagegevens voor enkele blobs wilt, moet u een afzonderlijke kopiëren sessie toocreate. Zie [eigenschappen instellen en metagegevens tijdens het importproces Hallo](storage-import-export-tool-setting-properties-metadata-import-v1.md)voor meer informatie.

> [!NOTE]
>  Als u meerdere machines die voldoen aan Hallo vereisten die worden beschreven hebt in [instellen hello Azure-hulpprogramma voor importeren/exporteren](storage-import-export-tool-setup-v1.md), kunt u vaste gegevensstations toomultiple parallel door een exemplaar van dit hulpprogramma wordt uitgevoerd op elke machine kopiëren.

 Voor elke harde schijf die u Hello Azure-hulpprogramma voor importeren/exporteren opstelt, maakt Hallo hulpprogramma een enkele journal-bestand. Hallo-logboek bestanden moet u in al uw stations toocreate Hallo import-taak. Hallo journal-bestand kan ook worden de gebruikte tooresume station voorbereiding als Hallo hulpprogramma wordt onderbroken is.

### <a name="azure-importexport-tool-syntax-for-an-import-job"></a>De syntaxis van het Azure Import/Export hulpprogramma voor een import-taak
 tooprepare stations voor een import-taak aanroepen hello Azure-hulpprogramma voor importeren/exporteren Hello **PrepImport** opdracht. Welke parameters die u wilt opnemen, is afhankelijk van of dit de eerste kopieersessie of een latere kopieersessie is Hallo.

 Hallo vereist eerste kopieersessie voor een station een aantal extra parameters toospecify hello opslagaccountsleutel; Hallo doel stationsletter; Hiermee wordt aangegeven of de Hallo station moet worden geformatteerd; of Hallo station moet worden versleuteld en zo ja, Hallo BitLocker-sleutel; en Hallo logboekmap. Hallo-syntaxis voor een eerste kopie sessie toocopy is hier een map of één bestand:

 **Sessie toocopy één map eerst kopiëren**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **Eerst sessie toocopy één bestand kopiëren**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 In latere kopie sessies hoeft u niet toospecify Hallo aanvankelijke parameters. Hallo-syntaxis voor een volgende kopie sessie toocopy is hier een map of één bestand:

 **Daaropvolgende kopie sessies toocopy één map**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **Daaropvolgende kopie sessies toocopy één bestand**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

### <a name="parameters-for-hello-first-copy-session-for-a-hard-drive"></a>Parameters voor Hallo eerst sessie voor een harde schijf kopiëren
 Telkens wanneer die u hello Azure-hulpprogramma voor importeren/exporteren toocopy bestanden toohello harde schijf uitvoeren, maakt Hallo hulpprogramma een kopieersessie. Elke sessie kopiëren kopieert één map of een enkel bestand tooa harde schijf. Hallo-status van Hallo kopieersessie geschreven toohello journal-bestand. Als een kopieersessie wordt onderbroken (bijvoorbeeld vervaldatum tooa system stroomstoring), kan het worden hervat door Hallo hulpprogramma opnieuw uit te voeren en Hallo journal-bestand op Hallo vanaf de opdrachtregel op te geven.

> [!WARNING]
>  Als u Hallo opgeeft **/opmaken** parameter voor de eerste kopieersessie Hallo Hallo schijf wordt geformatteerd en alle gegevens op Hallo station worden gewist. Het verdient aanbeveling dat u lege stations alleen voor uw sessie kopiëren gebruiken.

 Hallo opdracht die wordt gebruikt voor Hallo eerste kopieersessie voor elk station verschillende parameters dan Hallo-opdrachten voor latere kopie-sessies vereist. Hallo bevat volgende tabel Hallo extra parameters die beschikbaar voor Hallo eerste kopieersessie zijn:

|Opdrachtregelparameter|Beschrijving|
|-----------------------------|-----------------|
|**/SK:**< StorageAccountKey\>|`Optional.`Hallo-toegangssleutel voor Hallo storage account toowhich Hallo-gegevens worden geïmporteerd. U moet ofwel opnemen **/sk:**< StorageAccountKey\> of **/csas:**< ContainerSas\> in Hallo-opdracht.|
|**/csas:**< ContainerSas\>|`Optional`. Hallo container SAS toouse tooimport gegevens toohello storage-account. U moet ofwel opnemen **/sk:**< StorageAccountKey\> of **/csas:**< ContainerSas\> in Hallo-opdracht.<br /><br /> Hallo-waarde voor deze parameter moet beginnen met de containernaam hello, gevolgd door een vraagteken (?) en SAS-token Hallo. Bijvoorbeeld:<br /><br /> `mycontainer?sv=2014-02-14&sr=c&si=abcde&sig=LiqEmV%2Fs1LF4loC%2FJs9ZM91%2FkqfqHKhnz0JM6bqIqN0%3D&se=2014-11-20T23%3A54%3A14Z&sp=rwdl`<br /><br /> Hallo-machtigingen of opgegeven op het Hallo-URL of in een opgeslagen toegangsbeleid, lezen, moet bevatten schrijven en verwijderen voor de taken van gegevensimport en lezen, schrijven en lijst voor exporteren.<br /><br /> Als deze parameter wordt opgegeven, wordt alle blobs toobe geïmporteerd of geëxporteerd moet binnen het opgegeven in de shared access signature voor Hallo Hallo-container.|
|**/ t:**< TargetDriveLetter\>|`Required.`stationsletter Hallo Hallo doel harde schijf voor Hallo huidige kopie-sessie, zonder hallo afsluitende dubbele punt.|
|**/ Format**|`Optional.`Geef deze parameter als Hallo station toobe geformatteerd moet. anders weglaten. Voordat Hallo hulpprogramma Hallo station opgemaakt, wordt u gevraagd om een bevestiging van de console. toosuppress Hallo bevestiging Hallo /silentmode parameter opgeven.|
|**/silentmode**|`Optional.`Geef deze parameter toosuppress Hallo bevestiging voor het formatteren van Hallo targert schijf.|
|**/ versleutelen**|`Optional.`Deze parameter opgegeven tijdens het Hallo station nog niet zijn versleuteld met BitLocker en behoeften toobe versleuteld door Hallo-hulpprogramma. Als Hallo station al is versleuteld met BitLocker, deze parameter en geef Hallo `/bk` parameter, bieden Hallo bestaande BitLocker-sleutel.<br /><br /> Als u Hallo opgeeft `/format` parameter, dan hebt u moet ook opgeven Hallo `/encrypt` parameter.|
|**/BK:**< BitLockerKey\>|`Optional.`Als `/encrypt` is opgegeven, laat u deze parameter. Als `/encrypt` wordt weggelaten, moet u toohave al hebt Hallo-station met BitLocker is versleuteld. Gebruik deze parameter toospecify Hallo BitLocker-sleutel. BitLocker-versleuteling is vereist voor alle harde schijven voor de taken van gegevensimport.|
|**schakeloptie/LOGDIR op:**< LogDirectory\>|`Optional.`Hallo logboekmap geeft dat een toobe directory gebruikt uitgebreide logboeken toostore zoals tijdelijke manifestbestanden. Als niet wordt opgegeven, wordt de huidige map hello worden gebruikt als Hallo logboekmap.|

### <a name="parameters-required-for-all-copy-sessions"></a>Parameters die zijn vereist voor alle sessies van kopie
 Hallo journal-bestand bevat Hallo status voor alle kopie-sessies voor een harde schijf. Bevat ook informatie Hallo nodig toocreate Hallo importtaak. Wanneer uitgevoerd hello Azure-hulpprogramma voor importeren/exporteren, evenals een sessie-ID van het kopiëren, moet u altijd een journal-bestand opgeven:

|||
|-|-|
|Opdrachtregelparameter|Beschrijving|
|**/j:**< JournalFile\>|`Required.`Hallo pad toohello journal-bestand. Elk station moet precies één journaalbestand hebben. Houd er rekening mee dat Hallo journaal-bestand moet zich niet op Hallo doelstation. Hallo journaal bestandsextensie `.jrn`.|
|**/ID:**< sessie-id\>|`Required.`sessie-ID Hallo identificeert een kopieersessie. Het is gebruikte tooensure nauwkeurige herstel van een sessie onderbroken exemplaar. Bestanden die zijn gekopieerd in een kopieersessie worden opgeslagen in een map met de naam van sessie-ID op het doelstation Hallo Hallo.|

### <a name="parameters-for-copying-a-single-directory"></a>Parameters voor het kopiëren van een enkele map
 Bij het kopiëren van een enkele map toepassing hello volgende verplichte en optionele parameters:

|Opdrachtregelparameter|Beschrijving|
|----------------------------|-----------------|
|**/srcdir:**< SourceDirectory\>|`Required.`Hallo-bronmap met bestanden toobe toohello doelstation gekopieerd. Hallo mappad moet een absoluut pad (niet een relatief pad).|
|**/dstdir:**< DestinationBlobVirtualDirectory\>|`Required.`Hallo pad toohello bestemming virtuele map in uw Windows Azure-opslagaccount. de virtuele map Hallo mogelijk of bestaat mogelijk niet al.<br /><br /> U kunt opgeven dat een container of een blob-voorvoegsel, zoals `music/70s/`. Hallo moet doelmap beginnen met de containernaam hello, gevolgd door een slash '/', maar mogelijk ook optioneel een blob virtuele map die eindigt op "/".<br /><br /> Wanneer de doelcontainer Hallo Hallo hoofdcontainer is, moet expliciet Hallo-hoofdcontainer Hallo gewone slash, waaronder als `$root/`. Aangezien blobs onder Hallo hoofdcontainer niet opnemen '/' in hun naam eventuele submappen in de bronmap Hallo niet worden gekopieerd als doelmap Hallo Hallo root-container.<br /><br /> Niet zeker toouse geldig containernamen bij het opgeven van de doel-virtuele mappen of blobs. Houd er rekening mee dat de namen van containers in kleine letters moeten zijn. Zie voor naamgevingsregels voor container, [Naming en verwijzen naar Containers, Blobs en metagegevens](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).|
|**/ Toestand:**< naam &#124; Nee overschrijven &#124; overschrijven >|`Optional.`Hiermee geeft u Hallo gedrag wanneer een blob met de Hallo opgegeven adres bestaat al. Geldige waarden voor deze parameter zijn: `rename`, `no-overwrite` en `overwrite`. Houd er rekening mee dat deze waarden hoofdlettergevoelig zijn. Als geen waarde opgeeft, wordt Hallo standaard `rename`.<br /><br /> opgegeven waarde voor deze parameter is van invloed op alle Hallo-bestanden in Hallo map die is opgegeven door Hallo Hallo `/srcdir` parameter.|
|**/ BlobType:**< BlockBlob &#124; PageBlob >|`Optional.`Hiermee geeft u Hallo blobtype voor Hallo bestemming blobs. Geldige waarden zijn: `BlockBlob` en `PageBlob`. Houd er rekening mee dat deze waarden hoofdlettergevoelig zijn. Als geen waarde opgeeft, wordt Hallo standaard `BlockBlob`.<br /><br /> In de meeste gevallen `BlockBlob` wordt aanbevolen. Als u opgeeft `PageBlob`, lengte van elk bestand in map Hallo Hallo moet een veelvoud van 512, Hallo grootte van een pagina voor pagina-blobs.|
|**/ PropertyFile:**< PropertyFile\>|`Optional.`Pad toohello eigenschappenbestand voor Hallo bestemming blobs. Zie [Import/Export-service metagegevens en eigenschappen bestandsindeling](storage-import-export-file-format-metadata-and-properties.md) voor meer informatie.|
|**/ MetadataFile toe:**< MetadataFile toe\>|`Optional.`Pad toohello metagegevensbestand voor Hallo bestemming blobs. Zie [Import/Export-service metagegevens en eigenschappen bestandsindeling](storage-import-export-file-format-metadata-and-properties.md) voor meer informatie.|

### <a name="parameters-for-copying-a-single-file"></a>Parameters voor het kopiëren van een enkel bestand
 Bij het kopiëren van een enkel bestand hello volgende vereiste en optionele parameters van toepassing:

|Opdrachtregelparameter|Beschrijving|
|----------------------------|-----------------|
|**/srcfile:**< bronbestand\>|`Required.`Hallo volledig pad toohello bestand toobe gekopieerd. Hallo mappad moet een absoluut pad (niet een relatief pad).|
|**/dstblob:**< DestinationBlobPath\>|`Required.`Hallo pad toohello bestemmings-blob in uw Windows Azure-opslagaccount. Hallo blob mogelijk of bestaat mogelijk niet al.<br /><br /> Hallo blob naam die begint met de containernaam Hallo opgeven. Hallo blob-naam mag niet beginnen met '/' of Hallo opslagaccountnaam. Zie voor blob-naamgevingsregels, [Naming en verwijzen naar Containers, Blobs en metagegevens](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).<br /><br /> Wanneer de doelcontainer Hallo Hallo hoofdcontainer is, moet u expliciet opgeven `$root` als container, zoals Hallo `$root/sample.txt`. Let op: blobs onder Hallo hoofdcontainer niet opnemen '/' in hun naam.|
|**/ Toestand:**< naam &#124; Nee overschrijven &#124; overschrijven >|`Optional.`Hiermee geeft u Hallo gedrag wanneer een blob met de Hallo opgegeven adres bestaat al. Geldige waarden voor deze parameter zijn: `rename`, `no-overwrite` en `overwrite`. Houd er rekening mee dat deze waarden hoofdlettergevoelig zijn. Als geen waarde opgeeft, wordt Hallo standaard `rename`.|
|**/ BlobType:**< BlockBlob &#124; PageBlob >|`Optional.`Hiermee geeft u Hallo blobtype voor Hallo bestemming blobs. Geldige waarden zijn: `BlockBlob` en `PageBlob`. Houd er rekening mee dat deze waarden hoofdlettergevoelig zijn. Als geen waarde opgeeft, wordt Hallo standaard `BlockBlob`.<br /><br /> In de meeste gevallen `BlockBlob` wordt aanbevolen. Als u opgeeft `PageBlob`, lengte van elk bestand in map Hallo Hallo moet een veelvoud van 512, Hallo grootte van een pagina voor pagina-blobs.|
|**/ PropertyFile:**< PropertyFile\>|`Optional.`Pad toohello eigenschappenbestand voor Hallo bestemming blobs. Zie [Import/Export-service metagegevens en eigenschappen bestandsindeling](storage-import-export-file-format-metadata-and-properties.md) voor meer informatie.|
|**/ MetadataFile toe:**< MetadataFile toe\>|`Optional.`Pad toohello metagegevensbestand voor Hallo bestemming blobs. Zie [Import/Export-service metagegevens en eigenschappen bestandsindeling](storage-import-export-file-format-metadata-and-properties.md) voor meer informatie.|

### <a name="resuming-an-interrupted-copy-session"></a>Een onderbroken kopieersessie te hervatten
 Als een kopieersessie wordt onderbroken om welke reden, kunt u deze hervatten door Hallo hulpprogramma met alleen Hallo journaal-bestand opgegeven:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /ResumeSession
```

 Alleen Hallo meest recente kopieersessie, kan als is beëindigd, worden hervat.

> [!IMPORTANT]
>  Wanneer u een kopieersessie hervatten, mag niet worden gewijzigd Hallo de bronbestanden van gegevens en mappen toe te voegen of te verwijderen van bestanden.

### <a name="aborting-an-interrupted-copy-session"></a>Een onderbroken kopieersessie wordt afgebroken
 Als een kopieersessie wordt onderbroken en het is niet mogelijk tooresume (bijvoorbeeld als een bronmap bewezen ontoegankelijk), u moet afbreken Hallo huidige sessie zodat deze kan worden teruggedraaid kunnen vorige en nieuwe kopie-sessies worden gestart:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AbortSession
```

 Alleen Hallo kan laatste kopieersessie als beëindigd, worden afgebroken. Houd er rekening mee dat u kan niet afbreken Hallo eerste kopieersessie voor een station. U moet in plaats daarvan Hallo kopieersessie opnieuw met een nieuw journaalbestand.

## <a name="next-steps"></a>Volgende stappen

* [Hallo-instelling van Azure-hulpprogramma voor importeren/exporteren](storage-import-export-tool-setup-v1.md)
* [Instellen van eigenschappen en metagegevens tijdens Hallo importeren](storage-import-export-tool-setting-properties-metadata-import-v1.md)
* [Voorbeeld werkstroom tooprepare harde schijven voor een import-taak](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
* [Naslaggids voor veelgebruikte opdrachten](storage-import-export-tool-quick-reference-v1.md) 
* [De taakstatus controleren met kopielogboekbestanden](storage-import-export-tool-reviewing-job-status-v1.md)
* [Een importtaak herstellen](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Een exporttaak herstellen](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Het oplossen van problemen hello Azure-hulpprogramma voor importeren/exporteren](storage-import-export-tool-troubleshooting-v1.md)
