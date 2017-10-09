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
ms.openlocfilehash: ee39c311d996a046999b7fd4a4eb873f25b4eb86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="5a6cd-105">Gegevensoverdracht met AzCopy op Linux</span><span class="sxs-lookup"><span data-stu-id="5a6cd-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="5a6cd-106">AzCopy op Linux is een opdrachtregelprogramma dat is ontworpen voor het kopiëren van gegevens tooand van Microsoft Azure Blob- en bestandsopslag met eenvoudige opdrachten met optimale prestaties.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-106">AzCopy on Linux is a command-line utility designed for copying data tooand from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="5a6cd-107">U kunt gegevens kopiëren van een object tooanother binnen uw opslagaccount of tussen opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="5a6cd-108">Er zijn twee versies van AzCopy die u kunt downloaden.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="5a6cd-109">AzCopy op Linux is gebouwd met .NET Core Framework dat gericht is op Linux-platforms biedt POSIX-stijl opdrachtregelopties.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="5a6cd-110">[AzCopy op Windows](../storage-use-azcopy.md) is gebouwd met .NET Framework en Windows-stijl biedt opdrachtregelopties.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-110">[AzCopy on Windows](../storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="5a6cd-111">In dit artikel bevat informatie over AzCopy op Linux.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="5a6cd-112">Downloaden en installeren van AzCopy</span><span class="sxs-lookup"><span data-stu-id="5a6cd-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="5a6cd-113">Installatie op Linux</span><span class="sxs-lookup"><span data-stu-id="5a6cd-113">Installation on Linux</span></span>

