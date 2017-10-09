---
title: importtaak aaaSample werkstroom tooprep harde schijven voor een Azure Import/Export - v1 | Microsoft Docs
description: Zie een overzicht voor het volledige proces Hallo stations voorbereiden van een import-taak in hello Azure Import/Export-service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 6eb1b1b7-c69f-4365-b5ef-3cd5e05eb72a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: f836fc6104d8b4ad5660cb110a62f61b40b0b7ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>Voorbeeld werkstroom tooprepare harde schijven voor een import-taak
In dit onderwerp wordt u begeleid Hallo volledige proces van het voorbereiden van stations voor een import-taak.  
  
In dit voorbeeld volgt de gegevens in een venster Azure storage-account met de naam Hallo geïmporteerd `mystorageaccount`:  
  
|Locatie|Beschrijving|  
|--------------|-----------------|  
|H:\Video|Een verzameling van video's, 5 TB in totaal.|  
|H:\Photo|Een verzameling van foto's, 30 GB in totaal.|  
|K:\Temp\FavoriteMovie.ISO|A Blu-ray™ schijfimage, 25 GB.|  
|\\\bigshare\john\music|Een verzameling van muziekbestanden op een netwerkshare, 10 GB in totaal.|  
  
Hallo import-taak wordt deze gegevens importeren in Hallo bestemmingen in Hallo storage-account te volgen:  
  
|Bron|Doel-virtuele map of blob|  
|------------|-------------------------------------------|  
|H:\Video|https://mystorageaccount.BLOB.Core.Windows.NET/video|  
|H:\Photo|https://mystorageaccount.BLOB.Core.Windows.NET/Photo|  
|K:\Temp\FavoriteMovie.ISO|https://mystorageaccount.BLOB.Core.Windows.NET/Favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|https://mystorageaccount.BLOB.Core.Windows.NET/Music|  
  
Met deze toewijzing Hallo bestand `H:\Video\Drama\GreatMovie.mov` worden geïmporteerde toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.  
  
Vervolgens toodetermine hoeveel harde schijven nodig zijn, compute Hallo grootte van Hallo gegevens:  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
Twee 3TB harde schijven moet voldoende zijn voor dit voorbeeld. Echter sinds Hallo bronmap `H:\Video` 5TB aan gegevens en capaciteit van uw één harde schijf is alleen 3TB is noodzakelijk toobreak `H:\Video` Hallo in twee kleinere mappen voordat u Microsoft Azure-hulpprogramma voor importeren/exporteren: `H:\Video1` en `H:\Video2`. Deze stap levert Hallo bron mappen te volgen:  
  
|Locatie|Grootte|Doel-virtuele map of blob|  
|--------------|----------|-------------------------------------------|  
|H:\Video1|2.5 TB|https://mystorageaccount.BLOB.Core.Windows.NET/video|  
|H:\Video2|2.5 TB|https://mystorageaccount.BLOB.Core.Windows.NET/video|  
|H:\Photo|30 GB|https://mystorageaccount.BLOB.Core.Windows.NET/Photo|  
|K:\Temp\FavoriteMovies.ISO|25 GB|https://mystorageaccount.BLOB.Core.Windows.NET/Favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|10GB|https://mystorageaccount.BLOB.Core.Windows.NET/Music|  
  
 Let op: hoewel Hallo `H:\Video`directory tootwo mappen is gesplitst, ze toohello Wijs dezelfde virtuele map van de bestemming in Hallo storage-account. Op deze manier alle videobestanden worden beheerd via één `video` container in Hallo storage-account.  
  
 Hallo hierboven bron mappen gelijkmatig zijn verdeeld vervolgens toohello twee harde schijven:  
  
||||  
|-|-|-|  
|Harde schijf|Bron-mappen|Totale grootte|  
|Eerste schijf|H:\Video1|2,5 TB + 30 GB|  
||H:\Photo||  
|Tweede station|H:\Video2|2,5 TB + 35 GB|  
||K:\Temp\BlueRay.ISO||  
||\\\bigshare\john\music||  
  
U kunt bovendien Hallo metagegevens voor alle bestanden volgende instellen:  
  
-   **UploadMethod:** Windows Azure Import/Export-service  
  
-   **DataSetName:** SampleData  
  
-   **CreationDate:** 1/10/2013  
  
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
  
-   **Content-Type:** application/octet-stream  
  
-   **Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ ==  
  
-   **Cache-Control:** no-cache  
  
tooset deze eigenschappen, maak een tekstbestand, `c:\WAImportExport\SampleProperties.txt`:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
U bent nu klaar toorun hello Azure-hulpprogramma voor importeren/exporteren tooprepare Hallo twee harde schijven. Opmerking:  
  
-   de eerste schijf Hallo is als station X gekoppeld.  
  
-   de tweede schijf Hallo is als station Y gekoppeld.  
  
-   Hallo-sleutel voor opslagaccount hello `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a>Voorbereiden van schijf voor het importeren van gegevens vooraf is geladen
 
 Als Hallo gegevens toobe geïmporteerd al aanwezig op Hallo schijf is, gebruikt u Hallo vlag /skipwrite. Waarde van /t en /srcdir moet toohello schijf wordt voorbereid voor het importeren van gegevenspunt. Als niet alle gegevens op Hallo Hallo schijf toogo toohello moet dezelfde bestemming virtuele map of hoofdmap van het opslagaccount hello, Voer Hallo dezelfde opdracht voor elke map afzonderlijk houden Hallo-waarde van /id hetzelfde voor alle uitvoert.

>[!NOTE] 
>Geef geen/Format zoals deze wordt Hallo gegevens op Hallo schijf wissen. U kunt opgeven / versleutelen of /bk, afhankelijk van of Hallo schijf al is versleuteld of niet. 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a>Sessies - kopiëren eerst station

Voer voor de eerste schijf Hallo, hello Azure Import/Export Tool tweemaal toocopy Hallo twee bron mappen:  

**Eerste kopieersessie**
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

**Tweede kopieersessie**

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a>Kopieer sessies - tweede station
 
Voor Hallo tweede station, voer hello Azure-hulpprogramma voor importeren/exporteren drie keer wanneer elk voor Hallo bron mappen en eens Hallo zelfstandig Blu-Ray™ afbeeldingsbestand):  
  
**Eerste kopieersessie** 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
**Tweede kopieersessie**

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
**Derde kopieersessie**  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a>Kopiëren van de sessie is voltooid

Nadat Hallo kopie sessies hebt voltooid, kunt u Verbreek de verbinding tussen twee schijven Hallo Hallo kopie computer en toohello juiste Windows Azure-datacenter worden verzonden. U gaat Hallo twee journaal bestanden uploaden `FirstDrive.jrn` en `SecondDrive.jrn`, wanneer u Hallo import-taak in Hallo maken [Windows Azure-beheerportal](https://manage.windowsazure.com/).  
  
## <a name="next-steps"></a>Volgende stappen

* [Harde schijven voorbereiden voor een importtaak](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Naslaggids voor veelgebruikte opdrachten](storage-import-export-tool-quick-reference-v1.md) 
