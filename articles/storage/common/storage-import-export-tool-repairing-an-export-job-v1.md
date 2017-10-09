---
title: een exporttaak Azure Import/Export - v1 aaaRepairing | Microsoft Docs
description: Meer informatie over hoe toorepair een exporttaak die is gemaakt en uitgevoerd met behulp van Azure Import/Export Hallo service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 728e2a42-04ce-4be8-9375-e9e2bc6827a5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: e54bc66495c8a3473b8ec51bb254bce8bdc9eab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-export-job"></a>Een exporttaak herstellen
Nadat een taak voor het exporteren is voltooid, kunt u Microsoft Azure-hulpprogramma voor importeren/exporteren on-premises naar Hallo uitvoeren:  
  
1.  Download de bestanden dat hello Azure Import/Export-service kan geen tooexport heeft.  
  
2.  Valideren of Hallo-bestanden op Hallo station correct zijn geëxporteerd.  
  
Deze functionaliteit moet u connectiviteit tooAzure opslag toouse hebben.  
  
Hallo-opdracht voor het herstellen van een import-taak is **RepairExport**.

## <a name="repairexport-parameters"></a>RepairExport parameters

Hallo volgende parameters kunnen worden opgegeven met **RepairExport**:  
  
|Parameter|Beschrijving|  
|---------------|-----------------|  
|**/ r: < RepairFile\>**|Vereist. Pad toohello Herstel dit bestand houdt Hallo voortgang van Hallo herstel en kunt u tooresume reparatie van een onderbroken. Elk station moet slechts één repair-bestand hebben. Wanneer u een reparatie voor een bepaald station start, geeft u in Hallo pad tooa herstel het bestand nog niet bestaat. tooresume reparatie van een onderbroken, moet u doorgeven in Hallo-naam van een bestaand bestand voor herstel. Hallo reparatie bestand corresponderende toohello doelstation moet altijd worden opgegeven.|  
|**schakeloptie/LOGDIR op: < LogDirectory\>**|Optioneel. Hallo logboekmap. Uitgebreide logboekbestanden geschreven toothis directory. Als er geen logboekmap is opgegeven, wordt de huidige map hello worden gebruikt als Hallo logboekmap.|  
|**/ d: < TargetDirectory\>**|Vereist. Hallo directory toovalidate en herstel. Dit is meestal de hoofdmap Hallo van Hallo export station, maar kan ook worden een netwerkbestandsshare die een kopie van bestanden Hallo geëxporteerd.|  
|**/BK: < BitLockerKey\>**|Optioneel. Als u wilt dat Hallo hulpprogramma toounlock versleutelde waar Hallo geëxporteerd bestanden worden opgeslagen, moet u Hallo BitLocker-sleutel opgeven.|  
|**/sn: < StorageAccountName\>**|Vereist. Hallo-naam van Hallo storage-account voor Hallo taak exporteren.|  
|**/SK: < StorageAccountKey\>**|**Vereist** als een container SAS is niet opgegeven. Hallo-toegangssleutel voor opslagaccount Hallo voor Hallo taak exporteren.|  
|**/csas: < ContainerSas\>**|**Vereist** als Hallo opslagaccountsleutel is niet opgegeven. Hallo container SAS voor toegang tot Hallo blobs die zijn gekoppeld aan de exporttaak Hallo.|  
|**/ CopyLogFile: < DriveCopyLogFile\>**|Vereist. Hallo pad toohello station kopiëren logboekbestand. Hallo-bestand wordt gegenereerd door Hallo Windows Azure Import/Export-service en kan worden gedownload vanaf Hallo blob-opslag die is gekoppeld aan het Hallo-taak. Hallo kopie logboekbestand bevat informatie over mislukte blobs of bestanden die toobe hersteld zijn.|  
|**/ ManifestFile: < DriveManifestFile\>**|Optioneel. het manifestbestand Hallo pad toohello exporteren van het station. Dit bestand is gegenereerd door de Windows Azure Import/Export-service Hallo en opgeslagen op Hallo export station en optioneel in een blob in Hallo storage-account aan Hallo taak zijn gekoppeld.<br /><br /> Hallo zal inhoud van het Hallo-bestanden op Hallo export schijf worden gecontroleerd bij Hallo MD5-hashes die zijn opgenomen in dit bestand. Bestanden die bepaald toobe beschadigd zijn zijn gedownload en herschreven toohello doel mappen.|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a>Met behulp van RepairExport mislukt modus toocorrect uitvoer  
U kunt tooexport mislukte hello Azure-hulpprogramma voor importeren/exporteren toodownload bestanden gebruiken. Hallo kopie logboekbestand bevat een lijst met bestanden die niet zijn geslaagd tooexport.  
  
Hallo oorzaken van fouten van de uitvoer zijn Hallo mogelijkheden te volgen:  
  
-   Beschadigde schijven  
  
-   Hallo opslagaccountsleutel gewijzigd tijdens het proces van bestandsoverdracht Hallo  
  
Hallo-hulpprogramma toorun in **RepairExport** modus, moet u eerst tooconnect Hallo station met de Hallo geëxporteerde bestanden tooyour computer. Voer vervolgens hello Azure Import/Export Tool Hallo pad toothat station opgeven met Hallo `/d` parameter. U moet ook toospecify Hallo pad toohello van het station kopiëren logboekbestand dat u hebt gedownload. Hallo opdrachtregel voorbeeld hieronder wordt uitgevoerd Hallo hulpprogramma toorepair bestanden die tooexport is mislukt:  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
Hallo Hieronder volgt een voorbeeld van een logbestand kopiëren waarin wordt gemeld dat een blok in tooexport van Hallo blob is mislukt:  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/desert.jpg</BlobPath>  
    <FilePath>\pictures\wild\desert.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList>  
      <Block Offset="65536" Length="65536" Id="AQAAAA==" Status="Failed" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
