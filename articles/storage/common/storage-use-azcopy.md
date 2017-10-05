---
title: "Gegevens kopiëren of verplaatsen naar Azure Storage met AzCopy in Windows | Microsoft Docs"
description: "De AzCopy op Windows-hulpprogramma gebruiken om te verplaatsen of kopiëren van gegevens of naar blob, table en de inhoud van bestand. Gegevens van lokale bestanden kopiëren naar Azure Storage of kopiëren van gegevens binnen of tussen opslagaccounts. Uw gegevens eenvoudig migreren naar Azure Storage."
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
ms.openlocfilehash: 9806697747b2409d4bd0ae19dc0b9fe01f500dc0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="transfer-data-with-the-azcopy-on-windows"></a><span data-ttu-id="10539-105">Gegevensoverdracht met het AzCopy in Windows</span><span class="sxs-lookup"><span data-stu-id="10539-105">Transfer data with the AzCopy on Windows</span></span>
<span data-ttu-id="10539-106">AzCopy is een opdrachtregelprogramma dat is ontworpen voor het kopiëren van gegevens naar en van Microsoft Azure Blob-, bestands- en tabel opslag met behulp van eenvoudige opdrachten met optimale prestaties.</span><span class="sxs-lookup"><span data-stu-id="10539-106">AzCopy is a command-line utility designed for copying data to and from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="10539-107">U kunt gegevens van het ene object naar de andere kopiëren binnen uw opslagaccount of tussen opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="10539-107">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="10539-108">Er zijn twee versies van AzCopy die u kunt downloaden.</span><span class="sxs-lookup"><span data-stu-id="10539-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="10539-109">AzCopy in Windows is gebouwd met .NET Framework en Windows-stijl biedt opdrachtregelopties.</span><span class="sxs-lookup"><span data-stu-id="10539-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="10539-110">[AzCopy op Linux](storage-use-azcopy-linux.md) is gebouwd met .NET Core Framework die gericht is op Linux-platforms biedt POSIX-stijl opdrachtregelopties.</span><span class="sxs-lookup"><span data-stu-id="10539-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="10539-111">In dit artikel bevat informatie over AzCopy in Windows.</span><span class="sxs-lookup"><span data-stu-id="10539-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="10539-112">Downloaden en installeren van AzCopy</span><span class="sxs-lookup"><span data-stu-id="10539-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="10539-113">AzCopy in Windows</span><span class="sxs-lookup"><span data-stu-id="10539-113">AzCopy on Windows</span></span>
<span data-ttu-id="10539-114">Download de [meest recente versie van AzCopy op Windows](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="10539-114">Download the [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="10539-115">Installatie op Windows</span><span class="sxs-lookup"><span data-stu-id="10539-115">Installation on Windows</span></span>
<span data-ttu-id="10539-116">Na de installatie van AzCopy op Windows met behulp van het installatieprogramma, open een opdrachtvenster en navigeer naar de installatiemap van AzCopy op uw computer - waar de `AzCopy.exe` uitvoerbare bestand zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="10539-116">After installing AzCopy on Windows using the installer, open a command window and navigate to the AzCopy installation directory on your computer - where the `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="10539-117">Indien gewenst, kunt u de installatielocatie van AzCopy toevoegen aan het systeempad.</span><span class="sxs-lookup"><span data-stu-id="10539-117">If desired, you can add the AzCopy installation location to your system path.</span></span> <span data-ttu-id="10539-118">AzCopy is standaard geïnstalleerd te `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` of `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="10539-118">By default, AzCopy is installed to `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="10539-119">Schrijven van uw eerste AzCopy-opdracht</span><span class="sxs-lookup"><span data-stu-id="10539-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="10539-120">De algemene syntaxis voor opdrachten van AzCopy is:</span><span class="sxs-lookup"><span data-stu-id="10539-120">The basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="10539-121">De volgende voorbeelden ziet een aantal scenario's voor het kopiëren van gegevens naar en van Microsoft Azure Blobs, bestanden en tabellen.</span><span class="sxs-lookup"><span data-stu-id="10539-121">The following examples demonstrate a variety of scenarios for copying data to and from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="10539-122">Raadpleeg de [AzCopy Parameters](#azcopy-parameters) sectie voor een gedetailleerde beschrijving van de parameters in elk voorbeeld gebruikt.</span><span class="sxs-lookup"><span data-stu-id="10539-122">Refer to the [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of the parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="10539-123">BLOB: downloaden</span><span class="sxs-lookup"><span data-stu-id="10539-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="10539-124">Enkele blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="10539-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="10539-125">Houd er rekening mee dat als de map `C:\myfolder` niet bestaat, AzCopy maakt het en downloaden `abc.txt ` naar de nieuwe map.</span><span class="sxs-lookup"><span data-stu-id="10539-125">Note that if the folder `C:\myfolder` does not exist, AzCopy creates it and download `abc.txt ` into the new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="10539-126">Downloaden van één blob van de secundaire regio</span><span class="sxs-lookup"><span data-stu-id="10539-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="10539-127">Houd er rekening mee dat u geografisch redundante opslag met leestoegang ingeschakeld nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="10539-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="10539-128">Alle blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="10539-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="10539-129">Stel dat de volgende BLOB's zich bevinden in de opgegeven container:</span><span class="sxs-lookup"><span data-stu-id="10539-129">Assume the following blobs reside in the specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="10539-130">Na het opnieuw downloaden, de map `C:\myfolder` bevat de volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="10539-130">After the download operation, the directory `C:\myfolder` includes the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="10539-131">Als u geen optie opgeeft `/S`, geen blobs worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="10539-131">If you do not specify option `/S`, no blobs are downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="10539-132">Blobs met het opgegeven voorvoegsel downloaden</span><span class="sxs-lookup"><span data-stu-id="10539-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="10539-133">Stel dat de volgende BLOB's zich bevinden in de opgegeven container.</span><span class="sxs-lookup"><span data-stu-id="10539-133">Assume the following blobs reside in the specified container.</span></span> <span data-ttu-id="10539-134">Alle blobs die beginnen met het voorvoegsel `a` worden gedownload:</span><span class="sxs-lookup"><span data-stu-id="10539-134">All blobs beginning with the prefix `a` are downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="10539-135">Na het opnieuw downloaden, de map `C:\myfolder` bevat de volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="10539-135">After the download operation, the folder `C:\myfolder` includes the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="10539-136">Het voorvoegsel is van toepassing op de virtuele map die het eerste deel van de blob-naam.</span><span class="sxs-lookup"><span data-stu-id="10539-136">The prefix applies to the virtual directory, which forms the first part of the blob name.</span></span> <span data-ttu-id="10539-137">In het bovenstaande voorbeeld de virtuele map komt niet overeen met het opgegeven voorvoegsel, zodat deze niet is gedownload.</span><span class="sxs-lookup"><span data-stu-id="10539-137">In the example shown above, the virtual directory does not match the specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="10539-138">Bovendien, als de optie `\S` niet is opgegeven, AzCopy biedt niet alle blobs downloaden.</span><span class="sxs-lookup"><span data-stu-id="10539-138">In addition, if the option `\S` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a><span data-ttu-id="10539-139">De tijd laatste wijziging van de geëxporteerde bestanden moet hetzelfde zijn als de bron-blobs instellen</span><span class="sxs-lookup"><span data-stu-id="10539-139">Set the last-modified time of exported files to be same as the source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="10539-140">U kunt ook BLOB's uitsluiten van de downloadbewerking op basis van hun tijd voor het laatst is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="10539-140">You can also exclude blobs from the download operation based on their last-modified time.</span></span> <span data-ttu-id="10539-141">Bijvoorbeeld, als u wilt uitsluiten waarvan laatst gewijzigd om blobs is dezelfde of nieuwer is dan het doelbestand toevoegen de `/XN` optie:</span><span class="sxs-lookup"><span data-stu-id="10539-141">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="10539-142">Of als u wilt uitsluiten van blobs waarvan laatst gewijzigd om de dezelfde of een ouder is dan het doelbestand toevoegen de `/XO` optie:</span><span class="sxs-lookup"><span data-stu-id="10539-142">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="10539-143">BLOB: uploaden</span><span class="sxs-lookup"><span data-stu-id="10539-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="10539-144">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="10539-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="10539-145">Als de opgegeven bestemming-container niet bestaat, wordt AzCopy maakt en uploadt het bestand in de App.</span><span class="sxs-lookup"><span data-stu-id="10539-145">If the specified destination container does not exist, AzCopy creates it and uploads the file into it.</span></span>

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="10539-146">Bestand uploaden naar virtuele map</span><span class="sxs-lookup"><span data-stu-id="10539-146">Upload single file to virtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="10539-147">Als de opgegeven virtuele map niet bestaat, AzCopy uploadt het bestand in de naam van de virtuele map (*bijvoorbeeld*, `vd/abc.txt` in het bovenstaande voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="10539-147">If the specified virtual directory does not exist, AzCopy uploads the file to include the virtual directory in its name (*e.g.*, `vd/abc.txt` in the example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="10539-148">Alle bestanden uploaden</span><span class="sxs-lookup"><span data-stu-id="10539-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="10539-149">Optie `/S` wordt de inhoud van de opgegeven map geüpload naar Blob storage recursief, wat betekent dat alle submappen en de bestanden ook worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="10539-149">Specifying option `/S` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="10539-150">Bijvoorbeeld, wordt ervan uitgegaan dat de volgende bestanden bevinden zich in map `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="10539-150">For instance, assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="10539-151">Nadat de uploadbewerking van bevat de container de volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="10539-151">After the upload operation, the container includes the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="10539-152">Als u geen optie opgeeft `/S`, AzCopy biedt recursief niet uploaden.</span><span class="sxs-lookup"><span data-stu-id="10539-152">If you do not specify option `/S`, AzCopy does not upload recursively.</span></span> <span data-ttu-id="10539-153">Nadat de uploadbewerking van bevat de container de volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="10539-153">After the upload operation, the container includes the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="10539-154">Uploaden van bestanden die overeenkomen met opgegeven patroon</span><span class="sxs-lookup"><span data-stu-id="10539-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="10539-155">Wordt ervan uitgegaan dat de volgende bestanden bevinden zich in map `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="10539-155">Assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="10539-156">Nadat de uploadbewerking van bevat de container de volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="10539-156">After the upload operation, the container includes the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="10539-157">Als u geen optie opgeeft `/S`, AzCopy uploadt alleen blobs die zich niet in een virtuele map bevinden:</span><span class="sxs-lookup"><span data-stu-id="10539-157">If you do not specify option `/S`, AzCopy only uploads blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="10539-158">Geef het MIME-inhoudstype van een bestemmings-blob</span><span class="sxs-lookup"><span data-stu-id="10539-158">Specify the MIME content type of a destination blob</span></span>
<span data-ttu-id="10539-159">AzCopy wordt standaard ingesteld van het type inhoud van een bestemmings-blob naar `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="10539-159">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span></span> <span data-ttu-id="10539-160">Vanaf versie 3.1.0, kunt u expliciet opgeven het inhoudstype via de optie `/SetContentType:[content-type]`.</span><span class="sxs-lookup"><span data-stu-id="10539-160">Beginning with version 3.1.0, you can explicitly specify the content type via the option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="10539-161">Deze syntaxis wordt het type inhoud voor alle blobs in een uploadbewerking.</span><span class="sxs-lookup"><span data-stu-id="10539-161">This syntax sets the content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="10539-162">Als u opgeeft `/SetContentType` zonder een waarde ingesteld AzCopy elke blob of inhoudstype volgens de bestandsextensie van het bestand.</span><span class="sxs-lookup"><span data-stu-id="10539-162">If you specify `/SetContentType` without a value, AzCopy sets each blob or file's content type according to its file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="10539-163">BLOB: kopiëren</span><span class="sxs-lookup"><span data-stu-id="10539-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="10539-164">Één blob binnen opslagaccount kopiëren</span><span class="sxs-lookup"><span data-stu-id="10539-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="10539-165">Wanneer u een blob binnen een opslagaccount kopieert een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="10539-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="10539-166">Één blob kopiëren tussen opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="10539-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="10539-167">Wanneer u een blob tussen opslagaccounts kopieert, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="10539-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a><span data-ttu-id="10539-168">Kopiëren van één blob van de secundaire regio naar primaire regio</span><span class="sxs-lookup"><span data-stu-id="10539-168">Copy single blob from secondary region to primary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="10539-169">Houd er rekening mee dat u geografisch redundante opslag met leestoegang ingeschakeld nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="10539-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="10539-170">Één blob en bijbehorende momentopnamen kopiëren tussen opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="10539-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="10539-171">Na de kopieerbewerking omvat de doelcontainer de blob en bijbehorende momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="10539-171">After the copy operation, the target container includes the blob and its snapshots.</span></span> <span data-ttu-id="10539-172">Ervan uitgaande dat de blob in het bovenstaande voorbeeld heeft twee momentopnamen, bevat de container de volgende blob en momentopnamen:</span><span class="sxs-lookup"><span data-stu-id="10539-172">Assuming the blob in the example above has two snapshots, the container includes the following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="10539-173">Synchroon kopiëren van BLOB's tussen opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="10539-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="10539-174">AzCopy standaard worden de gegevens tussen de twee eindpunten voor opslag asynchroon gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="10539-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="10539-175">Daarom de kopieerbewerking wordt uitgevoerd in de achtergrond met behulp van ongebruikte bandbreedtecapaciteit die geen SLA in termen van hoe u snel heeft een blob wordt gekopieerd en AzCopy controleert periodiek de status van het exemplaar totdat het kopiëren is voltooid of mislukt.</span><span class="sxs-lookup"><span data-stu-id="10539-175">Therefore, the copy operation runs in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied, and AzCopy periodically checks the copy status until the copying is completed or failed.</span></span>

<span data-ttu-id="10539-176">De `/SyncCopy` optie zorgt ervoor dat de kopieerbewerking consistente snelheid opgehaald.</span><span class="sxs-lookup"><span data-stu-id="10539-176">The `/SyncCopy` option ensures that the copy operation gets consistent speed.</span></span> <span data-ttu-id="10539-177">AzCopy voert de synchrone kopie door te downloaden van de blobs kopiëren vanuit de opgegeven bron naar lokaal geheugen en vervolgens uploaden naar de bestemming van Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="10539-177">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="10539-178">`/SyncCopy`kan extra uitgaande kosten vergeleken met de asynchrone kopiëren, de aanbevolen aanpak is deze optie wilt gebruiken in een Azure-virtuele machine die zich in dezelfde regio bevinden als uw storage-account van de bron om te voorkomen dat de kosten voor uitgaande gegevens.</span><span class="sxs-lookup"><span data-stu-id="10539-178">`/SyncCopy` might generate additional egress cost compared to asynchronous copy, the recommended approach is to use this option in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="10539-179">Bestand: downloaden</span><span class="sxs-lookup"><span data-stu-id="10539-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="10539-180">Enkel bestand downloaden</span><span class="sxs-lookup"><span data-stu-id="10539-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="10539-181">Als de opgegeven bron een Azure-bestandsshare is en vervolgens moet u de exacte bestandsnaam opgeven (*bijvoorbeeld* `abc.txt`) moeten worden gedownload van één bestand of de optie `/S` om alle bestanden in de share recursief te downloaden.</span><span class="sxs-lookup"><span data-stu-id="10539-181">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `/S` to download all files in the share recursively.</span></span> <span data-ttu-id="10539-182">Poging een patroon en de optie opgeven `/S` samen resulteert in een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="10539-182">Attempting to specify both a file pattern and option `/S` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="10539-183">Alle bestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="10539-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="10539-184">Alle lege mappen zijn niet gedownload.</span><span class="sxs-lookup"><span data-stu-id="10539-184">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="10539-185">Bestand: uploaden</span><span class="sxs-lookup"><span data-stu-id="10539-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="10539-186">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="10539-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="10539-187">Alle bestanden uploaden</span><span class="sxs-lookup"><span data-stu-id="10539-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="10539-188">Houd er rekening mee dat alle lege mappen niet worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="10539-188">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="10539-189">Uploaden van bestanden die overeenkomen met opgegeven patroon</span><span class="sxs-lookup"><span data-stu-id="10539-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="10539-190">Bestand: kopiëren</span><span class="sxs-lookup"><span data-stu-id="10539-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="10539-191">Kopiëren via bestandsshares</span><span class="sxs-lookup"><span data-stu-id="10539-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="10539-192">Wanneer u een bestand via bestandsshares kopiëren, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="10539-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-to-blob"></a><span data-ttu-id="10539-193">Kopiëren van de bestandsshare naar de blob</span><span class="sxs-lookup"><span data-stu-id="10539-193">Copy from file share to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="10539-194">Wanneer u een bestand vanuit de bestandsshare kopiëren naar de blob, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="10539-194">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-to-file-share"></a><span data-ttu-id="10539-195">Kopiëren van blob naar de bestandsshare</span><span class="sxs-lookup"><span data-stu-id="10539-195">Copy from blob to file share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="10539-196">Wanneer u een bestand van blob naar de bestandsshare kopiëren, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="10539-196">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="10539-197">Synchroon bestanden kopiëren</span><span class="sxs-lookup"><span data-stu-id="10539-197">Synchronously copy files</span></span>
<span data-ttu-id="10539-198">U kunt opgeven de `/SyncCopy` optie om gegevens te kopiëren van File Storage tot bestandsopslag, uit de opslag van bestanden naar Blob Storage en Blob Storage tot bestandsopslag synchroon, AzCopy doet dit door het downloaden van de brongegevens naar lokaal geheugen en opnieuw uploaden naar de bestemming.</span><span class="sxs-lookup"><span data-stu-id="10539-198">You can specify the `/SyncCopy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously, AzCopy does this by downloading the source data to local memory and upload it again to destination.</span></span> <span data-ttu-id="10539-199">Standaard uitgaande kosten worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="10539-199">Standard egress cost applies.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="10539-200">Bij het kopiëren van de opslag van bestanden naar Blob Storage, de standaard blob-type blok-blob is, optie kunt u opgeven `/BlobType:page` blob doeltype wijzigen.</span><span class="sxs-lookup"><span data-stu-id="10539-200">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span></span>

<span data-ttu-id="10539-201">Houd er rekening mee dat `/SyncCopy` kan extra uitgaande kosten vergelijken met het asynchrone kopiëren, de aanbevolen aanpak is deze optie wilt gebruiken in de Azure-virtuele machine die zich in dezelfde regio bevinden als uw storage-account van de bron om te voorkomen dat de kosten voor uitgaande gegevens.</span><span class="sxs-lookup"><span data-stu-id="10539-201">Note that `/SyncCopy` might generate additional egress cost comparing to asynchronous copy, the recommended approach is to use this option in the Azure VM which is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="10539-202">Tabel: exporteren</span><span class="sxs-lookup"><span data-stu-id="10539-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="10539-203">Tabel exporteren</span><span class="sxs-lookup"><span data-stu-id="10539-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="10539-204">Een manifestbestand schrijft AzCopy naar de opgegeven doelmap.</span><span class="sxs-lookup"><span data-stu-id="10539-204">AzCopy writes a manifest file to the specified destination folder.</span></span> <span data-ttu-id="10539-205">Het manifestbestand is gebruikt in het importproces voor de gegevens die nodig zijn bestanden vinden en voer gegevensvalidatie.</span><span class="sxs-lookup"><span data-stu-id="10539-205">The manifest file is used in the import process to locate the necessary data files and perform data validation.</span></span> <span data-ttu-id="10539-206">Het manifestbestand maakt standaard gebruik van de volgende naamconventie:</span><span class="sxs-lookup"><span data-stu-id="10539-206">The manifest file uses the following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="10539-207">Gebruiker kan ook de optie opgeven `/Manifest:<manifest file name>` kunt u de naam van het manifestbestand instellen.</span><span class="sxs-lookup"><span data-stu-id="10539-207">User can also specify the option `/Manifest:<manifest file name>` to set the manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="10539-208">De export splitsen in meerdere bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="10539-209">AzCopy gebruikt een *volume index* in de bestandsnamen van de gesplitste gegevens te onderscheiden van meerdere bestanden.</span><span class="sxs-lookup"><span data-stu-id="10539-209">AzCopy uses a *volume index* in the split data file names to distinguish multiple files.</span></span> <span data-ttu-id="10539-210">De index van het volume bestaat uit twee delen: een *partitie sleutel bereikindex* en een *gesplitste bestandsindex*.</span><span class="sxs-lookup"><span data-stu-id="10539-210">The volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="10539-211">Beide indexen zijn gebaseerd op nul.</span><span class="sxs-lookup"><span data-stu-id="10539-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="10539-212">Het partitioneren van index sleutel bereik is 0 als de gebruiker geen optie geeft `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="10539-212">The partition key range index is 0 if the user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="10539-213">Stel bijvoorbeeld twee gegevensbestanden van AzCopy wordt gegenereerd nadat de gebruiker Hiermee kunt u de optie `/SplitSize`.</span><span class="sxs-lookup"><span data-stu-id="10539-213">For instance, suppose AzCopy generates two data files after the user specifies option `/SplitSize`.</span></span> <span data-ttu-id="10539-214">De resulterende bestandsnamen van gegevens is mogelijk:</span><span class="sxs-lookup"><span data-stu-id="10539-214">The resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="10539-215">Let op: de minimale mogelijke waarde voor de optie `/SplitSize` is 32 MB.</span><span class="sxs-lookup"><span data-stu-id="10539-215">Note that the minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="10539-216">Als de opgegeven bestemming is Blob-opslag, AzCopy het gegevensbestand splitst zodra de grootte bereikt de blob-groottebeperkingen (200GB), ongeacht of optie `/SplitSize` is opgegeven door de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="10539-216">If the specified destination is Blob storage, AzCopy splits the data file once its sizes reaches the blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by the user.</span></span>

### <a name="export-table-to-json-or-csv-data-file-format"></a><span data-ttu-id="10539-217">De tabel exporteren naar JSON- of CSV-bestandsindeling voor gegevens</span><span class="sxs-lookup"><span data-stu-id="10539-217">Export table to JSON or CSV data file format</span></span>
<span data-ttu-id="10539-218">AzCopy standaard exporteert tabellen naar JSON-gegevensbestanden.</span><span class="sxs-lookup"><span data-stu-id="10539-218">AzCopy by default exports tables to JSON data files.</span></span> <span data-ttu-id="10539-219">U kunt opgeven dat de optie `/PayloadFormat:JSON|CSV` te exporteren van de tabellen als JSON- of CSV.</span><span class="sxs-lookup"><span data-stu-id="10539-219">You can specify the option `/PayloadFormat:JSON|CSV` to export the tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="10539-220">Bij het opgeven van de indeling van de CSV-nettolading AzCopy ook genereert u een schemabestand met extensie `.schema.csv` voor elk gegevensbestand.</span><span class="sxs-lookup"><span data-stu-id="10539-220">When specifying the CSV payload format, AzCopy also generates a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="10539-221">Tabelentiteiten gelijktijdig exporteren</span><span class="sxs-lookup"><span data-stu-id="10539-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="10539-222">AzCopy begint gelijktijdige bewerkingen om te exporteren entiteiten wanneer de gebruiker Hiermee kunt u de optie `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="10539-222">AzCopy starts concurrent operations to export entities when the user specifies option `/PKRS`.</span></span> <span data-ttu-id="10539-223">Elke bewerking exporteert een partitiesleutelbereik.</span><span class="sxs-lookup"><span data-stu-id="10539-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="10539-224">Houd er rekening mee dat het aantal gelijktijdige bewerkingen ook wordt beheerd door de optie `/NC`.</span><span class="sxs-lookup"><span data-stu-id="10539-224">Note that the number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="10539-225">AzCopy gebruikt het aantal coreprocessors als de standaardwaarde van `/NC` bij het kopiëren van de tabelentiteiten, zelfs als `/NC` is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="10539-225">AzCopy uses the number of core processors as the default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="10539-226">Wanneer de gebruiker opgeeft optie `/PKRS`, AzCopy gebruikt de laagste waarde van de twee waarden - partitie sleutelbereiken versus impliciet of expliciet opgegeven gelijktijdige bewerkingen - te bepalen hoeveel gelijktijdige bewerkingen om te starten.</span><span class="sxs-lookup"><span data-stu-id="10539-226">When the user specifies option `/PKRS`, AzCopy uses the smaller of the two values - partition key ranges versus implicitly or explicitly specified concurrent operations - to determine the number of concurrent operations to start.</span></span> <span data-ttu-id="10539-227">Typ voor meer informatie `AzCopy /?:NC` op de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="10539-227">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="export-table-to-blob"></a><span data-ttu-id="10539-228">De tabel exporteren naar de blob</span><span class="sxs-lookup"><span data-stu-id="10539-228">Export table to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="10539-229">AzCopy genereert een JSON-gegevensbestand in de blob-container met de volgende naamconventie:</span><span class="sxs-lookup"><span data-stu-id="10539-229">AzCopy generates a JSON data file into the blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="10539-230">Het gegenereerde bestand van de JSON-gegevens volgt de indeling van nettolading voor minimale metagegevens.</span><span class="sxs-lookup"><span data-stu-id="10539-230">The generated JSON data file follows the payload format for minimal metadata.</span></span> <span data-ttu-id="10539-231">Zie voor meer informatie over deze indeling van nettolading [indeling van nettolading voor tabel servicebewerkingen](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span><span class="sxs-lookup"><span data-stu-id="10539-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="10539-232">Houd er rekening mee dat bij het tabellen exporteren naar blobs, AzCopy downloadt de tabelentiteiten naar lokale tijdelijke gegevensbestanden en uploadt u deze entiteiten naar de blob.</span><span class="sxs-lookup"><span data-stu-id="10539-232">Note that when exporting tables to blobs, AzCopy downloads the Table entities to local temporary data files and then uploads those entities to the blob.</span></span> <span data-ttu-id="10539-233">Deze tijdelijke gegevensbestanden in de logboekmap-bestand met het standaardpad zijn geplaatst '<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>', kunt u optie/Z: [journaal-map] te wijzigen van het journaal maplocatie bestands- en dus de locatie van tijdelijke bestanden te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="10539-233">These temporary data files are put into the journal file folder with the default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] to change the journal file folder location and thus change the temporary data files location.</span></span> <span data-ttu-id="10539-234">De grootte van de tijdelijke bestanden wordt bepaald door uw tabelentiteiten grootte en de grootte die u met de optie /SplitSize hebt opgegeven, hoewel het tijdelijke bestand in de lokale schijf wordt onmiddellijk verwijderd zodra deze is geüpload naar de blob, zorg ervoor dat u hebt onvoldoende lokale schijfruimte voor het opslaan van deze tijdelijke gegevensbestanden voordat ze worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="10539-234">The temporary data files' size is decided by your table entities' size and the size you specified with the option /SplitSize, although the temporary data file in local disk is deleted instantly once it has been uploaded to the blob, please make sure you have enough local disk space to store these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="10539-235">Tabel: importeren</span><span class="sxs-lookup"><span data-stu-id="10539-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="10539-236">Tabel importeren</span><span class="sxs-lookup"><span data-stu-id="10539-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="10539-237">De optie `/EntityOperation` wordt aangegeven hoe entiteiten in de tabel invoegen.</span><span class="sxs-lookup"><span data-stu-id="10539-237">The option `/EntityOperation` indicates how to insert entities into the table.</span></span> <span data-ttu-id="10539-238">Mogelijke waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="10539-238">Possible values are:</span></span>

* <span data-ttu-id="10539-239">`InsertOrSkip`: Hiermee slaat een bestaande entiteit of een nieuwe entiteit ingevoegd als het bestand niet in de tabel bestaat.</span><span class="sxs-lookup"><span data-stu-id="10539-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="10539-240">`InsertOrMerge`: Een bestaande entiteit samenvoegingen of een nieuwe entiteit ingevoegd als het bestand niet in de tabel bestaat.</span><span class="sxs-lookup"><span data-stu-id="10539-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="10539-241">`InsertOrReplace`: Een bestaande entiteit vervangt of een nieuwe entiteit ingevoegd als het bestand niet in de tabel bestaat.</span><span class="sxs-lookup"><span data-stu-id="10539-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="10539-242">Opmerking dat kunt u de optie opgeven `/PKRS` in het scenario voor importeren.</span><span class="sxs-lookup"><span data-stu-id="10539-242">Note that you cannot specify option `/PKRS` in the import scenario.</span></span> <span data-ttu-id="10539-243">In tegenstelling tot de export-scenario, waarin u de optie moet opgeven `/PKRS` voor het starten van gelijktijdige bewerkingen AzCopy gelijktijdige bewerkingen wordt standaard gestart bij het importeren van een tabel.</span><span class="sxs-lookup"><span data-stu-id="10539-243">Unlike the export scenario, in which you must specify option `/PKRS` to start concurrent operations, AzCopy starts concurrent operations by default when you import a table.</span></span> <span data-ttu-id="10539-244">Het aantal gelijktijdige bewerkingen gestart is gelijk aan het aantal coreprocessors; u kunt echter een verschillend aantal gelijktijdige met optie opgeven `/NC`.</span><span class="sxs-lookup"><span data-stu-id="10539-244">The default number of concurrent operations started is equal to the number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="10539-245">Typ voor meer informatie `AzCopy /?:NC` op de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="10539-245">For more details, type `AzCopy /?:NC` at the command line.</span></span>

<span data-ttu-id="10539-246">Houd er rekening mee dat AzCopy biedt alleen ondersteuning voor JSON, niet-CSV importeren.</span><span class="sxs-lookup"><span data-stu-id="10539-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="10539-247">AzCopy niet ondersteunt tabel invoer van gebruiker gemaakte JSON en manifest bestanden.</span><span class="sxs-lookup"><span data-stu-id="10539-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="10539-248">Beide bestanden moeten afkomstig zijn van het exporteren van een AzCopy-tabel.</span><span class="sxs-lookup"><span data-stu-id="10539-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="10539-249">Om fouten te voorkomen, neem geen wijzigen van de geëxporteerde JSON of manifestbestand.</span><span class="sxs-lookup"><span data-stu-id="10539-249">To avoid errors, please do not modify the exported JSON or manifest file.</span></span>

### <a name="import-entities-to-table-using-blobs"></a><span data-ttu-id="10539-250">Entiteiten aan een tabel met blobs importeren</span><span class="sxs-lookup"><span data-stu-id="10539-250">Import entities to table using blobs</span></span>
<span data-ttu-id="10539-251">Stel een Blob-container bevat het volgende: A JSON-bestand voor een Azure-tabel en het bijbehorende manifest-bestand.</span><span class="sxs-lookup"><span data-stu-id="10539-251">Assume a Blob container contains the following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="10539-252">U kunt de volgende opdracht voor het importeren van entiteiten in een tabel met behulp van het manifestbestand in de blobcontainer uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="10539-252">You can run the following command to import entities into a table using the manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="10539-253">Andere functies van AzCopy</span><span class="sxs-lookup"><span data-stu-id="10539-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a><span data-ttu-id="10539-254">Alleen gegevens die niet in de doel bestaat-gekopieerd</span><span class="sxs-lookup"><span data-stu-id="10539-254">Only copy data that doesn't exist in the destination</span></span>
<span data-ttu-id="10539-255">De `/XO` en `/XN` parameters kunt u oudere of nieuwere bron resources uitsluiten wordt gekopieerd, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="10539-255">The `/XO` and `/XN` parameters allow you to exclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="10539-256">Als u wilt kopiëren van de bron-resources die niet bestaan in de doel-, kunt u beide parameters in de AzCopy-opdracht opgeven:</span><span class="sxs-lookup"><span data-stu-id="10539-256">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="10539-257">Houd er rekening mee dat dit wordt niet ondersteund wanneer de bron- of doelserver een tabel wordt.</span><span class="sxs-lookup"><span data-stu-id="10539-257">Note that this is not supported when either the source or destination is a table.</span></span>

### <a name="use-a-response-file-to-specify-command-line-parameters"></a><span data-ttu-id="10539-258">Gebruik een responsbestand opdrachtregelparameters opgeven</span><span class="sxs-lookup"><span data-stu-id="10539-258">Use a response file to specify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="10539-259">U kunt eventuele opdrachtregelparameters AzCopy opnemen in een responsbestand.</span><span class="sxs-lookup"><span data-stu-id="10539-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="10539-260">AzCopy verwerkt de parameters in het bestand alsof ze had is opgegeven op de opdrachtregel voor het uitvoeren van een directe vervanging met de inhoud van het bestand.</span><span class="sxs-lookup"><span data-stu-id="10539-260">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span></span>

<span data-ttu-id="10539-261">Wordt ervan uitgegaan dat een antwoordbestand met de naam `copyoperation.txt`, die de volgende regels bevat.</span><span class="sxs-lookup"><span data-stu-id="10539-261">Assume a response file named `copyoperation.txt`, that contains the following lines.</span></span> <span data-ttu-id="10539-262">Elke parameter AzCopy kan op een enkele regel worden opgegeven</span><span class="sxs-lookup"><span data-stu-id="10539-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="10539-263">of op afzonderlijke regels:</span><span class="sxs-lookup"><span data-stu-id="10539-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="10539-264">AzCopy mislukt als u de parameter over twee regels verdelen, zoals hier wordt weergegeven voor de `/sourcekey` parameter:</span><span class="sxs-lookup"><span data-stu-id="10539-264">AzCopy fails if you split the parameter across two lines, as shown here for the `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-to-specify-command-line-parameters"></a><span data-ttu-id="10539-265">Meerdere antwoordbestanden gebruiken om op te geven van opdrachtregelparameters</span><span class="sxs-lookup"><span data-stu-id="10539-265">Use multiple response files to specify command-line parameters</span></span>
<span data-ttu-id="10539-266">Wordt ervan uitgegaan dat een antwoordbestand met de naam `source.txt` die aangeeft dat een Broncontainer:</span><span class="sxs-lookup"><span data-stu-id="10539-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="10539-267">En een antwoordbestand met de naam `dest.txt` waarmee een doelmap in het bestandssysteem:</span><span class="sxs-lookup"><span data-stu-id="10539-267">And a response file named `dest.txt` that specifies a destination folder in the file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="10539-268">En een antwoordbestand met de naam `options.txt` Hiermee worden de opties voor AzCopy:</span><span class="sxs-lookup"><span data-stu-id="10539-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="10539-269">AzCopy aanroepen met deze antwoordbestanden, die zich bevinden in een map `C:\responsefiles`, gebruikt u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="10539-269">To call AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="10539-270">AzCopy verwerkt met deze opdracht net zoals als u alle van de afzonderlijke parameters op de opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="10539-270">AzCopy processes this command just as it would if you included all of the individual parameters on the command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="10539-271">Geef een shared access signature (SAS)</span><span class="sxs-lookup"><span data-stu-id="10539-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="10539-272">U kunt ook een SAS voor de container URI opgeven:</span><span class="sxs-lookup"><span data-stu-id="10539-272">You can also specify a SAS on the container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="10539-273">Map voor logboek-bestand</span><span class="sxs-lookup"><span data-stu-id="10539-273">Journal file folder</span></span>
<span data-ttu-id="10539-274">Telkens wanneer die u een opdracht met AzCopy geven, controleert deze of een journal-bestand in de standaardmap bestaat en of deze bestaat in een map die u hebt opgegeven via deze optie.</span><span class="sxs-lookup"><span data-stu-id="10539-274">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="10539-275">De wijzigingslogboek-bestand bestaat niet op beide plaatsen, AzCopy wordt de bewerking wordt beschouwd als nieuwe als genereert een nieuw journaalbestand.</span><span class="sxs-lookup"><span data-stu-id="10539-275">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="10539-276">Als het journaalbestand bestaat, controleert AzCopy of de opdrachtregel die ingevoerde overeenkomt met de opdrachtregel in het logboek-bestand.</span><span class="sxs-lookup"><span data-stu-id="10539-276">If the journal file does exist, AzCopy checks whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="10539-277">Als de twee opdrachtregels overeenkomen, hervat AzCopy de bewerking niet voltooid.</span><span class="sxs-lookup"><span data-stu-id="10539-277">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="10539-278">Als ze niet overeenkomen, wordt u gevraagd of het journaalbestand te overschrijven naar een nieuwe bewerking starten of de huidige bewerking te annuleren.</span><span class="sxs-lookup"><span data-stu-id="10539-278">If they do not match, you are prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="10539-279">Als u de standaardlocatie voor het wijzigingslogboek-bestand gebruiken wilt:</span><span class="sxs-lookup"><span data-stu-id="10539-279">If you want to use the default location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="10539-280">Als u de optie weglaat `/Z`, of geef de optie `/Z` zonder het mappad, zoals hierboven, AzCopy wijzigingslogboek wordt het bestand gemaakt op de standaardlocatie `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="10539-280">If you omit option `/Z`, or specify option `/Z` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="10539-281">Als het wijzigingslogboek bestand al bestaat, hervat de bewerking op basis van het journaalbestand met AzCopy.</span><span class="sxs-lookup"><span data-stu-id="10539-281">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="10539-282">Als u een aangepaste locatie voor het wijzigingslogboek-bestand opgeven wilt:</span><span class="sxs-lookup"><span data-stu-id="10539-282">If you want to specify a custom location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="10539-283">In dit voorbeeld wordt het journaalbestand als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="10539-283">This example creates the journal file if it does not already exist.</span></span> <span data-ttu-id="10539-284">Als deze bestaat, hervat de bewerking op basis van het journaalbestand met AzCopy.</span><span class="sxs-lookup"><span data-stu-id="10539-284">If it does exist, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="10539-285">Als u een bewerking AzCopy hervatten wilt:</span><span class="sxs-lookup"><span data-stu-id="10539-285">If you want to resume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="10539-286">In dit voorbeeld hervat de laatste bewerking, die mogelijk niet voltooien.</span><span class="sxs-lookup"><span data-stu-id="10539-286">This example resumes the last operation, which may have failed to complete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="10539-287">Genereren van een logboekbestand</span><span class="sxs-lookup"><span data-stu-id="10539-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="10539-288">Als u de optie opgeven `/V` zonder op te geven van een pad naar het uitgebreide logboek, AzCopy maakt vervolgens het logboekbestand op de standaardlocatie `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="10539-288">If you specify option `/V` without providing a file path to the verbose log, then AzCopy creates the log file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="10539-289">Anders kunt u een logboekbestand maken in een aangepaste locatie:</span><span class="sxs-lookup"><span data-stu-id="10539-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="10539-290">Houd er rekening mee dat als u een relatief pad na optie opgeeft `/V`, zoals `/V:test/azcopy1.log`, wordt het uitgebreide logboek in de huidige werkmap in een submap met de naam gemaakt `test`.</span><span class="sxs-lookup"><span data-stu-id="10539-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then the verbose log is created in the current working directory within a subfolder named `test`.</span></span>

### <a name="specify-the-number-of-concurrent-operations-to-start"></a><span data-ttu-id="10539-291">Geef het aantal gelijktijdige bewerkingen starten</span><span class="sxs-lookup"><span data-stu-id="10539-291">Specify the number of concurrent operations to start</span></span>
<span data-ttu-id="10539-292">Optie `/NC` geeft het aantal gelijktijdige te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="10539-292">Option `/NC` specifies the number of concurrent copy operations.</span></span> <span data-ttu-id="10539-293">AzCopy wordt standaard een bepaald aantal gelijktijdige bewerkingen te verhogen van de overdracht gegevensdoorvoer gestart.</span><span class="sxs-lookup"><span data-stu-id="10539-293">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="10539-294">Voor bewerkingen van de tabel is het aantal gelijktijdige bewerkingen gelijk aan het aantal processors dat u hebt.</span><span class="sxs-lookup"><span data-stu-id="10539-294">For Table operations, the number of concurrent operations is equal to the number of processors you have.</span></span> <span data-ttu-id="10539-295">Voor Blob- en bewerkingen, het aantal gelijktijdige bewerkingen is gelijk aan 8 keer het aantal processors dat u hebt.</span><span class="sxs-lookup"><span data-stu-id="10539-295">For Blob and File operations, the number of concurrent operations is equal 8 times the number of processors you have.</span></span> <span data-ttu-id="10539-296">Als u via een netwerk met lage bandbreedte AzCopy uitvoert, kunt u een lager getal voor /NC om te voorkomen dat mislukt, omdat resource concurrentie opgeven.</span><span class="sxs-lookup"><span data-stu-id="10539-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC to avoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="10539-297">AzCopy uitvoeren op Azure-Opslagemulator</span><span class="sxs-lookup"><span data-stu-id="10539-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="10539-298">U kunt uitvoeren AzCopy tegen de [Azure-Opslagemulator](storage-use-emulator.md) voor Blobs:</span><span class="sxs-lookup"><span data-stu-id="10539-298">You can run AzCopy against the [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="10539-299">en tabellen:</span><span class="sxs-lookup"><span data-stu-id="10539-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="10539-300">AzCopy-Parameters</span><span class="sxs-lookup"><span data-stu-id="10539-300">AzCopy Parameters</span></span>
<span data-ttu-id="10539-301">Parameters voor AzCopy worden hieronder beschreven.</span><span class="sxs-lookup"><span data-stu-id="10539-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="10539-302">U kunt ook een van de volgende opdrachten uit vanaf de opdrachtregel voor hulp bij het gebruik van AzCopy typen:</span><span class="sxs-lookup"><span data-stu-id="10539-302">You can also type one of the following commands from the command line for help in using AzCopy:</span></span>

* <span data-ttu-id="10539-303">Voor gedetailleerde help voor AzCopy:`AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="10539-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="10539-304">Voor gedetailleerde hulp bij elke parameter AzCopy:`AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="10539-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="10539-305">Voor voorbeelden van opdrachtregels:`AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="10539-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="10539-306">/ Source: 'bron'</span><span class="sxs-lookup"><span data-stu-id="10539-306">/Source:"source"</span></span>
<span data-ttu-id="10539-307">Hiermee geeft u de brongegevens waaruit u wilt kopiëren.</span><span class="sxs-lookup"><span data-stu-id="10539-307">Specifies the source data from which to copy.</span></span> <span data-ttu-id="10539-308">De bron kan een bestandssysteemmap, een blob-container, een blob virtuele map, een bestandsshare voor opslag, een map voor opslag of een Azure-tabel zijn.</span><span class="sxs-lookup"><span data-stu-id="10539-308">The source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="10539-309">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="10539-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="10539-310">/ Dest: "doelmap"</span><span class="sxs-lookup"><span data-stu-id="10539-310">/Dest:"destination"</span></span>
<span data-ttu-id="10539-311">Hiermee geeft u het doel om naar te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="10539-311">Specifies the destination to copy to.</span></span> <span data-ttu-id="10539-312">Het doel mag een bestandssysteemmap, een blob-container, een blob virtuele map, een bestandsshare voor opslag, een map voor opslag of een Azure-tabel.</span><span class="sxs-lookup"><span data-stu-id="10539-312">The destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="10539-313">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="10539-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="10539-314">/ Patroon: "bestandspatroon"</span><span class="sxs-lookup"><span data-stu-id="10539-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="10539-315">Hiermee geeft u een patroon waarmee wordt aangegeven welke bestanden worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="10539-315">Specifies a file pattern that indicates which files to copy.</span></span> <span data-ttu-id="10539-316">Het gedrag van de parameter /Pattern wordt bepaald door de locatie van de brongegevens en de aanwezigheid van de optie recursieve modus.</span><span class="sxs-lookup"><span data-stu-id="10539-316">The behavior of the /Pattern parameter is determined by the location of the source data, and the presence of the recursive mode option.</span></span> <span data-ttu-id="10539-317">Recursieve modus wordt opgegeven via de optie/s.</span><span class="sxs-lookup"><span data-stu-id="10539-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="10539-318">De opgegeven bron is een map in het bestandssysteem, waarna standaard jokertekens zijn als het opgegeven bestandspatroon wordt vergeleken met de bestanden in de map.</span><span class="sxs-lookup"><span data-stu-id="10539-318">If the specified source is a directory in the file system, then standard wildcards are in effect, and the file pattern provided is matched against files within the directory.</span></span> <span data-ttu-id="10539-319">Als de optie/s is opgegeven, klikt u vervolgens AzCopy, overeenkomt met het opgegeven patroon tegen alle bestanden in alle submappen onder de map.</span><span class="sxs-lookup"><span data-stu-id="10539-319">If option /S is specified, then AzCopy also matches the specified pattern against all files in any subfolders beneath the directory.</span></span>

<span data-ttu-id="10539-320">Als de opgegeven bron een blob-container of de virtuele map is, worden klikt u vervolgens jokertekens niet toegepast.</span><span class="sxs-lookup"><span data-stu-id="10539-320">If the specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="10539-321">Als het opgegeven bestandspatroon optie die /s is opgegeven, klikt u vervolgens AzCopy geïnterpreteerd als een voorvoegsel van de blob.</span><span class="sxs-lookup"><span data-stu-id="10539-321">If option /S is specified, then AzCopy interprets the specified file pattern as a blob prefix.</span></span> <span data-ttu-id="10539-322">Als de optie/s niet is opgegeven, klikt u vervolgens AzCopy komt overeen met het bestandspatroon tegen exacte blob-namen.</span><span class="sxs-lookup"><span data-stu-id="10539-322">If option /S is not specified, then AzCopy matches the file pattern against exact blob names.</span></span>

<span data-ttu-id="10539-323">Als de opgegeven bron een Azure-bestandsshare is, wordt u moet de exacte bestandsnaam (bijvoorbeeld abc.txt) als u wilt kopiëren van één bestand opgeven, of de optie/s alle bestanden in de share recursief te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="10539-323">If the specified source is an Azure file share, then you must either specify the exact file name, (e.g. abc.txt) to copy a single file, or specify option /S to copy all files in the share recursively.</span></span> <span data-ttu-id="10539-324">Probeert op te geven van beide een bestand patroon en de optie/s samen met resultaten in een fout.</span><span class="sxs-lookup"><span data-stu-id="10539-324">Attempting to specify both a file pattern and option /S together results in an error.</span></span>

<span data-ttu-id="10539-325">AzCopy gebruikt hoofdlettergevoelig overeenkomende wanneer de/Source een blob-container of blob virtuele map is en maakt gebruik van niet-hoofdlettergevoelige overeenkomende in alle andere gevallen.</span><span class="sxs-lookup"><span data-stu-id="10539-325">AzCopy uses case-sensitive matching when the /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all the other cases.</span></span>

<span data-ttu-id="10539-326">Bestand standaardpatroon gebruikt wanneer er geen bestandspatroon is opgegeven is *.*</span><span class="sxs-lookup"><span data-stu-id="10539-326">The default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="10539-327">voor een locatie in het bestandssysteem of een leeg voorvoegsel voor een Azure-opslaglocatie.</span><span class="sxs-lookup"><span data-stu-id="10539-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="10539-328">Meerdere bestand patronen opgeven wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="10539-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="10539-329">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="10539-330">/ DestKey: 'opslagsleutel'</span><span class="sxs-lookup"><span data-stu-id="10539-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="10539-331">Hiermee geeft u de toegangssleutel voor de doelbron.</span><span class="sxs-lookup"><span data-stu-id="10539-331">Specifies the storage account key for the destination resource.</span></span>

<span data-ttu-id="10539-332">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="10539-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="10539-333">/ DestSAS: 'sas-token'</span><span class="sxs-lookup"><span data-stu-id="10539-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="10539-334">Hiermee geeft u een Shared Access Signature (SAS) met machtigingen voor lezen en schrijven voor de bestemming (indien van toepassing).</span><span class="sxs-lookup"><span data-stu-id="10539-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for the destination (if applicable).</span></span> <span data-ttu-id="10539-335">De SAS met dubbele aanhalingstekens rond omdat deze mogelijk speciale opdrachtregelprogramma tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="10539-335">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="10539-336">Als de doel-resource een blob-container, een bestandsshare of een tabel is, kunt u deze optie gevolgd door de SAS-token opgeven of u kunt de SAS opgeven als onderdeel van de doel-blob-container, bestandsshare of de URI van de tabel, zonder deze optie.</span><span class="sxs-lookup"><span data-stu-id="10539-336">If the destination resource is a blob container, file share or table, you can either specify this option followed by the SAS token, or you can specify the SAS as part of the destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="10539-337">Als de bron- en doelserver beide blobs zijn, moet de bestemmings-blob zich binnen hetzelfde opslagaccount als de bron-blob.</span><span class="sxs-lookup"><span data-stu-id="10539-337">If the source and destination are both blobs, then the destination blob must reside within the same storage account as the source blob.</span></span>

<span data-ttu-id="10539-338">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="10539-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="10539-339">/ SourceKey: 'opslagsleutel'</span><span class="sxs-lookup"><span data-stu-id="10539-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="10539-340">Hiermee geeft u de opslagaccountsleutel voor de bronresource.</span><span class="sxs-lookup"><span data-stu-id="10539-340">Specifies the storage account key for the source resource.</span></span>

<span data-ttu-id="10539-341">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="10539-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="10539-342">/ SourceSAS: 'sas-token'</span><span class="sxs-lookup"><span data-stu-id="10539-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="10539-343">Hiermee geeft u een Shared Access Signature met lees- en machtigingen voor de bron (indien van toepassing).</span><span class="sxs-lookup"><span data-stu-id="10539-343">Specifies a Shared Access Signature with READ and LIST permissions for the source (if applicable).</span></span> <span data-ttu-id="10539-344">De SAS met dubbele aanhalingstekens rond omdat deze mogelijk speciale opdrachtregelprogramma tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="10539-344">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="10539-345">Als de bron-bron een blob-container is en een sleutel noch een SAS is opgegeven, wordt de blob-container gelezen via anonieme toegang.</span><span class="sxs-lookup"><span data-stu-id="10539-345">If the source resource is a blob container, and neither a key nor a SAS is provided, then the blob container is read via anonymous access.</span></span>

<span data-ttu-id="10539-346">Als de bron een bestandsshare is of een sleutel of een SAS tabel moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="10539-346">If the source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="10539-347">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="10539-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="10539-348">/ S</span><span class="sxs-lookup"><span data-stu-id="10539-348">/S</span></span>
<span data-ttu-id="10539-349">Hiermee geeft u een recursieve modus voor het kopiëren van.</span><span class="sxs-lookup"><span data-stu-id="10539-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="10539-350">In de modus voor recursieve kopieert AzCopy alle blobs of bestanden die overeenkomen met het opgegeven bestandspatroon, inclusief verbindingen in submappen.</span><span class="sxs-lookup"><span data-stu-id="10539-350">In recursive mode, AzCopy copies all blobs or files that match the specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="10539-351">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="10539-352">/ BlobType: 'block' | "page" | "toevoegen"</span><span class="sxs-lookup"><span data-stu-id="10539-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="10539-353">Hiermee geeft u op of de bestemmings-blob een blok-blob, een pagina-blob of een toevoeg-blob is.</span><span class="sxs-lookup"><span data-stu-id="10539-353">Specifies whether the destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="10539-354">Deze optie is alleen toepasbaar wanneer u een blob uploadt.</span><span class="sxs-lookup"><span data-stu-id="10539-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="10539-355">Anders wordt er een fout gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="10539-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="10539-356">Als de bestemming een blob is en deze optie niet is opgegeven, standaard maakt AzCopy een blok-blob.</span><span class="sxs-lookup"><span data-stu-id="10539-356">If the destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="10539-357">**Van toepassing op:** Blobs</span><span class="sxs-lookup"><span data-stu-id="10539-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="10539-358">/ CheckMD5</span><span class="sxs-lookup"><span data-stu-id="10539-358">/CheckMD5</span></span>
<span data-ttu-id="10539-359">Een MD5-hash voor de gedownloade gegevens berekend en controleert of de MD5-hash wordt opgeslagen in de blob of Content-MD5-eigenschap van bestand overeenkomt met de berekende hash.</span><span class="sxs-lookup"><span data-stu-id="10539-359">Calculates an MD5 hash for downloaded data and verifies that the MD5 hash stored in the blob or file's Content-MD5 property matches the calculated hash.</span></span> <span data-ttu-id="10539-360">De MD5-controle is standaard uitgeschakeld, zodat u deze optie om de MD5-controle uitvoeren bij het downloaden van gegevens moet opgeven.</span><span class="sxs-lookup"><span data-stu-id="10539-360">The MD5 check is turned off by default, so you must specify this option to perform the MD5 check when downloading data.</span></span>

<span data-ttu-id="10539-361">Houd er rekening mee dat Azure Storage garandeert niet dat de MD5-hash die is opgeslagen voor de blob of het bestand bijgewerkt is.</span><span class="sxs-lookup"><span data-stu-id="10539-361">Note that Azure Storage doesn't guarantee that the MD5 hash stored for the blob or file is up-to-date.</span></span> <span data-ttu-id="10539-362">Het is de verantwoordelijkheid van de client de MD5 bijwerken wanneer de blob of het bestand is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="10539-362">It is client's responsibility to update the MD5 whenever the blob or file is modified.</span></span>

<span data-ttu-id="10539-363">AzCopy stelt altijd de Content-MD5-eigenschap voor een Azure-blob of het bestand nadat het uploaden naar de service.</span><span class="sxs-lookup"><span data-stu-id="10539-363">AzCopy always sets the Content-MD5 property for an Azure blob or file after uploading it to the service.</span></span>  

<span data-ttu-id="10539-364">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="10539-365">/ Momentopname</span><span class="sxs-lookup"><span data-stu-id="10539-365">/Snapshot</span></span>
<span data-ttu-id="10539-366">Geeft aan of om over te dragen van momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="10539-366">Indicates whether to transfer snapshots.</span></span> <span data-ttu-id="10539-367">Deze optie is alleen geldig wanneer de bron een blob is.</span><span class="sxs-lookup"><span data-stu-id="10539-367">This option is only valid when the source is a blob.</span></span>

<span data-ttu-id="10539-368">De overgebrachte blob-momentopnamen worden gewijzigd in deze indeling: .extensie blob-naam (momentopname-tijd)</span><span class="sxs-lookup"><span data-stu-id="10539-368">The transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="10539-369">Momentopnamen worden standaard niet gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="10539-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="10539-370">**Van toepassing op:** Blobs</span><span class="sxs-lookup"><span data-stu-id="10539-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="10539-371">/ V: [uitgebreide-log-bestand]</span><span class="sxs-lookup"><span data-stu-id="10539-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="10539-372">Uitvoer uitgebreide statusberichten in een logboekbestand.</span><span class="sxs-lookup"><span data-stu-id="10539-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="10539-373">Het logboekbestand heet standaard AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="10539-373">By default, the verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="10539-374">Als u een bestaande bestandslocatie voor deze optie opgeeft, wordt het uitgebreide logboek wordt toegevoegd aan of het bestand.</span><span class="sxs-lookup"><span data-stu-id="10539-374">If you specify an existing file location for this option, the verbose log is appended to that file.</span></span>  

<span data-ttu-id="10539-375">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="10539-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="10539-376">/ Z: [journaal-map]</span><span class="sxs-lookup"><span data-stu-id="10539-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="10539-377">Hiermee geeft u een map journaal-bestand voor het hervatten van een bewerking.</span><span class="sxs-lookup"><span data-stu-id="10539-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="10539-378">AzCopy ondersteunt altijd wordt hervat als een bewerking is onderbroken.</span><span class="sxs-lookup"><span data-stu-id="10539-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="10539-379">Als deze optie niet opgegeven is of deze is opgegeven zonder het pad naar een map, maakt AzCopy de journaalbestand in de standaardlocatie bevindt, % LocalAppData%\Microsoft\Azure\AzCopy is.</span><span class="sxs-lookup"><span data-stu-id="10539-379">If this option is not specified, or it is specified without a folder path, then AzCopy creates the journal file in the default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="10539-380">Telkens wanneer die u een opdracht met AzCopy geven, controleert deze of een journal-bestand in de standaardmap bestaat en of deze bestaat in een map die u hebt opgegeven via deze optie.</span><span class="sxs-lookup"><span data-stu-id="10539-380">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="10539-381">De wijzigingslogboek-bestand bestaat niet op beide plaatsen, AzCopy wordt de bewerking wordt beschouwd als nieuwe als genereert een nieuw journaalbestand.</span><span class="sxs-lookup"><span data-stu-id="10539-381">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="10539-382">Als het journaalbestand bestaat, controleert AzCopy of de opdrachtregel die ingevoerde overeenkomt met de opdrachtregel in het logboek-bestand.</span><span class="sxs-lookup"><span data-stu-id="10539-382">If the journal file does exist, AzCopy checks whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="10539-383">Als de twee opdrachtregels overeenkomen, hervat AzCopy de bewerking niet voltooid.</span><span class="sxs-lookup"><span data-stu-id="10539-383">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="10539-384">Als ze niet overeenkomen, wordt u gevraagd of het journaalbestand te overschrijven naar een nieuwe bewerking starten of de huidige bewerking te annuleren.</span><span class="sxs-lookup"><span data-stu-id="10539-384">If they do not match, you are prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="10539-385">De wijzigingslogboek-bestand wordt verwijderd bij de bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="10539-385">The journal file is deleted upon successful completion of the operation.</span></span>

<span data-ttu-id="10539-386">Houd er rekening mee dat het hervatten van een bewerking van een journal-bestand gemaakt met een eerdere versie van AzCopy niet wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="10539-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="10539-387">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="10539-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="10539-388">/@:"parameter-File'</span><span class="sxs-lookup"><span data-stu-id="10539-388">/@:"parameter-file"</span></span>
<span data-ttu-id="10539-389">Hiermee geeft u een bestand met parameters.</span><span class="sxs-lookup"><span data-stu-id="10539-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="10539-390">AzCopy verwerkt de parameters in het bestand alsof ze op de opdrachtregel is doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="10539-390">AzCopy processes the parameters in the file just as if they had been specified on the command line.</span></span>

<span data-ttu-id="10539-391">In een responsbestand kunt u meerdere parameters opgeven op één regel of geef elke parameter in op een aparte regel.</span><span class="sxs-lookup"><span data-stu-id="10539-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="10539-392">Houd er rekening mee dat een afzonderlijke parameter kan niet worden gebruikt voor het bereik van meerdere regels.</span><span class="sxs-lookup"><span data-stu-id="10539-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="10539-393">Antwoordbestanden kunnen opmerkingen regels die met het symbool beginnen # opnemen.</span><span class="sxs-lookup"><span data-stu-id="10539-393">Response files can include comments lines that begin with the # symbol.</span></span>

<span data-ttu-id="10539-394">U kunt meerdere antwoordbestanden opgeven.</span><span class="sxs-lookup"><span data-stu-id="10539-394">You can specify multiple response files.</span></span> <span data-ttu-id="10539-395">Houd er echter rekening mee AzCopy biedt geen ondersteuning voor geneste antwoordbestanden.</span><span class="sxs-lookup"><span data-stu-id="10539-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="10539-396">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="10539-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="10539-397">/Y</span><span class="sxs-lookup"><span data-stu-id="10539-397">/Y</span></span>
<span data-ttu-id="10539-398">Alle AzCopy bevestiging vragen onderdrukt.</span><span class="sxs-lookup"><span data-stu-id="10539-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="10539-399">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="10539-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="10539-400">/ L</span><span class="sxs-lookup"><span data-stu-id="10539-400">/L</span></span>
<span data-ttu-id="10539-401">Hiermee geeft u een bewerking in de lijst. Er zijn geen gegevens worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="10539-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="10539-402">AzCopy interpreteert de met behulp van deze optie als een simulatie voor het werken met de opdrachtregel zonder deze optie/l en tellingen hoeveel objecten worden gekopieerd, kunt u de optie /V op hetzelfde moment om te controleren welke objecten worden gekopieerd in het uitgebreide logboekbestand opgeven.</span><span class="sxs-lookup"><span data-stu-id="10539-402">AzCopy interprets the using of this option as a simulation for running the command line without this option /L and counts how many objects are copied, you can specify option /V at the same time to check which objects are copied in the verbose log.</span></span>

<span data-ttu-id="10539-403">Het gedrag van deze optie is ook afhankelijk van de locatie van de brongegevens en de aanwezigheid van de recursieve modus/s en de bestandsnaam patroon optie /Pattern.</span><span class="sxs-lookup"><span data-stu-id="10539-403">The behavior of this option is also determined by the location of the source data and the presence of the recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="10539-404">AzCopy vereist lijst weergeven en lezen van de bronlocatie van deze wanneer u deze optie.</span><span class="sxs-lookup"><span data-stu-id="10539-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="10539-405">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="10539-406">/MT</span><span class="sxs-lookup"><span data-stu-id="10539-406">/MT</span></span>
<span data-ttu-id="10539-407">Hiermee stelt u het gedownloade bestand tijd laatste wijziging moet dezelfde zijn als de bron-blob of van het bestand.</span><span class="sxs-lookup"><span data-stu-id="10539-407">Sets the downloaded file's last-modified time to be the same as the source blob or file's.</span></span>

<span data-ttu-id="10539-408">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="10539-409">/XN</span><span class="sxs-lookup"><span data-stu-id="10539-409">/XN</span></span>
<span data-ttu-id="10539-410">Sluit een nieuwere bronresource.</span><span class="sxs-lookup"><span data-stu-id="10539-410">Excludes a newer source resource.</span></span> <span data-ttu-id="10539-411">De resource niet als de tijd voor laatst gewijzigd van de bron dezelfde wordt gekopieerd of nieuwer zijn dan het doel.</span><span class="sxs-lookup"><span data-stu-id="10539-411">The resource is not copied if the last modified time of the source is the same or newer than destination.</span></span>

<span data-ttu-id="10539-412">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="10539-413">/XO</span><span class="sxs-lookup"><span data-stu-id="10539-413">/XO</span></span>
<span data-ttu-id="10539-414">Sluit een oudere bronserver resource.</span><span class="sxs-lookup"><span data-stu-id="10539-414">Excludes an older source resource.</span></span> <span data-ttu-id="10539-415">De resource niet als de tijd voor laatst gewijzigd van de bron dezelfde wordt gekopieerd of ouder zijn dan het doel.</span><span class="sxs-lookup"><span data-stu-id="10539-415">The resource is not copied if the last modified time of the source is the same or older than destination.</span></span>

<span data-ttu-id="10539-416">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="10539-417">/A</span><span class="sxs-lookup"><span data-stu-id="10539-417">/A</span></span>
<span data-ttu-id="10539-418">Alleen bestanden die het kenmerk Archief hebt geüpload.</span><span class="sxs-lookup"><span data-stu-id="10539-418">Uploads only files that have the Archive attribute set.</span></span>

<span data-ttu-id="10539-419">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="10539-420">/ IA: [RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="10539-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="10539-421">Alleen bestanden die een van de opgegeven kenmerken set hebt geüpload.</span><span class="sxs-lookup"><span data-stu-id="10539-421">Uploads only files that have any of the specified attributes set.</span></span>

<span data-ttu-id="10539-422">Beschikbare kenmerken zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="10539-422">Available attributes include:</span></span>

* <span data-ttu-id="10539-423">R = alleen-lezen bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-423">R = Read-only files</span></span>
* <span data-ttu-id="10539-424">Een = bestanden klaar voor archivering</span><span class="sxs-lookup"><span data-stu-id="10539-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="10539-425">S = systeembestanden</span><span class="sxs-lookup"><span data-stu-id="10539-425">S = System files</span></span>
* <span data-ttu-id="10539-426">H = Verborgen bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-426">H = Hidden files</span></span>
* <span data-ttu-id="10539-427">C = gecomprimeerde bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-427">C = Compressed files</span></span>
* <span data-ttu-id="10539-428">N = normale bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-428">N = Normal files</span></span>
* <span data-ttu-id="10539-429">E = versleutelde bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-429">E = Encrypted files</span></span>
* <span data-ttu-id="10539-430">T = tijdelijke bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-430">T = Temporary files</span></span>
* <span data-ttu-id="10539-431">O = offlinebestanden</span><span class="sxs-lookup"><span data-stu-id="10539-431">O = Offline files</span></span>
* <span data-ttu-id="10539-432">Ik = niet-geïndexeerde bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-432">I = Non-indexed files</span></span>

<span data-ttu-id="10539-433">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="10539-434">/ XA: [RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="10539-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="10539-435">Sluit bestanden die een of meer van de opgegeven kenmerken is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="10539-435">Excludes files that have any of the specified attributes set.</span></span>

<span data-ttu-id="10539-436">Beschikbare kenmerken zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="10539-436">Available attributes include:</span></span>

* <span data-ttu-id="10539-437">R = alleen-lezen bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-437">R = Read-only files</span></span>
* <span data-ttu-id="10539-438">Een = bestanden klaar voor archivering</span><span class="sxs-lookup"><span data-stu-id="10539-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="10539-439">S = systeembestanden</span><span class="sxs-lookup"><span data-stu-id="10539-439">S = System files</span></span>
* <span data-ttu-id="10539-440">H = Verborgen bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-440">H = Hidden files</span></span>
* <span data-ttu-id="10539-441">C = gecomprimeerde bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-441">C = Compressed files</span></span>
* <span data-ttu-id="10539-442">N = normale bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-442">N = Normal files</span></span>
* <span data-ttu-id="10539-443">E = versleutelde bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-443">E = Encrypted files</span></span>
* <span data-ttu-id="10539-444">T = tijdelijke bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-444">T = Temporary files</span></span>
* <span data-ttu-id="10539-445">O = offlinebestanden</span><span class="sxs-lookup"><span data-stu-id="10539-445">O = Offline files</span></span>
* <span data-ttu-id="10539-446">Ik = niet-geïndexeerde bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-446">I = Non-indexed files</span></span>

<span data-ttu-id="10539-447">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="10539-448">/ Scheidingsteken: "scheidingsteken"</span><span class="sxs-lookup"><span data-stu-id="10539-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="10539-449">Hiermee geeft u het scheidingsteken dat wordt gebruikt voor het scheiden van virtuele mappen in een blob-naam.</span><span class="sxs-lookup"><span data-stu-id="10539-449">Indicates the delimiter character used to delimit virtual directories in a blob name.</span></span>

<span data-ttu-id="10539-450">Standaard maakt gebruik van AzCopy / als scheidingsteken.</span><span class="sxs-lookup"><span data-stu-id="10539-450">By default, AzCopy uses / as the delimiter character.</span></span> <span data-ttu-id="10539-451">AzCopy ondersteunt echter met behulp van een algemene teken (zoals @, # of %) als scheidingsteken.</span><span class="sxs-lookup"><span data-stu-id="10539-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="10539-452">Als u een van deze speciale tekens op de opdrachtregel opnemen moet, plaatst u de bestandsnaam tussen dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="10539-452">If you need to include one of these special characters on the command line, enclose the file name with double quotes.</span></span>

<span data-ttu-id="10539-453">Deze optie is alleen van toepassing voor het downloaden van blobs.</span><span class="sxs-lookup"><span data-stu-id="10539-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="10539-454">**Van toepassing op:** Blobs</span><span class="sxs-lookup"><span data-stu-id="10539-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="10539-455">/ NC: 'getal-van-gelijktijdige-operations'</span><span class="sxs-lookup"><span data-stu-id="10539-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="10539-456">Hiermee geeft u het aantal gelijktijdige bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="10539-456">Specifies the number of concurrent operations.</span></span>

<span data-ttu-id="10539-457">AzCopy standaard wordt een bepaald aantal gelijktijdige bewerkingen te verhogen van de overdracht gegevensdoorvoer gestart.</span><span class="sxs-lookup"><span data-stu-id="10539-457">AzCopy by default starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="10539-458">Houd er rekening mee dat groot aantal gelijktijdige bewerkingen in een omgeving met lage bandbreedte mogelijk de netwerkverbinding overbelast en te voorkomen dat de bewerkingen volledig is voltooid.</span><span class="sxs-lookup"><span data-stu-id="10539-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm the network connection and prevent the operations from fully completing.</span></span> <span data-ttu-id="10539-459">Vertraging gelijktijdige bewerkingen op basis van de werkelijke beschikbare netwerkbandbreedte.</span><span class="sxs-lookup"><span data-stu-id="10539-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="10539-460">De maximale limiet voor gelijktijdige bewerkingen is 512.</span><span class="sxs-lookup"><span data-stu-id="10539-460">The upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="10539-461">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="10539-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="10539-462">/ SourceType: "Blob" | 'Tabel'</span><span class="sxs-lookup"><span data-stu-id="10539-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="10539-463">Hiermee wordt aangegeven dat de `source` bron is een blob beschikbaar zijn in de lokale ontwikkelomgeving wordt uitgevoerd in de opslagemulator.</span><span class="sxs-lookup"><span data-stu-id="10539-463">Specifies that the `source` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="10539-464">**Van toepassing op:** Blobs, tabellen</span><span class="sxs-lookup"><span data-stu-id="10539-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="10539-465">/ DestType: "Blob" | 'Tabel'</span><span class="sxs-lookup"><span data-stu-id="10539-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="10539-466">Hiermee wordt aangegeven dat de `destination` bron is een blob beschikbaar zijn in de lokale ontwikkelomgeving wordt uitgevoerd in de opslagemulator.</span><span class="sxs-lookup"><span data-stu-id="10539-466">Specifies that the `destination` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="10539-467">**Van toepassing op:** Blobs, tabellen</span><span class="sxs-lookup"><span data-stu-id="10539-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="10539-468">/ PKRS: "key&#1;key2 key&#3;..."</span><span class="sxs-lookup"><span data-stu-id="10539-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="10539-469">Splitst de partitiesleutelbereik zodat de tabelgegevens parallel de snelheid van de exportbewerking verhoogt te exporteren.</span><span class="sxs-lookup"><span data-stu-id="10539-469">Splits the partition key range to enable exporting table data in parallel, which increases the speed of the export operation.</span></span>

<span data-ttu-id="10539-470">Als deze optie niet is opgegeven, gebruikt AzCopy één thread tabelentiteiten exporteren.</span><span class="sxs-lookup"><span data-stu-id="10539-470">If this option is not specified, then AzCopy uses a single thread to export table entities.</span></span> <span data-ttu-id="10539-471">Bijvoorbeeld, als de gebruiker opgeeft /PKRS: "aa #bb" en vervolgens AzCopy begint drie gelijktijdige bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="10539-471">For example, if the user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="10539-472">Elke bewerking exporteert een van drie partitie sleutel bereiken, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="10539-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="10539-473">[eerste partitiesleutel, aa)</span><span class="sxs-lookup"><span data-stu-id="10539-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="10539-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="10539-474">[aa, bb)</span></span>

  <span data-ttu-id="10539-475">[bb, laatste partitiesleutel]</span><span class="sxs-lookup"><span data-stu-id="10539-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="10539-476">**Van toepassing op:** tabellen</span><span class="sxs-lookup"><span data-stu-id="10539-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="10539-477">/ SplitSize: 'bestandsgrootte'</span><span class="sxs-lookup"><span data-stu-id="10539-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="10539-478">Hiermee geeft u het geëxporteerde bestand met grootte in MB, de minimaal toegestane waarde splitsen is 32.</span><span class="sxs-lookup"><span data-stu-id="10539-478">Specifies the exported file split size in MB, the minimal value allowed is 32.</span></span>

<span data-ttu-id="10539-479">Als deze optie niet is opgegeven, wordt met AzCopy tabelgegevens exporteert naar één bestand.</span><span class="sxs-lookup"><span data-stu-id="10539-479">If this option is not specified, AzCopy exports table data to a single file.</span></span>

<span data-ttu-id="10539-480">Als de tabelgegevens worden geëxporteerd naar een blob en de grootte van het geëxporteerde bestand met de limiet van 200 GB voor de Blobgrootte van de bereikt, klikt u vervolgens splitst AzCopy het geëxporteerde bestand, zelfs als deze optie is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="10539-480">If the table data is exported to a blob, and the exported file size reaches the 200 GB limit for blob size, then AzCopy splits the exported file, even if this option is not specified.</span></span>

<span data-ttu-id="10539-481">**Van toepassing op:** tabellen</span><span class="sxs-lookup"><span data-stu-id="10539-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="10539-482">/ EntityOperation: 'InsertOrSkip' | 'InsertOrMerge' | 'InsertOrReplace'</span><span class="sxs-lookup"><span data-stu-id="10539-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="10539-483">Hiermee geeft u het gedrag van tabel gegevens importeren.</span><span class="sxs-lookup"><span data-stu-id="10539-483">Specifies the table data import behavior.</span></span>

* <span data-ttu-id="10539-484">InsertOrSkip - slaat een bestaande entiteit of een nieuwe entiteit ingevoegd als het bestand bestaat niet in de tabel.</span><span class="sxs-lookup"><span data-stu-id="10539-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="10539-485">InsertOrMerge - samenvoegingen van een bestaande entiteit of een nieuwe entiteit ingevoegd als het bestand bestaat niet in de tabel.</span><span class="sxs-lookup"><span data-stu-id="10539-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="10539-486">InsertOrReplace - wordt vervangen door een bestaande entiteit of een nieuwe entiteit ingevoegd als het bestand bestaat niet in de tabel.</span><span class="sxs-lookup"><span data-stu-id="10539-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="10539-487">**Van toepassing op:** tabellen</span><span class="sxs-lookup"><span data-stu-id="10539-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="10539-488">/ Manifest: 'manifest file'</span><span class="sxs-lookup"><span data-stu-id="10539-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="10539-489">Hiermee geeft u het manifestbestand voor de tabel exporteren en importeren.</span><span class="sxs-lookup"><span data-stu-id="10539-489">Specifies the manifest file for the table export and import operation.</span></span>

<span data-ttu-id="10539-490">Deze optie is optioneel tijdens de exportbewerking, AzCopy genereert een manifestbestand met vooraf gedefinieerde naam als deze optie niet is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="10539-490">This option is optional during the export operation, AzCopy generates a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="10539-491">Deze optie is vereist tijdens de importbewerking voor het zoeken van de gegevensbestanden.</span><span class="sxs-lookup"><span data-stu-id="10539-491">This option is required during the import operation for locating the data files.</span></span>

<span data-ttu-id="10539-492">**Van toepassing op:** tabellen</span><span class="sxs-lookup"><span data-stu-id="10539-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="10539-493">/ SyncCopy</span><span class="sxs-lookup"><span data-stu-id="10539-493">/SyncCopy</span></span>
<span data-ttu-id="10539-494">Geeft aan of synchroon kopiëren van bestanden tussen de twee eindpunten voor Azure Storage of BLOB's.</span><span class="sxs-lookup"><span data-stu-id="10539-494">Indicates whether to synchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="10539-495">AzCopy standaard gebruikt serverzijde asynchrone kopie.</span><span class="sxs-lookup"><span data-stu-id="10539-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="10539-496">Geef deze optie voor het uitvoeren van een synchrone kopie blobs of bestanden gedownload naar het lokale geheugen en vervolgens geüpload naar Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="10539-496">Specify this option to perform a synchronous copy, which downloads blobs or files to local memory and then uploads them to Azure Storage.</span></span>

<span data-ttu-id="10539-497">U kunt deze optie gebruiken bij het kopiëren van bestanden in Blob storage, binnen de opslag van bestanden of van Blob-opslag naar de opslag van bestanden of vice versa.</span><span class="sxs-lookup"><span data-stu-id="10539-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage to File storage or vice versa.</span></span>

<span data-ttu-id="10539-498">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="10539-499">/ SetContentType: 'content-type'</span><span class="sxs-lookup"><span data-stu-id="10539-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="10539-500">Hiermee geeft u het MIME-inhoudstype voor bestemming blobs of bestanden.</span><span class="sxs-lookup"><span data-stu-id="10539-500">Specifies the MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="10539-501">AzCopy wordt het type inhoud voor een blob of het bestand is ingesteld op application/octet-stream standaard.</span><span class="sxs-lookup"><span data-stu-id="10539-501">AzCopy sets the content type for a blob or file to application/octet-stream by default.</span></span> <span data-ttu-id="10539-502">U kunt het type inhoud voor alle blobs of bestanden instellen door een waarde op voor deze optie expliciet op te geven.</span><span class="sxs-lookup"><span data-stu-id="10539-502">You can set the content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="10539-503">Als u deze optie geen waarde opgeeft, stelt AzCopy elke blob of inhoudstype volgens de bestandsextensie van het bestand.</span><span class="sxs-lookup"><span data-stu-id="10539-503">If you specify this option without a value, then AzCopy sets each blob or file's content type according to its file extension.</span></span>

<span data-ttu-id="10539-504">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="10539-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="10539-505">/ PayloadFormat: 'JSON' | 'CSV'</span><span class="sxs-lookup"><span data-stu-id="10539-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="10539-506">Hiermee geeft u de indeling van het bestand met geëxporteerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="10539-506">Specifies the format of the table exported data file.</span></span>

<span data-ttu-id="10539-507">Als deze optie niet is opgegeven, standaard exporteert AzCopy gegevensbestand van de tabel in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="10539-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="10539-508">**Van toepassing op:** tabellen</span><span class="sxs-lookup"><span data-stu-id="10539-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="10539-509">Bekende problemen en aanbevolen procedures</span><span class="sxs-lookup"><span data-stu-id="10539-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="10539-510">Limiet voor gelijktijdige schrijfbewerkingen tijdens het kopiëren van gegevens</span><span class="sxs-lookup"><span data-stu-id="10539-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="10539-511">Als u blobs of bestanden met AzCopy kopieert, houd er rekening mee dat een andere toepassing de gegevens heeft terwijl u kopieert.</span><span class="sxs-lookup"><span data-stu-id="10539-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span></span> <span data-ttu-id="10539-512">Indien mogelijk, zorg dat de gegevens die u wilt kopiëren niet tijdens de kopieerbewerking wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="10539-512">If possible, ensure that the data you are copying is not being modified during the copy operation.</span></span> <span data-ttu-id="10539-513">Bijvoorbeeld bij het kopiëren van een VHD die is gekoppeld aan een virtuele machine van Azure, zorg dat er geen andere toepassingen momenteel voor de VHD schrijft.</span><span class="sxs-lookup"><span data-stu-id="10539-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span></span> <span data-ttu-id="10539-514">Een goede manier om dit te doen is door het leasen van de resource te worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="10539-514">A good way to do this is by leasing the resource to be copied.</span></span> <span data-ttu-id="10539-515">U kunt ook eerst een momentopname van de VHD maken en kopieer de momentopname.</span><span class="sxs-lookup"><span data-stu-id="10539-515">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span></span>

<span data-ttu-id="10539-516">Als u niet voorkomen andere toepassingen dat bij het schrijven naar blobs of bestanden, terwijl ze worden gekopieerd, klikt u vervolgens Houd er rekening mee dat op het moment dat de taak is voltooid, de gekopieerde resources niet meer mogelijk volledige pariteit met de bron-resources.</span><span class="sxs-lookup"><span data-stu-id="10539-516">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="10539-517">Één AzCopy-sessie uitvoeren op één computer.</span><span class="sxs-lookup"><span data-stu-id="10539-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="10539-518">AzCopy is ontworpen om u te maximaliseren van uw machinebron de gegevensoverdracht versnellen, is het raadzaam u slechts één exemplaar van AzCopy uitvoeren op één machine en selecteer de optie `/NC` als u meer gelijktijdige bewerkingen nodig.</span><span class="sxs-lookup"><span data-stu-id="10539-518">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="10539-519">Typ voor meer informatie `AzCopy /?:NC` op de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="10539-519">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="10539-520">FIPS-compatibele MD5-algoritmen voor AzCopy inschakelen wanneer u ' gebruik FIPS compatibele algoritmen voor versleuteling, hashing en ondertekening '.</span><span class="sxs-lookup"><span data-stu-id="10539-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="10539-521">AzCopy standaard .NET MD5-implementatie gebruikt voor het berekenen van de MD5 bij het kopiëren van objecten, maar er zijn bepaalde beveiligingsvereisten voor de die AzCopy inschakelen FIPS-compatibele MD5-instelling nodig.</span><span class="sxs-lookup"><span data-stu-id="10539-521">AzCopy by default uses .NET MD5 implementation to calculate the MD5 when copying objects, but there are some security requirements that need AzCopy to enable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="10539-522">U kunt een app.config-bestand maken `AzCopy.exe.config` met de eigenschap `AzureStorageUseV1MD5` en reserveer met AzCopy.exe plaatsen.</span><span class="sxs-lookup"><span data-stu-id="10539-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="10539-523">De standaardwaarde AzCopy gebruikt voor eigenschap 'AzureStorageUseV1MD5' • True - .NET MD5-implementatie.</span><span class="sxs-lookup"><span data-stu-id="10539-523">For property "AzureStorageUseV1MD5" • True - The default value, AzCopy uses .NET MD5 implementation.</span></span>
<span data-ttu-id="10539-524">• ONWAAR – AzCopy hierbij wordt gebruikgemaakt van FIPS-compatibele MD5-algoritmen.</span><span class="sxs-lookup"><span data-stu-id="10539-524">• False – AzCopy uses FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="10539-525">Houd er rekening mee dat FIPS-algoritmen is standaard uitgeschakeld in uw Windows-computer, kunt u secpol.msc typt in het venster uitvoeren en controleer of deze switch op beveiligingsinstelling -> lokaal beleid -> Beveiliging -> Systeemcryptografie: gebruik FIPS-algoritmen voor versleuteling, hashing en ondertekening.</span><span class="sxs-lookup"><span data-stu-id="10539-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10539-526">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="10539-526">Next steps</span></span>
<span data-ttu-id="10539-527">Zie de volgende bronnen voor meer informatie over Azure Storage en AzCopy:</span><span class="sxs-lookup"><span data-stu-id="10539-527">For more information about Azure Storage and AzCopy, see the following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="10539-528">Documentatie bij Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="10539-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="10539-529">Inleiding tot Azure Storage</span><span class="sxs-lookup"><span data-stu-id="10539-529">Introduction to Azure Storage</span></span>](../storage-introduction.md)
* [<span data-ttu-id="10539-530">Het Blob storage gebruiken met .NET</span><span class="sxs-lookup"><span data-stu-id="10539-530">How to use Blob storage from .NET</span></span>](../blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="10539-531">Hoe File storage gebruiken met .NET</span><span class="sxs-lookup"><span data-stu-id="10539-531">How to use File storage from .NET</span></span>](../storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="10539-532">Hoe Table storage gebruiken met .NET</span><span class="sxs-lookup"><span data-stu-id="10539-532">How to use Table storage from .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="10539-533">Het maken, beheren of een opslagaccount verwijderen</span><span class="sxs-lookup"><span data-stu-id="10539-533">How to create, manage, or delete a storage account</span></span>](../storage-create-storage-account.md)
* [<span data-ttu-id="10539-534">Gegevensoverdracht met AzCopy op Linux</span><span class="sxs-lookup"><span data-stu-id="10539-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="10539-535">Azure Storage-blogberichten:</span><span class="sxs-lookup"><span data-stu-id="10539-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="10539-536">Inleiding tot Azure Storage Data Movement bibliotheek-Preview</span><span class="sxs-lookup"><span data-stu-id="10539-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="10539-537">AzCopy: Introducing synchrone kopiëren en aangepaste type inhoud</span><span class="sxs-lookup"><span data-stu-id="10539-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="10539-538">AzCopy: Aangekondigd algemene beschikbaarheid van AzCopy 3.0 plus preview-versie van AzCopy 4.0 met de ondersteuning voor de tabel en de bestandsnaam</span><span class="sxs-lookup"><span data-stu-id="10539-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="10539-539">AzCopy: Geoptimaliseerd voor grootschalige kopie scenario 's</span><span class="sxs-lookup"><span data-stu-id="10539-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="10539-540">AzCopy: Ondersteuning voor geografisch redundante opslag met leestoegang</span><span class="sxs-lookup"><span data-stu-id="10539-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="10539-541">AzCopy: Gegevensoverdracht met modus opnieuw gestart en SAS-token</span><span class="sxs-lookup"><span data-stu-id="10539-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="10539-542">AzCopy: Cross-account kopiëren Blob met behulp</span><span class="sxs-lookup"><span data-stu-id="10539-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="10539-543">AzCopy: Uploaden/downloaden van bestanden voor Azure Blobs</span><span class="sxs-lookup"><span data-stu-id="10539-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

