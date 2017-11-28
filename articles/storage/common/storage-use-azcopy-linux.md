---
title: "Gegevens kopiëren of verplaatsen naar Azure Storage met AzCopy op Linux | Microsoft Docs"
description: "De AzCopy op Linux-hulpprogramma gebruiken om te verplaatsen of kopiëren van gegevens of naar blob- en -inhoud. Gegevens van lokale bestanden kopiëren naar Azure Storage of kopiëren van gegevens binnen of tussen opslagaccounts. Uw gegevens eenvoudig migreren naar Azure Storage."
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
ms.openlocfilehash: 441227d84b9c1ec721ae36fdc423ba797654f128
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="3c309-105">Gegevensoverdracht met AzCopy op Linux</span><span class="sxs-lookup"><span data-stu-id="3c309-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="3c309-106">AzCopy op Linux is een opdrachtregelprogramma dat is ontworpen voor het kopiëren van gegevens naar en van Microsoft Azure Blob- en bestandsopslag met eenvoudige opdrachten met optimale prestaties.</span><span class="sxs-lookup"><span data-stu-id="3c309-106">AzCopy on Linux is a command-line utility designed for copying data to and from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="3c309-107">U kunt gegevens van het ene object naar de andere kopiëren binnen uw opslagaccount of tussen opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="3c309-107">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="3c309-108">Er zijn twee versies van AzCopy die u kunt downloaden.</span><span class="sxs-lookup"><span data-stu-id="3c309-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="3c309-109">AzCopy op Linux is gebouwd met .NET Core Framework dat gericht is op Linux-platforms biedt POSIX-stijl opdrachtregelopties.</span><span class="sxs-lookup"><span data-stu-id="3c309-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="3c309-110">[AzCopy op Windows](../storage-use-azcopy.md) is gebouwd met .NET Framework en Windows-stijl biedt opdrachtregelopties.</span><span class="sxs-lookup"><span data-stu-id="3c309-110">[AzCopy on Windows](../storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="3c309-111">In dit artikel bevat informatie over AzCopy op Linux.</span><span class="sxs-lookup"><span data-stu-id="3c309-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="3c309-112">Downloaden en installeren van AzCopy</span><span class="sxs-lookup"><span data-stu-id="3c309-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="3c309-113">Installatie op Linux</span><span class="sxs-lookup"><span data-stu-id="3c309-113">Installation on Linux</span></span>

