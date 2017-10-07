---
title: aaaAzure voor importeren/exporteren manifestbestand indeling | Microsoft Docs
description: Meer informatie over het Hallo-indeling van Hallo station manifestbestand die beschrijft Hallo toewijzing tussen blobs in Azure Blob storage en bestanden op een station in een taak importeren of exporteren van Hallo Import/Export-service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f3119e1c-2c25-48ad-8752-a6ed4adadbb0
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: d7e5e1990482916f7ff5f891c97343b52e82b2f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-manifest-file-format"></a>Azure Import/Export-service manifest bestandsindeling
Hallo station manifestbestand beschrijft Hallo toewijzing tussen blobs in Azure Blob storage en bestanden op schijf, bestaande uit een taak worden geïmporteerd of geëxporteerd. Voor een importbewerking Hallo manifestbestand is gemaakt als onderdeel van het voorbereidingsproces Hallo-station en op Hallo schijf zijn opgeslagen voordat Hallo station toohello Azure-Datacenter wordt verzonden. Tijdens een exportbewerking Hallo manifest gemaakt en opgeslagen op schijf Hallo door hello Azure Import/Export-service.  
  
Voor beide importeren en exporteren, Hallo station manifestbestand is opgeslagen op Hallo importeren of exporteren van station; het is niet verzonden toohello service via een API-bewerking.  
  
Hallo-hieronder wordt beschreven Hallo algemene indeling van een manifestbestand station:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveManifest Version="2014-11-01">  
  <Drive>  
    <DriveId>drive-id</DriveId>  
    import-export-credential  
  
    <!-- First Blob List -->  
    <BlobList>  
      <!-- Global properties and metadata that applies tooall blobs -->  
      [<MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>]  
      [<PropertiesPath   
        Hash="md5-hash">global-properties-file-path</PropertiesPath>]  
  
      <!-- First Blob -->  
      <Blob>  
        <BlobPath>blob-path-relative-to-account</BlobPath>  
        <FilePath>file-path-relative-to-transfer-disk</FilePath>  
        [<ClientData>client-data</ClientData>]  
        [<Snapshot>snapshot</Snapshot>]  
        <Length>content-length</Length>  
        [<ImportDisposition>import-disposition</ImportDisposition>]  
        page-range-list-or-block-list          
        [<MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>]  
        [<PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>]  
      </Blob>  
  
      <!-- Second Blob -->  
      <Blob>  
      . . .  
      </Blob>  
    </BlobList>  
  
    <!-- Second Blob List -->  
    <BlobList>  
    . . .  
    </BlobList>  
  </Drive>  
</DriveManifest>  
  
import-export-credential ::=   
  <StorageAccountKey>storage-account-key</StorageAccountKey> | <ContainerSas>container-sas</ContainerSas>  
  
page-range-list-or-block-list ::=   
  page-range-list | block-list  
  
page-range-list ::=   
    <PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
    </PageRangeList>  
  
block-list ::=  
    <BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       Hash="md5-hash"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       Hash="md5-hash"/>]  
    </BlockList>  

