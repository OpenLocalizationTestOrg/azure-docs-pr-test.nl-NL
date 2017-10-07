---
title: een Azure Import/Export-import-taak - v1 aaaRepairing | Microsoft Docs
description: Meer informatie over hoe toorepair een import-taak die is gemaakt en uitgevoerd met behulp van Azure Import/Export Hallo service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: b1cb7d7832276a05c0912cf57505e2a5d79e7846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-import-job"></a>Een importtaak herstellen
Hallo Microsoft Azure Import/Export-service mogelijk toocopy enkele van uw bestanden of onderdelen van een bestand toohello Windows Azure Blob-service. Redenen voor fouten zijn onder andere:  
  
-   Beschadigde bestanden  
  
-   Beschadigde schijven  
  
-   Hallo opslagaccountsleutel gewijzigd terwijl het Hallo-bestand is worden overgebracht.  
  
U kunt Hallo Microsoft Azure Import/Export-hulpprogramma met Hallo importeren taak kopiëren logboek bestanden, en Hallo hulpprogramma uploads Hallo ontbrekende bestanden (of delen van een bestand) tooyour Windows Azure storage-account toocomplete Hallo import-taak uitvoeren.  
  
## <a name="repairimport-parameters"></a>RepairImport parameters

Hallo volgende parameters kunnen worden opgegeven met **RepairImport**: 
  
|||  
|-|-|  
|**/ r:**< RepairFile\>|**Vereist.** Pad toohello Herstel dit bestand houdt Hallo voortgang van Hallo herstel en kunt u tooresume reparatie van een onderbroken. Elk station moet slechts één repair-bestand hebben. Wanneer u een reparatie voor een bepaald station start, doorgeven in Hallo pad tooa reparatie bestand, dat nog niet bestaat. tooresume reparatie van een onderbroken, moet u doorgeven in Hallo-naam van een bestaand bestand voor herstel. Hallo reparatie bestand corresponderende toohello doelstation moet altijd worden opgegeven.|  
|**schakeloptie/LOGDIR op:**< LogDirectory\>|**Optioneel.** Hallo logboekmap. Uitgebreide logboekbestanden worden toothis map geschreven. Als er geen logboekmap is opgegeven, wordt de huidige map Hallo gebruikt als Hallo logboekmap.|  
|**/ d:**< TargetDirectories\>|**Vereist.** Een of meer door puntkomma's gescheiden mappen met Hallo oorspronkelijke bestanden die zijn geïmporteerd. Hallo importeren station kan ook worden gebruikt, maar is niet vereist als alternatieve locaties van de originele bestanden beschikbaar zijn.|  
|**/BK:**< BitLockerKey\>|**Optioneel.** Als u wilt dat Hallo hulpprogramma toounlock een versleuteld station waar de originele bestanden Hallo beschikbaar zijn, moet u Hallo BitLocker-sleutel opgeven.|  
|**/sn:**< StorageAccountName\>|**Vereist.** Hallo-naam van Hallo storage-account voor Hallo importeren taak.|  
|**/SK:**< StorageAccountKey\>|**Vereist** als een container SAS is niet opgegeven. Hallo-toegangssleutel voor opslagaccount Hallo voor Hallo importeren taak.|  
|**/csas:**< ContainerSas\>|**Vereist** als Hallo opslagaccountsleutel is niet opgegeven. Hallo container SAS voor toegang tot Hallo blobs die zijn gekoppeld aan Hallo import-taak.|  
|**/ CopyLogFile:**< DriveCopyLogFile\>|**Vereist.** Pad toohello station kopiëren logboekbestand (uitgebreid logboek of foutenlogboek). Hallo-bestand wordt gegenereerd door Hallo Windows Azure Import/Export-service en kan worden gedownload vanaf Hallo blob-opslag die is gekoppeld aan het Hallo-taak. Hallo kopie-logboekbestand bevat informatie over mislukte blobs of bestanden die toobe hersteld zijn.|  
|**/ PathMapFile:**< DrivePathMapFile\>|**Optioneel.** Pad tooa tekstbestand die kan worden gebruikt tooresolve dubbelzinnigheden als er meerdere bestanden met dezelfde naam dat u importeert zijn Hallo Hallo dezelfde taak. Hallo eerste tijd Hallo hulpprogramma wordt uitgevoerd, wordt dit bestand met alle niet-eenduidige namen Hallo kunt vullen. Latere uitvoeringen van Hallo-hulpprogramma gebruiken voor dit bestand tooresolve Hallo dubbelzinnigheden.|  
  
## <a name="using-hello-repairimport-command"></a>Hallo opdracht RepairImport  
gegevens van de toorepair importeren door Hallo gegevensstromen via Hallo netwerk, moet u Hallo Hallo mappen met oorspronkelijke Hallo-bestanden zijn u importeren met behulp van `/d` parameter. Hallo kopie-logboekbestand dat u hebt gedownload van uw storage-account, moet u ook opgeven. Een typische opdrachtregel toorepair een import-taak met gedeeltelijke fouten ziet eruit als:  
  