<span data-ttu-id="3c309-114">AzCopy op Linux vereist .NET Core framework van het platform.</span><span class="sxs-lookup"><span data-stu-id="3c309-114">AzCopy on Linux requires .NET Core framework on the platform.</span></span> <span data-ttu-id="3c309-115">Zie de installatie-instructies op de [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) pagina.</span><span class="sxs-lookup"><span data-stu-id="3c309-115">See the installation instructions on the [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="3c309-116">Installeer .NET Core op Ubuntu 16,10 als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="3c309-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="3c309-117">Voor de meest recente installatiehandleiding, gaat u naar [.NET Core op Linux](https://www.microsoft.com/net/core#linuxubuntu) op de installatiepagina.</span><span class="sxs-lookup"><span data-stu-id="3c309-117">For the latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="3c309-118">Als u .NET Core hebt geïnstalleerd, downloaden en installeren van AzCopy.</span><span class="sxs-lookup"><span data-stu-id="3c309-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="3c309-119">Nadat AzCopy op Linux is geïnstalleerd, kunt u de uitgepakte bestanden verwijderen.</span><span class="sxs-lookup"><span data-stu-id="3c309-119">You can remove the extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="3c309-120">Als u geen supergebruiker bevoegdheden, kunt u ook ook AzCopy met het shellscript 'azcopy' in de uitgepakte map uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3c309-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using the shell script 'azcopy' in the extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="3c309-121">Alternatieve installatie op Ubuntu</span><span class="sxs-lookup"><span data-stu-id="3c309-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="3c309-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="3c309-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="3c309-123">Apt-bron toevoegen voor .net Core:</span><span class="sxs-lookup"><span data-stu-id="3c309-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="3c309-124">Apt bron voor Linux Microsoft product opslagplaats toevoegen en AzCopy installeren:</span><span class="sxs-lookup"><span data-stu-id="3c309-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="3c309-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="3c309-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="3c309-126">Apt-bron toevoegen voor .net Core:</span><span class="sxs-lookup"><span data-stu-id="3c309-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="3c309-127">Apt bron voor Linux Microsoft product opslagplaats toevoegen en AzCopy installeren:</span><span class="sxs-lookup"><span data-stu-id="3c309-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="3c309-128">**Ubuntu 16,10**</span><span class="sxs-lookup"><span data-stu-id="3c309-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="3c309-129">Apt-bron toevoegen voor .net Core:</span><span class="sxs-lookup"><span data-stu-id="3c309-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="3c309-130">Apt bron voor Linux Microsoft product opslagplaats toevoegen en AzCopy installeren:</span><span class="sxs-lookup"><span data-stu-id="3c309-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="3c309-131">Schrijven van uw eerste AzCopy-opdracht</span><span class="sxs-lookup"><span data-stu-id="3c309-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="3c309-132">De algemene syntaxis voor opdrachten van AzCopy is:</span><span class="sxs-lookup"><span data-stu-id="3c309-132">The basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="3c309-133">De volgende voorbeelden worden de verschillende scenario's voor het kopiëren van gegevens naar en van Microsoft Azure Blobs en -bestanden.</span><span class="sxs-lookup"><span data-stu-id="3c309-133">The following examples demonstrate various scenarios for copying data to and from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="3c309-134">Raadpleeg de `azcopy --help` menu voor een gedetailleerde beschrijving van de parameters in elk voorbeeld gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3c309-134">Refer to the `azcopy --help` menu for a detailed explanation of the parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="3c309-135">BLOB: downloaden</span><span class="sxs-lookup"><span data-stu-id="3c309-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="3c309-136">Enkele blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="3c309-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="3c309-137">Als de map `/mnt/myfiles` niet bestaat, AzCopy wordt deze gemaakt en gedownload `abc.txt ` naar de nieuwe map.</span><span class="sxs-lookup"><span data-stu-id="3c309-137">If the folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into the new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="3c309-138">Downloaden van één blob van de secundaire regio</span><span class="sxs-lookup"><span data-stu-id="3c309-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="3c309-139">Houd er rekening mee dat u geografisch redundante opslag met leestoegang ingeschakeld nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="3c309-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="3c309-140">Alle blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="3c309-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="3c309-141">Stel dat de volgende BLOB's zich bevinden in de opgegeven container:</span><span class="sxs-lookup"><span data-stu-id="3c309-141">Assume the following blobs reside in the specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="3c309-142">Na het opnieuw downloaden, de map `/mnt/myfiles` bevat de volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="3c309-142">After the download operation, the directory `/mnt/myfiles` includes the following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="3c309-143">Als u geen optie opgeeft `--recursive`, geen blob worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="3c309-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="3c309-144">Blobs met het opgegeven voorvoegsel downloaden</span><span class="sxs-lookup"><span data-stu-id="3c309-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="3c309-145">Stel dat de volgende BLOB's zich bevinden in de opgegeven container.</span><span class="sxs-lookup"><span data-stu-id="3c309-145">Assume the following blobs reside in the specified container.</span></span> <span data-ttu-id="3c309-146">Alle blobs die beginnen met het voorvoegsel `a` worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="3c309-146">All blobs beginning with the prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="3c309-147">Na het opnieuw downloaden, de map `/mnt/myfiles` bevat de volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="3c309-147">After the download operation, the folder `/mnt/myfiles` includes the following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="3c309-148">Het voorvoegsel is van toepassing op de virtuele map die het eerste deel van de blob-naam.</span><span class="sxs-lookup"><span data-stu-id="3c309-148">The prefix applies to the virtual directory, which forms the first part of the blob name.</span></span> <span data-ttu-id="3c309-149">In het bovenstaande voorbeeld de virtuele map komt niet overeen met het opgegeven voorvoegsel, zodat geen blob wordt gedownload.</span><span class="sxs-lookup"><span data-stu-id="3c309-149">In the example shown above, the virtual directory does not match the specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="3c309-150">Bovendien, als de optie `--recursive` niet is opgegeven, AzCopy biedt niet alle blobs downloaden.</span><span class="sxs-lookup"><span data-stu-id="3c309-150">In addition, if the option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a><span data-ttu-id="3c309-151">De tijd laatste wijziging van de geëxporteerde bestanden moet hetzelfde zijn als de bron-blobs instellen</span><span class="sxs-lookup"><span data-stu-id="3c309-151">Set the last-modified time of exported files to be same as the source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="3c309-152">U kunt ook BLOB's uitsluiten van de downloadbewerking op basis van hun tijd voor het laatst is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="3c309-152">You can also exclude blobs from the download operation based on their last-modified time.</span></span> <span data-ttu-id="3c309-153">Bijvoorbeeld, als u wilt uitsluiten waarvan laatst gewijzigd om blobs is dezelfde of nieuwer is dan het doelbestand toevoegen de `--exclude-newer` optie:</span><span class="sxs-lookup"><span data-stu-id="3c309-153">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="3c309-154">Of als u wilt uitsluiten van blobs waarvan laatst gewijzigd om de dezelfde of een ouder is dan het doelbestand toevoegen de `--exclude-older` optie:</span><span class="sxs-lookup"><span data-stu-id="3c309-154">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="3c309-155">BLOB: uploaden</span><span class="sxs-lookup"><span data-stu-id="3c309-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="3c309-156">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="3c309-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="3c309-157">Als de opgegeven bestemming-container niet bestaat, wordt AzCopy maakt en uploadt het bestand in de App.</span><span class="sxs-lookup"><span data-stu-id="3c309-157">If the specified destination container does not exist, AzCopy creates it and uploads the file into it.</span></span>

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="3c309-158">Bestand uploaden naar virtuele map</span><span class="sxs-lookup"><span data-stu-id="3c309-158">Upload single file to virtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="3c309-159">Als de opgegeven virtuele map niet bestaat, AzCopy uploadt het bestand voor het opnemen van de virtuele map in de blob-naam (*bijvoorbeeld*, `vd/abc.txt` in het bovenstaande voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="3c309-159">If the specified virtual directory does not exist, AzCopy uploads the file to include the virtual directory in the blob name (*e.g.*, `vd/abc.txt` in the example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="3c309-160">Alle bestanden uploaden</span><span class="sxs-lookup"><span data-stu-id="3c309-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="3c309-161">Optie `--recursive` wordt de inhoud van de opgegeven map geüpload naar Blob storage recursief, wat betekent dat alle submappen en de bestanden ook worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="3c309-161">Specifying option `--recursive` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="3c309-162">Bijvoorbeeld, wordt ervan uitgegaan dat de volgende bestanden bevinden zich in map `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="3c309-162">For instance, assume the following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="3c309-163">Nadat de uploadbewerking van bevat de container de volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="3c309-163">After the upload operation, the container includes the following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="3c309-164">Wanneer de optie `--recursive` niet is opgegeven, worden alleen de volgende drie bestanden geüpload:</span><span class="sxs-lookup"><span data-stu-id="3c309-164">When the option `--recursive` is not specified, only the following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="3c309-165">Uploaden van bestanden die overeenkomen met opgegeven patroon</span><span class="sxs-lookup"><span data-stu-id="3c309-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="3c309-166">Wordt ervan uitgegaan dat de volgende bestanden bevinden zich in map `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="3c309-166">Assume the following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="3c309-167">Nadat de uploadbewerking van bevat de container de volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="3c309-167">After the upload operation, the container includes the following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="3c309-168">Wanneer de optie `--recursive` niet is opgegeven, AzCopy slaat bestanden in submappen:</span><span class="sxs-lookup"><span data-stu-id="3c309-168">When the option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="3c309-169">Geef het MIME-inhoudstype van een bestemmings-blob</span><span class="sxs-lookup"><span data-stu-id="3c309-169">Specify the MIME content type of a destination blob</span></span>
<span data-ttu-id="3c309-170">AzCopy wordt standaard ingesteld van het type inhoud van een bestemmings-blob naar `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="3c309-170">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span></span> <span data-ttu-id="3c309-171">U kunt echter expliciet opgeven het inhoudstype via de optie `--set-content-type [content-type]`.</span><span class="sxs-lookup"><span data-stu-id="3c309-171">However, you can explicitly specify the content type via the option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="3c309-172">Deze syntaxis wordt het type inhoud voor alle blobs in een uploadbewerking.</span><span class="sxs-lookup"><span data-stu-id="3c309-172">This syntax sets the content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="3c309-173">Als de optie `--set-content-type` is opgegeven zonder een waarde worden AzCopy elke blob of inhoudstype volgens de bestandsextensie van het bestand stelt.</span><span class="sxs-lookup"><span data-stu-id="3c309-173">If the option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according to its file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="3c309-174">BLOB: kopiëren</span><span class="sxs-lookup"><span data-stu-id="3c309-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="3c309-175">Één blob binnen opslagaccount kopiëren</span><span class="sxs-lookup"><span data-stu-id="3c309-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="3c309-176">Wanneer u een blob zonder--gesynchroniseerde kopie-optie, kopieert een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3c309-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="3c309-177">Één blob kopiëren tussen opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="3c309-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="3c309-178">Wanneer u een blob zonder--gesynchroniseerde kopie-optie, kopieert een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3c309-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a><span data-ttu-id="3c309-179">Kopiëren van één blob van de secundaire regio naar primaire regio</span><span class="sxs-lookup"><span data-stu-id="3c309-179">Copy single blob from secondary region to primary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="3c309-180">Houd er rekening mee dat u geografisch redundante opslag met leestoegang ingeschakeld nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="3c309-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="3c309-181">Één blob en bijbehorende momentopnamen kopiëren tussen opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="3c309-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="3c309-182">Na de kopieerbewerking omvat de doelcontainer de blob en bijbehorende momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="3c309-182">After the copy operation, the target container includes the blob and its snapshots.</span></span> <span data-ttu-id="3c309-183">De container bevat de volgende blob en bijbehorende momentopnamen:</span><span class="sxs-lookup"><span data-stu-id="3c309-183">The container includes the following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="3c309-184">Synchroon kopiëren van BLOB's tussen opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="3c309-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="3c309-185">AzCopy standaard worden de gegevens tussen de twee eindpunten voor opslag asynchroon gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="3c309-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="3c309-186">Daarom wordt de kopie-bewerking wordt uitgevoerd op de achtergrond met behulp van ongebruikte bandbreedtecapaciteit die geen SLA in termen van hoe snel een blob heeft gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="3c309-186">Therefore, the copy operation runs in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="3c309-187">De `--sync-copy` optie zorgt ervoor dat de kopieerbewerking consistente snelheid opgehaald.</span><span class="sxs-lookup"><span data-stu-id="3c309-187">The `--sync-copy` option ensures that the copy operation gets consistent speed.</span></span> <span data-ttu-id="3c309-188">AzCopy voert de synchrone kopie door te downloaden van de blobs kopiëren vanuit de opgegeven bron naar lokaal geheugen en vervolgens uploaden naar de bestemming van Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="3c309-188">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="3c309-189">`--sync-copy`Als u meer uitgaande kosten vergeleken met de asynchrone exemplaar kunnen worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="3c309-189">`--sync-copy` might generate additional egress cost compared to asynchronous copy.</span></span> <span data-ttu-id="3c309-190">De aanbevolen aanpak is het gebruik van deze optie in een Azure VM, die zich in dezelfde regio bevinden als uw storage-account van de bron om te voorkomen dat de kosten voor uitgaande gegevens.</span><span class="sxs-lookup"><span data-stu-id="3c309-190">The recommended approach is to use this option in an Azure VM, that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="3c309-191">Bestand: downloaden</span><span class="sxs-lookup"><span data-stu-id="3c309-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="3c309-192">Enkel bestand downloaden</span><span class="sxs-lookup"><span data-stu-id="3c309-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="3c309-193">Als de opgegeven bron een Azure-bestandsshare is en vervolgens moet u de exacte bestandsnaam opgeven (*bijvoorbeeld* `abc.txt`) moeten worden gedownload van één bestand of de optie `--recursive` om alle bestanden in de share recursief te downloaden.</span><span class="sxs-lookup"><span data-stu-id="3c309-193">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `--recursive` to download all files in the share recursively.</span></span> <span data-ttu-id="3c309-194">Poging een patroon en de optie opgeven `--recursive` samen resulteert in een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="3c309-194">Attempting to specify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="3c309-195">Alle bestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="3c309-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="3c309-196">Alle lege mappen zijn niet gedownload.</span><span class="sxs-lookup"><span data-stu-id="3c309-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="3c309-197">Bestand: uploaden</span><span class="sxs-lookup"><span data-stu-id="3c309-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="3c309-198">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="3c309-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="3c309-199">Alle bestanden uploaden</span><span class="sxs-lookup"><span data-stu-id="3c309-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="3c309-200">Houd er rekening mee dat alle lege mappen niet worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="3c309-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="3c309-201">Uploaden van bestanden die overeenkomen met opgegeven patroon</span><span class="sxs-lookup"><span data-stu-id="3c309-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="3c309-202">Bestand: kopiëren</span><span class="sxs-lookup"><span data-stu-id="3c309-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="3c309-203">Kopiëren via bestandsshares</span><span class="sxs-lookup"><span data-stu-id="3c309-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="3c309-204">Wanneer u een bestand via bestandsshares kopiëren, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3c309-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-to-blob"></a><span data-ttu-id="3c309-205">Kopiëren van de bestandsshare naar de blob</span><span class="sxs-lookup"><span data-stu-id="3c309-205">Copy from file share to blob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="3c309-206">Wanneer u een bestand vanuit de bestandsshare kopiëren naar de blob, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3c309-206">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-to-file-share"></a><span data-ttu-id="3c309-207">Kopiëren van blob naar de bestandsshare</span><span class="sxs-lookup"><span data-stu-id="3c309-207">Copy from blob to file share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="3c309-208">Wanneer u een bestand van blob naar de bestandsshare kopiëren, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3c309-208">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="3c309-209">Synchroon bestanden kopiëren</span><span class="sxs-lookup"><span data-stu-id="3c309-209">Synchronously copy files</span></span>
<span data-ttu-id="3c309-210">U kunt opgeven de `--sync-copy` optie om gegevens te kopiëren van File Storage File Storage, uit de opslag van bestanden naar Blob Storage en naar Blob Storage tot bestandsopslag synchroon.</span><span class="sxs-lookup"><span data-stu-id="3c309-210">You can specify the `--sync-copy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously.</span></span> <span data-ttu-id="3c309-211">Deze bewerking AzCopy uitgevoerd door de brongegevens downloaden naar het lokale geheugen en vervolgens uploaden naar de bestemming.</span><span class="sxs-lookup"><span data-stu-id="3c309-211">AzCopy runs this operation by downloading the source data to local memory, and then uploading it to destination.</span></span> <span data-ttu-id="3c309-212">In dit geval de standaard uitgaande kosten van toepassing.</span><span class="sxs-lookup"><span data-stu-id="3c309-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="3c309-213">Bij het kopiëren van de opslag van bestanden naar Blob Storage, de standaard blob-type blok-blob is, optie kunt u opgeven `/BlobType:page` blob doeltype wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3c309-213">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span></span>

<span data-ttu-id="3c309-214">Houd er rekening mee dat `--sync-copy` extra uitgaande kosten vergelijken met het asynchrone kopie kan genereren.</span><span class="sxs-lookup"><span data-stu-id="3c309-214">Note that `--sync-copy` might generate additional egress cost comparing to asynchronous copy.</span></span> <span data-ttu-id="3c309-215">De aanbevolen aanpak is het gebruik van deze optie in een Azure VM, die zich in dezelfde regio bevinden als uw storage-account van de bron om te voorkomen dat de kosten voor uitgaande gegevens.</span><span class="sxs-lookup"><span data-stu-id="3c309-215">The recommended approach is to use this option in an Azure VM, that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="3c309-216">Andere functies van AzCopy</span><span class="sxs-lookup"><span data-stu-id="3c309-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a><span data-ttu-id="3c309-217">Alleen gegevens die niet in de doel bestaat-gekopieerd</span><span class="sxs-lookup"><span data-stu-id="3c309-217">Only copy data that doesn't exist in the destination</span></span>
<span data-ttu-id="3c309-218">De `--exclude-older` en `--exclude-newer` parameters kunt u oudere of nieuwere bron resources uitsluiten wordt gekopieerd, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="3c309-218">The `--exclude-older` and `--exclude-newer` parameters allow you to exclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="3c309-219">Als u wilt kopiëren van de bron-resources die niet bestaan in de doel-, kunt u beide parameters in de AzCopy-opdracht opgeven:</span><span class="sxs-lookup"><span data-stu-id="3c309-219">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-to-specify-command-line-parameters"></a><span data-ttu-id="3c309-220">Gebruik een configuratiebestand om op te geven van opdrachtregelparameters</span><span class="sxs-lookup"><span data-stu-id="3c309-220">Use a configuration file to specify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="3c309-221">U kunt eventuele opdrachtregelparameters AzCopy opnemen in een configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="3c309-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="3c309-222">AzCopy verwerkt de parameters in het bestand alsof ze had is opgegeven op de opdrachtregel voor het uitvoeren van een directe vervanging met de inhoud van het bestand.</span><span class="sxs-lookup"><span data-stu-id="3c309-222">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span></span>

<span data-ttu-id="3c309-223">Stel een configuratiebestand met de naam `copyoperation`, die de volgende regels bevat.</span><span class="sxs-lookup"><span data-stu-id="3c309-223">Assume a configuration file named `copyoperation`, that contains the following lines.</span></span> <span data-ttu-id="3c309-224">Elke parameter AzCopy kan worden opgegeven op één regel.</span><span class="sxs-lookup"><span data-stu-id="3c309-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="3c309-225">of op afzonderlijke regels:</span><span class="sxs-lookup"><span data-stu-id="3c309-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="3c309-226">AzCopy mislukt als u de parameter over twee regels verdelen, zoals hier wordt weergegeven voor de `--source-key` parameter:</span><span class="sxs-lookup"><span data-stu-id="3c309-226">AzCopy fails if you split the parameter across two lines, as shown here for the `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="3c309-227">Geef een shared access signature (SAS)</span><span class="sxs-lookup"><span data-stu-id="3c309-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="3c309-228">U kunt ook een SAS voor de container URI opgeven:</span><span class="sxs-lookup"><span data-stu-id="3c309-228">You can also specify a SAS on the container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="3c309-229">Let op: AzCopy momenteel alleen ondersteunt de [Account-SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="3c309-229">Note that AzCopy currently only supports the [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="3c309-230">Map voor logboek-bestand</span><span class="sxs-lookup"><span data-stu-id="3c309-230">Journal file folder</span></span>
<span data-ttu-id="3c309-231">Telkens wanneer die u een opdracht met AzCopy geven, controleert deze of een journal-bestand in de standaardmap bestaat en of deze bestaat in een map die u hebt opgegeven via deze optie.</span><span class="sxs-lookup"><span data-stu-id="3c309-231">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="3c309-232">De wijzigingslogboek-bestand bestaat niet op beide plaatsen, AzCopy wordt de bewerking wordt beschouwd als nieuwe als genereert een nieuw journaalbestand.</span><span class="sxs-lookup"><span data-stu-id="3c309-232">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="3c309-233">Als het journaalbestand bestaat, controleert AzCopy of de opdrachtregel die ingevoerde overeenkomt met de opdrachtregel in het logboek-bestand.</span><span class="sxs-lookup"><span data-stu-id="3c309-233">If the journal file does exist, AzCopy checks whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="3c309-234">Als de twee opdrachtregels overeenkomen, hervat AzCopy de bewerking niet voltooid.</span><span class="sxs-lookup"><span data-stu-id="3c309-234">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="3c309-235">Als ze niet overeenkomen, wordt AzCopy gebruiker of het journaalbestand te overschrijven naar een nieuwe bewerking starten of de huidige bewerking te annuleren.</span><span class="sxs-lookup"><span data-stu-id="3c309-235">If they do not match, AzCopy prompts user to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="3c309-236">Als u de standaardlocatie voor het wijzigingslogboek-bestand gebruiken wilt:</span><span class="sxs-lookup"><span data-stu-id="3c309-236">If you want to use the default location for the journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="3c309-237">Als u de optie weglaat `--resume`, of geef de optie `--resume` zonder het mappad, zoals hierboven, AzCopy wijzigingslogboek wordt het bestand gemaakt op de standaardlocatie `~\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="3c309-237">If you omit option `--resume`, or specify option `--resume` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="3c309-238">Als het wijzigingslogboek bestand al bestaat, hervat de bewerking op basis van het journaalbestand met AzCopy.</span><span class="sxs-lookup"><span data-stu-id="3c309-238">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="3c309-239">Als u een aangepaste locatie voor het wijzigingslogboek-bestand opgeven wilt:</span><span class="sxs-lookup"><span data-stu-id="3c309-239">If you want to specify a custom location for the journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="3c309-240">In dit voorbeeld wordt het journaalbestand als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="3c309-240">This example creates the journal file if it does not already exist.</span></span> <span data-ttu-id="3c309-241">Als deze bestaat, hervat de bewerking op basis van het journaalbestand met AzCopy.</span><span class="sxs-lookup"><span data-stu-id="3c309-241">If it does exist, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="3c309-242">Als u een bewerking AzCopy hervatten wilt, herhaalt u dezelfde opdracht.</span><span class="sxs-lookup"><span data-stu-id="3c309-242">If you want to resume an AzCopy operation, repeat the same command.</span></span> <span data-ttu-id="3c309-243">AzCopy op Linux vervolgens wordt om bevestiging gevraagd:</span><span class="sxs-lookup"><span data-stu-id="3c309-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at the journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want to resume the operation? Choose Yes to resume, choose No to overwrite the journal to start a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="3c309-244">Uitgebreide uitvoer-Logboeken</span><span class="sxs-lookup"><span data-stu-id="3c309-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-the-number-of-concurrent-operations-to-start"></a><span data-ttu-id="3c309-245">Geef het aantal gelijktijdige bewerkingen starten</span><span class="sxs-lookup"><span data-stu-id="3c309-245">Specify the number of concurrent operations to start</span></span>
<span data-ttu-id="3c309-246">Optie `--parallel-level` geeft het aantal gelijktijdige te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="3c309-246">Option `--parallel-level` specifies the number of concurrent copy operations.</span></span> <span data-ttu-id="3c309-247">AzCopy wordt standaard een bepaald aantal gelijktijdige bewerkingen te verhogen van de overdracht gegevensdoorvoer gestart.</span><span class="sxs-lookup"><span data-stu-id="3c309-247">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="3c309-248">Het aantal gelijktijdige bewerkingen gelijk is 8 maal het aantal processors dat u hebt.</span><span class="sxs-lookup"><span data-stu-id="3c309-248">The number of concurrent operations is equal eight times the number of processors you have.</span></span> <span data-ttu-id="3c309-249">Als u via een netwerk met lage bandbreedte AzCopy uitvoert, kunt u een lager getal voor--parallel-niveau om te voorkomen dat mislukt, omdat resource concurrentie opgeven.</span><span class="sxs-lookup"><span data-stu-id="3c309-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level to avoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="3c309-250">Bekijk de volledige lijst van AzCopy parameters wilt weergeven, 'azcopy--help-menu.</span><span class="sxs-lookup"><span data-stu-id="3c309-250">To view the complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="3c309-251">Bekende problemen en aanbevolen procedures</span><span class="sxs-lookup"><span data-stu-id="3c309-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-the-system"></a><span data-ttu-id="3c309-252">Fout: .NET Core is niet gevonden in het systeem.</span><span class="sxs-lookup"><span data-stu-id="3c309-252">Error: .NET Core is not found in the system.</span></span>
<span data-ttu-id="3c309-253">Als u een foutmelding weergegeven dat .NET Core niet is geïnstalleerd in het systeem, het pad naar de binary .NET Core ondervindt `dotnet` ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="3c309-253">If you encounter an error stating that .NET Core is not installed in the system, the PATH to the .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="3c309-254">Om dit probleem kunt oplossen, vindt u de .NET Core binaire in het systeem:</span><span class="sxs-lookup"><span data-stu-id="3c309-254">In order to address this issue, find the .NET Core binary in the system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="3c309-255">Dit retourneert het pad naar de dotnet binaire.</span><span class="sxs-lookup"><span data-stu-id="3c309-255">This returns the path to the dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="3c309-256">Nu dit pad toevoegen aan de padvariabele.</span><span class="sxs-lookup"><span data-stu-id="3c309-256">Now add this path to the PATH variable.</span></span> <span data-ttu-id="3c309-257">Voor sudo, secure_path bevat het pad naar de binaire dotnet te bewerken:</span><span class="sxs-lookup"><span data-stu-id="3c309-257">For sudo, edit secure_path to contain the path to the dotnet binary:</span></span>
```bash 
sudo visudo
### Append the path found in the preceding example to 'secure_path' variable
```

<span data-ttu-id="3c309-258">In dit voorbeeld secure_path variabele worden gelezen:</span><span class="sxs-lookup"><span data-stu-id="3c309-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="3c309-259">Voor de huidige gebruiker bewerken.bash_profile/.profile zodanig dat het pad naar de binaire in padvariabele dotnet</span><span class="sxs-lookup"><span data-stu-id="3c309-259">For the current user, edit .bash_profile/.profile to include the path to the dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append the path found in the preceding example to 'PATH' variable
```

<span data-ttu-id="3c309-260">Controleer of .NET Core nu in pad:</span><span class="sxs-lookup"><span data-stu-id="3c309-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="3c309-261">Fout bij het installeren van AzCopy</span><span class="sxs-lookup"><span data-stu-id="3c309-261">Error Installing AzCopy</span></span>
<span data-ttu-id="3c309-262">Als u problemen met de installatie van AzCopy, u kunt proberen om uit te voeren met de bash-script in de uitgepakte AzCopy `azcopy` map.</span><span class="sxs-lookup"><span data-stu-id="3c309-262">If you encounter issues with AzCopy installation, you may try to run AzCopy using the bash script in the extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="3c309-263">Limiet voor gelijktijdige schrijfbewerkingen tijdens het kopiëren van gegevens</span><span class="sxs-lookup"><span data-stu-id="3c309-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="3c309-264">Als u blobs of bestanden met AzCopy kopieert, houd er rekening mee dat een andere toepassing de gegevens heeft terwijl u kopieert.</span><span class="sxs-lookup"><span data-stu-id="3c309-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span></span> <span data-ttu-id="3c309-265">Indien mogelijk, zorg dat de gegevens die u wilt kopiëren niet tijdens de kopieerbewerking wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="3c309-265">If possible, ensure that the data you are copying is not being modified during the copy operation.</span></span> <span data-ttu-id="3c309-266">Bijvoorbeeld bij het kopiëren van een VHD die is gekoppeld aan een virtuele machine van Azure, zorg dat er geen andere toepassingen momenteel voor de VHD schrijft.</span><span class="sxs-lookup"><span data-stu-id="3c309-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span></span> <span data-ttu-id="3c309-267">Een goede manier om dit te doen is door het leasen van de resource te worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="3c309-267">A good way to do this is by leasing the resource to be copied.</span></span> <span data-ttu-id="3c309-268">U kunt ook eerst een momentopname van de VHD maken en kopieer de momentopname.</span><span class="sxs-lookup"><span data-stu-id="3c309-268">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span></span>

<span data-ttu-id="3c309-269">Als u niet voorkomen andere toepassingen dat bij het schrijven naar blobs of bestanden, terwijl ze worden gekopieerd, klikt u vervolgens Houd er rekening mee dat op het moment dat de taak is voltooid, de gekopieerde resources niet meer mogelijk volledige pariteit met de bron-resources.</span><span class="sxs-lookup"><span data-stu-id="3c309-269">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="3c309-270">Één AzCopy-sessie uitvoeren op één computer.</span><span class="sxs-lookup"><span data-stu-id="3c309-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="3c309-271">AzCopy is ontworpen om u te maximaliseren van uw machinebron de gegevensoverdracht versnellen, is het raadzaam u slechts één exemplaar van AzCopy uitvoeren op één machine en selecteer de optie `--parallel-level` als u meer gelijktijdige bewerkingen nodig.</span><span class="sxs-lookup"><span data-stu-id="3c309-271">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="3c309-272">Typ voor meer informatie `AzCopy --help parallel-level` op de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="3c309-272">For more details, type `AzCopy --help parallel-level` at the command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c309-273">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3c309-273">Next steps</span></span>
<span data-ttu-id="3c309-274">Zie de volgende bronnen voor meer informatie over Azure Storage en AzCopy:</span><span class="sxs-lookup"><span data-stu-id="3c309-274">For more information about Azure Storage and AzCopy, see the following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="3c309-275">Documentatie bij Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="3c309-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="3c309-276">Inleiding tot Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3c309-276">Introduction to Azure Storage</span></span>](../storage-introduction.md)
* [<span data-ttu-id="3c309-277">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="3c309-277">Create a storage account</span></span>](../storage-create-storage-account.md)
* [<span data-ttu-id="3c309-278">BLOB Storage Explorer beheren</span><span class="sxs-lookup"><span data-stu-id="3c309-278">Manage blobs with Storage Explorer</span></span>](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [<span data-ttu-id="3c309-279">De Azure CLI 2.0 gebruiken met Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3c309-279">Using the Azure CLI 2.0 with Azure Storage</span></span>](../storage-azure-cli.md)
* [<span data-ttu-id="3c309-280">Het Blob storage gebruiken met C++</span><span class="sxs-lookup"><span data-stu-id="3c309-280">How to use Blob storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="3c309-281">Blob Storage gebruiken met Java</span><span class="sxs-lookup"><span data-stu-id="3c309-281">How to use Blob storage from Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="3c309-282">Blob Storage gebruiken met Node.js</span><span class="sxs-lookup"><span data-stu-id="3c309-282">How to use Blob storage from Node.js</span></span>](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="3c309-283">Blob Storage gebruiken met Python</span><span class="sxs-lookup"><span data-stu-id="3c309-283">How to use Blob storage from Python</span></span>](../blobs/storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="3c309-284">Azure Storage-blogberichten:</span><span class="sxs-lookup"><span data-stu-id="3c309-284">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="3c309-285">AzCopy aangekondigd op Linux-Preview</span><span class="sxs-lookup"><span data-stu-id="3c309-285">Announcing AzCopy on Linux Preview</span></span>](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [<span data-ttu-id="3c309-286">Inleiding tot Azure Storage Data Movement bibliotheek-Preview</span><span class="sxs-lookup"><span data-stu-id="3c309-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="3c309-287">AzCopy: Introducing synchrone kopiëren en aangepaste type inhoud</span><span class="sxs-lookup"><span data-stu-id="3c309-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="3c309-288">AzCopy: Aangekondigd algemene beschikbaarheid van AzCopy 3.0 plus preview-versie van AzCopy 4.0 met de ondersteuning voor de tabel en de bestandsnaam</span><span class="sxs-lookup"><span data-stu-id="3c309-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="3c309-289">AzCopy: Geoptimaliseerd voor grootschalige kopie scenario 's</span><span class="sxs-lookup"><span data-stu-id="3c309-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="3c309-290">AzCopy: Ondersteuning voor geografisch redundante opslag met leestoegang</span><span class="sxs-lookup"><span data-stu-id="3c309-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="3c309-291">AzCopy: Gegevensoverdracht met modus voor opnieuw starten en SAS-token</span><span class="sxs-lookup"><span data-stu-id="3c309-291">AzCopy: Transfer data with restartable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="3c309-292">AzCopy: Cross-account kopiëren Blob met behulp</span><span class="sxs-lookup"><span data-stu-id="3c309-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="3c309-293">AzCopy: Uploaden/downloaden van bestanden voor Azure Blobs</span><span class="sxs-lookup"><span data-stu-id="3c309-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

