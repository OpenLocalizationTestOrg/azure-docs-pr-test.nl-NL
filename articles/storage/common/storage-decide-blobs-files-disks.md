---
title: aaaDeciding wanneer toouse Azure Blobs, Azure-bestanden of Azure gegevensschijven
description: Meer informatie over Hallo verschillende manieren toostore en toegang tot gegevens in Azure toohelp dat u welke technologie toouse beslist.
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: robinsh
ms.openlocfilehash: cd43abde43daf33dd7c43aa2696a9c8d5cd19612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deciding-when-toouse-azure-blobs-azure-files-or-azure-data-disks"></a>Bepalen wanneer toouse Azure Blobs, Azure-bestanden of Azure gegevensschijven

Microsoft Azure biedt verschillende functies in Azure Storage voor het opslaan en toegang tot uw gegevens in de cloud Hallo. In dit artikel bevat informatie over Azure Files, Blobs en gegevensschijven en is ontworpen toohelp u tussen deze functies kiezen.

## <a name="scenarios"></a>Scenario's

Hallo volgende tabel vergelijkt bestanden, Blobs en gegevensschijven en voorbeeldscenario's geschikt is voor elk worden weergegeven.

| Functie | Beschrijving | Wanneer toouse |
|--------------|-------------|-------------|
| **Azure Files** | Biedt een interface SMB, de clientbibliotheken, en een [REST-interface](/rest/api/storageservices/file-service-rest-api) waardoor toegang vanaf elke locatie toostored bestanden. | Gewenste te 'lift- en verschuiven' een toepassing toohello cloud dat al gebruikmaakt van Hallo systeemeigen bestand door het systeem-API's tooshare gegevens tussen deze en andere toepassingen worden uitgevoerd in Azure.<br/><br/>Wilt u toostore ontwikkeling en foutopsporing hulpmiddelen die toobe toegankelijk vanuit veel virtuele machines nodig. |
| **Azure Blobs** | Biedt clientbibliotheken en een [REST-interface](/rest/api/storageservices/blob-service-rest-api) waarmee ongestructureerde gegevens te worden opgeslagen en gebruikt een grootschalige in blok-blobs. | Wilt u uw toepassing toosupport streaming en willekeurige-scenario's.<br/><br/>Wilt u toobe kunnen tooaccess toepassingsgegevens vanaf elke locatie. |
| **Azure gegevensschijven** | Biedt clientbibliotheken en een [REST-interface](/rest/api/compute/virtualmachines/virtualmachines-create-or-update) waarmee gegevens toobe permanent opgeslagen en is toegankelijk vanuit een gekoppelde virtuele harde schijf. | U wilt toolift en toepassingen die gebruikmaken van systeemeigen file system-API's tooread en gegevensschijven toopersistent schrijven verschuiven.<br/><br/>Wilt u toostore gegevens die niet vereist toobe toegankelijk van buiten Hallo virtuele machine toowhich Hallo schijf is gekoppeld. |

## <a name="comparison-files-and-blobs"></a>Vergelijking: De bestanden en de Blobs

Hallo volgende tabel vergelijkt de Azure-bestanden met Azure Blobs.  
  
||||  
|-|-|-|  
|**Kenmerk**|**Azure Blobs**|**Azure Files**|  
|Opties voor duurzaamheid|LRS, ZRS, GRS (en RA-GRS voor hogere beschikbaarheid)|LRS, GRS|  
|Toegankelijkheid|REST-API’s|REST-API’s<br /><br /> SMB 2.1 als SMB 3.0 (standaard bestandssysteem API's)|  
|Connectiviteit|REST-API's--wereldwijd|REST-API's - wereldwijd<br /><br /> SMB 2.1--binnen de regio<br /><br /> SMB 3.0--wereldwijd|  
|Eindpunten|`http://myaccount.blob.core.windows.net/mycontainer/myblob`|`\\myaccount.file.core.windows.net\myshare\myfile.txt`<br /><br /> `http://myaccount.file.core.windows.net/myshare/myfile.txt`|  
|Mappen|Platte naamruimte|De waarde True directory-objecten|  
|Hoofdlettergevoeligheid van namen|Hoofdlettergevoelig|Niet hoofdlettergevoelig, maar case behouden|  
|Capaciteit|Up too500 TB containers|Bestandsshares 5 TB|  
|Doorvoer|Up too60 MB/s per blok-blob|Up too60 MB/s per share|  
|Grootte van object|Up too200 GB/blok-blob|Up too1TB per bestand|  
|Gefactureerd capaciteit|Op basis van geschreven bytes|Op basis van de bestandsgrootte|  
|Clientbibliotheken|Meerdere talen|Meerdere talen|  
  
## <a name="comparison-files-and-data-disks"></a>Vergelijking: De bestanden en de gegevensschijven

Azure Files een aanvulling op Azure gegevensschijven. Een gegevensschijf kan alleen bijgevoegde tooone Azure virtuele Machine tegelijk worden. Gegevensschijven vaste indeling VHD's opgeslagen als pagina-blobs in Azure Storage zijn en worden gebruikt door Hallo virtuele machine toostore duurzame gegevens. Bestandsshares in de Azure-bestanden kunnen worden geopend in Hallo dezelfde manier als Hallo lokale schijf (met behulp van systeemeigen API's van het bestandssysteem) wordt geopend en kunnen worden gedeeld door veel virtuele machines.  
 
Hallo volgende tabel vergelijkt de Azure-bestanden met Azure gegevensschijven.  
 
||||  
|-|-|-|  
|**Kenmerk**|**Azure gegevensschijven**|**Azure Files**|  
|Bereik|Exclusieve tooa één virtuele machine|Gedeelde toegang over meerdere virtuele machines|  
|Momentopnamen en kopiëren|Ja|Nee|  
|Configuratie|Bij het opstarten van Hallo virtuele machine verbonden|Verbonden nadat Hallo virtuele machine is gestart|  
|Authentication|Ingebouwd|Met net use instellen|  
|Opruimen|Automatisch|Handmatig|  
|Toegang met behulp van REST|Bestanden in Hallo VHD kunnen niet worden geopend.|Bestanden die zijn opgeslagen op een share kunnen worden geopend|  
|Maximale grootte|Schijf van 1 TB|5 TB-bestandsshare en 1 TB bestand binnen share|  
|Max. 8KB IOP 's|500 IOP 's|1000 IOP 's|  
|Doorvoer|Up too60 MB/s per schijf|Up too60 MB/s per bestandsshare|  

## <a name="next-steps"></a>Volgende stappen

Wanneer u beslissingen neemt over hoe uw gegevens worden opgeslagen en toegankelijk is, moet u ook overwegen Hallo kosten die zijn betrokken. Zie voor meer informatie [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/).
  
Sommige SMB-functies zijn niet van toepassing toohello cloud. Zie voor meer informatie [functies die niet wordt ondersteund door Azure File service Hallo](/rest/api/storageservices/features-not-supported-by-the-azure-file-service).
  
Zie voor meer informatie over gegevensschijven [beheren van schijven en installatiekopieën](../../virtual-machines/windows/about-disks-and-vhds.md) en [hoe tooAttach een gegevensschijf tooa virtuele Windows-Machine](../../virtual-machines/windows/classic/attach-disk.md).
