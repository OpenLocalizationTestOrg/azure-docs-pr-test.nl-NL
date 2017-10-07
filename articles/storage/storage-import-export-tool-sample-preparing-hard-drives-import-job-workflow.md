---
title: aaaSample werkstroom tooprep harde schijven voor een Azure Import/Export importtaak | Microsoft Docs
description: Zie een overzicht voor het volledige proces Hallo stations voorbereiden van een import-taak in hello Azure Import/Export-service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: muralikk
ms.openlocfilehash: 560220b7dc9f87416f1fec1ff30fa5cd65812ce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>Voorbeeld werkstroom tooprepare harde schijven voor een import-taak

In dit artikel begeleidt u bij Hallo complete proces van het voorbereiden van stations voor een import-taak.

## <a name="sample-data"></a>Voorbeeldgegevens

In dit voorbeeld volgt de gegevens in Azure storage-account met de naam Hallo geïmporteerd `mystorageaccount`:

|Locatie|Beschrijving|Gegevensgrootte|
|--------------|-----------------|-----|
|H:\Video\ |Een verzameling van video 's|12 TB|
|H:\Photo\ |Een verzameling van foto 's|30 GB|
|K:\Temp\FavoriteMovie.ISO|De schijfimage A Blu-ray™|25 GB|
|\\\bigshare\john\music\|Een verzameling van muziekbestanden op een netwerkshare|10 GB|

## <a name="storage-account-destinations"></a>Storage-account bestemmingen

Hallo import-taak wordt Hallo gegevens importeren in Hallo bestemmingen in Hallo storage-account te volgen:

|Bron|Doel-virtuele map of blob|
|------------|-------------------------------------------|
|H:\Video\ |video /|
|H:\Photo\ |Photo /|
|K:\Temp\FavoriteMovie.ISO|favorite/FavoriteMovies.ISO|
|\\\bigshare\john\music\ |Music|

Met deze toewijzing Hallo bestand `H:\Video\Drama\GreatMovie.mov` worden geïmporteerde toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.

## <a name="determine-hard-drive-requirements"></a>Harde schijf vereisten bepalen

Vervolgens toodetermine hoeveel harde schijven nodig zijn, compute Hallo grootte van Hallo gegevens:

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

Twee harde schijven van 8TB moet voldoende zijn voor dit voorbeeld. Echter sinds Hallo bronmap `H:\Video` heeft 12TB aan gegevens en capaciteit van uw één harde schijf is alleen 8TB, kunt u zich kunt toospecify dit op Hallo volgende manier in Hallo **driveset.csv** bestand:

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
Hallo-hulpprogramma wordt gegevens verdelen over twee harde schijven op een geoptimaliseerde manier.

## <a name="attach-drives-and-configure-hello-job"></a>Koppelen van stations en Hallo taak configureren
U koppelt beide schijven toohello machine en volumes maken. Vervolgens auteur **dataset.csv** bestand:
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

U kunt bovendien Hallo metagegevens voor alle bestanden volgende instellen:

* **UploadMethod:** Windows Azure Import/Export-service
* **DataSetName:** SampleData
* **CreationDate:** 1/10/2013

tooset metagegevens voor Hallo geïmporteerd bestanden, maak een tekstbestand, `c:\WAImportExport\SampleMetadata.txt`, hello volgende inhoud:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

U kunt ook een aantal eigenschappen instellen voor Hallo `FavoriteMovie.ISO` blob:

* **Content-Type:** application/octet-stream
* **Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ ==
* **Cache-Control:** no-cache

tooset deze eigenschappen, maak een tekstbestand, `c:\WAImportExport\SampleProperties.txt`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a>Voer hello Azure-hulpprogramma voor importeren/exporteren (WAImportExport.exe)

U bent nu klaar toorun hello Azure-hulpprogramma voor importeren/exporteren tooprepare Hallo twee harde schijven.

**Voor de eerste sessie Hallo:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

Als geen gegevens meer toobe toegevoegd moet, maakt u een andere dataset-bestand (dezelfde indeling als Initialdataset).

**Voor Hallo tweede sessie:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

Nadat Hallo kopie sessies hebt voltooid, kunt u Verbreek de verbinding tussen twee schijven Hallo Hallo kopie computer en toohello juiste Azure-datacenter worden verzonden. U gaat Hallo twee journaal bestanden uploaden `<FirstDriveSerialNumber>.xml` en `<SecondDriveSerialNumber>.xml`, wanneer u Hallo import-taak in hello Azure-portal maken.

## <a name="next-steps"></a>Volgende stappen

* [Harde schijven voorbereiden voor een importtaak](storage-import-export-tool-preparing-hard-drives-import.md)
* [Naslaggids voor veelgebruikte opdrachten](storage-import-export-tool-quick-reference.md)
