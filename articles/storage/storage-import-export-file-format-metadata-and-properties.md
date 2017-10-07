---
title: aaaAzure-Import/Export metagegevens en eigenschappen bestandsindeling | Microsoft Docs
description: Meer informatie over hoe toospecify metagegevens en eigenschappen van een of meer blobs die deel uitmaken van een importeren of exporteren van de taak.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 840364c6-d9a8-4b43-a9f3-f7441c625069
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: bb13c1f1a27baea77298cb224970cd521d02d8c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a>Azure Import/Export-service metagegevens en eigenschappen bestandsindeling
U kunt de eigenschappen voor een of meer blobs en metagegevens als onderdeel van een import-taak of een taak voor exporteren opgeven. tooset metagegevens of eigenschappen voor blobs als onderdeel van een import-taak wordt gemaakt, kunt u een bestand met metagegevens of eigenschappen op de harde schijf Hallo Hallo gegevens toobe geïmporteerd met opgeven. Voor een exporttaak worden metagegevens en eigenschappen geschreven tooa eigenschappen van metagegevens of bestand dat is opgenomen op de harde schijf Hallo tooyou geretourneerd.  
  
## <a name="metadata-file-format"></a>Bestandsindeling voor metagegevens  
Hallo-indeling van een bestand met metagegevens is als volgt:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|XML-Element|Type|Beschrijving|  
|-----------------|----------|-----------------|  
|`Metadata`|Hoofdelement|Hallo-hoofdelement van het metagegevensbestand Hallo.|  
|`metadata-name`|Tekenreeks|Optioneel. Hallo XML-element Hallo-naam van Hallo metagegevens voor Hallo blob en de waarde geeft aan Hallo-waarde van de instelling voor Hallo-metagegevens.|  
  
## <a name="properties-file-format"></a>Eigenschappen-bestandsindeling  
Hallo-indeling van een eigenschappenbestand is als volgt:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
[<Last-Modified>date-time-value</Last-Modified>]  
[<Etag>etag</Etag>]  
[<Content-Length>size-in-bytes<Content-Length>]  
[<Content-Type>content-type</Content-Type>]  
[<Content-MD5>content-md5</Content-MD5>]  
[<Content-Encoding>content-encoding</Content-Encoding>]  
[<Content-Language>content-language</Content-Language>]  
[<Cache-Control>cache-control</Cache-Control>]  
</Properties>  
```
  
|XML-Element|Type|Beschrijving|  
|-----------------|----------|-----------------|  
|`Properties`|Hoofdelement|Hallo-hoofdelement van Hallo eigenschappenbestand.|  
|`Last-Modified`|Tekenreeks|Optioneel. Hallo tijd laatste wijziging voor Hallo blob. Voor exporttaken.|  
|`Etag`|Tekenreeks|Optioneel. Hallo ETag-waarde van de blob. Voor exporttaken.|  
|`Content-Length`|Tekenreeks|Optioneel. Hallo grootte van de blob Hallo in bytes. Voor exporttaken.|  
|`Content-Type`|Tekenreeks|Optioneel. Hallo-inhoudstype van Hallo blob.|  
|`Content-MD5`|Tekenreeks|Optioneel. Hallo MD5-hash van de blob.|  
|`Content-Encoding`|Tekenreeks|Optioneel. Hallo van blob-inhoud codering.|  
|`Content-Language`|Tekenreeks|Optioneel. Hallo inhoud van de blob-taal.|  
|`Cache-Control`|Tekenreeks|Optioneel. Hallo cache besturingselement tekenreeks voor Hallo blob.|  

## <a name="next-steps"></a>Volgende stappen

Zie [blob-eigenschappen instellen](/rest/api/storageservices/set-blob-properties), [Blobmetagegevens ingesteld](/rest/api/storageservices/set-blob-metadata), en [instelling en het bij het ophalen van eigenschappen en metagegevens voor blob-bronnen](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) voor gedetailleerde informatie over het instellen van eigenschappen en blobmetagegevens-regels.