```

## <a name="manifest-xml-elements-and-attributes"></a>XML-elementen en kenmerken manifest

Hallo gegevenselementen en kenmerken van Hallo station manifest XML-indeling zijn opgegeven in de volgende tabel Hallo.  
  
|XML-Element|Type|Beschrijving|  
|-----------------|----------|-----------------|  
|`DriveManifest`|Hoofdelement|Hallo-hoofdelement van het manifestbestand Hallo. Alle elementen in Hallo-bestand zijn onder dit element.|  
|`Version`|Kenmerk, tekenreeks|Hallo-versie van het manifestbestand Hallo.|  
|`Drive`|Geneste XML-element|Hallo-manifest voor elk station bevat.|  
|`DriveId`|Tekenreeks|Hallo station unieke id voor Hallo station. Hallo stations-id worden gevonden door het Hallo-station voor het serienummer opvragen. Hallo station serienummer wordt meestal afgedrukt op Hallo buiten ook Hallo-station. Hallo `DriveID` element moet worden weergegeven voordat een `BlobList` -element in het manifestbestand Hallo.|  
|`StorageAccountKey`|Tekenreeks|Vereist is voor de import taken als en alleen als `ContainerSas` is niet opgegeven. Hallo-toegangssleutel voor hello Azure storage-account aan Hallo taak zijn gekoppeld.<br /><br /> Dit element wordt weggelaten uit het Hallo-manifest voor een exportbewerking.|  
|`ContainerSas`|Tekenreeks|Vereist is voor de import taken als en alleen als `StorageAccountKey` is niet opgegeven. Hallo container SAS voor toegang tot Hallo blobs die zijn gekoppeld aan het Hallo-taak. Zie [taak plaatsen](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) voor de indeling. Dit element wordt weggelaten uit het Hallo-manifest voor een exportbewerking.|  
|`ClientCreator`|Tekenreeks|Hiermee geeft u Hallo-client die Hallo XML-bestand gemaakt. Deze waarde niet wordt geïnterpreteerd door Hallo Import/Export-service.|  
|`BlobList`|Geneste XML-element|Bevat een lijst met blobs die deel uitmaken van Hallo importeren of exporteren van de taak. Elke blob in een lijst met blob shares Hallo dezelfde metagegevens en eigenschappen.|  
|`BlobList/MetadataPath`|Tekenreeks|Optioneel. Hiermee geeft u Hallo relatieve pad van een bestand op de schijf Hallo Hallo standaard metagegevens die worden ingesteld op blobs in de lijst met de Hallo blob voor een importbewerking bevat. Deze metagegevens kan eventueel worden genegeerd op basis van de blob met blob.<br /><br /> Dit element wordt weggelaten uit het Hallo-manifest voor een exportbewerking.|  
|`BlobList/MetadataPath/@Hash`|Kenmerk, tekenreeks|Hiermee geeft u Hallo Base16 gecodeerd MD5-hash-waarde voor Hallo metagegevensbestand.|  
|`BlobList/PropertiesPath`|Tekenreeks|Optioneel. Hiermee geeft u Hallo relatieve pad van een bestand op de schijf Hallo Hallo standaardeigenschappen die worden ingesteld op blobs in de lijst met de Hallo blob voor een importbewerking bevat. Deze eigenschappen kunnen eventueel worden genegeerd op basis van de blob met blob.<br /><br /> Dit element wordt weggelaten uit het Hallo-manifest voor een exportbewerking.|  
|`BlobList/PropertiesPath/@Hash`|Kenmerk, tekenreeks|Hiermee geeft u Hallo Base16 gecodeerd MD5-hash-waarde voor Hallo eigenschappenbestand.|  
|`Blob`|Geneste XML-element|Bevat informatie over elke blob in elke blob-lijst.|  
|`Blob/BlobPath`|Tekenreeks|Hallo relatieve URI toohello blob, beginnend met Hallo containernaam. Als hoofdcontainer Hallo blob, moet beginnen met `$root`.|  
|`Blob/FilePath`|Tekenreeks|Hiermee geeft u Hallo relatief pad toohello bestand op Hallo-station. Voor exporttaken, wordt Hallo blobpad gebruikt voor Hallo bestandspad indien mogelijk; *bijvoorbeeld*, `pictures/bob/wild/desert.jpg` te worden geëxporteerd`\pictures\bob\wild\desert.jpg`. Echter, vanwege toohello beperkingen van NTFS-namen, een blob mogelijk tooa geëxporteerde bestand met een pad dat niet op Hallo blobpad lijkt.|  
|`Blob/ClientData`|Tekenreeks|Optioneel. Opmerkingen van de klant Hallo bevat. Deze waarde niet wordt geïnterpreteerd door Hallo Import/Export-service.|  
|`Blob/Snapshot`|Datum/tijd|Optioneel voor exporteren. Hiermee geeft u Hallo momentopname-id voor een momentopname van de geëxporteerde blob.|  
|`Blob/Length`|Geheel getal|Geeft de totale lengte van Hallo blob Hallo in bytes. Hallo waarde mogelijk too200 GB voor een blok-blob en van too1 TB voor een pagina-blob. Deze waarde moet een veelvoud van 512 bytes, voor een pagina-blob.|  
|`Blob/ImportDisposition`|Tekenreeks|Optioneel voor de taken van gegevensimport weggelaten voor exporteren. Hiermee wordt aangegeven hoe Hallo Import/Export-service moet verwerken Hallo-aanvraag voor een import-taak waarbij een blob met de Hallo dezelfde naam al bestaat. Als deze waarde wordt weggelaten uit Hallo importeren manifest, wordt de standaardwaarde Hallo `rename`.<br /><br /> Hallo behoren voor dit element:<br /><br /> -   `no-overwrite`: Als een bestemmings-blob al aanwezig zijn bij Hallo is dezelfde naam Hallo importbewerking slaat dit bestand te importeren.<br />-   `overwrite`: Alle bestaande bestemmings-blob is volledig door Hallo zojuist geïmporteerde bestand overschreven.<br />-   `rename`: de nieuwe blob Hallo wordt geüpload met een gewijzigde naam.<br /><br /> Hallo-naam van regel is als volgt:<br /><br /> -Als Hallo blob-naam niet een punt bevat, een nieuwe naam wordt gegenereerd door toe te voegen `(2)` toohello oorspronkelijke blob-naam; als deze nieuwe naam ook veroorzaakt een met de blobnaam van een bestaande, klikt u vervolgens conflict `(3)` wordt toegevoegd in plaats van `(2)`; enzovoort.<br />-Hallo blob-naam bevat een punt, Hallo gedeelte na het laatste punt Hallo worden beschouwd als Hallo extensienaam. Vergelijkbare toohello hierboven procedure `(2)` wordt ingevoegd vóór laatste punt toogenerate een nieuwe naam Hallo; als de nieuwe naam Hallo wordt nog steeds met de blobnaam van een bestaande conflicteert, Hallo-service probeert vervolgens `(3)`, `(4)`, enzovoort, totdat een niet-conflicterende naam is gevonden.<br /><br /> Enkele voorbeelden:<br /><br /> Hallo blob `BlobNameWithoutDot` worden gewijzigd in:<br /><br /> `BlobNameWithoutDot (2)  // if BlobNameWithoutDot exists`<br /><br /> `BlobNameWithoutDot (3)  // if both BlobNameWithoutDot and BlobNameWithoutDot (2) exist`<br /><br /> Hallo blob `Seattle.jpg` worden gewijzigd in:<br /><br /> `Seattle (2).jpg  // if Seattle.jpg exists`<br /><br /> `Seattle (3).jpg  // if both Seattle.jpg and Seattle (2).jpg exist`|  
|`PageRangeList`|Geneste XML-element|Vereist voor een pagina-blob.<br /><br /> Voor een import geeft bewerking, een lijst met bereiken in bytes van een bestand toobe geïmporteerd. Elk paginabereik is beschreven door een verschuiving en lengte in Hallo-bronbestand die Hallo paginabereik, samen met een MD5-hash van Hallo regio beschrijft. Hallo `Hash` kenmerk van een paginabereik is vereist. Hallo service valideert dat Hallo hash van gegevens in blob Hallo Hallo overeenkomt met Hallo berekend MD5-hash van Hallo paginabereik. Een willekeurig aantal paginabereiken mogelijk gebruikte toodescribe een bestand voor een import, met de totale grootte van de Hallo van too1 TB. Alle bereiken moeten worden gerangschikt op offset en geen overlappingen zijn toegestaan.<br /><br /> Voor een exportbewerking, geeft een set met bereiken in bytes van een blob die zijn geëxporteerd toohello station.<br /><br /> Hallo-paginabereiken kunnen samen alleen onderliggende bereiken van een blob of het bestand omvatten.  Hallo resterende deel van Hallo-bestand niet wordt gedekt door een paginabereik wordt verwacht en de inhoud ervan kan worden gedefinieerd.|  
|`PageRange`|XML-element|Hiermee geeft u een paginabereik.|  
|`PageRange/@Offset`|Kenmerk, geheel getal|Hiermee geeft u op Hallo-offset in hello overdrachtsbestand en Hallo blob waarbij Hallo paginabereik opgegeven begint. Deze waarde moet een veelvoud van 512 bytes zijn.|  
|`PageRange/@Length`|Kenmerk, geheel getal|Hiermee geeft u Hallo Hallo paginabereik. Deze waarde moet een veelvoud van 512 en niet meer dan 4 MB.|  
|`PageRange/@Hash`|Kenmerk, tekenreeks|Hiermee geeft u Hallo Base16 gecodeerd MD5-hash-waarde voor Hallo paginabereik.|  
|`BlockList`|Geneste XML-element|Vereist voor een blok-blob met benoemde blokken.<br /><br /> Een importbewerking Hallo blokkeringslijst Hiermee geeft u een reeks blokken die worden geïmporteerd in Azure Storage. Voor een exportbewerking geeft Hallo blokkeringslijst aan waar elk blok in Hallo-bestand op Hallo export schijf zijn opgeslagen. Elk blok is beschreven door een offset in Hallo bestands- en de bloklengte van een. elk blok is bovendien met de naam door een blok-ID-kenmerk en een MD5-hash voor Hallo blok bevat. Up too50 mogelijk 000 blokken gebruikte toodescribe een blob.  Alle blokken moeten worden geordend door de verschuiving en samen moeten voldoende zijn voor volledige reeks Hallo-bestand, Hallo *dat wil zeggen*, moet er geen tussenruimte tussen blokken. Als het Hallo-blob is niet meer dan 64 MB, Hallo blok-id's voor elk blok moet alle ontbreekt of al aanwezig. Blok-id's zijn vereist toobe Base64-gecodeerde tekenreeksen. Zie [plaatsen blok](/rest/api/storageservices/put-block) voor verdere vereisten voor blok-id's.|  
|`Block`|XML-element|Hiermee geeft u een blok.|  
|`Block/@Offset`|Kenmerk, geheel getal|Geeft Hallo verschuiving waar Hallo opgegeven blok begint.|  
|`Block/@Length`|Kenmerk, geheel getal|Hiermee geeft u Hallo aantal bytes in Hallo blok; Deze waarde moet niet meer dan 4MB.|  
|`Block/@Id`|Kenmerk, tekenreeks|Hiermee geeft u een tekenreeks voor Hallo blok-ID voor Hallo blok.|  
|`Block/@Hash`|Kenmerk, tekenreeks|Hiermee geeft u Hallo Base16 gecodeerd MD5-hash van Hallo blok.|  
|`Blob/MetadataPath`|Tekenreeks|Optioneel. Hiermee geeft u Hallo relatieve pad van een bestand met metagegevens. Hallo metagegevens is tijdens het importeren ingesteld op Hallo bestemmings-blob. Hallo blobmetagegevens wordt tijdens een exportbewerking opgeslagen in Hallo metagegevensbestand op Hallo-station.|  
|`Blob/MetadataPath/@Hash`|Kenmerk, tekenreeks|Hiermee geeft u Hallo Base16 gecodeerd MD5-hash van het metagegevensbestand Hallo-blob.|  
|`Blob/PropertiesPath`|Tekenreeks|Optioneel. Hiermee geeft u Hallo relatieve pad van een eigenschappenbestand. Tijdens het importeren, Hallo eigenschappen ingesteld op Hallo bestemmings-blob. Tijdens een exportbewerking worden Hallo blob eigenschappen opgeslagen in Hallo eigenschappenbestand op Hallo-station.|  
|`Blob/PropertiesPath/@Hash`|Kenmerk, tekenreeks|Hiermee geeft u Hallo Base16 gecodeerd MD5-hash van bestand Hallo-blob-eigenschappen.|  
  
## <a name="next-steps"></a>Volgende stappen
 
* [REST-API van Storage Import/Export](/rest/api/storageimportexport/)
