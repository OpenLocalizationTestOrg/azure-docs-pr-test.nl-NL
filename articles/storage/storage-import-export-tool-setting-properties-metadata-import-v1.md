---
title: aaaSetting eigenschappen en metagegevens met behulp van Azure Import/Export - v1 | Microsoft Docs
description: Meer informatie over hoe de eigenschappen en metagegevens toobe toospecify ingesteld op Hallo bestemming blobs wanneer uitgevoerd hello Azure-hulpprogramma voor importeren/exporteren tooprepare uw schijven. Dit verwijst toov1 Hallo hulpprogramma voor importeren/exporteren.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: e8541695-bcfb-4bf0-84d9-72c9de32a0a8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 66e55c2076fbcda9b78302f17b5ff2cf96bb24e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a>Instellen van eigenschappen en metagegevens tijdens Hallo importeren
Wanneer u op uw stations Hallo Microsoft Azure-hulpprogramma voor importeren/exporteren tooprepare uitvoert, kunt u eigenschappen en metagegevens toobe ingesteld op Hallo bestemming blobs. Volg deze stappen:  
  
1.  Eigenschappen van de blob tooset, maak een tekstbestand op uw lokale computer waarmee u de namen en waarden.  
  
2.  tooset blob-metagegevens, maak een tekstbestand op uw lokale computer waarmee metagegevens namen en waarden.  
  
3.  Hallo volledig pad tooone of beide van deze bestanden toohello Azure-hulpprogramma voor importeren/exporteren doorgeven als onderdeel van Hallo `PrepImport` bewerking.  
  
> [!NOTE]
>  Wanneer u een bestand eigenschappen of metagegevens als onderdeel van een sessie exemplaar opgeeft, worden deze eigenschappen of metagegevens zijn ingesteld voor elke blob die is geïmporteerd als onderdeel van die sessie kopiëren. Als u een andere set eigenschappen of metagegevens toospecify voor een aantal Hallo BLOB's worden geïmporteerd wilt, moet u een afzonderlijke kopiëren een sessie met andere eigenschappen of bestanden met metagegevens toocreate.  
  
## <a name="specify-blob-properties-in-a-text-file"></a>Blob-eigenschappen opgeven in een tekstbestand  
Eigenschappen van de blob toospecify, een lokaal tekstbestand maken en XML waarmee de namen van eigenschappen als elementen en eigenschapswaarden als waarden bevatten. Hier volgt een voorbeeld waarin sommige eigenschapswaarden:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
Hallo tooa lokale bestandslocatie zoals opslaan `C:\WAImportExport\ImportProperties.txt`.  
  
## <a name="specify-blob-metadata-in-a-text-file"></a>Blobmetagegevens opgeven in een tekstbestand  
Op deze manier toospecify blob-metagegevens, maakt u een lokaal tekstbestand met namen van metagegevens als elementen en metagegevenswaarden als waarden. Hier volgt een voorbeeld waarin enkele metagegevenswaarden:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
Hallo tooa lokale bestandslocatie zoals opslaan `C:\WAImportExport\ImportMetadata.txt`.  
  
## <a name="create-a-copy-session-including-hello-properties-or-metadata-files"></a>Een kopie sessie inclusief Hallo eigenschappen of bestanden met metagegevens maken  
Wanneer u hello Azure-hulpprogramma voor importeren/exporteren tooprepare Hallo import-taak uitvoert, geef Hallo eigenschappenbestand op Hallo-opdrachtregel met behulp van Hallo `PropertyFile` parameter. Geef Hallo metagegevensbestand op Hallo-opdrachtregel met behulp van Hallo `/MetadataFile` parameter. Hier volgt een voorbeeld waarin beide bestanden:  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a>Volgende stappen

* [Bestandsindeling van het metagegevens- en eigenschappenbestand van de Import/Export-service](storage-import-export-file-format-metadata-and-properties.md)
