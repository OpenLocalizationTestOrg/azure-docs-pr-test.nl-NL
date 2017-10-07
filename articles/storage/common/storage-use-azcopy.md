---
title: aaaCopy of verplaats gegevens tooAzure opslag met AzCopy in Windows | Microsoft Docs
description: "Hallo AzCopy gebruiken op Windows-hulpprogramma toomove of een kopie van gegevens tooor van blob, table en de inhoud van bestand. Kopiëren van gegevens tooAzure opslag van lokale bestanden of kopiëren van gegevens binnen of tussen opslagaccounts. Eenvoudig uw gegevens tooAzure opslag migreren."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: aa155738-7c69-4a83-94f8-b97af4461274
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/14/2017
ms.author: seguler
ms.openlocfilehash: a063a0380b7b8e6b212d0cec276f7d0f421936ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-azcopy-on-windows"></a>Gegevensoverdracht met Hallo AzCopy in Windows
AzCopy is een opdrachtregelprogramma dat is ontworpen voor het kopiëren van gegevens tooand van Microsoft Azure Blob-, bestands- en tabel opslag met behulp van eenvoudige opdrachten met optimale prestaties. U kunt gegevens kopiëren van een object tooanother binnen uw opslagaccount of tussen opslagaccounts.

Er zijn twee versies van AzCopy die u kunt downloaden. AzCopy in Windows is gebouwd met .NET Framework en Windows-stijl biedt opdrachtregelopties. [AzCopy op Linux](storage-use-azcopy-linux.md) is gebouwd met .NET Core Framework die gericht is op Linux-platforms biedt POSIX-stijl opdrachtregelopties. In dit artikel bevat informatie over AzCopy in Windows.

