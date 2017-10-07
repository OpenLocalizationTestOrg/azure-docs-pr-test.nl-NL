---
title: aaaCopy of verplaats gegevens tooAzure opslag met AzCopy op Linux | Microsoft Docs
description: "Hallo AzCopy op Linux hulpprogramma toomove of een kopie van gegevens tooor van blob- en inhoud gebruiken. Kopiëren van gegevens tooAzure opslag van lokale bestanden of kopiëren van gegevens binnen of tussen opslagaccounts. Eenvoudig uw gegevens tooAzure opslag migreren."
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
ms.date: 05/11/2017
ms.author: seguler
ms.openlocfilehash: dccb03c9e8cc3ea661494e7834f307b0e3e30cb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a>Gegevensoverdracht met AzCopy op Linux
AzCopy op Linux is een opdrachtregelprogramma dat is ontworpen voor het kopiëren van gegevens tooand van Microsoft Azure Blob- en bestandsopslag met eenvoudige opdrachten met optimale prestaties. U kunt gegevens kopiëren van een object tooanother binnen uw opslagaccount of tussen opslagaccounts.

Er zijn twee versies van AzCopy die u kunt downloaden. AzCopy op Linux is gebouwd met .NET Core Framework dat gericht is op Linux-platforms biedt POSIX-stijl opdrachtregelopties. [AzCopy op Windows](storage-use-azcopy.md) is gebouwd met .NET Framework en Windows-stijl biedt opdrachtregelopties. In dit artikel bevat informatie over AzCopy op Linux.

## <a name="download-and-install-azcopy"></a>Downloaden en installeren van AzCopy
### <a name="installation-on-linux"></a>Installatie op Linux

AzCopy op Linux vereist .NET Core framework op Hallo-platform. Zie de installatie-instructies Hallo op Hallo [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) pagina.