<span data-ttu-id="5a6cd-114">AzCopy op Linux vereist .NET Core framework op Hallo-platform.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-114">AzCopy on Linux requires .NET Core framework on hello platform.</span></span> <span data-ttu-id="5a6cd-115">Zie de installatie-instructies Hallo op Hallo [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) pagina.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-115">See hello installation instructions on hello [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="5a6cd-116">Installeer .NET Core op Ubuntu 16,10 als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="5a6cd-117">Voor het meest recente installatiehandleiding hello, gaat u naar [.NET Core op Linux](https://www.microsoft.com/net/core#linuxubuntu) op de installatiepagina.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-117">For hello latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="5a6cd-118">Als u .NET Core hebt geïnstalleerd, downloaden en installeren van AzCopy.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="5a6cd-119">Nadat AzCopy op Linux is geïnstalleerd, kunt u bestanden hebt uitgepakt Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-119">You can remove hello extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="5a6cd-120">Als u geen supergebruiker bevoegdheden, kunt u ook ook uitvoeren met behulp van de shell-script Hallo AzCopy 'azcopy' in de uitgepakte map Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using hello shell script 'azcopy' in hello extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="5a6cd-121">Alternatieve installatie op Ubuntu</span><span class="sxs-lookup"><span data-stu-id="5a6cd-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="5a6cd-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="5a6cd-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="5a6cd-123">Apt-bron toevoegen voor .net Core:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="5a6cd-124">Apt bron voor Linux Microsoft product opslagplaats toevoegen en AzCopy installeren:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="5a6cd-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="5a6cd-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="5a6cd-126">Apt-bron toevoegen voor .net Core:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="5a6cd-127">Apt bron voor Linux Microsoft product opslagplaats toevoegen en AzCopy installeren:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="5a6cd-128">**Ubuntu 16,10**</span><span class="sxs-lookup"><span data-stu-id="5a6cd-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="5a6cd-129">Apt-bron toevoegen voor .net Core:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="5a6cd-130">Apt bron voor Linux Microsoft product opslagplaats toevoegen en AzCopy installeren:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="5a6cd-131">Schrijven van uw eerste AzCopy-opdracht</span><span class="sxs-lookup"><span data-stu-id="5a6cd-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="5a6cd-132">Hallo basic syntaxis voor opdrachten van AzCopy is:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-132">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="5a6cd-133">Hallo volgen voorbeelden laten zien dat verschillende scenario's voor het kopiëren van gegevens tooand van Microsoft Azure Blobs en bestanden.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-133">hello following examples demonstrate various scenarios for copying data tooand from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="5a6cd-134">Raadpleeg toohello `azcopy --help` menu voor een gedetailleerde beschrijving van het Hallo-parameters die worden gebruikt in elk voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-134">Refer toohello `azcopy --help` menu for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="5a6cd-135">BLOB: downloaden</span><span class="sxs-lookup"><span data-stu-id="5a6cd-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="5a6cd-136">Enkele blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="5a6cd-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="5a6cd-137">Als Hallo map `/mnt/myfiles` niet bestaat, AzCopy wordt deze gemaakt en gedownload `abc.txt ` in Hallo nieuwe map.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-137">If hello folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="5a6cd-138">Downloaden van één blob van de secundaire regio</span><span class="sxs-lookup"><span data-stu-id="5a6cd-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="5a6cd-139">Houd er rekening mee dat u geografisch redundante opslag met leestoegang ingeschakeld nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="5a6cd-140">Alle blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="5a6cd-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="5a6cd-141">Wordt ervan uitgegaan dat de volgende Hallo BLOB's zich bevinden in de opgegeven container Hallo:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-141">Assume hello following blobs reside in hello specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="5a6cd-142">Na de bewerking van de download hello, Hallo directory `/mnt/myfiles` omvat Hallo volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-142">After hello download operation, hello directory `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="5a6cd-143">Als u geen optie opgeeft `--recursive`, geen blob worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="5a6cd-144">Blobs met het opgegeven voorvoegsel downloaden</span><span class="sxs-lookup"><span data-stu-id="5a6cd-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="5a6cd-145">Wordt ervan uitgegaan dat de volgende Hallo BLOB's zich bevinden in de opgegeven container Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-145">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="5a6cd-146">Alle blobs vanaf Hallo voorvoegsel `a` worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-146">All blobs beginning with hello prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="5a6cd-147">Na de bewerking van de download hello, Hallo map `/mnt/myfiles` bevat Hallo volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-147">After hello download operation, hello folder `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="5a6cd-148">Hallo-voorvoegsel is van toepassing toohello virtuele map, die Hallo eerste deel van Hallo blob-naam uitmaakt.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-148">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="5a6cd-149">In het bovenstaande voorbeeld Hallo, Hallo virtuele map komt niet overeen met het opgegeven voorvoegsel hello, dus geen blob wordt gedownload.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-149">In hello example shown above, hello virtual directory does not match hello specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="5a6cd-150">Bovendien, als hello optie `--recursive` niet is opgegeven, AzCopy biedt niet alle blobs downloaden.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-150">In addition, if hello option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="5a6cd-151">Hallo tijd laatste wijziging van de geëxporteerde bestanden toobe instellen hetzelfde als de bron blobs Hallo</span><span class="sxs-lookup"><span data-stu-id="5a6cd-151">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="5a6cd-152">U kunt ook BLOB's uitsluiten van Hallo downloaden van de bewerking op basis van hun tijd voor het laatst is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-152">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="5a6cd-153">Bijvoorbeeld, als u tooexclude blobs waarvan laatst gewijzigd-tijd Hallo dezelfde of een nieuwer is dan het doelbestand hello wilt is, toevoegen Hallo `--exclude-newer` optie:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-153">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="5a6cd-154">Of als u tooexclude blobs waarvan laatst gewijzigd-tijd Hallo dezelfde of een ouder is dan het doelbestand hello wilt is, toe te voegen Hallo `--exclude-older` optie:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-154">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="5a6cd-155">BLOB: uploaden</span><span class="sxs-lookup"><span data-stu-id="5a6cd-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="5a6cd-156">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="5a6cd-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="5a6cd-157">Als Hallo opgegeven bestemmingscontainer niet bestaat, AzCopy wordt deze gemaakt en uploads Hallo bestand in de App.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-157">If hello specified destination container does not exist, AzCopy creates it and uploads hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="5a6cd-158">Enkel bestand toovirtual directory uploaden</span><span class="sxs-lookup"><span data-stu-id="5a6cd-158">Upload single file toovirtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="5a6cd-159">Als Hallo virtuele map bestaat niet opgegeven, AzCopy Hallo bestand tooinclude Hallo virtuele map in de blob-naam Hallo uploadt (*bijvoorbeeld*, `vd/abc.txt` in bovenstaande Hallo voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="5a6cd-159">If hello specified virtual directory does not exist, AzCopy uploads hello file tooinclude hello virtual directory in hello blob name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="5a6cd-160">Alle bestanden uploaden</span><span class="sxs-lookup"><span data-stu-id="5a6cd-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="5a6cd-161">Optie `--recursive` uploads Hallo inhoud Hallo opgegeven directory tooBlob opslag recursief, wat betekent dat alle submappen en de bestanden ook worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-161">Specifying option `--recursive` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="5a6cd-162">Voor het exemplaar wordt ervan uitgegaan dat de volgende Hallo bestanden bevinden zich in map `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-162">For instance, assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="5a6cd-163">Na het Hallo-uploadbewerking bevat Hallo container Hallo volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-163">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="5a6cd-164">Wanneer Hallo optie `--recursive` niet is opgegeven, alleen hello volgende drie bestanden worden geüpload:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-164">When hello option `--recursive` is not specified, only hello following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="5a6cd-165">Uploaden van bestanden die overeenkomen met opgegeven patroon</span><span class="sxs-lookup"><span data-stu-id="5a6cd-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="5a6cd-166">Wordt ervan uitgegaan dat de volgende Hallo bestanden bevinden zich in map `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-166">Assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="5a6cd-167">Na het Hallo-uploadbewerking bevat Hallo container Hallo volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-167">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="5a6cd-168">Wanneer Hallo optie `--recursive` niet is opgegeven, AzCopy slaat bestanden in submappen:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-168">When hello option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="5a6cd-169">Geef Hallo MIME-inhoudstype van een bestemmings-blob</span><span class="sxs-lookup"><span data-stu-id="5a6cd-169">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="5a6cd-170">Standaard stelt AzCopy Hallo-inhoudstype van een bestemmings-blob te`application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-170">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="5a6cd-171">U kunt echter expliciet opgeven Hallo inhoudstype via Hallo-optie `--set-content-type [content-type]`.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-171">However, you can explicitly specify hello content type via hello option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="5a6cd-172">Deze syntaxis wordt Hallo inhoudstype voor alle blobs in een uploadbewerking.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-172">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="5a6cd-173">Als hello optie `--set-content-type` is opgegeven zonder een waarde worden AzCopy elke blob of bestand stelt het type inhoud op basis van tooits bestandsextensie.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-173">If hello option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according tooits file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="5a6cd-174">BLOB: kopiëren</span><span class="sxs-lookup"><span data-stu-id="5a6cd-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="5a6cd-175">Één blob binnen opslagaccount kopiëren</span><span class="sxs-lookup"><span data-stu-id="5a6cd-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="5a6cd-176">Wanneer u een blob zonder--gesynchroniseerde kopie-optie, kopieert een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="5a6cd-177">Één blob kopiëren tussen opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="5a6cd-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="5a6cd-178">Wanneer u een blob zonder--gesynchroniseerde kopie-optie, kopieert een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="5a6cd-179">Één blob kopiëren van de secundaire regio tooprimary regio</span><span class="sxs-lookup"><span data-stu-id="5a6cd-179">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="5a6cd-180">Houd er rekening mee dat u geografisch redundante opslag met leestoegang ingeschakeld nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="5a6cd-181">Één blob en bijbehorende momentopnamen kopiëren tussen opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="5a6cd-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="5a6cd-182">Na de kopieerbewerking hello omvat doelcontainer Hallo Hallo blob en het bijbehorende momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-182">After hello copy operation, hello target container includes hello blob and its snapshots.</span></span> <span data-ttu-id="5a6cd-183">Hallo container omvat Hallo volgende blob en het bijbehorende momentopnamen:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-183">hello container includes hello following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="5a6cd-184">Synchroon kopiëren van BLOB's tussen opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="5a6cd-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="5a6cd-185">AzCopy standaard worden de gegevens tussen de twee eindpunten voor opslag asynchroon gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="5a6cd-186">Daarom Hallo kopie-bewerking wordt uitgevoerd op Hallo achtergrond met behulp van ongebruikte bandbreedtecapaciteit die geen SLA in termen van hoe snel een blob heeft wordt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-186">Therefore, hello copy operation runs in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="5a6cd-187">Hallo `--sync-copy` optie zorgt ervoor dat de kopieerbewerking Hallo consistente snelheid opgehaald.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-187">hello `--sync-copy` option ensures that hello copy operation gets consistent speed.</span></span> <span data-ttu-id="5a6cd-188">AzCopy voert synchrone kopie Hallo Hallo blobs downloaden toocopy van Hallo opgegeven bron toolocal geheugen en uploadt deze toohello Blob-opslaglocatie.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-188">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="5a6cd-189">`--sync-copy`Als u meer uitgaande kosten vergeleken tooasynchronous exemplaar kunnen worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-189">`--sync-copy` might generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="5a6cd-190">Hallo aanbevolen benadering toouse is deze optie in een Azure-VM in Hallo dezelfde regio bevinden als uw gegevensbron account tooavoid uitgaande opslagkosten.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-190">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="5a6cd-191">Bestand: downloaden</span><span class="sxs-lookup"><span data-stu-id="5a6cd-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="5a6cd-192">Enkel bestand downloaden</span><span class="sxs-lookup"><span data-stu-id="5a6cd-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="5a6cd-193">Als Hallo bron is een Azure-bestandsshare opgegeven, moet u de exacte bestandsnaam hello, opgeven (*bijvoorbeeld* `abc.txt`) toodownload één bestand of de optie `--recursive` toodownload alle bestanden in de share Hallo recursief.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-193">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `--recursive` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="5a6cd-194">Toospecify poging een patroon en de optie `--recursive` samen resulteert in een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-194">Attempting toospecify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="5a6cd-195">Alle bestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="5a6cd-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="5a6cd-196">Alle lege mappen zijn niet gedownload.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="5a6cd-197">Bestand: uploaden</span><span class="sxs-lookup"><span data-stu-id="5a6cd-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="5a6cd-198">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="5a6cd-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="5a6cd-199">Alle bestanden uploaden</span><span class="sxs-lookup"><span data-stu-id="5a6cd-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="5a6cd-200">Houd er rekening mee dat alle lege mappen niet worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="5a6cd-201">Uploaden van bestanden die overeenkomen met opgegeven patroon</span><span class="sxs-lookup"><span data-stu-id="5a6cd-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="5a6cd-202">Bestand: kopiëren</span><span class="sxs-lookup"><span data-stu-id="5a6cd-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="5a6cd-203">Kopiëren via bestandsshares</span><span class="sxs-lookup"><span data-stu-id="5a6cd-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="5a6cd-204">Wanneer u een bestand via bestandsshares kopiëren, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="5a6cd-205">Kopiëren van bestandsshare tooblob</span><span class="sxs-lookup"><span data-stu-id="5a6cd-205">Copy from file share tooblob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="5a6cd-206">Wanneer u een bestand vanuit bestandsshare tooblob kopiëren, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-206">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="5a6cd-207">Kopiëren van blob toofile share</span><span class="sxs-lookup"><span data-stu-id="5a6cd-207">Copy from blob toofile share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="5a6cd-208">Wanneer u een bestand van blob toofile share kopiëren, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-208">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="5a6cd-209">Synchroon bestanden kopiëren</span><span class="sxs-lookup"><span data-stu-id="5a6cd-209">Synchronously copy files</span></span>
<span data-ttu-id="5a6cd-210">U kunt opgeven dat Hallo `--sync-copy` toocopy gegevens uit de File Storage tooFile opslag, van File Storage tooBlob opslag en Blob Storage tooFile opslag synchroon optie.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-210">You can specify hello `--sync-copy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously.</span></span> <span data-ttu-id="5a6cd-211">Deze bewerking AzCopy uitgevoerd door te downloaden van Hallo bron gegevens toolocal geheugen en uploadt deze toodestination.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-211">AzCopy runs this operation by downloading hello source data toolocal memory, and then uploading it toodestination.</span></span> <span data-ttu-id="5a6cd-212">In dit geval de standaard uitgaande kosten van toepassing.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="5a6cd-213">Bij het kopiëren van File Storage tooBlob opslag, Hallo standaard blob-type blok-blob is, optie kunt u opgeven `/BlobType:page` toochange Hallo doeltype blob.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-213">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="5a6cd-214">Houd er rekening mee dat `--sync-copy` extra uitgaande vergelijken tooasynchronous kopie kosten kunnen genereren.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-214">Note that `--sync-copy` might generate additional egress cost comparing tooasynchronous copy.</span></span> <span data-ttu-id="5a6cd-215">Hallo aanbevolen benadering toouse is deze optie in een Azure-VM in Hallo dezelfde regio bevinden als uw gegevensbron account tooavoid uitgaande opslagkosten.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-215">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="5a6cd-216">Andere functies van AzCopy</span><span class="sxs-lookup"><span data-stu-id="5a6cd-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="5a6cd-217">Alleen gegevens die niet in het Hallo-doel bestaat gekopieerd</span><span class="sxs-lookup"><span data-stu-id="5a6cd-217">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="5a6cd-218">Hallo `--exclude-older` en `--exclude-newer` parameters kunt u tooexclude oudere of nieuwere bron resources wordt gekopieerd, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-218">hello `--exclude-older` and `--exclude-newer` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="5a6cd-219">Als u alleen toocopy bron bronnen die niet bestaan in Hallo bestemming wilt, kunt u beide parameters in Hallo AzCopy-opdracht:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-219">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a><span data-ttu-id="5a6cd-220">Gebruik een bestand toospecify opdrachtregelprogramma configuratieparameters</span><span class="sxs-lookup"><span data-stu-id="5a6cd-220">Use a configuration file toospecify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="5a6cd-221">U kunt eventuele opdrachtregelparameters AzCopy opnemen in een configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="5a6cd-222">AzCopy processen Hallo parameters in Hallo bestand alsof ze op de opdrachtregel hello, uitvoeren van een directe vervanging met Hallo inhoud van Hallo bestand had is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-222">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="5a6cd-223">Stel een configuratiebestand met de naam `copyoperation`, die Hallo volgende regels bevat.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-223">Assume a configuration file named `copyoperation`, that contains hello following lines.</span></span> <span data-ttu-id="5a6cd-224">Elke parameter AzCopy kan worden opgegeven op één regel.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="5a6cd-225">of op afzonderlijke regels:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="5a6cd-226">AzCopy mislukt als u de parameter Hallo over twee regels verdelen, zoals hier wordt weergegeven voor Hallo `--source-key` parameter:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-226">AzCopy fails if you split hello parameter across two lines, as shown here for hello `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="5a6cd-227">Geef een shared access signature (SAS)</span><span class="sxs-lookup"><span data-stu-id="5a6cd-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="5a6cd-228">U kunt ook een SAS voor Hallo container URI opgeven:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-228">You can also specify a SAS on hello container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="5a6cd-229">AzCopy momenteel alleen ondersteuning voor Hallo [Account-SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="5a6cd-229">Note that AzCopy currently only supports hello [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="5a6cd-230">Map voor logboek-bestand</span><span class="sxs-lookup"><span data-stu-id="5a6cd-230">Journal file folder</span></span>
<span data-ttu-id="5a6cd-231">Telkens wanneer die u een tooAzCopy opdracht de opdracht die wordt gecontroleerd of een journal-bestand in de standaardmap Hallo bestaat en of deze bestaat in een map die u hebt opgegeven via deze optie.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-231">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="5a6cd-232">Hallo journaalbestand bestaat niet op beide plaatsen, AzCopy Hallo bewerking behandelt als nieuwe als genereert een nieuw journaalbestand.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-232">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="5a6cd-233">Als Hallo journal-bestand bestaat, wordt door AzCopy gecontroleerd of Hallo-opdrachtregel die ingevoerde overeenkomt met Hallo vanaf de opdrachtregel in Hallo journal-bestand.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-233">If hello journal file does exist, AzCopy checks whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="5a6cd-234">Als twee opdrachtregels Hallo overeenkomen, hervat AzCopy onvolledige Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-234">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="5a6cd-235">Als ze niet overeenkomen, vraagt AzCopy gebruiker tooeither overschrijven Hallo journaal bestand toostart een nieuwe bewerking of toocancel Hallo huidige bewerking.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-235">If they do not match, AzCopy prompts user tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="5a6cd-236">Als u wilt dat toouse Hallo-standaardlocatie voor Hallo journal-bestand:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-236">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="5a6cd-237">Als u de optie weglaat `--resume`, of geef de optie `--resume` zonder Hallo mappad, zoals hierboven, AzCopy maakt Hallo journal-bestand in Hallo standaardlocatie is `~\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-237">If you omit option `--resume`, or specify option `--resume` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="5a6cd-238">Als Hallo journaalbestand al bestaat, hervat AzCopy Hallo-bewerking op basis van Hallo journal-bestand.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-238">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="5a6cd-239">Als u wilt dat een aangepaste locatie voor Hallo journaalbestand toospecify:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-239">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="5a6cd-240">In dit voorbeeld maakt Hallo journal-bestand als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-240">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="5a6cd-241">Als deze bestaat, hervat AzCopy Hallo-bewerking op basis van Hallo journal-bestand.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-241">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="5a6cd-242">Als u wilt dat een bewerking AzCopy tooresume, herhaalt u dezelfde opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-242">If you want tooresume an AzCopy operation, repeat hello same command.</span></span> <span data-ttu-id="5a6cd-243">AzCopy op Linux vervolgens wordt om bevestiging gevraagd:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="5a6cd-244">Uitgebreide uitvoer-Logboeken</span><span class="sxs-lookup"><span data-stu-id="5a6cd-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="5a6cd-245">Geef het aantal gelijktijdige bewerkingen toostart Hallo</span><span class="sxs-lookup"><span data-stu-id="5a6cd-245">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="5a6cd-246">Optie `--parallel-level` geeft het aantal gelijktijdige kopieerbewerkingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-246">Option `--parallel-level` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="5a6cd-247">AzCopy wordt standaard een bepaald aantal gelijktijdige bewerkingen tooincrease Hallo-gegevensdoorvoer overdracht gestart.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-247">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="5a6cd-248">het aantal gelijktijdige bewerkingen Hallo is gelijk acht keer Hallo aantal processors dat u hebt.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-248">hello number of concurrent operations is equal eight times hello number of processors you have.</span></span> <span data-ttu-id="5a6cd-249">Als u via een netwerk met lage bandbreedte AzCopy uitvoert, kunt u een lager getal voor--parallel niveau tooavoid mislukt, omdat resource concurrentie opgeven.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level tooavoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="5a6cd-250">tooview hello volledige lijst van AzCopy-parameters, bekijk 'azcopy--help-menu.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-250">tooview hello complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="5a6cd-251">Bekende problemen en aanbevolen procedures</span><span class="sxs-lookup"><span data-stu-id="5a6cd-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-hello-system"></a><span data-ttu-id="5a6cd-252">Fout: .NET Core is niet gevonden in Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-252">Error: .NET Core is not found in hello system.</span></span>
<span data-ttu-id="5a6cd-253">Als u een foutmelding weergegeven dat .NET Core niet is geïnstalleerd in Hallo systeem tegenkomt, Hallo pad toohello .NET Core binair `dotnet` ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-253">If you encounter an error stating that .NET Core is not installed in hello system, hello PATH toohello .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="5a6cd-254">In order tooaddress dit probleem, Hallo .NET Core binair niet vinden in het Hallo-systeem:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-254">In order tooaddress this issue, find hello .NET Core binary in hello system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="5a6cd-255">Dit retourneert Hallo pad toohello dotnet binaire.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-255">This returns hello path toohello dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="5a6cd-256">Voeg nu deze padvariabele toohello-pad.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-256">Now add this path toohello PATH variable.</span></span> <span data-ttu-id="5a6cd-257">Voor sudo, secure_path toocontain Hallo pad toohello dotnet binaire te bewerken:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-257">For sudo, edit secure_path toocontain hello path toohello dotnet binary:</span></span>
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

<span data-ttu-id="5a6cd-258">In dit voorbeeld secure_path variabele worden gelezen:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="5a6cd-259">Bewerken voor de huidige gebruiker hello,.bash_profile/.profile tooinclude Hallo pad toohello dotnet binaire in padvariabele</span><span class="sxs-lookup"><span data-stu-id="5a6cd-259">For hello current user, edit .bash_profile/.profile tooinclude hello path toohello dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

<span data-ttu-id="5a6cd-260">Controleer of .NET Core nu in pad:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="5a6cd-261">Fout bij het installeren van AzCopy</span><span class="sxs-lookup"><span data-stu-id="5a6cd-261">Error Installing AzCopy</span></span>
<span data-ttu-id="5a6cd-262">Als u problemen met de installatie van AzCopy, u kunt proberen het toorun AzCopy met Hallo bash script in Hallo uitgepakt `azcopy` map.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-262">If you encounter issues with AzCopy installation, you may try toorun AzCopy using hello bash script in hello extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="5a6cd-263">Limiet voor gelijktijdige schrijfbewerkingen tijdens het kopiëren van gegevens</span><span class="sxs-lookup"><span data-stu-id="5a6cd-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="5a6cd-264">Als u blobs of bestanden met AzCopy kopieert, houd er rekening mee dat een andere toepassing Hallo gegevens heeft terwijl u kopieert.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="5a6cd-265">Indien mogelijk, zorg dat u kopieert Hallo-gegevens niet wordt gewijzigd tijdens de kopieerbewerking Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-265">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="5a6cd-266">Bijvoorbeeld bij het kopiëren van een VHD die is gekoppeld aan een virtuele machine van Azure, zorg dat er geen andere toepassingen toohello VHD momenteel schrijft.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="5a6cd-267">Een goede manier toodo die deze wordt door het Hallo resource toobe leasing gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-267">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="5a6cd-268">U kunt ook eerst een momentopname van Hallo VHD maken en vervolgens kopieert Hallo momentopname.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-268">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="5a6cd-269">Als u niet voorkomen andere toepassingen dat bij het schrijven van tooblobs of bestanden terwijl ze worden gekopieerd en vervolgens Houd er rekening mee dat door Hallo tijd Hallo taak is voltooid, hello gekopieerde resources niet meer mogelijk volledige pariteit met Hallo bron resources.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-269">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="5a6cd-270">Één AzCopy-sessie uitvoeren op één computer.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="5a6cd-271">AzCopy is ontworpen toomaximize Hallo gebruik van uw machine resource tooaccelerate Hallo gegevens worden overgedragen, is het raadzaam u slechts één exemplaar van AzCopy uitvoeren op één machine en geef Hallo optie `--parallel-level` als u meer gelijktijdige bewerkingen nodig.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-271">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="5a6cd-272">Typ voor meer informatie `AzCopy --help parallel-level` op Hallo-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="5a6cd-272">For more details, type `AzCopy --help parallel-level` at hello command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a6cd-273">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5a6cd-273">Next steps</span></span>
<span data-ttu-id="5a6cd-274">Zie voor meer informatie over Azure Storage en AzCopy Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-274">For more information about Azure Storage and AzCopy, see hello following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="5a6cd-275">Documentatie bij Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="5a6cd-276">Inleiding tooAzure opslag</span><span class="sxs-lookup"><span data-stu-id="5a6cd-276">Introduction tooAzure Storage</span></span>](../storage-introduction.md)
* [<span data-ttu-id="5a6cd-277">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="5a6cd-277">Create a storage account</span></span>](../storage-create-storage-account.md)
* [<span data-ttu-id="5a6cd-278">BLOB Storage Explorer beheren</span><span class="sxs-lookup"><span data-stu-id="5a6cd-278">Manage blobs with Storage Explorer</span></span>](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [<span data-ttu-id="5a6cd-279">Hello Azure CLI 2.0 gebruiken met Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5a6cd-279">Using hello Azure CLI 2.0 with Azure Storage</span></span>](../storage-azure-cli.md)
* [<span data-ttu-id="5a6cd-280">Hoe toouse C++ Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="5a6cd-280">How toouse Blob storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="5a6cd-281">Hoe toouse Blob-opslag met Java</span><span class="sxs-lookup"><span data-stu-id="5a6cd-281">How toouse Blob storage from Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="5a6cd-282">Hoe toouse Blob-opslag met Node.js</span><span class="sxs-lookup"><span data-stu-id="5a6cd-282">How toouse Blob storage from Node.js</span></span>](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="5a6cd-283">Hoe toouse Blob-opslag met Python</span><span class="sxs-lookup"><span data-stu-id="5a6cd-283">How toouse Blob storage from Python</span></span>](../blobs/storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="5a6cd-284">Azure Storage-blogberichten:</span><span class="sxs-lookup"><span data-stu-id="5a6cd-284">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="5a6cd-285">AzCopy aangekondigd op Linux-Preview</span><span class="sxs-lookup"><span data-stu-id="5a6cd-285">Announcing AzCopy on Linux Preview</span></span>](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [<span data-ttu-id="5a6cd-286">Inleiding tot Azure Storage Data Movement bibliotheek-Preview</span><span class="sxs-lookup"><span data-stu-id="5a6cd-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="5a6cd-287">AzCopy: Introducing synchrone kopiëren en aangepaste type inhoud</span><span class="sxs-lookup"><span data-stu-id="5a6cd-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="5a6cd-288">AzCopy: Aangekondigd algemene beschikbaarheid van AzCopy 3.0 plus preview-versie van AzCopy 4.0 met de ondersteuning voor de tabel en de bestandsnaam</span><span class="sxs-lookup"><span data-stu-id="5a6cd-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="5a6cd-289">AzCopy: Geoptimaliseerd voor grootschalige kopie scenario 's</span><span class="sxs-lookup"><span data-stu-id="5a6cd-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="5a6cd-290">AzCopy: Ondersteuning voor geografisch redundante opslag met leestoegang</span><span class="sxs-lookup"><span data-stu-id="5a6cd-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="5a6cd-291">AzCopy: Gegevensoverdracht met modus voor opnieuw starten en SAS-token</span><span class="sxs-lookup"><span data-stu-id="5a6cd-291">AzCopy: Transfer data with restartable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="5a6cd-292">AzCopy: Cross-account kopiëren Blob met behulp</span><span class="sxs-lookup"><span data-stu-id="5a6cd-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="5a6cd-293">AzCopy: Uploaden/downloaden van bestanden voor Azure Blobs</span><span class="sxs-lookup"><span data-stu-id="5a6cd-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