## <a name="download-and-install-azcopy"></a>Downloaden en installeren van AzCopy
### <a name="azcopy-on-windows"></a>AzCopy in Windows
Hallo downloaden [meest recente versie van AzCopy op Windows](http://aka.ms/downloadazcopy).

#### <a name="installation-on-windows"></a>Installatie op Windows
Na de installatie van AzCopy op Windows installer hello gebruiken, open een opdrachtvenster en navigeer toohello AzCopy-installatiemap op uw computer - waar hello `AzCopy.exe` uitvoerbare bestand zich bevindt. Indien gewenst, kunt u Hallo AzCopy locatie tooyour system installatiepad kunt toevoegen. AzCopy is standaard te`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` of `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.

## <a name="writing-your-first-azcopy-command"></a>Schrijven van uw eerste AzCopy-opdracht
Hallo basic syntaxis voor opdrachten van AzCopy is:

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

Hallo volgen voorbeelden laten zien dat verschillende scenario's voor het kopiëren van gegevens tooand van Microsoft Azure Blobs, bestanden en tabellen. Raadpleeg toohello [AzCopy Parameters](#azcopy-parameters) sectie voor een gedetailleerde beschrijving van het Hallo-parameters die worden gebruikt in elk voorbeeld.

## <a name="blob-download"></a>BLOB: downloaden
### <a name="download-single-blob"></a>Enkele blobs downloaden

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

Houd er rekening mee dat als Hallo map `C:\myfolder` niet bestaat, AzCopy maakt het en downloaden `abc.txt ` in Hallo nieuwe map.

### <a name="download-single-blob-from-secondary-region"></a>Downloaden van één blob van de secundaire regio

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Houd er rekening mee dat u geografisch redundante opslag met leestoegang ingeschakeld nodig hebt.

### <a name="download-all-blobs"></a>Alle blobs downloaden

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

Wordt ervan uitgegaan dat de volgende Hallo BLOB's zich bevinden in de opgegeven container Hallo:  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

Na de bewerking van de download hello, Hallo directory `C:\myfolder` omvat Hallo volgende bestanden:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

Als u geen optie opgeeft `/S`, geen blobs worden gedownload.

### <a name="download-blobs-with-specified-prefix"></a>Blobs met het opgegeven voorvoegsel downloaden

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

Wordt ervan uitgegaan dat de volgende Hallo BLOB's zich bevinden in de opgegeven container Hallo. Alle blobs vanaf Hallo voorvoegsel `a` worden gedownload:

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

Na de bewerking van de download hello, Hallo map `C:\myfolder` bevat Hallo volgende bestanden:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

Hallo-voorvoegsel is van toepassing toohello virtuele map, die Hallo eerste deel van Hallo blob-naam uitmaakt. In het bovenstaande voorbeeld hello, Hallo virtuele map komt niet overeen met het opgegeven voorvoegsel hello, zodat deze niet is gedownload. Bovendien, als hello optie `\S` niet is opgegeven, AzCopy biedt niet alle blobs downloaden.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>Hallo tijd laatste wijziging van de geëxporteerde bestanden toobe instellen hetzelfde als de bron blobs Hallo

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

U kunt ook BLOB's uitsluiten van Hallo downloaden van de bewerking op basis van hun tijd voor het laatst is gewijzigd. Bijvoorbeeld, als u tooexclude blobs waarvan laatst gewijzigd-tijd Hallo dezelfde of een nieuwer is dan het doelbestand hello wilt is, toevoegen Hallo `/XN` optie:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

Of als u tooexclude blobs waarvan laatst gewijzigd-tijd Hallo dezelfde of een ouder is dan het doelbestand hello wilt is, toe te voegen Hallo `/XO` optie:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a>BLOB: uploaden
### <a name="upload-single-file"></a>Bestand uploaden

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

Als Hallo opgegeven bestemmingscontainer niet bestaat, AzCopy wordt deze gemaakt en uploads Hallo bestand in de App.

### <a name="upload-single-file-toovirtual-directory"></a>Enkel bestand toovirtual directory uploaden

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

Als Hallo virtuele map bestaat niet opgegeven, AzCopy uploadt Hallo bestand tooinclude Hallo virtuele map in de naam (*bijvoorbeeld*, `vd/abc.txt` in bovenstaande Hallo voorbeeld).

### <a name="upload-all-files"></a>Alle bestanden uploaden

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

Optie `/S` uploads Hallo inhoud Hallo opgegeven directory tooBlob opslag recursief, wat betekent dat alle submappen en de bestanden ook worden geüpload. Voor het exemplaar wordt ervan uitgegaan dat de volgende Hallo bestanden bevinden zich in map `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Na het Hallo-uploadbewerking bevat Hallo container Hallo volgende bestanden:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Als u geen optie opgeeft `/S`, AzCopy biedt recursief niet uploaden. Na het Hallo-uploadbewerking bevat Hallo container Hallo volgende bestanden:

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a>Uploaden van bestanden die overeenkomen met opgegeven patroon

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

Wordt ervan uitgegaan dat de volgende Hallo bestanden bevinden zich in map `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Na het Hallo-uploadbewerking bevat Hallo container Hallo volgende bestanden:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Als u geen optie opgeeft `/S`, AzCopy uploadt alleen blobs die zich niet in een virtuele map bevinden:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>Geef Hallo MIME-inhoudstype van een bestemmings-blob
Standaard stelt AzCopy Hallo-inhoudstype van een bestemmings-blob te`application/octet-stream`. Vanaf versie 3.1.0, kunt u expliciet opgeven Hallo inhoudstype via Hallo-optie `/SetContentType:[content-type]`. Deze syntaxis wordt Hallo inhoudstype voor alle blobs in een uploadbewerking.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

Als u opgeeft `/SetContentType` zonder een waarde ingesteld AzCopy elke blob of inhoudstype van het bestand volgens tooits bestandsextensie.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a>BLOB: kopiëren
### <a name="copy-single-blob-within-storage-account"></a>Één blob binnen opslagaccount kopiëren

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

Wanneer u een blob binnen een opslagaccount kopieert een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.

### <a name="copy-single-blob-across-storage-accounts"></a>Één blob kopiëren tussen opslagaccounts

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

Wanneer u een blob tussen opslagaccounts kopieert, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>Één blob kopiëren van de secundaire regio tooprimary regio

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

Houd er rekening mee dat u geografisch redundante opslag met leestoegang ingeschakeld nodig hebt.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>Één blob en bijbehorende momentopnamen kopiëren tussen opslagaccounts

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

Na de kopieerbewerking hello omvat doelcontainer Hallo Hallo blob en het bijbehorende momentopnamen. Ervan uitgaande dat Hallo blob in bovenstaande Hallo voorbeeld heeft twee momentopnamen, Hallo container bevat Hallo volgende blob en momentopnamen:

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>Synchroon kopiëren van BLOB's tussen opslagaccounts
AzCopy standaard worden de gegevens tussen de twee eindpunten voor opslag asynchroon gekopieerd. Daarom Hallo kopie-bewerking wordt uitgevoerd op Hallo achtergrond met behulp van ongebruikte bandbreedtecapaciteit die geen SLA in termen van hoe snel een blob heeft wordt gekopieerd en AzCopy controleert periodiek Hallo kopiestatus totdat Hallo kopiëren is voltooid of mislukt.

Hallo `/SyncCopy` optie zorgt ervoor dat de kopieerbewerking Hallo consistente snelheid opgehaald. AzCopy voert synchrone kopie Hallo Hallo blobs downloaden toocopy van Hallo opgegeven bron toolocal geheugen en uploadt deze toohello Blob-opslaglocatie.

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

`/SyncCopy`Als u meer uitgaande kosten vergeleken tooasynchronous kopiëren, hello mogelijk gegenereerd aanbevolen benadering toouse is deze optie in een Azure VM in Hallo dezelfde regio bevinden als uw gegevensbron account tooavoid uitgaande opslagkosten.

## <a name="file-download"></a>Bestand: downloaden
### <a name="download-single-file"></a>Enkel bestand downloaden

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Als Hallo bron is een Azure-bestandsshare opgegeven, moet u de exacte bestandsnaam hello, opgeven (*bijvoorbeeld* `abc.txt`) toodownload één bestand of de optie `/S` toodownload alle bestanden in de share Hallo recursief. Toospecify poging een patroon en de optie `/S` samen resulteert in een fout opgetreden.

### <a name="download-all-files"></a>Alle bestanden downloaden

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

Alle lege mappen zijn niet gedownload.

## <a name="file-upload"></a>Bestand: uploaden
### <a name="upload-single-file"></a>Bestand uploaden

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a>Alle bestanden uploaden

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

Houd er rekening mee dat alle lege mappen niet worden geüpload.

### <a name="upload-files-matching-specified-pattern"></a>Uploaden van bestanden die overeenkomen met opgegeven patroon

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a>Bestand: kopiëren
### <a name="copy-across-file-shares"></a>Kopiëren via bestandsshares

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
Wanneer u een bestand via bestandsshares kopiëren, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.

### <a name="copy-from-file-share-tooblob"></a>Kopiëren van bestandsshare tooblob

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
Wanneer u een bestand vanuit bestandsshare tooblob kopiëren, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.


### <a name="copy-from-blob-toofile-share"></a>Kopiëren van blob toofile share

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
Wanneer u een bestand van blob toofile share kopiëren, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.

### <a name="synchronously-copy-files"></a>Synchroon bestanden kopiëren
U kunt opgeven dat Hallo `/SyncCopy` optie toocopy gegevens van File Storage tooFile opslag van File Storage tooBlob opslag en van Blob Storage tooFile opslag synchroon, AzCopy doet dit door Hallo bron gegevens toolocal geheugen downloaden en te uploaden opnieuw toodestination. Standaard uitgaande kosten worden toegepast.

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

Bij het kopiëren van File Storage tooBlob opslag, Hallo standaard blob-type blok-blob is, optie kunt u opgeven `/BlobType:page` toochange Hallo doeltype blob.

Houd er rekening mee dat `/SyncCopy` kan extra uitgaande kosten vergelijken tooasynchronous kopiëren, Hallo aanbevolen aanpak is deze optie in Azure VM is in Hallo Hallo toouse dezelfde regio bevinden als uw gegevensbron account tooavoid uitgaande opslagkosten.

## <a name="table-export"></a>Tabel: exporteren
### <a name="export-table"></a>Tabel exporteren

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

AzCopy schrijft een doelmap manifestbestand toohello opgegeven. Hallo-manifestbestand wordt gebruikt in Hallo importeren proces toolocate Hallo gegevens die nodig zijn bestanden en gegevensvalidatie is uitgevoerd. Hallo-manifestbestand Hallo naamconventie volgen standaard gebruikt:

    <account name>_<table name>_<timestamp>.manifest

Gebruiker kan ook Hallo optie opgeven `/Manifest:<manifest file name>` tooset Hallo manifestbestand naam.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a>De export splitsen in meerdere bestanden

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

AzCopy gebruikt een *volume index* in Hallo gegevens splitsen bestandsnamen toodistinguish meerdere bestanden. Hallo volume index bestaat uit twee delen: een *partitie sleutel bereikindex* en een *gesplitste bestandsindex*. Beide indexen zijn gebaseerd op nul.

Hallo partitioneren van index sleutel bereik is 0 als Hallo gebruiker geen optie geeft `/PKRS`.

Stel AzCopy genereert twee gegevensbestanden nadat Hallo gebruiker Hiermee kunt u de optie `/SplitSize`. Hallo resulterende bestandsnamen gegevens mogelijk:

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

Houd er rekening mee dat Hallo mogelijke minimumwaarde voor de optie `/SplitSize` is 32 MB. Als Hallo opgegeven bestemming is Blob-opslag, AzCopy Hallo gegevensbestand splitst zodra de grootte bereikt Hallo blob de maximale grootte (200GB), ongeacht of optie `/SplitSize` is opgegeven door de gebruiker Hallo.

### <a name="export-table-toojson-or-csv-data-file-format"></a>Tabel tooJSON of CSV-gegevensbestandsindeling exporteren
AzCopy standaard exporteert tabellen tooJSON gegevensbestanden worden opgeslagen. U kunt de optie Hallo opgeven `/PayloadFormat:JSON|CSV` tooexport Hallo tabellen als JSON- of CSV.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

Bij het opgeven van de indeling van nettolading CSV Hallo AzCopy ook genereert u een schemabestand met extensie `.schema.csv` voor elk gegevensbestand.

### <a name="export-table-entities-concurrently"></a>Tabelentiteiten gelijktijdig exporteren

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

AzCopy gelijktijdige bewerkingen tooexport entiteiten wordt gestart wanneer Hallo gebruiker Hiermee kunt u de optie `/PKRS`. Elke bewerking exporteert een partitiesleutelbereik.

Houd er rekening mee dat het aantal gelijktijdige bewerkingen Hallo ook wordt beheerd door de optie `/NC`. AzCopy gebruikt Hallo aantal coreprocessors als standaardwaarde Hallo van `/NC` bij het kopiëren van de tabelentiteiten, zelfs als `/NC` is niet opgegeven. Als de gebruiker Hallo optie opgeeft `/PKRS`, AzCopy Hallo kleinere van Hallo twee waarden - partitie sleutelbereiken versus impliciet of expliciet opgegeven gelijktijdige bewerkingen - toodetermine Hallo aantal gelijktijdige bewerkingen toostart gebruikt. Typ voor meer informatie `AzCopy /?:NC` op Hallo-opdrachtregel.

### <a name="export-table-tooblob"></a>Tabel tooblob exporteren

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

AzCopy genereert een JSON-gegevensbestand in Hallo blob-container met de volgende naamconventie:

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

Hallo gegenereerd JSON-gegevensbestand heeft Hallo nettolading indeling voor minimale metagegevens. Zie voor meer informatie over deze indeling van nettolading [indeling van nettolading voor tabel servicebewerkingen](http://msdn.microsoft.com/library/azure/dn535600.aspx).

Houd er rekening mee dat bij het exporteren van tabellen tooblobs AzCopy Hallo tabel entiteiten toolocal gegevens tijdelijke bestanden worden gedownload en uploadt u deze entiteiten toohello blob. Deze tijdelijke gegevensbestanden in Hallo journaal bestandsmap door het standaardpad Hallo zijn geplaatst '<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>', kunt u optie/Z: [journaal-map] toochange Hallo journaal bestandsmaplocatie en dus wijzigen Hallo tijdelijke locatie van bestanden. Hallo tijdelijke gegevens voor de grootte van bestanden wordt bepaald door de grootte en het Hallo-grootte Hallo optie /SplitSize opgegeven, uw tabelentiteiten Hoewel Hallo tijdelijke gegevensbestand in de lokale schijf onmiddellijk is verwijderd nadat deze is geüpload toohello blob, zorg dat u hebt Onvoldoende lokale schijf ruimte toostore deze tijdelijke gegevensbestanden voordat ze worden verwijderd.

## <a name="table-import"></a>Tabel: importeren
### <a name="import-table"></a>Tabel importeren

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

Hallo optie `/EntityOperation` geeft aan hoe tooinsert entiteiten in de tabel Hallo. Mogelijke waarden zijn:

* `InsertOrSkip`: Hiermee slaat een bestaande entiteit of een nieuwe entiteit ingevoegd als het bestand niet in de tabel Hallo bestaat.
* `InsertOrMerge`: Een bestaande entiteit samenvoegingen of een nieuwe entiteit ingevoegd als het bestand niet in de tabel Hallo bestaat.
* `InsertOrReplace`: Een bestaande entiteit vervangt of een nieuwe entiteit ingevoegd als het bestand niet in de tabel Hallo bestaat.

Opmerking dat kunt u de optie opgeven `/PKRS` in Hallo importeren scenario. In tegenstelling tot Hallo export scenario, waarin u de optie moet opgeven `/PKRS` toostart gelijktijdige bewerkingen, AzCopy gelijktijdige bewerkingen wordt standaard gestart bij het importeren van een tabel. Hallo standaardaantal gelijktijdige bewerkingen gestart is gelijk toohello aantal coreprocessors; u kunt echter een verschillend aantal gelijktijdige met optie opgeven `/NC`. Typ voor meer informatie `AzCopy /?:NC` op Hallo-opdrachtregel.

Houd er rekening mee dat AzCopy biedt alleen ondersteuning voor JSON, niet-CSV importeren. AzCopy niet ondersteunt tabel invoer van gebruiker gemaakte JSON en manifest bestanden. Beide bestanden moeten afkomstig zijn van het exporteren van een AzCopy-tabel. tooavoid fouten, mag niet worden gewijzigd Hallo JSON of manifestbestand geëxporteerd.

### <a name="import-entities-tootable-using-blobs"></a>Importeren entiteiten tootable met behulp van BLOB 's
Een Blob-container Hallo volgende bevat: een JSON-bestand voor een Azure-tabel en het bijbehorende manifest-bestand.

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

U kunt na de opdracht tooimport entiteiten in een tabel met behulp van manifestbestand in de blobcontainer Hallo Hallo uitvoeren:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a>Andere functies van AzCopy
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Alleen gegevens die niet in het Hallo-doel bestaat gekopieerd
Hallo `/XO` en `/XN` parameters kunt u tooexclude oudere of nieuwere bron resources wordt gekopieerd, respectievelijk. Als u alleen toocopy bron bronnen die niet bestaan in Hallo bestemming wilt, kunt u beide parameters in Hallo AzCopy-opdracht:

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

Houd er rekening mee dat dit wordt niet ondersteund wanneer het Hallo-bron- of doelserver een tabel wordt.

### <a name="use-a-response-file-toospecify-command-line-parameters"></a>Gebruik een toospecify opdrachtregelprogramma responsbestandsparameters

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

U kunt eventuele opdrachtregelparameters AzCopy opnemen in een responsbestand. AzCopy processen Hallo parameters in Hallo bestand alsof ze op de opdrachtregel hello, uitvoeren van een directe vervanging met Hallo inhoud van Hallo bestand had is opgegeven.

Wordt ervan uitgegaan dat een antwoordbestand met de naam `copyoperation.txt`, die Hallo volgende regels bevat. Elke parameter AzCopy kan op een enkele regel worden opgegeven

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

of op afzonderlijke regels:

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

AzCopy mislukt als u de parameter Hallo over twee regels verdelen, zoals hier wordt weergegeven voor Hallo `/sourcekey` parameter:

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a>Gebruik van meerdere antwoord bestanden toospecify opdrachtregelparameters
Wordt ervan uitgegaan dat een antwoordbestand met de naam `source.txt` die aangeeft dat een Broncontainer:

    /Source:http://myaccount.blob.core.windows.net/mycontainer

En een antwoordbestand met de naam `dest.txt` waarmee een doelmap in het bestandssysteem Hallo:

    /Dest:C:\myfolder

En een antwoordbestand met de naam `options.txt` Hiermee worden de opties voor AzCopy:

    /S /Y

toocall AzCopy met deze antwoordbestanden die zich bevinden in een map `C:\responsefiles`, gebruikt u deze opdracht:

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

AzCopy verwerkt met deze opdracht net zoals als u alle afzonderlijke parameters op opdrachtregel Hallo Hallo opgenomen:

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a>Geef een shared access signature (SAS)

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

U kunt ook een SAS voor Hallo container URI opgeven:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a>Map voor logboek-bestand
Telkens wanneer die u een tooAzCopy opdracht de opdracht die wordt gecontroleerd of een journal-bestand in de standaardmap Hallo bestaat en of deze bestaat in een map die u hebt opgegeven via deze optie. Hallo journaalbestand bestaat niet op beide plaatsen, AzCopy Hallo bewerking behandelt als nieuwe als genereert een nieuw journaalbestand.

Als Hallo journal-bestand bestaat, wordt door AzCopy gecontroleerd of Hallo-opdrachtregel die ingevoerde overeenkomt met Hallo vanaf de opdrachtregel in Hallo journal-bestand. Als twee opdrachtregels Hallo overeenkomen, hervat AzCopy onvolledige Hallo-bewerking. Als ze niet overeenkomen, bent u na vragen aan gebruiker tooeither overschrijven Hallo journaal bestand toostart een nieuwe bewerking of toocancel Hallo huidige bewerking.

Als u wilt dat toouse Hallo-standaardlocatie voor Hallo journal-bestand:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

Als u de optie weglaat `/Z`, of geef de optie `/Z` zonder Hallo mappad, zoals hierboven, AzCopy maakt Hallo journal-bestand in Hallo standaardlocatie is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`. Als Hallo journaalbestand al bestaat, hervat AzCopy Hallo-bewerking op basis van Hallo journal-bestand.

Als u wilt dat een aangepaste locatie voor Hallo journaalbestand toospecify:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

In dit voorbeeld maakt Hallo journal-bestand als deze niet al bestaat. Als deze bestaat, hervat AzCopy Hallo-bewerking op basis van Hallo journal-bestand.

Als u wilt dat een bewerking AzCopy tooresume:

```azcopy
AzCopy /Z:C:\journalfolder\
```

In dit voorbeeld hervat Hallo laatste bewerking, die mogelijk niet toocomplete.

### <a name="generate-a-log-file"></a>Genereren van een logboekbestand

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

Als u de optie opgeven `/V` zonder op te geven van een bestand pad toohello uitgebreid logboek, AzCopy maakt vervolgens logboekbestand Hallo in Hallo standaardlocatie is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.

Anders kunt u een logboekbestand maken in een aangepaste locatie:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

Houd er rekening mee dat als u een relatief pad na optie opgeeft `/V`, zoals `/V:test/azcopy1.log`, en vervolgens Hallo uitgebreide logboek in de huidige werkmap in een submap met de naam Hallo gemaakt `test`.

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Geef het aantal gelijktijdige bewerkingen toostart Hallo
Optie `/NC` geeft het aantal gelijktijdige kopieerbewerkingen Hallo. AzCopy wordt standaard een bepaald aantal gelijktijdige bewerkingen tooincrease Hallo-gegevensdoorvoer overdracht gestart. Voor bewerkingen van de tabel is het aantal gelijktijdige bewerkingen Hallo gelijk toohello aantal processors dat u hebt. Voor Blob- en bewerkingen, het aantal gelijktijdige bewerkingen Hallo is gelijk aan 8 keer Hallo aantal processors dat u hebt. Als u via een netwerk met lage bandbreedte AzCopy uitvoert, kunt u een lager getal voor /NC tooavoid mislukt, omdat resource concurrentie opgeven.

### <a name="run-azcopy-against-azure-storage-emulator"></a>AzCopy uitvoeren op Azure-Opslagemulator
U kunt AzCopy uitvoeren op Hallo [Azure-Opslagemulator](storage-use-emulator.md) voor Blobs:

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

en tabellen:

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a>AzCopy-Parameters
Parameters voor AzCopy worden hieronder beschreven. U kunt ook een van de volgende opdrachten uit vanaf de opdrachtregel voor hulp bij het gebruik van AzCopy Hallo Hallo typen:

* Voor gedetailleerde help voor AzCopy:`AzCopy /?`
* Voor gedetailleerde hulp bij elke parameter AzCopy:`AzCopy /?:SourceKey`
* Voor voorbeelden van opdrachtregels:`AzCopy /?:Samples`

### <a name="sourcesource"></a>/ Source: 'bron'
Hiermee geeft u de brongegevens Hallo uit welke toocopy. Hallo bron mag een bestandssysteemmap, een blob-container, een blob virtuele map, een bestandsshare voor opslag, een map voor opslag of een Azure-tabel.

**Van toepassing op:** Blobs, bestanden, tabellen

### <a name="destdestination"></a>/ Dest: "doelmap"
Hiermee geeft u Hallo bestemming toocopy aan. Hallo bestemming mag een bestandssysteemmap, een blob-container, een blob virtuele map, een bestandsshare voor opslag, een map voor opslag of een Azure-tabel.

**Van toepassing op:** Blobs, bestanden, tabellen

### <a name="patternfile-pattern"></a>/ Patroon: "bestandspatroon"
Hiermee geeft u een patroon waarmee wordt aangegeven welke toocopy bestanden. Hallo gedrag van Hallo /Pattern parameter wordt bepaald door het Hallo-locatie van de brongegevens Hallo en Hallo aanwezigheid van Hallo recursieve modusoptie. Recursieve modus wordt opgegeven via de optie/s.

Als Hallo opgegeven bron een map in het bestandssysteem hello, is wordt standaard jokertekens van kracht zijn en Hallo patroon opgegeven wordt vergeleken met de bestanden in de map Hallo. Als de optie die /s is opgegeven, klikt u vervolgens AzCopy, overeenkomt met opgegeven patroon Hallo tegen alle bestanden in eventuele submappen Hallo-directory.

Als de opgegeven bron Hallo een blob-container of de virtuele map is, worden klikt u vervolgens jokertekens niet toegepast. Als de optie/s is opgegeven, klikt u vervolgens AzCopy interpreteert Hallo opgegeven patroon als voorvoegsel van de blob. Als de optie/s niet is opgegeven, klikt u vervolgens AzCopy komt overeen met patroon Hallo tegen exacte blob-namen.

Als Hallo bron is een Azure-bestandsshare opgegeven, moet u Hallo exacte bestandsnaam (bijvoorbeeld abc.txt) opgeven toocopy één bestand of het opgeven van de optie/s toocopy alle bestanden in Hallo share recursief. Toospecify beide wordt geprobeerd een bestand patroon en de optie/s samen met resultaten in een fout.

AzCopy gebruikt hoofdlettergevoelig overeenkomende wanneer Hallo/Source een blob-container of blob virtuele map is en maakt gebruik van niet-hoofdlettergevoelige die overeenkomt met alle andere gevallen Hallo.

Hallo bestand standaardpatroon gebruikt wanneer er geen bestandspatroon is opgegeven is *.* voor een locatie in het bestandssysteem of een leeg voorvoegsel voor een Azure-opslaglocatie. Meerdere bestand patronen opgeven wordt niet ondersteund.

**Van toepassing op:** Blobs, bestanden

### <a name="destkeystorage-key"></a>/ DestKey: 'opslagsleutel'
Hiermee geeft u Hallo-toegangssleutel voor Hallo doelbron.

**Van toepassing op:** Blobs, bestanden, tabellen

### <a name="destsassas-token"></a>/ DestSAS: 'sas-token'
Hiermee geeft u een Shared Access Signature (SAS) met machtigingen voor lezen en schrijven voor Hallo doel (indien van toepassing). Hallo SAS met dubbele aanhalingstekens rond omdat deze mogelijk speciale opdrachtregelprogramma tekens bevat.

Als Hallo doelbron een blob-container, een bestandsshare of een tabel is, kunt u deze optie gevolgd door de SAS-token Hallo opgeven of u Hallo SAS als onderdeel van Hallo bestemming blob-container, bestandsshare of de URI van de tabel, zonder deze optie kunt opgeven.

Als Hallo bron- en doelserver beide blobs zijn, en vervolgens Hallo bestemmings-blob zich binnen Hallo dezelfde bevinden moet als Hallo bron blob storage-account.

**Van toepassing op:** Blobs, bestanden, tabellen

### <a name="sourcekeystorage-key"></a>/ SourceKey: 'opslagsleutel'
Hiermee geeft u Hallo opslagaccountsleutel voor Hallo bronresource.

**Van toepassing op:** Blobs, bestanden, tabellen

### <a name="sourcesassas-token"></a>/ SourceSAS: 'sas-token'
Hiermee geeft u een Shared Access Signature met lees- en machtigingen voor het Hallo-bron (indien van toepassing). Hallo SAS met dubbele aanhalingstekens rond omdat deze mogelijk speciale opdrachtregelprogramma tekens bevat.

Als Hallo bron bron een blob-container is en een sleutel noch een SAS is opgegeven, wordt Hallo blob-container gelezen via anonieme toegang.

Als het Hallo-bron is een bestandsshare of een sleutel of een SAS tabel moet worden opgegeven.

**Van toepassing op:** Blobs, bestanden, tabellen

### <a name="s"></a>/ S
Hiermee geeft u een recursieve modus voor het kopiëren van. In de modus voor recursieve kopieert AzCopy alle blobs of bestanden die overeenkomen met Hallo opgegeven bestandspatroon, inclusief verbindingen in submappen.

**Van toepassing op:** Blobs, bestanden

### <a name="blobtypeblock--page--append"></a>/ BlobType: 'block' | "page" | "toevoegen"
Hiermee geeft u op of Hallo bestemmings-blob een blok-blob, een pagina-blob of een toevoeg-blob is. Deze optie is alleen toepasbaar wanneer u een blob uploadt. Anders wordt er een fout gegenereerd. Als Hallo bestemming een blob is en deze optie niet is opgegeven, standaard maakt AzCopy een blok-blob.

**Van toepassing op:** Blobs

### <a name="checkmd5"></a>/ CheckMD5
Een MD5-hash voor de gedownloade gegevens berekend en controleert of Hallo MD5-hash wordt opgeslagen in blob Hallo of Content-MD5-eigenschap van bestand overeenkomt met Hallo berekende hash. Hallo MD5 selectievakje is standaard uitgeschakeld, dus u deze optie tooperform Hallo MD5 controle opgeven moet bij het downloaden van gegevens.

Houd er rekening mee dat Azure Storage niet dat Hallo MD5-hash voor Hallo blob worden opgeslagen garandeert of het bestand is up-to-date. Het is van de client verantwoordelijkheid tooupdate Hallo MD5 als Hallo blob of het bestand wordt gewijzigd.

Na het uploaden van deze wordt AzCopy altijd Hallo Content-MD5-eigenschap voor een Azure-blob of een bestand toohello-service.  

**Van toepassing op:** Blobs, bestanden

### <a name="snapshot"></a>/ Momentopname
Hiermee wordt aangegeven of tootransfer momentopnamen. Deze optie is alleen geldig wanneer het Hallo-bron is een blob.

Hallo overgebrachte blob momentopnamen hernoemd in deze indeling: .extensie blob-naam (momentopname-tijd)

Momentopnamen worden standaard niet gekopieerd.

**Van toepassing op:** Blobs

### <a name="vverbose-log-file"></a>/ V: [uitgebreide-log-bestand]
Uitvoer uitgebreide statusberichten in een logboekbestand.

Hallo uitgebreide logboekbestand heet standaard AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`. Als u een bestaande bestandslocatie voor deze optie opgeeft, is uitgebreid logboek Hallo toegevoegde toothat-bestand.  

**Van toepassing op:** Blobs, bestanden, tabellen

### <a name="zjournal-file-folder"></a>/ Z: [journaal-map]
Hiermee geeft u een map journaal-bestand voor het hervatten van een bewerking.

AzCopy ondersteunt altijd wordt hervat als een bewerking is onderbroken.

Als deze optie niet opgegeven is of deze is opgegeven zonder het pad naar een map, maakt AzCopy Hallo journaal-bestand in Hallo standaardlocatie bevindt, % LocalAppData%\Microsoft\Azure\AzCopy is.

Telkens wanneer die u een tooAzCopy opdracht de opdracht die wordt gecontroleerd of een journal-bestand in de standaardmap Hallo bestaat en of deze bestaat in een map die u hebt opgegeven via deze optie. Hallo journaalbestand bestaat niet op beide plaatsen, AzCopy Hallo bewerking behandelt als nieuwe als genereert een nieuw journaalbestand.

Als Hallo journal-bestand bestaat, wordt door AzCopy gecontroleerd of Hallo-opdrachtregel die ingevoerde overeenkomt met Hallo vanaf de opdrachtregel in Hallo journal-bestand. Als twee opdrachtregels Hallo overeenkomen, hervat AzCopy onvolledige Hallo-bewerking. Als ze niet overeenkomen, bent u na vragen aan gebruiker tooeither overschrijven Hallo journaal bestand toostart een nieuwe bewerking of toocancel Hallo huidige bewerking.

Hallo journaal-bestand wordt verwijderd bij het Hallo-bewerking is voltooid.

Houd er rekening mee dat het hervatten van een bewerking van een journal-bestand gemaakt met een eerdere versie van AzCopy niet wordt ondersteund.

**Van toepassing op:** Blobs, bestanden, tabellen

### <a name="parameter-file"></a>/@:"parameter-File'
Hiermee geeft u een bestand met parameters. AzCopy processen Hallo parameters in Hallo bestand alsof ze op de opdrachtregel Hallo had opgegeven.

In een responsbestand kunt u meerdere parameters opgeven op één regel of geef elke parameter in op een aparte regel. Houd er rekening mee dat een afzonderlijke parameter kan niet worden gebruikt voor het bereik van meerdere regels.

Antwoordbestanden kunnen opmerkingen regels die met Hallo # symbool beginnen bevatten.

U kunt meerdere antwoordbestanden opgeven. Houd er echter rekening mee AzCopy biedt geen ondersteuning voor geneste antwoordbestanden.

**Van toepassing op:** Blobs, bestanden, tabellen

### <a name="y"></a>/Y
Alle AzCopy bevestiging vragen onderdrukt.

**Van toepassing op:** Blobs, bestanden, tabellen

### <a name="l"></a>/ L
Hiermee geeft u een bewerking in de lijst. Er zijn geen gegevens worden gekopieerd.

AzCopy interpreteert Hallo met behulp van deze optie als een simulatie voor actieve Hallo opdrachtregel zonder deze optie/l en tellingen hoeveel objecten zijn gekopieerd, kunt u optie /V op Hallo dezelfde tijd toocheck welke objecten in de uitgebreide logboek Hallo worden gekopieerd.

Hallo-gedrag van deze optie is ook afhankelijk van Hallo-locatie van de brongegevens Hallo en Hallo aanwezigheid van Hallo recursieve modus/s en de bestandsnaam patroon optie /Pattern.

AzCopy vereist lijst weergeven en lezen van de bronlocatie van deze wanneer u deze optie.

**Van toepassing op:** Blobs, bestanden

### <a name="mt"></a>/MT
Hiermee stelt Hallo gedownloade bestand laatst gewijzigd-tijd toobe Hallo dezelfde als de bron-blob Hallo of van het bestand.

**Van toepassing op:** Blobs, bestanden

### <a name="xn"></a>/XN
Sluit een nieuwere bronresource. Hallo wordt resource niet gekopieerd als hello laatst gewijzigd-tijd van de bron Hallo Hallo dezelfde of een nieuwer is dan het doel.

**Van toepassing op:** Blobs, bestanden

### <a name="xo"></a>/XO
Sluit een oudere bronserver resource. Hallo wordt resource niet gekopieerd als hello laatst gewijzigd-tijd van de bron Hallo Hallo dezelfde of een ouder zijn dan het doel.

**Van toepassing op:** Blobs, bestanden

### <a name="a"></a>/A
Alleen bestanden die Hallo kenmerk Archief hebben geüpload.

**Van toepassing op:** Blobs, bestanden

### <a name="iarashcnetoi"></a>/ IA: [RASHCNETOI]
Uploads alleen bestanden die een Hallo opgegeven set kenmerken.

Beschikbare kenmerken zijn onder andere:

* R = alleen-lezen bestanden
* Een = bestanden klaar voor archivering
* S = systeembestanden
* H = Verborgen bestanden
* C = gecomprimeerde bestanden
* N = normale bestanden
* E = versleutelde bestanden
* T = tijdelijke bestanden
* O = offlinebestanden
* Ik = niet-geïndexeerde bestanden

**Van toepassing op:** Blobs, bestanden

### <a name="xarashcnetoi"></a>/ XA: [RASHCNETOI]
Sluit bestanden die een opgegeven Hallo set kenmerken.

Beschikbare kenmerken zijn onder andere:

* R = alleen-lezen bestanden
* Een = bestanden klaar voor archivering
* S = systeembestanden
* H = Verborgen bestanden
* C = gecomprimeerde bestanden
* N = normale bestanden
* E = versleutelde bestanden
* T = tijdelijke bestanden
* O = offlinebestanden
* Ik = niet-geïndexeerde bestanden

**Van toepassing op:** Blobs, bestanden

### <a name="delimiterdelimiter"></a>/ Scheidingsteken: "scheidingsteken"
Hiermee wordt aangegeven op Hallo scheidingsteken toodelimit virtuele mappen in een blob-naam gebruikt.

Standaard maakt gebruik van AzCopy / als Hallo scheidingsteken. AzCopy ondersteunt echter met behulp van een algemene teken (zoals @, # of %) als scheidingsteken. Als u tooinclude een van deze speciale tekens op Hallo-opdrachtregel moet, plaatst u de bestandsnaam Hallo met dubbele aanhalingstekens.

Deze optie is alleen van toepassing voor het downloaden van blobs.

**Van toepassing op:** Blobs

### <a name="ncnumber-of-concurrent-operations"></a>/ NC: 'getal-van-gelijktijdige-operations'
Hiermee geeft u het aantal gelijktijdige bewerkingen Hallo.

AzCopy standaard wordt een bepaald aantal gelijktijdige bewerkingen tooincrease Hallo-gegevensdoorvoer overdracht gestart. Vergeet niet dat groot aantal gelijktijdige bewerkingen in een omgeving met lage bandbreedte mogelijk Hallo netwerkverbinding overbelast en te voorkomen dat Hallo bewerkingen volledig is voltooid. Vertraging gelijktijdige bewerkingen op basis van de werkelijke beschikbare netwerkbandbreedte.

Hallo bovengrens voor gelijktijdige bewerkingen is 512.

**Van toepassing op:** Blobs, bestanden, tabellen

### <a name="sourcetypeblob--table"></a>/ SourceType: "Blob" | 'Tabel'
Hiermee geeft u op dat Hallo `source` bron is een blob in Hallo lokale ontwikkelomgeving wordt uitgevoerd in de opslagemulator Hallo beschikbaar.

**Van toepassing op:** Blobs, tabellen

### <a name="desttypeblob--table"></a>/ DestType: "Blob" | 'Tabel'
Hiermee geeft u op dat Hallo `destination` bron is een blob in Hallo lokale ontwikkelomgeving wordt uitgevoerd in de opslagemulator Hallo beschikbaar.

**Van toepassing op:** Blobs, tabellen

### <a name="pkrskey1key2key3"></a>/ PKRS: "key&#1;key2 key&#3;..."
Splitsingen Hallo partitie sleutel bereik tooenable tabelgegevens parallel verhoogt de snelheid van de exportbewerking Hallo Hallo exporteren.

Als deze optie niet is opgegeven, gebruikt een enkele thread tooexport tabelentiteiten met AzCopy. Bijvoorbeeld, als hello gebruiker geeft op /PKRS: "aa #bb" en vervolgens AzCopy begint drie gelijktijdige bewerkingen.

Elke bewerking exporteert een van drie partitie sleutel bereiken, zoals hieronder wordt weergegeven:

  [eerste partitiesleutel, aa)

  [aa, bb)

  [bb, laatste partitiesleutel]

**Van toepassing op:** tabellen

### <a name="splitsizefile-size"></a>/ SplitSize: 'bestandsgrootte'
Hiermee geeft u op Hallo geëxporteerde bestand splitsen grootte in MB, Hallo minimaal toegestane waarde is 32.

Als deze optie niet is opgegeven, exporteert AzCopy tabel gegevens tooa enkel bestand.

Als Hallo tabelgegevens geëxporteerde tooa blob is en hello geëxporteerde bestandsgrootte Hallo 200 GB limiet voor de Blobgrootte van de bereikt, klikt u vervolgens splitst AzCopy het geëxporteerde bestand hello, zelfs als deze optie is niet opgegeven.

**Van toepassing op:** tabellen

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a>/ EntityOperation: 'InsertOrSkip' | 'InsertOrMerge' | 'InsertOrReplace'
Hiermee geeft u gegevens Hallo-import tabelgedrag.

* InsertOrSkip - slaat een bestaande entiteit of een nieuwe entiteit ingevoegd als het bestand bestaat niet in de tabel Hallo.
* InsertOrMerge - samenvoegingen van een bestaande entiteit of een nieuwe entiteit ingevoegd als het bestand bestaat niet in de tabel Hallo.
* InsertOrReplace - wordt vervangen door een bestaande entiteit of een nieuwe entiteit ingevoegd als het bestand bestaat niet in de tabel Hallo.

**Van toepassing op:** tabellen

### <a name="manifestmanifest-file"></a>/ Manifest: 'manifest file'
Hiermee geeft u Hallo manifestbestand voor Hallo tabel exporteren en importeren.

Deze optie is optioneel tijdens de exportbewerking hello, AzCopy genereert een manifestbestand met vooraf gedefinieerde naam als deze optie niet is opgegeven.

Deze optie is vereist tijdens de importbewerking hello om de gegevensbestanden hello te vinden.

**Van toepassing op:** tabellen

### <a name="synccopy"></a>/ SyncCopy
Hiermee wordt aangegeven of toosynchronously blobs of bestanden tussen de twee eindpunten voor Azure Storage kopiëren.

AzCopy standaard gebruikt serverzijde asynchrone kopie. Geef deze optie tooperform een synchrone die downloadt blobs of bestanden toolocal geheugen en uploadt deze tooAzure Storage kopiëren.

U kunt deze optie gebruiken bij het kopiëren van bestanden in Blob storage, binnen de opslag van bestanden of van Blob storage tooFile opslag of vice versa.

**Van toepassing op:** Blobs, bestanden

### <a name="setcontenttypecontent-type"></a>/ SetContentType: 'content-type'
Hiermee geeft u Hallo MIME-inhoudstype voor bestemming blobs of bestanden.

AzCopy sets Hallo inhoudstype voor een blob of tooapplication/octet-stream standaard bestand. U kunt Hallo inhoudstype voor alle blobs of bestanden instellen door een waarde op voor deze optie expliciet op te geven.

Als u deze optie geen waarde opgeeft, stelt AzCopy elke blob of inhoudstype van het bestand volgens tooits bestandsextensie.

**Van toepassing op:** Blobs, bestanden

### <a name="payloadformatjson--csv"></a>/ PayloadFormat: 'JSON' | 'CSV'
Hiermee geeft u Hallo-indeling van bestand met geëxporteerde gegevens Hallo.

Als deze optie niet is opgegeven, standaard exporteert AzCopy gegevensbestand van de tabel in JSON-indeling.

**Van toepassing op:** tabellen

## <a name="known-issues-and-best-practices"></a>Bekende problemen en aanbevolen procedures
### <a name="limit-concurrent-writes-while-copying-data"></a>Limiet voor gelijktijdige schrijfbewerkingen tijdens het kopiëren van gegevens
Als u blobs of bestanden met AzCopy kopieert, houd er rekening mee dat een andere toepassing Hallo gegevens heeft terwijl u kopieert. Indien mogelijk, zorg dat u kopieert Hallo-gegevens niet wordt gewijzigd tijdens de kopieerbewerking Hallo. Bijvoorbeeld bij het kopiëren van een VHD die is gekoppeld aan een virtuele machine van Azure, zorg dat er geen andere toepassingen toohello VHD momenteel schrijft. Een goede manier toodo die deze wordt door het Hallo resource toobe leasing gekopieerd. U kunt ook eerst een momentopname van Hallo VHD maken en vervolgens kopieert Hallo momentopname.

Als u niet voorkomen andere toepassingen dat bij het schrijven van tooblobs of bestanden terwijl ze worden gekopieerd en vervolgens Houd er rekening mee dat door Hallo tijd Hallo taak is voltooid, hello gekopieerde resources niet meer mogelijk volledige pariteit met Hallo bron resources.

### <a name="run-one-azcopy-instance-on-one-machine"></a>Één AzCopy-sessie uitvoeren op één computer.
AzCopy is ontworpen toomaximize Hallo gebruik van uw machine resource tooaccelerate Hallo gegevens worden overgedragen, is het raadzaam u slechts één exemplaar van AzCopy uitvoeren op één machine en geef Hallo optie `/NC` als u meer gelijktijdige bewerkingen nodig. Typ voor meer informatie `AzCopy /?:NC` op Hallo-opdrachtregel.

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a>FIPS-compatibele MD5-algoritmen voor AzCopy inschakelen wanneer u ' gebruik FIPS compatibele algoritmen voor versleuteling, hashing en ondertekening '.
AzCopy standaard .NET MD5 implementatie toocalculate Hallo MD5 gebruikt bij het kopiëren van objecten, maar er zijn bepaalde beveiligingsvereisten voor de die AzCopy tooenable FIPS compatibele MD5-instelling nodig.

U kunt een app.config-bestand maken `AzCopy.exe.config` met de eigenschap `AzureStorageUseV1MD5` en reserveer met AzCopy.exe plaatsen.

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

Voor de eigenschap 'AzureStorageUseV1MD5' • waar - Hallo-standaardwaarde, AzCopy .NET MD5 implementatie gebruikt.
• ONWAAR – AzCopy hierbij wordt gebruikgemaakt van FIPS-compatibele MD5-algoritmen.

Houd er rekening mee dat FIPS-algoritmen is standaard uitgeschakeld in uw Windows-computer, kunt u secpol.msc typt in het venster uitvoeren en controleer of deze switch op beveiligingsinstelling -> lokaal beleid -> Beveiliging -> Systeemcryptografie: gebruik FIPS-algoritmen voor versleuteling, hashing en ondertekening.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over Azure Storage en AzCopy Hallo resources te volgen:

### <a name="azure-storage-documentation"></a>Documentatie bij Azure Storage:
* [Inleiding tooAzure opslag](../storage-introduction.md)
* [Hoe toouse .NET Blob-opslag](../blobs/storage-dotnet-how-to-use-blobs.md)
* [Hoe toouse File storage in .NET](../storage-dotnet-how-to-use-files.md)
* [Hoe toouse Table storage uit het .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Hoe toocreate, beheren of verwijderen van een opslagaccount](../storage-create-storage-account.md)
* [Gegevensoverdracht met AzCopy op Linux](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a>Azure Storage-blogberichten:
* [Inleiding tot Azure Storage Data Movement bibliotheek-Preview](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: Introducing synchrone kopiëren en aangepaste type inhoud](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: Aangekondigd algemene beschikbaarheid van AzCopy 3.0 plus preview-versie van AzCopy 4.0 met de ondersteuning voor de tabel en de bestandsnaam](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: Geoptimaliseerd voor grootschalige kopie scenario 's](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy: Ondersteuning voor geografisch redundante opslag met leestoegang](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy: Gegevensoverdracht met modus opnieuw gestart en SAS-token](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [AzCopy: Cross-account kopiëren Blob met behulp](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: Uploaden/downloaden van bestanden voor Azure Blobs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