Installeer .NET Core op Ubuntu 16,10 als voorbeeld. Voor het meest recente installatiehandleiding hello, gaat u naar [.NET Core op Linux](https://www.microsoft.com/net/core#linuxubuntu) op de installatiepagina.


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

Als u .NET Core hebt geïnstalleerd, downloaden en installeren van AzCopy.

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

Nadat AzCopy op Linux is geïnstalleerd, kunt u bestanden hebt uitgepakt Hallo verwijderen. Als u geen supergebruiker bevoegdheden, kunt u ook ook uitvoeren met behulp van de shell-script Hallo AzCopy 'azcopy' in de uitgepakte map Hallo. 

### <a name="alternative-installation-on-ubuntu"></a>Alternatieve installatie op Ubuntu

**Ubuntu 14.04**

Apt-bron toevoegen voor .net Core:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Apt bron voor Linux Microsoft product opslagplaats toevoegen en AzCopy installeren:

```bash
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.04**

Apt-bron toevoegen voor .net Core:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Apt bron voor Linux Microsoft product opslagplaats toevoegen en AzCopy installeren:

```bash
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16,10**

Apt-bron toevoegen voor .net Core:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Apt bron voor Linux Microsoft product opslagplaats toevoegen en AzCopy installeren:

```bash
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

## <a name="writing-your-first-azcopy-command"></a>Schrijven van uw eerste AzCopy-opdracht
Hallo basic syntaxis voor opdrachten van AzCopy is:

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

Hallo volgen voorbeelden laten zien dat verschillende scenario's voor het kopiëren van gegevens tooand van Microsoft Azure Blobs en bestanden. Raadpleeg toohello `azcopy --help` menu voor een gedetailleerde beschrijving van het Hallo-parameters die worden gebruikt in elk voorbeeld.

## <a name="blob-download"></a>BLOB: downloaden
### <a name="download-single-blob"></a>Enkele blobs downloaden

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Als Hallo map `/mnt/myfiles` niet bestaat, AzCopy wordt deze gemaakt en gedownload `abc.txt ` in Hallo nieuwe map.

### <a name="download-single-blob-from-secondary-region"></a>Downloaden van één blob van de secundaire regio

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Houd er rekening mee dat u geografisch redundante opslag met leestoegang ingeschakeld nodig hebt.

### <a name="download-all-blobs"></a>Alle blobs downloaden

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Wordt ervan uitgegaan dat de volgende Hallo BLOB's zich bevinden in de opgegeven container Hallo:  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

Na de bewerking van de download hello, Hallo directory `/mnt/myfiles` omvat Hallo volgende bestanden:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

Als u geen optie opgeeft `--recursive`, geen blob worden gedownload.

### <a name="download-blobs-with-specified-prefix"></a>Blobs met het opgegeven voorvoegsel downloaden

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

Wordt ervan uitgegaan dat de volgende Hallo BLOB's zich bevinden in de opgegeven container Hallo. Alle blobs vanaf Hallo voorvoegsel `a` worden gedownload.

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

Na de bewerking van de download hello, Hallo map `/mnt/myfiles` bevat Hallo volgende bestanden:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

Hallo-voorvoegsel is van toepassing toohello virtuele map, die Hallo eerste deel van Hallo blob-naam uitmaakt. In het bovenstaande voorbeeld Hallo, Hallo virtuele map komt niet overeen met het opgegeven voorvoegsel hello, dus geen blob wordt gedownload. Bovendien, als hello optie `--recursive` niet is opgegeven, AzCopy biedt niet alle blobs downloaden.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>Hallo tijd laatste wijziging van de geëxporteerde bestanden toobe instellen hetzelfde als de bron blobs Hallo

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

U kunt ook BLOB's uitsluiten van Hallo downloaden van de bewerking op basis van hun tijd voor het laatst is gewijzigd. Bijvoorbeeld, als u tooexclude blobs waarvan laatst gewijzigd-tijd Hallo dezelfde of een nieuwer is dan het doelbestand hello wilt is, toevoegen Hallo `--exclude-newer` optie:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

Of als u tooexclude blobs waarvan laatst gewijzigd-tijd Hallo dezelfde of een ouder is dan het doelbestand hello wilt is, toe te voegen Hallo `--exclude-older` optie:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a>BLOB: uploaden
### <a name="upload-single-file"></a>Bestand uploaden

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

Als Hallo opgegeven bestemmingscontainer niet bestaat, AzCopy wordt deze gemaakt en uploads Hallo bestand in de App.

### <a name="upload-single-file-toovirtual-directory"></a>Enkel bestand toovirtual directory uploaden

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

Als Hallo virtuele map bestaat niet opgegeven, AzCopy Hallo bestand tooinclude Hallo virtuele map in de blob-naam Hallo uploadt (*bijvoorbeeld*, `vd/abc.txt` in bovenstaande Hallo voorbeeld).

### <a name="upload-all-files"></a>Alle bestanden uploaden

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

Optie `--recursive` uploads Hallo inhoud Hallo opgegeven directory tooBlob opslag recursief, wat betekent dat alle submappen en de bestanden ook worden geüpload. Voor het exemplaar wordt ervan uitgegaan dat de volgende Hallo bestanden bevinden zich in map `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Na het Hallo-uploadbewerking bevat Hallo container Hallo volgende bestanden:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Wanneer Hallo optie `--recursive` niet is opgegeven, alleen hello volgende drie bestanden worden geüpload:

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a>Uploaden van bestanden die overeenkomen met opgegeven patroon

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

Wordt ervan uitgegaan dat de volgende Hallo bestanden bevinden zich in map `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Na het Hallo-uploadbewerking bevat Hallo container Hallo volgende bestanden:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Wanneer Hallo optie `--recursive` niet is opgegeven, AzCopy slaat bestanden in submappen:

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>Geef Hallo MIME-inhoudstype van een bestemmings-blob
Standaard stelt AzCopy Hallo-inhoudstype van een bestemmings-blob te`application/octet-stream`. U kunt echter expliciet opgeven Hallo inhoudstype via Hallo-optie `--set-content-type [content-type]`. Deze syntaxis wordt Hallo inhoudstype voor alle blobs in een uploadbewerking.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

Als hello optie `--set-content-type` is opgegeven zonder een waarde worden AzCopy elke blob of bestand stelt het type inhoud op basis van tooits bestandsextensie.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a>BLOB: kopiëren
### <a name="copy-single-blob-within-storage-account"></a>Één blob binnen opslagaccount kopiëren

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

Wanneer u een blob zonder--gesynchroniseerde kopie-optie, kopieert een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.

### <a name="copy-single-blob-across-storage-accounts"></a>Één blob kopiëren tussen opslagaccounts

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

Wanneer u een blob zonder--gesynchroniseerde kopie-optie, kopieert een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>Één blob kopiëren van de secundaire regio tooprimary regio

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

Houd er rekening mee dat u geografisch redundante opslag met leestoegang ingeschakeld nodig hebt.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>Één blob en bijbehorende momentopnamen kopiëren tussen opslagaccounts

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

Na de kopieerbewerking hello omvat doelcontainer Hallo Hallo blob en het bijbehorende momentopnamen. Hallo container omvat Hallo volgende blob en het bijbehorende momentopnamen:

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>Synchroon kopiëren van BLOB's tussen opslagaccounts
AzCopy standaard worden de gegevens tussen de twee eindpunten voor opslag asynchroon gekopieerd. Daarom Hallo kopie-bewerking wordt uitgevoerd op Hallo achtergrond met behulp van ongebruikte bandbreedtecapaciteit die geen SLA in termen van hoe snel een blob heeft wordt gekopieerd. 

Hallo `--sync-copy` optie zorgt ervoor dat de kopieerbewerking Hallo consistente snelheid opgehaald. AzCopy voert synchrone kopie Hallo Hallo blobs downloaden toocopy van Hallo opgegeven bron toolocal geheugen en uploadt deze toohello Blob-opslaglocatie.

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

`--sync-copy`Als u meer uitgaande kosten vergeleken tooasynchronous exemplaar kunnen worden gegenereerd. Hallo aanbevolen benadering toouse is deze optie in een Azure-VM in Hallo dezelfde regio bevinden als uw gegevensbron account tooavoid uitgaande opslagkosten.

## <a name="file-download"></a>Bestand: downloaden
### <a name="download-single-file"></a>Enkel bestand downloaden

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Als Hallo bron is een Azure-bestandsshare opgegeven, moet u de exacte bestandsnaam hello, opgeven (*bijvoorbeeld* `abc.txt`) toodownload één bestand of de optie `--recursive` toodownload alle bestanden in de share Hallo recursief. Toospecify poging een patroon en de optie `--recursive` samen resulteert in een fout opgetreden.

### <a name="download-all-files"></a>Alle bestanden downloaden

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Alle lege mappen zijn niet gedownload.

## <a name="file-upload"></a>Bestand: uploaden
### <a name="upload-single-file"></a>Bestand uploaden

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a>Alle bestanden uploaden

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

Houd er rekening mee dat alle lege mappen niet worden geüpload.

### <a name="upload-files-matching-specified-pattern"></a>Uploaden van bestanden die overeenkomen met opgegeven patroon

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a>Bestand: kopiëren
### <a name="copy-across-file-shares"></a>Kopiëren via bestandsshares

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Wanneer u een bestand via bestandsshares kopiëren, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.

### <a name="copy-from-file-share-tooblob"></a>Kopiëren van bestandsshare tooblob

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Wanneer u een bestand vanuit bestandsshare tooblob kopiëren, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.

### <a name="copy-from-blob-toofile-share"></a>Kopiëren van blob toofile share

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Wanneer u een bestand van blob toofile share kopiëren, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.

### <a name="synchronously-copy-files"></a>Synchroon bestanden kopiëren
U kunt opgeven dat Hallo `--sync-copy` toocopy gegevens uit de File Storage tooFile opslag, van File Storage tooBlob opslag en Blob Storage tooFile opslag synchroon optie. Deze bewerking AzCopy uitgevoerd door te downloaden van Hallo bron gegevens toolocal geheugen en uploadt deze toodestination. In dit geval de standaard uitgaande kosten van toepassing.

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

Bij het kopiëren van File Storage tooBlob opslag, Hallo standaard blob-type blok-blob is, optie kunt u opgeven `/BlobType:page` toochange Hallo doeltype blob.

Houd er rekening mee dat `--sync-copy` extra uitgaande vergelijken tooasynchronous kopie kosten kunnen genereren. Hallo aanbevolen benadering toouse is deze optie in een Azure-VM in Hallo dezelfde regio bevinden als uw gegevensbron account tooavoid uitgaande opslagkosten.

## <a name="other-azcopy-features"></a>Andere functies van AzCopy
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Alleen gegevens die niet in het Hallo-doel bestaat gekopieerd
Hallo `--exclude-older` en `--exclude-newer` parameters kunt u tooexclude oudere of nieuwere bron resources wordt gekopieerd, respectievelijk. Als u alleen toocopy bron bronnen die niet bestaan in Hallo bestemming wilt, kunt u beide parameters in Hallo AzCopy-opdracht:

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a>Gebruik een bestand toospecify opdrachtregelprogramma configuratieparameters

```azcopy
azcopy --config-file "azcopy-config.ini"
```

U kunt eventuele opdrachtregelparameters AzCopy opnemen in een configuratiebestand. AzCopy processen Hallo parameters in Hallo bestand alsof ze op de opdrachtregel hello, uitvoeren van een directe vervanging met Hallo inhoud van Hallo bestand had is opgegeven.

Stel een configuratiebestand met de naam `copyoperation`, die Hallo volgende regels bevat. Elke parameter AzCopy kan worden opgegeven op één regel.

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

of op afzonderlijke regels:

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

AzCopy mislukt als u de parameter Hallo over twee regels verdelen, zoals hier wordt weergegeven voor Hallo `--source-key` parameter:

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a>Geef een shared access signature (SAS)

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

U kunt ook een SAS voor Hallo container URI opgeven:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

AzCopy momenteel alleen ondersteuning voor Hallo [Account-SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).

### <a name="journal-file-folder"></a>Map voor logboek-bestand
Telkens wanneer die u een tooAzCopy opdracht de opdracht die wordt gecontroleerd of een journal-bestand in de standaardmap Hallo bestaat en of deze bestaat in een map die u hebt opgegeven via deze optie. Hallo journaalbestand bestaat niet op beide plaatsen, AzCopy Hallo bewerking behandelt als nieuwe als genereert een nieuw journaalbestand.

Als Hallo journal-bestand bestaat, wordt door AzCopy gecontroleerd of Hallo-opdrachtregel die ingevoerde overeenkomt met Hallo vanaf de opdrachtregel in Hallo journal-bestand. Als twee opdrachtregels Hallo overeenkomen, hervat AzCopy onvolledige Hallo-bewerking. Als ze niet overeenkomen, vraagt AzCopy gebruiker tooeither overschrijven Hallo journaal bestand toostart een nieuwe bewerking of toocancel Hallo huidige bewerking.

Als u wilt dat toouse Hallo-standaardlocatie voor Hallo journal-bestand:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

Als u de optie weglaat `--resume`, of geef de optie `--resume` zonder Hallo mappad, zoals hierboven, AzCopy maakt Hallo journal-bestand in Hallo standaardlocatie is `~\Microsoft\Azure\AzCopy`. Als Hallo journaalbestand al bestaat, hervat AzCopy Hallo-bewerking op basis van Hallo journal-bestand.

Als u wilt dat een aangepaste locatie voor Hallo journaalbestand toospecify:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

In dit voorbeeld maakt Hallo journal-bestand als deze niet al bestaat. Als deze bestaat, hervat AzCopy Hallo-bewerking op basis van Hallo journal-bestand.

Als u wilt dat een bewerking AzCopy tooresume, herhaalt u dezelfde opdracht Hallo. AzCopy op Linux vervolgens wordt om bevestiging gevraagd:

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a>Uitgebreide uitvoer-Logboeken

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Geef het aantal gelijktijdige bewerkingen toostart Hallo
Optie `--parallel-level` geeft het aantal gelijktijdige kopieerbewerkingen Hallo. AzCopy wordt standaard een bepaald aantal gelijktijdige bewerkingen tooincrease Hallo-gegevensdoorvoer overdracht gestart. het aantal gelijktijdige bewerkingen Hallo is gelijk acht keer Hallo aantal processors dat u hebt. Als u via een netwerk met lage bandbreedte AzCopy uitvoert, kunt u een lager getal voor--parallel niveau tooavoid mislukt, omdat resource concurrentie opgeven.

[!TIP]
>tooview hello volledige lijst van AzCopy-parameters, bekijk 'azcopy--help-menu.

## <a name="known-issues-and-best-practices"></a>Bekende problemen en aanbevolen procedures
### <a name="error-net-core-is-not-found-in-hello-system"></a>Fout: .NET Core is niet gevonden in Hallo-systeem.
Als u een foutmelding weergegeven dat .NET Core niet is geïnstalleerd in Hallo systeem tegenkomt, Hallo pad toohello .NET Core binair `dotnet` ontbreekt.

In order tooaddress dit probleem, Hallo .NET Core binair niet vinden in het Hallo-systeem:
```bash
sudo find / -name dotnet
```

Dit retourneert Hallo pad toohello dotnet binaire. 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

Voeg nu deze padvariabele toohello-pad. Voor sudo, secure_path toocontain Hallo pad toohello dotnet binaire te bewerken:
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

In dit voorbeeld secure_path variabele worden gelezen:

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

Bewerken voor de huidige gebruiker hello,.bash_profile/.profile tooinclude Hallo pad toohello dotnet binaire in padvariabele 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

Controleer of .NET Core nu in pad:
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a>Fout bij het installeren van AzCopy
Als u problemen met de installatie van AzCopy, u kunt proberen het toorun AzCopy met Hallo bash script in Hallo uitgepakt `azcopy` map.

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a>Limiet voor gelijktijdige schrijfbewerkingen tijdens het kopiëren van gegevens
Als u blobs of bestanden met AzCopy kopieert, houd er rekening mee dat een andere toepassing Hallo gegevens heeft terwijl u kopieert. Indien mogelijk, zorg dat u kopieert Hallo-gegevens niet wordt gewijzigd tijdens de kopieerbewerking Hallo. Bijvoorbeeld bij het kopiëren van een VHD die is gekoppeld aan een virtuele machine van Azure, zorg dat er geen andere toepassingen toohello VHD momenteel schrijft. Een goede manier toodo die deze wordt door het Hallo resource toobe leasing gekopieerd. U kunt ook eerst een momentopname van Hallo VHD maken en vervolgens kopieert Hallo momentopname.

Als u niet voorkomen andere toepassingen dat bij het schrijven van tooblobs of bestanden terwijl ze worden gekopieerd en vervolgens Houd er rekening mee dat door Hallo tijd Hallo taak is voltooid, hello gekopieerde resources niet meer mogelijk volledige pariteit met Hallo bron resources.

### <a name="run-one-azcopy-instance-on-one-machine"></a>Één AzCopy-sessie uitvoeren op één computer.
AzCopy is ontworpen toomaximize Hallo gebruik van uw machine resource tooaccelerate Hallo gegevens worden overgedragen, is het raadzaam u slechts één exemplaar van AzCopy uitvoeren op één machine en geef Hallo optie `--parallel-level` als u meer gelijktijdige bewerkingen nodig. Typ voor meer informatie `AzCopy --help parallel-level` op Hallo-opdrachtregel.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over Azure Storage en AzCopy Hallo resources te volgen:

### <a name="azure-storage-documentation"></a>Documentatie bij Azure Storage:
* [Inleiding tooAzure opslag](storage-introduction.md)
* [Een opslagaccount maken](storage-create-storage-account.md)
* [BLOB Storage Explorer beheren](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [Hello Azure CLI 2.0 gebruiken met Azure Storage](storage-azure-cli.md)
* [Hoe toouse C++ Blob-opslag](storage-c-plus-plus-how-to-use-blobs.md)
* [Hoe toouse Blob-opslag met Java](storage-java-how-to-use-blob-storage.md)
* [Hoe toouse Blob-opslag met Node.js](storage-nodejs-how-to-use-blob-storage.md)
* [Hoe toouse Blob-opslag met Python](storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a>Azure Storage-blogberichten:
* [AzCopy aangekondigd op Linux-Preview](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [Inleiding tot Azure Storage Data Movement bibliotheek-Preview](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: Introducing synchrone kopiëren en aangepaste type inhoud](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: Aangekondigd algemene beschikbaarheid van AzCopy 3.0 plus preview-versie van AzCopy 4.0 met de ondersteuning voor de tabel en de bestandsnaam](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: Geoptimaliseerd voor grootschalige kopie scenario 's](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy: Ondersteuning voor geografisch redundante opslag met leestoegang](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy: Gegevensoverdracht met modus voor opnieuw starten en SAS-token](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [AzCopy: Cross-account kopiëren Blob met behulp](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: Uploaden/downloaden van bestanden voor Azure Blobs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