```  
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log  
```  
  
Hallo is volgende voorbeeld van een logbestand kopiëren, gegevenselementen 64 K van een bestand beschadigd op Hallo station dat is verzonden voor Hallo import-taak. Hallo rest Hallo blobs in Hallo taak zijn geïmporteerd, omdat dit alleen Hallo fout die wordt aangegeven.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
 <DriveId>9WM35C2V</DriveId>  
 <Blob Status="CompletedWithErrors">  
 <BlobPath>pictures/animals/koala.jpg</BlobPath>  
 <FilePath>\animals\koala.jpg</FilePath>  
 <Length>163840</Length>  
 <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
 <PageRangeList>  
  <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted" />  
 </PageRangeList>  
 </Blob>  
 <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
Wanneer dit logboek kopie wordt doorgegeven toohello Azure-hulpprogramma voor importeren/exporteren, probeert Hallo hulpprogramma toofinish Hallo importeren voor dit bestand Hallo ontbrekende door inhoud te kopiëren via Hallo-netwerk. Volgende Hallo bovenstaande voorbeeld Hallo hulpprogramma zoekt naar het oorspronkelijke bestand Hallo `\animals\koala.jpg` binnen Hallo twee mappen `C:\Users\bob\Pictures` en `X:\BobBackup\photos`. Als hello bestand `C:\Users\bob\Pictures\animals\koala.jpg` bestaat, Hallo Hallo ontbrekende bereik van Azure-hulpprogramma voor importeren/exporteren kopieën van gegevens toohello bijbehorende blob `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`.  
  
## <a name="resolving-conflicts-when-using-repairimport"></a>Het oplossen van conflicten bij gebruik van RepairImport  
In sommige situaties Hallo hulpprogramma mogen niet worden kunnen toofind of open Hallo vereiste bestand voor een van de volgende redenen Hallo: Hallo-bestand kan niet worden gevonden, Hallo-bestand is niet toegankelijk, Hallo-bestandsnaam is niet eenduidig of Hallo inhoud van het Hallo-bestand zijn niet langer juist.  
  
Een niet-eenduidige fout kan optreden als Hallo hulpprogramma toolocate probeert `\animals\koala.jpg` en er is een bestand met die naam onder beide `C:\Users\bob\pictures` en `X:\BobBackup\photos`. Dat wil zeggen, beide `C:\Users\bob\pictures\animals\koala.jpg` en `X:\BobBackup\photos\animals\koala.jpg` op Hallo import-taak stations bestaan.  
  
Hallo `/PathMapFile` optie kunt u tooresolve deze fouten. U kunt opgeven Hallo-naam van Hallo-bestand, waarin Hallo lijst met bestanden die Hallo hulpprogramma is niet in staat toocorrectly identificeren. Hallo volgende opdrachtregelprogramma voorbeeld gevuld `9WM35C2V_pathmap.txt`:  
  
```
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log /PathMapFile:C:\WAImportExport\9WM35C2V_pathmap.txt  
```
  
Hallo-hulpprogramma wordt Hallo problematisch bestandspaden vervolgens te schrijven`9WM35C2V_pathmap.txt`, één op elke regel. Hallo-bestand bevat bijvoorbeeld Hallo vermeldingen volgen na het Hallo-opdracht uitvoeren:  
 
```
\animals\koala.jpg  
\animals\kangaroo.jpg  
```
  
 U moet voor elk bestand in de lijst Hallo toolocate proberen en Hallo bestand tooensure beschikbaar toohello hulpprogramma is open. Als u wilt tootell Hallo hulpprogramma expliciet waar toofind een bestand, kunt u Hallo pad toewijzen van bestand en Hallo pad tooeach bestand op Hallo toevoegen dezelfde lijn, gescheiden door een tab-teken:  
  
```
\animals\koala.jpg           C:\Users\bob\Pictures\animals\koala.jpg  
\animals\kangaroo.jpg        X:\BobBackup\photos\animals\kangaroo.jpg  
```
  
Na het aanbrengen Hallo benodigde bestanden beschikbaar toohello hulpprogramma of bijwerken toewijzingsbestand van Hallo pad, kunt u Hallo hulpprogramma toocomplete Hallo-importproces opnieuw uitvoeren.  
  
## <a name="next-steps"></a>Volgende stappen
 
* [Hallo-instelling van Azure-hulpprogramma voor importeren/exporteren](storage-import-export-tool-setup-v1.md)   
* [Harde schijven voorbereiden voor een importtaak](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [De taakstatus controleren met kopielogboekbestanden](storage-import-export-tool-reviewing-job-status-v1.md)   
* [Een exporttaak herstellen](../storage-import-export-tool-repairing-an-export-job-v1.md)   
* [Het oplossen van problemen hello Azure-hulpprogramma voor importeren/exporteren](storage-import-export-tool-troubleshooting-v1.md)