Hallo kopie logboekbestand geeft aan dat is een fout opgetreden tijdens het Hallo Windows Azure Import/Export-service is Hallo-blob blokken toohello bestandsshare op Hallo export station downloaden. Hallo van andere onderdelen van Hallo-bestand met succes is gedownload en Hallo bestandslengte is correct ingesteld. Hallo-hulpprogramma wordt in dit geval Hallo-bestand op Hallo schijf openen, Hallo blok downloaden van Hallo storage-account en schrijf deze toohello bestand bereik vanaf verschuiving 65536 met lengte 65536.  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a>Met behulp van RepairExport toovalidate station inhoud  
U kunt ook Azure Import/Export Hello **RepairExport** optie toovalidate Hallo inhoud op Hallo station juist zijn. Hallo-manifestbestand op elk station export bevat MD5s voor Hallo inhoud van Hallo-station.  
  
Hello Azure Import/Export-service kunt ook bestanden opslaan Hallo manifest tooa storage-account tijdens Hallo exporteren. Hallo locatie van de manifestbestanden Hallo beschikbaar is via Hallo [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) bewerking als het Hallo-taak is voltooid. Zie [Import/Export-service Manifest bestandsindeling](storage-import-export-file-format-metadata-and-properties.md) voor meer informatie over het Hallo-indeling van het manifestbestand van een station.  
  
Hallo volgende voorbeeld laat zien hoe toorun Azure-hulpprogramma voor importeren/exporteren Hallo Hello **/ManifestFile** en **/CopyLogFile** parameters:  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
Hallo Hieronder volgt een voorbeeld van een manifestbestand:  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveManifest Version="2011-10-01">  
  <Drive>  
    <DriveId>9WM35C3U</DriveId>  
    <ClientCreator>Windows Azure Import/Export service</ClientCreator>  
    <BlobList>
      <Blob>  
        <BlobPath>pictures/city/redmond.jpg</BlobPath>  
        <FilePath>\pictures\city\redmond.jpg</FilePath>  
        <Length>15360</Length>  
        <PageRangeList>  
          <PageRange Offset="0" Length="3584" Hash="72FC55ED9AFDD40A0C8D5C4193208416" />  
          <PageRange Offset="3584" Length="3584" Hash="68B28A561B73D1DA769D4C24AA427DB8" />  
          <PageRange Offset="7168" Length="512" Hash="F521DF2F50C46BC5F9EA9FB787A23EED" />  
        </PageRangeList>  
        <PropertiesPath Hash="E72A22EA959566066AD89E3B49020C0A">\pictures\city\redmond.jpg.properties</PropertiesPath>  
      </Blob>  
      <Blob>  
        <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
        <FilePath>\pictures\wild\canyon.jpg</FilePath>  
        <Length>10884</Length>  
        <BlockList>  
          <Block Offset="0" Length="2721" Id="AAAAAA==" Hash="263DC9C4B99C2177769C5EBE04787037" />  
          <Block Offset="2721" Length="2721" Id="AQAAAA==" Hash="0C52BAE2CC20EFEC15CC1E3045517AA6" />  
          <Block Offset="5442" Length="2721" Id="AgAAAA==" Hash="73D1CB62CB426230C34C9F57B7148F10" />  
          <Block Offset="8163" Length="2721" Id="AwAAAA==" Hash="11210E665C5F8E7E4F136D053B243E6A" />  
        </BlockList>  
        <PropertiesPath Hash="81D7F81B2C29F10D6E123D386C3A4D5A">\pictures\wild\canyon.jpg.properties</PropertiesPath>  
      </Blob> 
    </BlobList>  
 </Drive>  
</DriveManifest>  
``` 
  
Na het herstelproces bijna afgelopen hello, Hallo Lees elk bestand waarnaar wordt verwezen in het manifestbestand Hallo en hulpprogramma controleren de integriteit van Hallo-bestand met de Hallo MD5-hashes. Voor Hallo manifest hierboven gaat dit via de volgende onderdelen Hallo.  

```  
G:\pictures\city\redmond.jpg, offset 0, length 3584  
  
G:\pictures\city\redmond.jpg, offset 3584, length 3584  
  
G:\pictures\city\redmond.jpg, offset 7168, length 3584  
  
G:\pictures\city\redmond.jpg.properties  
  
G:\pictures\wild\canyon.jpg, offset 0, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 2721, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 5442, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 8163, length 2721  
  
G:\pictures\wild\canyon.jpg.properties  
```

Een onderdeel Hallo verificatie mislukt door Hallo hulpprogramma wordt gedownload en herschreven toohello hetzelfde bestand op Hallo-station.  
  
## <a name="next-steps"></a>Volgende stappen
 
* [Hallo-instelling van Azure-hulpprogramma voor importeren/exporteren](storage-import-export-tool-setup-v1.md)   
* [Harde schijven voorbereiden voor een importtaak](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [De taakstatus controleren met kopielogboekbestanden](storage-import-export-tool-reviewing-job-status-v1.md)   
* [Een importtaak herstellen](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Het oplossen van problemen hello Azure-hulpprogramma voor importeren/exporteren](storage-import-export-tool-troubleshooting-v1.md)
