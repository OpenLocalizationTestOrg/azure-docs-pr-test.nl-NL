---
title: indeling van logboekbestand aaaAzure voor importeren/exporteren | Microsoft Docs
description: Meer informatie over het Hallo-indeling van logboekbestanden Hallo gemaakt wanneer de stappen worden uitgevoerd voor een taak van Import/Export-service.
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
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a>Azure Import/Export-service indeling van logboekbestand
Wanneer een actie op een station Hallo Microsoft Azure Import/Export-service als onderdeel van een import-taak of een taak voor het exporteren uitvoert, worden logboeken tooblock blobs geschreven in Hallo storage-account dat is gekoppeld met deze taak.  
  
Er zijn twee logboekbestanden die kunnen worden geschreven door Hallo Import/Export-service:  
  
-   Hallo-foutenlogboek is altijd Hallo geval van een fout gegenereerd.  
  
-   Hallo uitgebreide logboek is standaard niet ingeschakeld, maar kan worden ingeschakeld door de instelling Hallo `EnableVerboseLog` -eigenschap op een [taak plaatsen](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) of [Update taakeigenschappen](/rest/api/storageimportexport/jobs#Jobs_Update) bewerking.  
  
## <a name="log-file-location"></a>De locatie van logboekbestand  
Hallo Logboeken geschreven tooblock blobs in Hallo-container of virtuele map die is opgegeven door Hallo `ImportExportStatesPath` instelling, die u kunt instellen op een `Put Job` bewerking. Hallo locatie toowhich Hallo Logboeken geschreven is afhankelijk van hoe verificatie is opgegeven voor de taak hello, samen met de Hallo-waarde opgegeven voor `ImportExportStatesPath`. Verificatie voor Hallo taak mag worden opgegeven via de sleutel van een opslagaccount of een container SAS (shared access signature).  
  
Hallo-naam van het Hallo-container of virtuele map kan ofwel worden de standaardnaam Hallo van `waimportexport`, of een andere container of de naam van de virtuele map die u opgeeft.  
  
Hallo in de volgende tabel ziet u Hallo mogelijke opties:  
  
|Verificatiemethode|Waarde van `ImportExportStatesPath`Element|Locatie van het logboek Blobs|  
|---------------------------|----------------------------------------------|---------------------------|  
|De sleutel van opslagaccount|Standaardwaarde|Een container met de naam `waimportexport`, die de standaardcontainer Hallo is. Bijvoorbeeld:<br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|De sleutel van opslagaccount|Gebruiker opgegeven waarde|Een container met de naam door Hallo-gebruiker. Bijvoorbeeld:<br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|Container SAS|Standaardwaarde|Een virtuele map met de naam `waimportexport`, dit is de standaardnaam Hallo onder Hallo-container die zijn opgegeven in Hallo SAS.<br /><br /> Bijvoorbeeld, als Hallo SAS voor het opgegeven Hallo-taak is `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, en vervolgens de locatie van het logboekbestand Hallo zou zijn`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`|  
|Container SAS|Gebruiker opgegeven waarde|Een virtuele map met de naam van de gebruiker hello, onder Hallo-container die zijn opgegeven in Hallo SAS.<br /><br /> Bijvoorbeeld, als Hallo SAS voor het opgegeven Hallo-taak is `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, en Hallo opgegeven virtuele map heet `mylogblobs`, en vervolgens de locatie van het logboekbestand Hallo zou worden `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.|  
  
U kunt aanroepen Hallo Hallo-URL voor Hallo foutinformatie en de uitgebreide logboeken ophalen [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) bewerking. Hallo logboeken zijn beschikbaar nadat de verwerking van Hallo station is voltooid.  
  
## <a name="log-file-format"></a>Indeling van logboekbestand  
Hallo-indeling voor beide logboeken is Hallo dezelfde: een blob met beschrijvingen van Hallo-gebeurtenissen die zijn opgetreden tijdens het kopiëren van BLOB's tussen Hallo harde schijf en Hallo klantaccount XML.  
  
Hallo uitgebreide logboek bevat volledige informatie over Hallo status van de kopieerbewerking Hallo voor elke blob (voor een import-taak) of het bestand (voor een exporttaak) terwijl Hallo foutenlogboek bevat alleen informatie Hallo voor blobs of bestanden die fouten tijdens het Hallo aangetroffen importeren of exporteren van de taak.  
  
Hallo uitgebreide logboekindeling worden hieronder weergegeven. Hallo-foutenlogboek heeft Hallo dezelfde structuur, maar geslaagde bewerkingen, worden uitgefilterd.  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

Hallo beschrijft volgende tabel Hallo elementen van het logboekbestand Hallo.  
  
|XML-Element|Type|Beschrijving|  
|-----------------|----------|-----------------|  
|`DriveLog`|XML-Element|Hiermee geeft u een station voor logboekbestanden.|  
|`Version`|Kenmerk, tekenreeks|Hallo-versie van Hallo-logboekindeling.|  
|`DriveId`|Tekenreeks|Hallo serienummer van het station-hardware.|  
|`Status`|Tekenreeks|Status van Hallo station verwerking. Zie Hallo `Drive Status Codes` tabel hieronder voor meer informatie.|  
|`Blob`|Geneste XML-element|Hiermee geeft u een blob.|  
|`Blob/BlobPath`|Tekenreeks|Hallo-URI van Hallo blob.|  
|`Blob/FilePath`|Tekenreeks|Hallo relatief pad toohello bestand op Hallo-station.|  
|`Blob/Snapshot`|Datum/tijd|Hallo momentopname versie van de blob hello, voor een exporttaak.|  
|`Blob/Length`|Geheel getal|Hallo totale lengte van de blob Hallo in bytes.|  
|`Blob/LastModified`|Datum/tijd|Hallo datum/tijd Hallo blob voor een exporttaak het laatst is gewijzigd.|  
|`Blob/ImportDisposition`|Tekenreeks|Hallo disposition Hallo BLOB, voor een import-taak alleen importeren.|  
|`Blob/ImportDisposition/@Status`|Kenmerk, tekenreeks|Hallo-status van Hallo importeren toestand.|  
|`PageRangeList`|Geneste XML-element|Hiermee geeft u een lijst met paginabereiken voor een pagina-blob.|  
|`PageRange`|XML-element|Hiermee geeft u een paginabereik.|  
|`PageRange/@Offset`|Kenmerk, geheel getal|Hallo blob vanaf verschuiving van Hallo paginabereik.|  
|`PageRange/@Length`|Kenmerk, geheel getal|De lengte in bytes van Hallo paginabereik.|  
|`PageRange/@Hash`|Kenmerk, tekenreeks|Base16 gecodeerd MD5-hash van Hallo paginabereik.|  
|`PageRange/@Status`|Kenmerk, tekenreeks|Status van de verwerking van Hallo paginabereik.|  
|`BlockList`|Geneste XML-element|Hiermee geeft u een lijst met bouwstenen voor een blok-blob.|  
|`Block`|XML-element|Hiermee geeft u een blok.|  
|`Block/@Offset`|Kenmerk, geheel getal|Vanaf verschuiving van Hallo blok Hallo blob.|  
|`Block/@Length`|Kenmerk, geheel getal|De lengte in bytes van Hallo blok.|  
|`Block/@Id`|Kenmerk, tekenreeks|Hallo-blok-id.|  
|`Block/@Hash`|Kenmerk, tekenreeks|Base16 gecodeerd MD5-hash van Hallo blok.|  
|`Block/@Status`|Kenmerk, tekenreeks|Status van de verwerking van Hallo blok.|  
|`Metadata`|Geneste XML-element|Hallo blobmetagegevens vertegenwoordigt.|  
|`Metadata/@Status`|Kenmerk, tekenreeks|Status van de verwerking van Hallo blobmetagegevens.|  
|`Metadata/GlobalPath`|Tekenreeks|Relatief pad toohello globale metagegevensbestand.|  
|`Metadata/GlobalPath/@Hash`|Kenmerk, tekenreeks|Base16 gecodeerd MD5-hash van de globale metagegevensbestand Hallo.|  
|`Metadata/Path`|Tekenreeks|Relatief pad toohello metagegevensbestand.|  
|`Metadata/Path/@Hash`|Kenmerk, tekenreeks|Base16 gecodeerd MD5-hash van het metagegevensbestand Hallo.|  
|`Properties`|Geneste XML-element|Hallo blob eigenschappen vertegenwoordigt.|  
|`Properties/@Status`|Kenmerk, tekenreeks|Status van de verwerking van Hallo blob-eigenschappen, bijvoorbeeld bestand niet gevonden, voltooid.|  
|`Properties/GlobalPath`|Tekenreeks|Relatief pad toohello algemene eigenschappenbestand.|  
|`Properties/GlobalPath/@Hash`|Kenmerk, tekenreeks|Base16 gecodeerd MD5-hash van Hallo algemene eigenschappenbestand.|  
|`Properties/Path`|Tekenreeks|Relatief pad toohello eigenschappenbestand.|  
|`Properties/Path/@Hash`|Kenmerk, tekenreeks|Base16 gecodeerd MD5-hash van Hallo eigenschappenbestand.|  
|`Blob/Status`|Tekenreeks|De status van de verwerking van Hallo blob.|  
  
# <a name="drive-status-codes"></a>Statuscodes van station  
Hallo bevat volgende tabel de statuscodes Hallo voor het verwerken van een station.  
  
|Statuscode|Beschrijving|  
|-----------------|-----------------|  
|`Completed`|Hallo-station heeft verwerking zonder fouten voltooid.|  
|`CompletedWithWarnings`|Hallo-station zijn verwerkt met waarschuwingen in een of meer blobs per Hallo importeren dispositions opgegeven voor Hallo blobs.|  
|`CompletedWithErrors`|Hallo-station is voltooid met fouten in een of meer blobs of segmenten.|  
|`DiskNotFound`|Er is geen schijf is gevonden op Hallo-station.|  
|`VolumeNotNtfs`|Hallo eerste gegevensvolume op Hallo schijf is niet in de NTFS-indeling.|  
|`DiskOperationFailed`|Een onbekende fout opgetreden bij het uitvoeren van bewerkingen op Hallo station.|  
|`BitLockerVolumeNotFound`|Er is geen BitLocker encryptable volume gevonden.|  
|`BitLockerNotActivated`|BitLocker is niet ingeschakeld op Hallo volume.|  
|`BitLockerProtectorNotFound`|Hallo numerieke wachtwoordsleutelbeveiliging bestaat niet op Hallo volume.|  
|`BitLockerKeyInvalid`|Hallo numerieke opgegeven wachtwoord ontgrendelen niet Hallo volume.|  
|`BitLockerUnlockVolumeFailed`|Is een onbekende fout opgetreden bij het toounlock Hallo volume.|  
|`BitLockerFailed`|Een onbekende fout opgetreden tijdens het uitvoeren van BitLocker-bewerkingen.|  
|`ManifestNameInvalid`|Hallo manifestbestand naam is ongeldig.|  
|`ManifestNameTooLong`|Hallo manifestbestand naam is te lang.|  
|`ManifestNotFound`|Hallo-manifestbestand is niet gevonden.|  
|`ManifestAccessDenied`|Manifestbestand van de toohello toegang is geweigerd.|  
|`ManifestCorrupted`|Hallo manifestbestand is beschadigd (Hallo inhoud komt niet overeen met de hash).|  
|`ManifestFormatInvalid`|Hallo manifest inhoud komt niet overeen voor vereiste toohello-indeling.|  
|`ManifestDriveIdMismatch`|Hallo-ID in het manifestbestand Hallo komt niet overeen met een van Hallo station lezen Hallo station.|  
|`ReadManifestFailed`|Er is een schijf-i/o-fout opgetreden tijdens het lezen van Hallo manifest.|  
|`BlobListFormatInvalid`|Hallo export blob lijst blob komt niet overeen voor vereiste toohello-indeling.|  
|`BlobRequestForbidden`|Toegang tot toohello blobs in Hallo storage-account is niet toegestaan. Dit kan zijn vanwege de opslagaccountsleutel tooinvalid of SAS-container.|  
|`InternalError`|En er is een interne fout opgetreden tijdens het verwerken van Hallo-station.|  
  
## <a name="blob-status-codes"></a>Statuscodes BLOB  
Hallo bevat volgende tabel de statuscodes Hallo voor het verwerken van een blob.  
  
|Statuscode|Beschrijving|  
|-----------------|-----------------|  
|`Completed`|Hallo blob heeft verwerking zonder fouten voltooid.|  
|`CompletedWithErrors`|Hallo blob zijn met fouten in een of meer paginabereiken of blokken, metagegevens of eigenschappen verwerkt.|  
|`FileNameInvalid`|Hallo-bestandsnaam is ongeldig.|  
|`FileNameTooLong`|Hallo-bestandsnaam is te lang.|  
|`FileNotFound`|Hallo-bestand is niet gevonden.|  
|`FileAccessDenied`|Toegang tot toohello bestand is geweigerd.|  
|`BlobRequestFailed`|Hallo Blob-serviceaanvraag tooaccess Hallo blob is mislukt.|  
|`BlobRequestForbidden`|Hallo Blob-serviceaanvraag tooaccess Hallo blob is verboden. Dit kan zijn vanwege de opslagaccountsleutel tooinvalid of SAS-container.|  
|`RenameFailed`|Kan toorename Hallo-blob (voor een import-taak) of Hallo-bestand (voor een taak voor het exporteren).|  
|`BlobUnexpectedChange`|Onverwachte wijziging is opgetreden met de blob hello (voor een taak voor het exporteren).|  
|`LeasePresent`|Er is een lease aanwezig is op Hallo blob.|  
|`IOFailed`|Een schijf of een netwerk-i/o-fout is opgetreden tijdens het verwerken van Hallo blob.|  
|`Failed`|Een onbekende fout opgetreden tijdens het verwerken van Hallo blob.|  
  
## <a name="import-disposition-status-codes"></a>Statuscodes disposition importeren  
Hallo bevat volgende tabel Hallo statuscodes voor het oplossen van een toestand importeren.  
  
|Statuscode|Beschrijving|  
|-----------------|-----------------|  
|`Created`|Hallo-blob is gemaakt.|  
|`Renamed`|Hallo blob heeft per rename importeren bestemming gekregen. Hallo `Blob/BlobPath` element Hallo URI voor Hallo hernoemd blob bevat.|  
|`Skipped`|Hallo-blob is overgeslagen `no-overwrite` toestand importeren.|  
|`Overwritten`|Hallo blob heeft een bestaande blob per overschreven `overwrite` toestand importeren.|  
|`Cancelled`|Een eerdere fout is gestopt verdere verwerking van Hallo importeren toestand.|  
  
## <a name="page-rangeblock-status-codes"></a>Statuscodes voor pagina-bereik/blok  
Hallo bevat volgende tabel de statuscodes Hallo voor het verwerken van een paginabereik of een blok.  
  
|Statuscode|Beschrijving|  
|-----------------|-----------------|  
|`Completed`|Hallo paginabereik of blok is verwerking zonder fouten voltooid.|  
|`Committed`|Hallo blok is doorgevoerd, maar niet in Hallo volledige blokkeringslijst omdat andere blokken is mislukt, of de volledige lijst met geblokkeerde websites zelf plaatsen is mislukt.|  
|`Uncommitted`|Hallo blok is geüpload, maar niet zijn doorgevoerd.|  
|`Corrupted`|Hallo paginabereik of blok is beschadigd (Hallo inhoud komt niet overeen met de hash).|  
|`FileUnexpectedEnd`|Een onverwacht bestandseinde er is opgetreden.|  
|`BlobUnexpectedEnd`|Een onverwacht einde van de blob is opgetreden.|  
|`BlobRequestFailed`|Hallo Blob serviceaanvraag tooaccess Hallo paginabereik of blok is mislukt.|  
|`IOFailed`|Een schijf of een netwerk-i/o-fout is opgetreden tijdens het verwerken van Hallo paginabereik of blok.|  
|`Failed`|Een onbekende fout opgetreden tijdens het verwerken van Hallo paginabereik of blok.|  
|`Cancelled`|Er is een eerdere fout gestopt verdere verwerking van het Hallo paginabereik of blok.|  
  
## <a name="metadata-status-codes"></a>Statuscodes van metagegevens  
Hallo bevat volgende tabel Hallo statuscodes voor verwerking van blob-metagegevens.  
  
|Statuscode|Beschrijving|  
|-----------------|-----------------|  
|`Completed`|Hallo-metagegevens heeft verwerking zonder fouten voltooid.|  
|`FileNameInvalid`|Hallo metagegevens bestandsnaam is ongeldig.|  
|`FileNameTooLong`|Hallo metagegevens bestandsnaam is te lang.|  
|`FileNotFound`|Hallo-metagegevensbestand is niet gevonden.|  
|`FileAccessDenied`|Bestand met metagegevens toohello toegang is geweigerd.|  
|`Corrupted`|Hallo metagegevensbestand is beschadigd (Hallo inhoud komt niet overeen met de hash).|  
|`XmlReadFailed`|Hallo metagegevens inhoud komt niet overeen voor vereiste toohello-indeling.|  
|`XmlWriteFailed`|Schrijven van Hallo metagegevens die is mislukt.|  
|`BlobRequestFailed`|Hallo Blob-serviceaanvraag tooaccess Hallo metagegevens is mislukt.|  
|`IOFailed`|Een schijf of het netwerk-i/o-fout opgetreden tijdens het verwerken van Hallo metagegevens.|  
|`Failed`|Een onbekende fout opgetreden tijdens het verwerken van Hallo metagegevens.|  
|`Cancelled`|Een eerdere fout is gestopt verdere verwerking van Hallo metagegevens.|  
  
## <a name="properties-status-codes"></a>Statuscodes van eigenschappen  
Hallo bevat volgende tabel de statuscodes Hallo voor het verwerken van blob-eigenschappen.  
  
|Statuscode|Beschrijving|  
|-----------------|-----------------|  
|`Completed`|Hallo eigenschappen verwerken zonder fouten is voltooid.|  
|`FileNameInvalid`|Hallo eigenschappen bestandsnaam is ongeldig.|  
|`FileNameTooLong`|Hallo eigenschappen bestandsnaam is te lang.|  
|`FileNotFound`|Hallo eigenschappenbestand is niet gevonden.|  
|`FileAccessDenied`|Toegang tot toohello eigenschappenbestand is geweigerd.|  
|`Corrupted`|Hallo eigenschappenbestand is beschadigd (Hallo inhoud komt niet overeen met de hash).|  
|`XmlReadFailed`|Hallo eigenschappen inhoud komt niet overeen voor vereiste toohello-indeling.|  
|`XmlWriteFailed`|Schrijven van Hallo-eigenschappen die is mislukt.|  
|`BlobRequestFailed`|Hallo Blob-serviceaanvraag tooaccess Hallo eigenschappen is mislukt.|  
|`IOFailed`|Een schijf of het netwerk-i/o-fout opgetreden tijdens het verwerken van Hallo-eigenschappen.|  
|`Failed`|Een onbekende fout opgetreden tijdens het verwerken van Hallo-eigenschappen.|  
|`Cancelled`|Een eerdere fout is gestopt verdere verwerking van Hallo-eigenschappen.|  
  
## <a name="sample-logs"></a>Voorbeeld-Logboeken  
Hallo Hieronder volgt een voorbeeld van uitgebreide logboek.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
de bijbehorende foutenlogboek Hallo worden hieronder weergegeven.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 Hallo Volg-foutenlogboek voor een import-taak bevat een fout over een bestand niet gevonden op Hallo importeren station. Houd er rekening mee dat Hallo status van de volgende onderdelen is `Cancelled`.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

Hallo volgende foutenlogboek voor een taak voor het exporteren geeft aan dat de blob-inhoud Hallo is geschreven toohello station, maar is een fout opgetreden tijdens het exporteren van de eigenschappen van het Hallo-blob.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a>Volgende stappen
 
* [REST-API van Storage Import/Export](/rest/api/storageimportexport/)
