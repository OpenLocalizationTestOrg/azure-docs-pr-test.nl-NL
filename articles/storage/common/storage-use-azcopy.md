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
# <a name="transfer-data-with-hello-azcopy-on-windows"></a><span data-ttu-id="f97b3-105">Gegevensoverdracht met Hallo AzCopy in Windows</span><span class="sxs-lookup"><span data-stu-id="f97b3-105">Transfer data with hello AzCopy on Windows</span></span>
<span data-ttu-id="f97b3-106">AzCopy is een opdrachtregelprogramma dat is ontworpen voor het kopiëren van gegevens tooand van Microsoft Azure Blob-, bestands- en tabel opslag met behulp van eenvoudige opdrachten met optimale prestaties.</span><span class="sxs-lookup"><span data-stu-id="f97b3-106">AzCopy is a command-line utility designed for copying data tooand from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="f97b3-107">U kunt gegevens kopiëren van een object tooanother binnen uw opslagaccount of tussen opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="f97b3-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="f97b3-108">Er zijn twee versies van AzCopy die u kunt downloaden.</span><span class="sxs-lookup"><span data-stu-id="f97b3-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="f97b3-109">AzCopy in Windows is gebouwd met .NET Framework en Windows-stijl biedt opdrachtregelopties.</span><span class="sxs-lookup"><span data-stu-id="f97b3-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="f97b3-110">[AzCopy op Linux](storage-use-azcopy-linux.md) is gebouwd met .NET Core Framework die gericht is op Linux-platforms biedt POSIX-stijl opdrachtregelopties.</span><span class="sxs-lookup"><span data-stu-id="f97b3-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="f97b3-111">In dit artikel bevat informatie over AzCopy in Windows.</span><span class="sxs-lookup"><span data-stu-id="f97b3-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="f97b3-112">Downloaden en installeren van AzCopy</span><span class="sxs-lookup"><span data-stu-id="f97b3-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="f97b3-113">AzCopy in Windows</span><span class="sxs-lookup"><span data-stu-id="f97b3-113">AzCopy on Windows</span></span>
<span data-ttu-id="f97b3-114">Hallo downloaden [meest recente versie van AzCopy op Windows](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="f97b3-114">Download hello [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="f97b3-115">Installatie op Windows</span><span class="sxs-lookup"><span data-stu-id="f97b3-115">Installation on Windows</span></span>
<span data-ttu-id="f97b3-116">Na de installatie van AzCopy op Windows installer hello gebruiken, open een opdrachtvenster en navigeer toohello AzCopy-installatiemap op uw computer - waar hello `AzCopy.exe` uitvoerbare bestand zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="f97b3-116">After installing AzCopy on Windows using hello installer, open a command window and navigate toohello AzCopy installation directory on your computer - where hello `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="f97b3-117">Indien gewenst, kunt u Hallo AzCopy locatie tooyour system installatiepad kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f97b3-117">If desired, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="f97b3-118">AzCopy is standaard te`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` of `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="f97b3-118">By default, AzCopy is installed too`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="f97b3-119">Schrijven van uw eerste AzCopy-opdracht</span><span class="sxs-lookup"><span data-stu-id="f97b3-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="f97b3-120">Hallo basic syntaxis voor opdrachten van AzCopy is:</span><span class="sxs-lookup"><span data-stu-id="f97b3-120">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="f97b3-121">Hallo volgen voorbeelden laten zien dat verschillende scenario's voor het kopiëren van gegevens tooand van Microsoft Azure Blobs, bestanden en tabellen.</span><span class="sxs-lookup"><span data-stu-id="f97b3-121">hello following examples demonstrate a variety of scenarios for copying data tooand from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="f97b3-122">Raadpleeg toohello [AzCopy Parameters](#azcopy-parameters) sectie voor een gedetailleerde beschrijving van het Hallo-parameters die worden gebruikt in elk voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f97b3-122">Refer toohello [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="f97b3-123">BLOB: downloaden</span><span class="sxs-lookup"><span data-stu-id="f97b3-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="f97b3-124">Enkele blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="f97b3-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="f97b3-125">Houd er rekening mee dat als Hallo map `C:\myfolder` niet bestaat, AzCopy maakt het en downloaden `abc.txt ` in Hallo nieuwe map.</span><span class="sxs-lookup"><span data-stu-id="f97b3-125">Note that if hello folder `C:\myfolder` does not exist, AzCopy creates it and download `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="f97b3-126">Downloaden van één blob van de secundaire regio</span><span class="sxs-lookup"><span data-stu-id="f97b3-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="f97b3-127">Houd er rekening mee dat u geografisch redundante opslag met leestoegang ingeschakeld nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="f97b3-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="f97b3-128">Alle blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="f97b3-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="f97b3-129">Wordt ervan uitgegaan dat de volgende Hallo BLOB's zich bevinden in de opgegeven container Hallo:</span><span class="sxs-lookup"><span data-stu-id="f97b3-129">Assume hello following blobs reside in hello specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="f97b3-130">Na de bewerking van de download hello, Hallo directory `C:\myfolder` omvat Hallo volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="f97b3-130">After hello download operation, hello directory `C:\myfolder` includes hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="f97b3-131">Als u geen optie opgeeft `/S`, geen blobs worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="f97b3-131">If you do not specify option `/S`, no blobs are downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="f97b3-132">Blobs met het opgegeven voorvoegsel downloaden</span><span class="sxs-lookup"><span data-stu-id="f97b3-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="f97b3-133">Wordt ervan uitgegaan dat de volgende Hallo BLOB's zich bevinden in de opgegeven container Hallo.</span><span class="sxs-lookup"><span data-stu-id="f97b3-133">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="f97b3-134">Alle blobs vanaf Hallo voorvoegsel `a` worden gedownload:</span><span class="sxs-lookup"><span data-stu-id="f97b3-134">All blobs beginning with hello prefix `a` are downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="f97b3-135">Na de bewerking van de download hello, Hallo map `C:\myfolder` bevat Hallo volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="f97b3-135">After hello download operation, hello folder `C:\myfolder` includes hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="f97b3-136">Hallo-voorvoegsel is van toepassing toohello virtuele map, die Hallo eerste deel van Hallo blob-naam uitmaakt.</span><span class="sxs-lookup"><span data-stu-id="f97b3-136">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="f97b3-137">In het bovenstaande voorbeeld hello, Hallo virtuele map komt niet overeen met het opgegeven voorvoegsel hello, zodat deze niet is gedownload.</span><span class="sxs-lookup"><span data-stu-id="f97b3-137">In hello example shown above, hello virtual directory does not match hello specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="f97b3-138">Bovendien, als hello optie `\S` niet is opgegeven, AzCopy biedt niet alle blobs downloaden.</span><span class="sxs-lookup"><span data-stu-id="f97b3-138">In addition, if hello option `\S` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="f97b3-139">Hallo tijd laatste wijziging van de geëxporteerde bestanden toobe instellen hetzelfde als de bron blobs Hallo</span><span class="sxs-lookup"><span data-stu-id="f97b3-139">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="f97b3-140">U kunt ook BLOB's uitsluiten van Hallo downloaden van de bewerking op basis van hun tijd voor het laatst is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="f97b3-140">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="f97b3-141">Bijvoorbeeld, als u tooexclude blobs waarvan laatst gewijzigd-tijd Hallo dezelfde of een nieuwer is dan het doelbestand hello wilt is, toevoegen Hallo `/XN` optie:</span><span class="sxs-lookup"><span data-stu-id="f97b3-141">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="f97b3-142">Of als u tooexclude blobs waarvan laatst gewijzigd-tijd Hallo dezelfde of een ouder is dan het doelbestand hello wilt is, toe te voegen Hallo `/XO` optie:</span><span class="sxs-lookup"><span data-stu-id="f97b3-142">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="f97b3-143">BLOB: uploaden</span><span class="sxs-lookup"><span data-stu-id="f97b3-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="f97b3-144">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="f97b3-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="f97b3-145">Als Hallo opgegeven bestemmingscontainer niet bestaat, AzCopy wordt deze gemaakt en uploads Hallo bestand in de App.</span><span class="sxs-lookup"><span data-stu-id="f97b3-145">If hello specified destination container does not exist, AzCopy creates it and uploads hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="f97b3-146">Enkel bestand toovirtual directory uploaden</span><span class="sxs-lookup"><span data-stu-id="f97b3-146">Upload single file toovirtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="f97b3-147">Als Hallo virtuele map bestaat niet opgegeven, AzCopy uploadt Hallo bestand tooinclude Hallo virtuele map in de naam (*bijvoorbeeld*, `vd/abc.txt` in bovenstaande Hallo voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="f97b3-147">If hello specified virtual directory does not exist, AzCopy uploads hello file tooinclude hello virtual directory in its name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="f97b3-148">Alle bestanden uploaden</span><span class="sxs-lookup"><span data-stu-id="f97b3-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="f97b3-149">Optie `/S` uploads Hallo inhoud Hallo opgegeven directory tooBlob opslag recursief, wat betekent dat alle submappen en de bestanden ook worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="f97b3-149">Specifying option `/S` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="f97b3-150">Voor het exemplaar wordt ervan uitgegaan dat de volgende Hallo bestanden bevinden zich in map `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="f97b3-150">For instance, assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="f97b3-151">Na het Hallo-uploadbewerking bevat Hallo container Hallo volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="f97b3-151">After hello upload operation, hello container includes hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="f97b3-152">Als u geen optie opgeeft `/S`, AzCopy biedt recursief niet uploaden.</span><span class="sxs-lookup"><span data-stu-id="f97b3-152">If you do not specify option `/S`, AzCopy does not upload recursively.</span></span> <span data-ttu-id="f97b3-153">Na het Hallo-uploadbewerking bevat Hallo container Hallo volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="f97b3-153">After hello upload operation, hello container includes hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="f97b3-154">Uploaden van bestanden die overeenkomen met opgegeven patroon</span><span class="sxs-lookup"><span data-stu-id="f97b3-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="f97b3-155">Wordt ervan uitgegaan dat de volgende Hallo bestanden bevinden zich in map `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="f97b3-155">Assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="f97b3-156">Na het Hallo-uploadbewerking bevat Hallo container Hallo volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="f97b3-156">After hello upload operation, hello container includes hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="f97b3-157">Als u geen optie opgeeft `/S`, AzCopy uploadt alleen blobs die zich niet in een virtuele map bevinden:</span><span class="sxs-lookup"><span data-stu-id="f97b3-157">If you do not specify option `/S`, AzCopy only uploads blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="f97b3-158">Geef Hallo MIME-inhoudstype van een bestemmings-blob</span><span class="sxs-lookup"><span data-stu-id="f97b3-158">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="f97b3-159">Standaard stelt AzCopy Hallo-inhoudstype van een bestemmings-blob te`application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="f97b3-159">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="f97b3-160">Vanaf versie 3.1.0, kunt u expliciet opgeven Hallo inhoudstype via Hallo-optie `/SetContentType:[content-type]`.</span><span class="sxs-lookup"><span data-stu-id="f97b3-160">Beginning with version 3.1.0, you can explicitly specify hello content type via hello option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="f97b3-161">Deze syntaxis wordt Hallo inhoudstype voor alle blobs in een uploadbewerking.</span><span class="sxs-lookup"><span data-stu-id="f97b3-161">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="f97b3-162">Als u opgeeft `/SetContentType` zonder een waarde ingesteld AzCopy elke blob of inhoudstype van het bestand volgens tooits bestandsextensie.</span><span class="sxs-lookup"><span data-stu-id="f97b3-162">If you specify `/SetContentType` without a value, AzCopy sets each blob or file's content type according tooits file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="f97b3-163">BLOB: kopiëren</span><span class="sxs-lookup"><span data-stu-id="f97b3-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="f97b3-164">Één blob binnen opslagaccount kopiëren</span><span class="sxs-lookup"><span data-stu-id="f97b3-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="f97b3-165">Wanneer u een blob binnen een opslagaccount kopieert een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f97b3-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="f97b3-166">Één blob kopiëren tussen opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="f97b3-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="f97b3-167">Wanneer u een blob tussen opslagaccounts kopieert, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f97b3-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="f97b3-168">Één blob kopiëren van de secundaire regio tooprimary regio</span><span class="sxs-lookup"><span data-stu-id="f97b3-168">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="f97b3-169">Houd er rekening mee dat u geografisch redundante opslag met leestoegang ingeschakeld nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="f97b3-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="f97b3-170">Één blob en bijbehorende momentopnamen kopiëren tussen opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="f97b3-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="f97b3-171">Na de kopieerbewerking hello omvat doelcontainer Hallo Hallo blob en het bijbehorende momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="f97b3-171">After hello copy operation, hello target container includes hello blob and its snapshots.</span></span> <span data-ttu-id="f97b3-172">Ervan uitgaande dat Hallo blob in bovenstaande Hallo voorbeeld heeft twee momentopnamen, Hallo container bevat Hallo volgende blob en momentopnamen:</span><span class="sxs-lookup"><span data-stu-id="f97b3-172">Assuming hello blob in hello example above has two snapshots, hello container includes hello following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="f97b3-173">Synchroon kopiëren van BLOB's tussen opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="f97b3-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="f97b3-174">AzCopy standaard worden de gegevens tussen de twee eindpunten voor opslag asynchroon gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="f97b3-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="f97b3-175">Daarom Hallo kopie-bewerking wordt uitgevoerd op Hallo achtergrond met behulp van ongebruikte bandbreedtecapaciteit die geen SLA in termen van hoe snel een blob heeft wordt gekopieerd en AzCopy controleert periodiek Hallo kopiestatus totdat Hallo kopiëren is voltooid of mislukt.</span><span class="sxs-lookup"><span data-stu-id="f97b3-175">Therefore, hello copy operation runs in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied, and AzCopy periodically checks hello copy status until hello copying is completed or failed.</span></span>

<span data-ttu-id="f97b3-176">Hallo `/SyncCopy` optie zorgt ervoor dat de kopieerbewerking Hallo consistente snelheid opgehaald.</span><span class="sxs-lookup"><span data-stu-id="f97b3-176">hello `/SyncCopy` option ensures that hello copy operation gets consistent speed.</span></span> <span data-ttu-id="f97b3-177">AzCopy voert synchrone kopie Hallo Hallo blobs downloaden toocopy van Hallo opgegeven bron toolocal geheugen en uploadt deze toohello Blob-opslaglocatie.</span><span class="sxs-lookup"><span data-stu-id="f97b3-177">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="f97b3-178">`/SyncCopy`Als u meer uitgaande kosten vergeleken tooasynchronous kopiëren, hello mogelijk gegenereerd aanbevolen benadering toouse is deze optie in een Azure VM in Hallo dezelfde regio bevinden als uw gegevensbron account tooavoid uitgaande opslagkosten.</span><span class="sxs-lookup"><span data-stu-id="f97b3-178">`/SyncCopy` might generate additional egress cost compared tooasynchronous copy, hello recommended approach is toouse this option in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="f97b3-179">Bestand: downloaden</span><span class="sxs-lookup"><span data-stu-id="f97b3-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="f97b3-180">Enkel bestand downloaden</span><span class="sxs-lookup"><span data-stu-id="f97b3-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="f97b3-181">Als Hallo bron is een Azure-bestandsshare opgegeven, moet u de exacte bestandsnaam hello, opgeven (*bijvoorbeeld* `abc.txt`) toodownload één bestand of de optie `/S` toodownload alle bestanden in de share Hallo recursief.</span><span class="sxs-lookup"><span data-stu-id="f97b3-181">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `/S` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="f97b3-182">Toospecify poging een patroon en de optie `/S` samen resulteert in een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="f97b3-182">Attempting toospecify both a file pattern and option `/S` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="f97b3-183">Alle bestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="f97b3-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="f97b3-184">Alle lege mappen zijn niet gedownload.</span><span class="sxs-lookup"><span data-stu-id="f97b3-184">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="f97b3-185">Bestand: uploaden</span><span class="sxs-lookup"><span data-stu-id="f97b3-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="f97b3-186">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="f97b3-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="f97b3-187">Alle bestanden uploaden</span><span class="sxs-lookup"><span data-stu-id="f97b3-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="f97b3-188">Houd er rekening mee dat alle lege mappen niet worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="f97b3-188">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="f97b3-189">Uploaden van bestanden die overeenkomen met opgegeven patroon</span><span class="sxs-lookup"><span data-stu-id="f97b3-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="f97b3-190">Bestand: kopiëren</span><span class="sxs-lookup"><span data-stu-id="f97b3-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="f97b3-191">Kopiëren via bestandsshares</span><span class="sxs-lookup"><span data-stu-id="f97b3-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="f97b3-192">Wanneer u een bestand via bestandsshares kopiëren, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f97b3-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="f97b3-193">Kopiëren van bestandsshare tooblob</span><span class="sxs-lookup"><span data-stu-id="f97b3-193">Copy from file share tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="f97b3-194">Wanneer u een bestand vanuit bestandsshare tooblob kopiëren, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f97b3-194">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="f97b3-195">Kopiëren van blob toofile share</span><span class="sxs-lookup"><span data-stu-id="f97b3-195">Copy from blob toofile share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="f97b3-196">Wanneer u een bestand van blob toofile share kopiëren, een [serverversie](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f97b3-196">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="f97b3-197">Synchroon bestanden kopiëren</span><span class="sxs-lookup"><span data-stu-id="f97b3-197">Synchronously copy files</span></span>
<span data-ttu-id="f97b3-198">U kunt opgeven dat Hallo `/SyncCopy` optie toocopy gegevens van File Storage tooFile opslag van File Storage tooBlob opslag en van Blob Storage tooFile opslag synchroon, AzCopy doet dit door Hallo bron gegevens toolocal geheugen downloaden en te uploaden opnieuw toodestination.</span><span class="sxs-lookup"><span data-stu-id="f97b3-198">You can specify hello `/SyncCopy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously, AzCopy does this by downloading hello source data toolocal memory and upload it again toodestination.</span></span> <span data-ttu-id="f97b3-199">Standaard uitgaande kosten worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="f97b3-199">Standard egress cost applies.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="f97b3-200">Bij het kopiëren van File Storage tooBlob opslag, Hallo standaard blob-type blok-blob is, optie kunt u opgeven `/BlobType:page` toochange Hallo doeltype blob.</span><span class="sxs-lookup"><span data-stu-id="f97b3-200">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="f97b3-201">Houd er rekening mee dat `/SyncCopy` kan extra uitgaande kosten vergelijken tooasynchronous kopiëren, Hallo aanbevolen aanpak is deze optie in Azure VM is in Hallo Hallo toouse dezelfde regio bevinden als uw gegevensbron account tooavoid uitgaande opslagkosten.</span><span class="sxs-lookup"><span data-stu-id="f97b3-201">Note that `/SyncCopy` might generate additional egress cost comparing tooasynchronous copy, hello recommended approach is toouse this option in hello Azure VM which is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="f97b3-202">Tabel: exporteren</span><span class="sxs-lookup"><span data-stu-id="f97b3-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="f97b3-203">Tabel exporteren</span><span class="sxs-lookup"><span data-stu-id="f97b3-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="f97b3-204">AzCopy schrijft een doelmap manifestbestand toohello opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f97b3-204">AzCopy writes a manifest file toohello specified destination folder.</span></span> <span data-ttu-id="f97b3-205">Hallo-manifestbestand wordt gebruikt in Hallo importeren proces toolocate Hallo gegevens die nodig zijn bestanden en gegevensvalidatie is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f97b3-205">hello manifest file is used in hello import process toolocate hello necessary data files and perform data validation.</span></span> <span data-ttu-id="f97b3-206">Hallo-manifestbestand Hallo naamconventie volgen standaard gebruikt:</span><span class="sxs-lookup"><span data-stu-id="f97b3-206">hello manifest file uses hello following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="f97b3-207">Gebruiker kan ook Hallo optie opgeven `/Manifest:<manifest file name>` tooset Hallo manifestbestand naam.</span><span class="sxs-lookup"><span data-stu-id="f97b3-207">User can also specify hello option `/Manifest:<manifest file name>` tooset hello manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="f97b3-208">De export splitsen in meerdere bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="f97b3-209">AzCopy gebruikt een *volume index* in Hallo gegevens splitsen bestandsnamen toodistinguish meerdere bestanden.</span><span class="sxs-lookup"><span data-stu-id="f97b3-209">AzCopy uses a *volume index* in hello split data file names toodistinguish multiple files.</span></span> <span data-ttu-id="f97b3-210">Hallo volume index bestaat uit twee delen: een *partitie sleutel bereikindex* en een *gesplitste bestandsindex*.</span><span class="sxs-lookup"><span data-stu-id="f97b3-210">hello volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="f97b3-211">Beide indexen zijn gebaseerd op nul.</span><span class="sxs-lookup"><span data-stu-id="f97b3-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="f97b3-212">Hallo partitioneren van index sleutel bereik is 0 als Hallo gebruiker geen optie geeft `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="f97b3-212">hello partition key range index is 0 if hello user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="f97b3-213">Stel AzCopy genereert twee gegevensbestanden nadat Hallo gebruiker Hiermee kunt u de optie `/SplitSize`.</span><span class="sxs-lookup"><span data-stu-id="f97b3-213">For instance, suppose AzCopy generates two data files after hello user specifies option `/SplitSize`.</span></span> <span data-ttu-id="f97b3-214">Hallo resulterende bestandsnamen gegevens mogelijk:</span><span class="sxs-lookup"><span data-stu-id="f97b3-214">hello resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="f97b3-215">Houd er rekening mee dat Hallo mogelijke minimumwaarde voor de optie `/SplitSize` is 32 MB.</span><span class="sxs-lookup"><span data-stu-id="f97b3-215">Note that hello minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="f97b3-216">Als Hallo opgegeven bestemming is Blob-opslag, AzCopy Hallo gegevensbestand splitst zodra de grootte bereikt Hallo blob de maximale grootte (200GB), ongeacht of optie `/SplitSize` is opgegeven door de gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="f97b3-216">If hello specified destination is Blob storage, AzCopy splits hello data file once its sizes reaches hello blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by hello user.</span></span>

### <a name="export-table-toojson-or-csv-data-file-format"></a><span data-ttu-id="f97b3-217">Tabel tooJSON of CSV-gegevensbestandsindeling exporteren</span><span class="sxs-lookup"><span data-stu-id="f97b3-217">Export table tooJSON or CSV data file format</span></span>
<span data-ttu-id="f97b3-218">AzCopy standaard exporteert tabellen tooJSON gegevensbestanden worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f97b3-218">AzCopy by default exports tables tooJSON data files.</span></span> <span data-ttu-id="f97b3-219">U kunt de optie Hallo opgeven `/PayloadFormat:JSON|CSV` tooexport Hallo tabellen als JSON- of CSV.</span><span class="sxs-lookup"><span data-stu-id="f97b3-219">You can specify hello option `/PayloadFormat:JSON|CSV` tooexport hello tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="f97b3-220">Bij het opgeven van de indeling van nettolading CSV Hallo AzCopy ook genereert u een schemabestand met extensie `.schema.csv` voor elk gegevensbestand.</span><span class="sxs-lookup"><span data-stu-id="f97b3-220">When specifying hello CSV payload format, AzCopy also generates a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="f97b3-221">Tabelentiteiten gelijktijdig exporteren</span><span class="sxs-lookup"><span data-stu-id="f97b3-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="f97b3-222">AzCopy gelijktijdige bewerkingen tooexport entiteiten wordt gestart wanneer Hallo gebruiker Hiermee kunt u de optie `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="f97b3-222">AzCopy starts concurrent operations tooexport entities when hello user specifies option `/PKRS`.</span></span> <span data-ttu-id="f97b3-223">Elke bewerking exporteert een partitiesleutelbereik.</span><span class="sxs-lookup"><span data-stu-id="f97b3-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="f97b3-224">Houd er rekening mee dat het aantal gelijktijdige bewerkingen Hallo ook wordt beheerd door de optie `/NC`.</span><span class="sxs-lookup"><span data-stu-id="f97b3-224">Note that hello number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="f97b3-225">AzCopy gebruikt Hallo aantal coreprocessors als standaardwaarde Hallo van `/NC` bij het kopiëren van de tabelentiteiten, zelfs als `/NC` is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f97b3-225">AzCopy uses hello number of core processors as hello default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="f97b3-226">Als de gebruiker Hallo optie opgeeft `/PKRS`, AzCopy Hallo kleinere van Hallo twee waarden - partitie sleutelbereiken versus impliciet of expliciet opgegeven gelijktijdige bewerkingen - toodetermine Hallo aantal gelijktijdige bewerkingen toostart gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f97b3-226">When hello user specifies option `/PKRS`, AzCopy uses hello smaller of hello two values - partition key ranges versus implicitly or explicitly specified concurrent operations - toodetermine hello number of concurrent operations toostart.</span></span> <span data-ttu-id="f97b3-227">Typ voor meer informatie `AzCopy /?:NC` op Hallo-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="f97b3-227">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="export-table-tooblob"></a><span data-ttu-id="f97b3-228">Tabel tooblob exporteren</span><span class="sxs-lookup"><span data-stu-id="f97b3-228">Export table tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="f97b3-229">AzCopy genereert een JSON-gegevensbestand in Hallo blob-container met de volgende naamconventie:</span><span class="sxs-lookup"><span data-stu-id="f97b3-229">AzCopy generates a JSON data file into hello blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="f97b3-230">Hallo gegenereerd JSON-gegevensbestand heeft Hallo nettolading indeling voor minimale metagegevens.</span><span class="sxs-lookup"><span data-stu-id="f97b3-230">hello generated JSON data file follows hello payload format for minimal metadata.</span></span> <span data-ttu-id="f97b3-231">Zie voor meer informatie over deze indeling van nettolading [indeling van nettolading voor tabel servicebewerkingen](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span><span class="sxs-lookup"><span data-stu-id="f97b3-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="f97b3-232">Houd er rekening mee dat bij het exporteren van tabellen tooblobs AzCopy Hallo tabel entiteiten toolocal gegevens tijdelijke bestanden worden gedownload en uploadt u deze entiteiten toohello blob.</span><span class="sxs-lookup"><span data-stu-id="f97b3-232">Note that when exporting tables tooblobs, AzCopy downloads hello Table entities toolocal temporary data files and then uploads those entities toohello blob.</span></span> <span data-ttu-id="f97b3-233">Deze tijdelijke gegevensbestanden in Hallo journaal bestandsmap door het standaardpad Hallo zijn geplaatst '<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>', kunt u optie/Z: [journaal-map] toochange Hallo journaal bestandsmaplocatie en dus wijzigen Hallo tijdelijke locatie van bestanden.</span><span class="sxs-lookup"><span data-stu-id="f97b3-233">These temporary data files are put into hello journal file folder with hello default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] toochange hello journal file folder location and thus change hello temporary data files location.</span></span> <span data-ttu-id="f97b3-234">Hallo tijdelijke gegevens voor de grootte van bestanden wordt bepaald door de grootte en het Hallo-grootte Hallo optie /SplitSize opgegeven, uw tabelentiteiten Hoewel Hallo tijdelijke gegevensbestand in de lokale schijf onmiddellijk is verwijderd nadat deze is geüpload toohello blob, zorg dat u hebt Onvoldoende lokale schijf ruimte toostore deze tijdelijke gegevensbestanden voordat ze worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f97b3-234">hello temporary data files' size is decided by your table entities' size and hello size you specified with hello option /SplitSize, although hello temporary data file in local disk is deleted instantly once it has been uploaded toohello blob, please make sure you have enough local disk space toostore these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="f97b3-235">Tabel: importeren</span><span class="sxs-lookup"><span data-stu-id="f97b3-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="f97b3-236">Tabel importeren</span><span class="sxs-lookup"><span data-stu-id="f97b3-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="f97b3-237">Hallo optie `/EntityOperation` geeft aan hoe tooinsert entiteiten in de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="f97b3-237">hello option `/EntityOperation` indicates how tooinsert entities into hello table.</span></span> <span data-ttu-id="f97b3-238">Mogelijke waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="f97b3-238">Possible values are:</span></span>

* <span data-ttu-id="f97b3-239">`InsertOrSkip`: Hiermee slaat een bestaande entiteit of een nieuwe entiteit ingevoegd als het bestand niet in de tabel Hallo bestaat.</span><span class="sxs-lookup"><span data-stu-id="f97b3-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="f97b3-240">`InsertOrMerge`: Een bestaande entiteit samenvoegingen of een nieuwe entiteit ingevoegd als het bestand niet in de tabel Hallo bestaat.</span><span class="sxs-lookup"><span data-stu-id="f97b3-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="f97b3-241">`InsertOrReplace`: Een bestaande entiteit vervangt of een nieuwe entiteit ingevoegd als het bestand niet in de tabel Hallo bestaat.</span><span class="sxs-lookup"><span data-stu-id="f97b3-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="f97b3-242">Opmerking dat kunt u de optie opgeven `/PKRS` in Hallo importeren scenario.</span><span class="sxs-lookup"><span data-stu-id="f97b3-242">Note that you cannot specify option `/PKRS` in hello import scenario.</span></span> <span data-ttu-id="f97b3-243">In tegenstelling tot Hallo export scenario, waarin u de optie moet opgeven `/PKRS` toostart gelijktijdige bewerkingen, AzCopy gelijktijdige bewerkingen wordt standaard gestart bij het importeren van een tabel.</span><span class="sxs-lookup"><span data-stu-id="f97b3-243">Unlike hello export scenario, in which you must specify option `/PKRS` toostart concurrent operations, AzCopy starts concurrent operations by default when you import a table.</span></span> <span data-ttu-id="f97b3-244">Hallo standaardaantal gelijktijdige bewerkingen gestart is gelijk toohello aantal coreprocessors; u kunt echter een verschillend aantal gelijktijdige met optie opgeven `/NC`.</span><span class="sxs-lookup"><span data-stu-id="f97b3-244">hello default number of concurrent operations started is equal toohello number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="f97b3-245">Typ voor meer informatie `AzCopy /?:NC` op Hallo-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="f97b3-245">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

<span data-ttu-id="f97b3-246">Houd er rekening mee dat AzCopy biedt alleen ondersteuning voor JSON, niet-CSV importeren.</span><span class="sxs-lookup"><span data-stu-id="f97b3-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="f97b3-247">AzCopy niet ondersteunt tabel invoer van gebruiker gemaakte JSON en manifest bestanden.</span><span class="sxs-lookup"><span data-stu-id="f97b3-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="f97b3-248">Beide bestanden moeten afkomstig zijn van het exporteren van een AzCopy-tabel.</span><span class="sxs-lookup"><span data-stu-id="f97b3-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="f97b3-249">tooavoid fouten, mag niet worden gewijzigd Hallo JSON of manifestbestand geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="f97b3-249">tooavoid errors, please do not modify hello exported JSON or manifest file.</span></span>

### <a name="import-entities-tootable-using-blobs"></a><span data-ttu-id="f97b3-250">Importeren entiteiten tootable met behulp van BLOB 's</span><span class="sxs-lookup"><span data-stu-id="f97b3-250">Import entities tootable using blobs</span></span>
<span data-ttu-id="f97b3-251">Een Blob-container Hallo volgende bevat: een JSON-bestand voor een Azure-tabel en het bijbehorende manifest-bestand.</span><span class="sxs-lookup"><span data-stu-id="f97b3-251">Assume a Blob container contains hello following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="f97b3-252">U kunt na de opdracht tooimport entiteiten in een tabel met behulp van manifestbestand in de blobcontainer Hallo Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f97b3-252">You can run hello following command tooimport entities into a table using hello manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="f97b3-253">Andere functies van AzCopy</span><span class="sxs-lookup"><span data-stu-id="f97b3-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="f97b3-254">Alleen gegevens die niet in het Hallo-doel bestaat gekopieerd</span><span class="sxs-lookup"><span data-stu-id="f97b3-254">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="f97b3-255">Hallo `/XO` en `/XN` parameters kunt u tooexclude oudere of nieuwere bron resources wordt gekopieerd, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="f97b3-255">hello `/XO` and `/XN` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="f97b3-256">Als u alleen toocopy bron bronnen die niet bestaan in Hallo bestemming wilt, kunt u beide parameters in Hallo AzCopy-opdracht:</span><span class="sxs-lookup"><span data-stu-id="f97b3-256">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="f97b3-257">Houd er rekening mee dat dit wordt niet ondersteund wanneer het Hallo-bron- of doelserver een tabel wordt.</span><span class="sxs-lookup"><span data-stu-id="f97b3-257">Note that this is not supported when either hello source or destination is a table.</span></span>

### <a name="use-a-response-file-toospecify-command-line-parameters"></a><span data-ttu-id="f97b3-258">Gebruik een toospecify opdrachtregelprogramma responsbestandsparameters</span><span class="sxs-lookup"><span data-stu-id="f97b3-258">Use a response file toospecify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="f97b3-259">U kunt eventuele opdrachtregelparameters AzCopy opnemen in een responsbestand.</span><span class="sxs-lookup"><span data-stu-id="f97b3-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="f97b3-260">AzCopy processen Hallo parameters in Hallo bestand alsof ze op de opdrachtregel hello, uitvoeren van een directe vervanging met Hallo inhoud van Hallo bestand had is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f97b3-260">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="f97b3-261">Wordt ervan uitgegaan dat een antwoordbestand met de naam `copyoperation.txt`, die Hallo volgende regels bevat.</span><span class="sxs-lookup"><span data-stu-id="f97b3-261">Assume a response file named `copyoperation.txt`, that contains hello following lines.</span></span> <span data-ttu-id="f97b3-262">Elke parameter AzCopy kan op een enkele regel worden opgegeven</span><span class="sxs-lookup"><span data-stu-id="f97b3-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="f97b3-263">of op afzonderlijke regels:</span><span class="sxs-lookup"><span data-stu-id="f97b3-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="f97b3-264">AzCopy mislukt als u de parameter Hallo over twee regels verdelen, zoals hier wordt weergegeven voor Hallo `/sourcekey` parameter:</span><span class="sxs-lookup"><span data-stu-id="f97b3-264">AzCopy fails if you split hello parameter across two lines, as shown here for hello `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a><span data-ttu-id="f97b3-265">Gebruik van meerdere antwoord bestanden toospecify opdrachtregelparameters</span><span class="sxs-lookup"><span data-stu-id="f97b3-265">Use multiple response files toospecify command-line parameters</span></span>
<span data-ttu-id="f97b3-266">Wordt ervan uitgegaan dat een antwoordbestand met de naam `source.txt` die aangeeft dat een Broncontainer:</span><span class="sxs-lookup"><span data-stu-id="f97b3-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="f97b3-267">En een antwoordbestand met de naam `dest.txt` waarmee een doelmap in het bestandssysteem Hallo:</span><span class="sxs-lookup"><span data-stu-id="f97b3-267">And a response file named `dest.txt` that specifies a destination folder in hello file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="f97b3-268">En een antwoordbestand met de naam `options.txt` Hiermee worden de opties voor AzCopy:</span><span class="sxs-lookup"><span data-stu-id="f97b3-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="f97b3-269">toocall AzCopy met deze antwoordbestanden die zich bevinden in een map `C:\responsefiles`, gebruikt u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="f97b3-269">toocall AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="f97b3-270">AzCopy verwerkt met deze opdracht net zoals als u alle afzonderlijke parameters op opdrachtregel Hallo Hallo opgenomen:</span><span class="sxs-lookup"><span data-stu-id="f97b3-270">AzCopy processes this command just as it would if you included all of hello individual parameters on hello command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="f97b3-271">Geef een shared access signature (SAS)</span><span class="sxs-lookup"><span data-stu-id="f97b3-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="f97b3-272">U kunt ook een SAS voor Hallo container URI opgeven:</span><span class="sxs-lookup"><span data-stu-id="f97b3-272">You can also specify a SAS on hello container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="f97b3-273">Map voor logboek-bestand</span><span class="sxs-lookup"><span data-stu-id="f97b3-273">Journal file folder</span></span>
<span data-ttu-id="f97b3-274">Telkens wanneer die u een tooAzCopy opdracht de opdracht die wordt gecontroleerd of een journal-bestand in de standaardmap Hallo bestaat en of deze bestaat in een map die u hebt opgegeven via deze optie.</span><span class="sxs-lookup"><span data-stu-id="f97b3-274">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="f97b3-275">Hallo journaalbestand bestaat niet op beide plaatsen, AzCopy Hallo bewerking behandelt als nieuwe als genereert een nieuw journaalbestand.</span><span class="sxs-lookup"><span data-stu-id="f97b3-275">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="f97b3-276">Als Hallo journal-bestand bestaat, wordt door AzCopy gecontroleerd of Hallo-opdrachtregel die ingevoerde overeenkomt met Hallo vanaf de opdrachtregel in Hallo journal-bestand.</span><span class="sxs-lookup"><span data-stu-id="f97b3-276">If hello journal file does exist, AzCopy checks whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="f97b3-277">Als twee opdrachtregels Hallo overeenkomen, hervat AzCopy onvolledige Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="f97b3-277">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="f97b3-278">Als ze niet overeenkomen, bent u na vragen aan gebruiker tooeither overschrijven Hallo journaal bestand toostart een nieuwe bewerking of toocancel Hallo huidige bewerking.</span><span class="sxs-lookup"><span data-stu-id="f97b3-278">If they do not match, you are prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="f97b3-279">Als u wilt dat toouse Hallo-standaardlocatie voor Hallo journal-bestand:</span><span class="sxs-lookup"><span data-stu-id="f97b3-279">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="f97b3-280">Als u de optie weglaat `/Z`, of geef de optie `/Z` zonder Hallo mappad, zoals hierboven, AzCopy maakt Hallo journal-bestand in Hallo standaardlocatie is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="f97b3-280">If you omit option `/Z`, or specify option `/Z` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="f97b3-281">Als Hallo journaalbestand al bestaat, hervat AzCopy Hallo-bewerking op basis van Hallo journal-bestand.</span><span class="sxs-lookup"><span data-stu-id="f97b3-281">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="f97b3-282">Als u wilt dat een aangepaste locatie voor Hallo journaalbestand toospecify:</span><span class="sxs-lookup"><span data-stu-id="f97b3-282">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="f97b3-283">In dit voorbeeld maakt Hallo journal-bestand als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="f97b3-283">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="f97b3-284">Als deze bestaat, hervat AzCopy Hallo-bewerking op basis van Hallo journal-bestand.</span><span class="sxs-lookup"><span data-stu-id="f97b3-284">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="f97b3-285">Als u wilt dat een bewerking AzCopy tooresume:</span><span class="sxs-lookup"><span data-stu-id="f97b3-285">If you want tooresume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="f97b3-286">In dit voorbeeld hervat Hallo laatste bewerking, die mogelijk niet toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f97b3-286">This example resumes hello last operation, which may have failed toocomplete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="f97b3-287">Genereren van een logboekbestand</span><span class="sxs-lookup"><span data-stu-id="f97b3-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="f97b3-288">Als u de optie opgeven `/V` zonder op te geven van een bestand pad toohello uitgebreid logboek, AzCopy maakt vervolgens logboekbestand Hallo in Hallo standaardlocatie is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="f97b3-288">If you specify option `/V` without providing a file path toohello verbose log, then AzCopy creates hello log file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="f97b3-289">Anders kunt u een logboekbestand maken in een aangepaste locatie:</span><span class="sxs-lookup"><span data-stu-id="f97b3-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="f97b3-290">Houd er rekening mee dat als u een relatief pad na optie opgeeft `/V`, zoals `/V:test/azcopy1.log`, en vervolgens Hallo uitgebreide logboek in de huidige werkmap in een submap met de naam Hallo gemaakt `test`.</span><span class="sxs-lookup"><span data-stu-id="f97b3-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then hello verbose log is created in hello current working directory within a subfolder named `test`.</span></span>

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="f97b3-291">Geef het aantal gelijktijdige bewerkingen toostart Hallo</span><span class="sxs-lookup"><span data-stu-id="f97b3-291">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="f97b3-292">Optie `/NC` geeft het aantal gelijktijdige kopieerbewerkingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="f97b3-292">Option `/NC` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="f97b3-293">AzCopy wordt standaard een bepaald aantal gelijktijdige bewerkingen tooincrease Hallo-gegevensdoorvoer overdracht gestart.</span><span class="sxs-lookup"><span data-stu-id="f97b3-293">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="f97b3-294">Voor bewerkingen van de tabel is het aantal gelijktijdige bewerkingen Hallo gelijk toohello aantal processors dat u hebt.</span><span class="sxs-lookup"><span data-stu-id="f97b3-294">For Table operations, hello number of concurrent operations is equal toohello number of processors you have.</span></span> <span data-ttu-id="f97b3-295">Voor Blob- en bewerkingen, het aantal gelijktijdige bewerkingen Hallo is gelijk aan 8 keer Hallo aantal processors dat u hebt.</span><span class="sxs-lookup"><span data-stu-id="f97b3-295">For Blob and File operations, hello number of concurrent operations is equal 8 times hello number of processors you have.</span></span> <span data-ttu-id="f97b3-296">Als u via een netwerk met lage bandbreedte AzCopy uitvoert, kunt u een lager getal voor /NC tooavoid mislukt, omdat resource concurrentie opgeven.</span><span class="sxs-lookup"><span data-stu-id="f97b3-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC tooavoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="f97b3-297">AzCopy uitvoeren op Azure-Opslagemulator</span><span class="sxs-lookup"><span data-stu-id="f97b3-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="f97b3-298">U kunt AzCopy uitvoeren op Hallo [Azure-Opslagemulator](storage-use-emulator.md) voor Blobs:</span><span class="sxs-lookup"><span data-stu-id="f97b3-298">You can run AzCopy against hello [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="f97b3-299">en tabellen:</span><span class="sxs-lookup"><span data-stu-id="f97b3-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="f97b3-300">AzCopy-Parameters</span><span class="sxs-lookup"><span data-stu-id="f97b3-300">AzCopy Parameters</span></span>
<span data-ttu-id="f97b3-301">Parameters voor AzCopy worden hieronder beschreven.</span><span class="sxs-lookup"><span data-stu-id="f97b3-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="f97b3-302">U kunt ook een van de volgende opdrachten uit vanaf de opdrachtregel voor hulp bij het gebruik van AzCopy Hallo Hallo typen:</span><span class="sxs-lookup"><span data-stu-id="f97b3-302">You can also type one of hello following commands from hello command line for help in using AzCopy:</span></span>

* <span data-ttu-id="f97b3-303">Voor gedetailleerde help voor AzCopy:`AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="f97b3-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="f97b3-304">Voor gedetailleerde hulp bij elke parameter AzCopy:`AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="f97b3-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="f97b3-305">Voor voorbeelden van opdrachtregels:`AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="f97b3-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="f97b3-306">/ Source: 'bron'</span><span class="sxs-lookup"><span data-stu-id="f97b3-306">/Source:"source"</span></span>
<span data-ttu-id="f97b3-307">Hiermee geeft u de brongegevens Hallo uit welke toocopy.</span><span class="sxs-lookup"><span data-stu-id="f97b3-307">Specifies hello source data from which toocopy.</span></span> <span data-ttu-id="f97b3-308">Hallo bron mag een bestandssysteemmap, een blob-container, een blob virtuele map, een bestandsshare voor opslag, een map voor opslag of een Azure-tabel.</span><span class="sxs-lookup"><span data-stu-id="f97b3-308">hello source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="f97b3-309">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="f97b3-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="f97b3-310">/ Dest: "doelmap"</span><span class="sxs-lookup"><span data-stu-id="f97b3-310">/Dest:"destination"</span></span>
<span data-ttu-id="f97b3-311">Hiermee geeft u Hallo bestemming toocopy aan.</span><span class="sxs-lookup"><span data-stu-id="f97b3-311">Specifies hello destination toocopy to.</span></span> <span data-ttu-id="f97b3-312">Hallo bestemming mag een bestandssysteemmap, een blob-container, een blob virtuele map, een bestandsshare voor opslag, een map voor opslag of een Azure-tabel.</span><span class="sxs-lookup"><span data-stu-id="f97b3-312">hello destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="f97b3-313">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="f97b3-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="f97b3-314">/ Patroon: "bestandspatroon"</span><span class="sxs-lookup"><span data-stu-id="f97b3-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="f97b3-315">Hiermee geeft u een patroon waarmee wordt aangegeven welke toocopy bestanden.</span><span class="sxs-lookup"><span data-stu-id="f97b3-315">Specifies a file pattern that indicates which files toocopy.</span></span> <span data-ttu-id="f97b3-316">Hallo gedrag van Hallo /Pattern parameter wordt bepaald door het Hallo-locatie van de brongegevens Hallo en Hallo aanwezigheid van Hallo recursieve modusoptie.</span><span class="sxs-lookup"><span data-stu-id="f97b3-316">hello behavior of hello /Pattern parameter is determined by hello location of hello source data, and hello presence of hello recursive mode option.</span></span> <span data-ttu-id="f97b3-317">Recursieve modus wordt opgegeven via de optie/s.</span><span class="sxs-lookup"><span data-stu-id="f97b3-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="f97b3-318">Als Hallo opgegeven bron een map in het bestandssysteem hello, is wordt standaard jokertekens van kracht zijn en Hallo patroon opgegeven wordt vergeleken met de bestanden in de map Hallo.</span><span class="sxs-lookup"><span data-stu-id="f97b3-318">If hello specified source is a directory in hello file system, then standard wildcards are in effect, and hello file pattern provided is matched against files within hello directory.</span></span> <span data-ttu-id="f97b3-319">Als de optie die /s is opgegeven, klikt u vervolgens AzCopy, overeenkomt met opgegeven patroon Hallo tegen alle bestanden in eventuele submappen Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="f97b3-319">If option /S is specified, then AzCopy also matches hello specified pattern against all files in any subfolders beneath hello directory.</span></span>

<span data-ttu-id="f97b3-320">Als de opgegeven bron Hallo een blob-container of de virtuele map is, worden klikt u vervolgens jokertekens niet toegepast.</span><span class="sxs-lookup"><span data-stu-id="f97b3-320">If hello specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="f97b3-321">Als de optie/s is opgegeven, klikt u vervolgens AzCopy interpreteert Hallo opgegeven patroon als voorvoegsel van de blob.</span><span class="sxs-lookup"><span data-stu-id="f97b3-321">If option /S is specified, then AzCopy interprets hello specified file pattern as a blob prefix.</span></span> <span data-ttu-id="f97b3-322">Als de optie/s niet is opgegeven, klikt u vervolgens AzCopy komt overeen met patroon Hallo tegen exacte blob-namen.</span><span class="sxs-lookup"><span data-stu-id="f97b3-322">If option /S is not specified, then AzCopy matches hello file pattern against exact blob names.</span></span>

<span data-ttu-id="f97b3-323">Als Hallo bron is een Azure-bestandsshare opgegeven, moet u Hallo exacte bestandsnaam (bijvoorbeeld abc.txt) opgeven toocopy één bestand of het opgeven van de optie/s toocopy alle bestanden in Hallo share recursief.</span><span class="sxs-lookup"><span data-stu-id="f97b3-323">If hello specified source is an Azure file share, then you must either specify hello exact file name, (e.g. abc.txt) toocopy a single file, or specify option /S toocopy all files in hello share recursively.</span></span> <span data-ttu-id="f97b3-324">Toospecify beide wordt geprobeerd een bestand patroon en de optie/s samen met resultaten in een fout.</span><span class="sxs-lookup"><span data-stu-id="f97b3-324">Attempting toospecify both a file pattern and option /S together results in an error.</span></span>

<span data-ttu-id="f97b3-325">AzCopy gebruikt hoofdlettergevoelig overeenkomende wanneer Hallo/Source een blob-container of blob virtuele map is en maakt gebruik van niet-hoofdlettergevoelige die overeenkomt met alle andere gevallen Hallo.</span><span class="sxs-lookup"><span data-stu-id="f97b3-325">AzCopy uses case-sensitive matching when hello /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all hello other cases.</span></span>

<span data-ttu-id="f97b3-326">Hallo bestand standaardpatroon gebruikt wanneer er geen bestandspatroon is opgegeven is *.*</span><span class="sxs-lookup"><span data-stu-id="f97b3-326">hello default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="f97b3-327">voor een locatie in het bestandssysteem of een leeg voorvoegsel voor een Azure-opslaglocatie.</span><span class="sxs-lookup"><span data-stu-id="f97b3-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="f97b3-328">Meerdere bestand patronen opgeven wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="f97b3-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="f97b3-329">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="f97b3-330">/ DestKey: 'opslagsleutel'</span><span class="sxs-lookup"><span data-stu-id="f97b3-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="f97b3-331">Hiermee geeft u Hallo-toegangssleutel voor Hallo doelbron.</span><span class="sxs-lookup"><span data-stu-id="f97b3-331">Specifies hello storage account key for hello destination resource.</span></span>

<span data-ttu-id="f97b3-332">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="f97b3-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="f97b3-333">/ DestSAS: 'sas-token'</span><span class="sxs-lookup"><span data-stu-id="f97b3-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="f97b3-334">Hiermee geeft u een Shared Access Signature (SAS) met machtigingen voor lezen en schrijven voor Hallo doel (indien van toepassing).</span><span class="sxs-lookup"><span data-stu-id="f97b3-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for hello destination (if applicable).</span></span> <span data-ttu-id="f97b3-335">Hallo SAS met dubbele aanhalingstekens rond omdat deze mogelijk speciale opdrachtregelprogramma tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="f97b3-335">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="f97b3-336">Als Hallo doelbron een blob-container, een bestandsshare of een tabel is, kunt u deze optie gevolgd door de SAS-token Hallo opgeven of u Hallo SAS als onderdeel van Hallo bestemming blob-container, bestandsshare of de URI van de tabel, zonder deze optie kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="f97b3-336">If hello destination resource is a blob container, file share or table, you can either specify this option followed by hello SAS token, or you can specify hello SAS as part of hello destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="f97b3-337">Als Hallo bron- en doelserver beide blobs zijn, en vervolgens Hallo bestemmings-blob zich binnen Hallo dezelfde bevinden moet als Hallo bron blob storage-account.</span><span class="sxs-lookup"><span data-stu-id="f97b3-337">If hello source and destination are both blobs, then hello destination blob must reside within hello same storage account as hello source blob.</span></span>

<span data-ttu-id="f97b3-338">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="f97b3-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="f97b3-339">/ SourceKey: 'opslagsleutel'</span><span class="sxs-lookup"><span data-stu-id="f97b3-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="f97b3-340">Hiermee geeft u Hallo opslagaccountsleutel voor Hallo bronresource.</span><span class="sxs-lookup"><span data-stu-id="f97b3-340">Specifies hello storage account key for hello source resource.</span></span>

<span data-ttu-id="f97b3-341">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="f97b3-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="f97b3-342">/ SourceSAS: 'sas-token'</span><span class="sxs-lookup"><span data-stu-id="f97b3-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="f97b3-343">Hiermee geeft u een Shared Access Signature met lees- en machtigingen voor het Hallo-bron (indien van toepassing).</span><span class="sxs-lookup"><span data-stu-id="f97b3-343">Specifies a Shared Access Signature with READ and LIST permissions for hello source (if applicable).</span></span> <span data-ttu-id="f97b3-344">Hallo SAS met dubbele aanhalingstekens rond omdat deze mogelijk speciale opdrachtregelprogramma tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="f97b3-344">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="f97b3-345">Als Hallo bron bron een blob-container is en een sleutel noch een SAS is opgegeven, wordt Hallo blob-container gelezen via anonieme toegang.</span><span class="sxs-lookup"><span data-stu-id="f97b3-345">If hello source resource is a blob container, and neither a key nor a SAS is provided, then hello blob container is read via anonymous access.</span></span>

<span data-ttu-id="f97b3-346">Als het Hallo-bron is een bestandsshare of een sleutel of een SAS tabel moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f97b3-346">If hello source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="f97b3-347">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="f97b3-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="f97b3-348">/ S</span><span class="sxs-lookup"><span data-stu-id="f97b3-348">/S</span></span>
<span data-ttu-id="f97b3-349">Hiermee geeft u een recursieve modus voor het kopiëren van.</span><span class="sxs-lookup"><span data-stu-id="f97b3-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="f97b3-350">In de modus voor recursieve kopieert AzCopy alle blobs of bestanden die overeenkomen met Hallo opgegeven bestandspatroon, inclusief verbindingen in submappen.</span><span class="sxs-lookup"><span data-stu-id="f97b3-350">In recursive mode, AzCopy copies all blobs or files that match hello specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="f97b3-351">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="f97b3-352">/ BlobType: 'block' | "page" | "toevoegen"</span><span class="sxs-lookup"><span data-stu-id="f97b3-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="f97b3-353">Hiermee geeft u op of Hallo bestemmings-blob een blok-blob, een pagina-blob of een toevoeg-blob is.</span><span class="sxs-lookup"><span data-stu-id="f97b3-353">Specifies whether hello destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="f97b3-354">Deze optie is alleen toepasbaar wanneer u een blob uploadt.</span><span class="sxs-lookup"><span data-stu-id="f97b3-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="f97b3-355">Anders wordt er een fout gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="f97b3-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="f97b3-356">Als Hallo bestemming een blob is en deze optie niet is opgegeven, standaard maakt AzCopy een blok-blob.</span><span class="sxs-lookup"><span data-stu-id="f97b3-356">If hello destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="f97b3-357">**Van toepassing op:** Blobs</span><span class="sxs-lookup"><span data-stu-id="f97b3-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="f97b3-358">/ CheckMD5</span><span class="sxs-lookup"><span data-stu-id="f97b3-358">/CheckMD5</span></span>
<span data-ttu-id="f97b3-359">Een MD5-hash voor de gedownloade gegevens berekend en controleert of Hallo MD5-hash wordt opgeslagen in blob Hallo of Content-MD5-eigenschap van bestand overeenkomt met Hallo berekende hash.</span><span class="sxs-lookup"><span data-stu-id="f97b3-359">Calculates an MD5 hash for downloaded data and verifies that hello MD5 hash stored in hello blob or file's Content-MD5 property matches hello calculated hash.</span></span> <span data-ttu-id="f97b3-360">Hallo MD5 selectievakje is standaard uitgeschakeld, dus u deze optie tooperform Hallo MD5 controle opgeven moet bij het downloaden van gegevens.</span><span class="sxs-lookup"><span data-stu-id="f97b3-360">hello MD5 check is turned off by default, so you must specify this option tooperform hello MD5 check when downloading data.</span></span>

<span data-ttu-id="f97b3-361">Houd er rekening mee dat Azure Storage niet dat Hallo MD5-hash voor Hallo blob worden opgeslagen garandeert of het bestand is up-to-date.</span><span class="sxs-lookup"><span data-stu-id="f97b3-361">Note that Azure Storage doesn't guarantee that hello MD5 hash stored for hello blob or file is up-to-date.</span></span> <span data-ttu-id="f97b3-362">Het is van de client verantwoordelijkheid tooupdate Hallo MD5 als Hallo blob of het bestand wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="f97b3-362">It is client's responsibility tooupdate hello MD5 whenever hello blob or file is modified.</span></span>

<span data-ttu-id="f97b3-363">Na het uploaden van deze wordt AzCopy altijd Hallo Content-MD5-eigenschap voor een Azure-blob of een bestand toohello-service.</span><span class="sxs-lookup"><span data-stu-id="f97b3-363">AzCopy always sets hello Content-MD5 property for an Azure blob or file after uploading it toohello service.</span></span>  

<span data-ttu-id="f97b3-364">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="f97b3-365">/ Momentopname</span><span class="sxs-lookup"><span data-stu-id="f97b3-365">/Snapshot</span></span>
<span data-ttu-id="f97b3-366">Hiermee wordt aangegeven of tootransfer momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="f97b3-366">Indicates whether tootransfer snapshots.</span></span> <span data-ttu-id="f97b3-367">Deze optie is alleen geldig wanneer het Hallo-bron is een blob.</span><span class="sxs-lookup"><span data-stu-id="f97b3-367">This option is only valid when hello source is a blob.</span></span>

<span data-ttu-id="f97b3-368">Hallo overgebrachte blob momentopnamen hernoemd in deze indeling: .extensie blob-naam (momentopname-tijd)</span><span class="sxs-lookup"><span data-stu-id="f97b3-368">hello transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="f97b3-369">Momentopnamen worden standaard niet gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="f97b3-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="f97b3-370">**Van toepassing op:** Blobs</span><span class="sxs-lookup"><span data-stu-id="f97b3-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="f97b3-371">/ V: [uitgebreide-log-bestand]</span><span class="sxs-lookup"><span data-stu-id="f97b3-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="f97b3-372">Uitvoer uitgebreide statusberichten in een logboekbestand.</span><span class="sxs-lookup"><span data-stu-id="f97b3-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="f97b3-373">Hallo uitgebreide logboekbestand heet standaard AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="f97b3-373">By default, hello verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="f97b3-374">Als u een bestaande bestandslocatie voor deze optie opgeeft, is uitgebreid logboek Hallo toegevoegde toothat-bestand.</span><span class="sxs-lookup"><span data-stu-id="f97b3-374">If you specify an existing file location for this option, hello verbose log is appended toothat file.</span></span>  

<span data-ttu-id="f97b3-375">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="f97b3-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="f97b3-376">/ Z: [journaal-map]</span><span class="sxs-lookup"><span data-stu-id="f97b3-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="f97b3-377">Hiermee geeft u een map journaal-bestand voor het hervatten van een bewerking.</span><span class="sxs-lookup"><span data-stu-id="f97b3-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="f97b3-378">AzCopy ondersteunt altijd wordt hervat als een bewerking is onderbroken.</span><span class="sxs-lookup"><span data-stu-id="f97b3-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="f97b3-379">Als deze optie niet opgegeven is of deze is opgegeven zonder het pad naar een map, maakt AzCopy Hallo journaal-bestand in Hallo standaardlocatie bevindt, % LocalAppData%\Microsoft\Azure\AzCopy is.</span><span class="sxs-lookup"><span data-stu-id="f97b3-379">If this option is not specified, or it is specified without a folder path, then AzCopy creates hello journal file in hello default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="f97b3-380">Telkens wanneer die u een tooAzCopy opdracht de opdracht die wordt gecontroleerd of een journal-bestand in de standaardmap Hallo bestaat en of deze bestaat in een map die u hebt opgegeven via deze optie.</span><span class="sxs-lookup"><span data-stu-id="f97b3-380">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="f97b3-381">Hallo journaalbestand bestaat niet op beide plaatsen, AzCopy Hallo bewerking behandelt als nieuwe als genereert een nieuw journaalbestand.</span><span class="sxs-lookup"><span data-stu-id="f97b3-381">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="f97b3-382">Als Hallo journal-bestand bestaat, wordt door AzCopy gecontroleerd of Hallo-opdrachtregel die ingevoerde overeenkomt met Hallo vanaf de opdrachtregel in Hallo journal-bestand.</span><span class="sxs-lookup"><span data-stu-id="f97b3-382">If hello journal file does exist, AzCopy checks whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="f97b3-383">Als twee opdrachtregels Hallo overeenkomen, hervat AzCopy onvolledige Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="f97b3-383">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="f97b3-384">Als ze niet overeenkomen, bent u na vragen aan gebruiker tooeither overschrijven Hallo journaal bestand toostart een nieuwe bewerking of toocancel Hallo huidige bewerking.</span><span class="sxs-lookup"><span data-stu-id="f97b3-384">If they do not match, you are prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="f97b3-385">Hallo journaal-bestand wordt verwijderd bij het Hallo-bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f97b3-385">hello journal file is deleted upon successful completion of hello operation.</span></span>

<span data-ttu-id="f97b3-386">Houd er rekening mee dat het hervatten van een bewerking van een journal-bestand gemaakt met een eerdere versie van AzCopy niet wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="f97b3-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="f97b3-387">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="f97b3-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="f97b3-388">/@:"parameter-File'</span><span class="sxs-lookup"><span data-stu-id="f97b3-388">/@:"parameter-file"</span></span>
<span data-ttu-id="f97b3-389">Hiermee geeft u een bestand met parameters.</span><span class="sxs-lookup"><span data-stu-id="f97b3-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="f97b3-390">AzCopy processen Hallo parameters in Hallo bestand alsof ze op de opdrachtregel Hallo had opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f97b3-390">AzCopy processes hello parameters in hello file just as if they had been specified on hello command line.</span></span>

<span data-ttu-id="f97b3-391">In een responsbestand kunt u meerdere parameters opgeven op één regel of geef elke parameter in op een aparte regel.</span><span class="sxs-lookup"><span data-stu-id="f97b3-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="f97b3-392">Houd er rekening mee dat een afzonderlijke parameter kan niet worden gebruikt voor het bereik van meerdere regels.</span><span class="sxs-lookup"><span data-stu-id="f97b3-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="f97b3-393">Antwoordbestanden kunnen opmerkingen regels die met Hallo # symbool beginnen bevatten.</span><span class="sxs-lookup"><span data-stu-id="f97b3-393">Response files can include comments lines that begin with hello # symbol.</span></span>

<span data-ttu-id="f97b3-394">U kunt meerdere antwoordbestanden opgeven.</span><span class="sxs-lookup"><span data-stu-id="f97b3-394">You can specify multiple response files.</span></span> <span data-ttu-id="f97b3-395">Houd er echter rekening mee AzCopy biedt geen ondersteuning voor geneste antwoordbestanden.</span><span class="sxs-lookup"><span data-stu-id="f97b3-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="f97b3-396">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="f97b3-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="f97b3-397">/Y</span><span class="sxs-lookup"><span data-stu-id="f97b3-397">/Y</span></span>
<span data-ttu-id="f97b3-398">Alle AzCopy bevestiging vragen onderdrukt.</span><span class="sxs-lookup"><span data-stu-id="f97b3-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="f97b3-399">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="f97b3-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="f97b3-400">/ L</span><span class="sxs-lookup"><span data-stu-id="f97b3-400">/L</span></span>
<span data-ttu-id="f97b3-401">Hiermee geeft u een bewerking in de lijst. Er zijn geen gegevens worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="f97b3-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="f97b3-402">AzCopy interpreteert Hallo met behulp van deze optie als een simulatie voor actieve Hallo opdrachtregel zonder deze optie/l en tellingen hoeveel objecten zijn gekopieerd, kunt u optie /V op Hallo dezelfde tijd toocheck welke objecten in de uitgebreide logboek Hallo worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="f97b3-402">AzCopy interprets hello using of this option as a simulation for running hello command line without this option /L and counts how many objects are copied, you can specify option /V at hello same time toocheck which objects are copied in hello verbose log.</span></span>

<span data-ttu-id="f97b3-403">Hallo-gedrag van deze optie is ook afhankelijk van Hallo-locatie van de brongegevens Hallo en Hallo aanwezigheid van Hallo recursieve modus/s en de bestandsnaam patroon optie /Pattern.</span><span class="sxs-lookup"><span data-stu-id="f97b3-403">hello behavior of this option is also determined by hello location of hello source data and hello presence of hello recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="f97b3-404">AzCopy vereist lijst weergeven en lezen van de bronlocatie van deze wanneer u deze optie.</span><span class="sxs-lookup"><span data-stu-id="f97b3-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="f97b3-405">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="f97b3-406">/MT</span><span class="sxs-lookup"><span data-stu-id="f97b3-406">/MT</span></span>
<span data-ttu-id="f97b3-407">Hiermee stelt Hallo gedownloade bestand laatst gewijzigd-tijd toobe Hallo dezelfde als de bron-blob Hallo of van het bestand.</span><span class="sxs-lookup"><span data-stu-id="f97b3-407">Sets hello downloaded file's last-modified time toobe hello same as hello source blob or file's.</span></span>

<span data-ttu-id="f97b3-408">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="f97b3-409">/XN</span><span class="sxs-lookup"><span data-stu-id="f97b3-409">/XN</span></span>
<span data-ttu-id="f97b3-410">Sluit een nieuwere bronresource.</span><span class="sxs-lookup"><span data-stu-id="f97b3-410">Excludes a newer source resource.</span></span> <span data-ttu-id="f97b3-411">Hallo wordt resource niet gekopieerd als hello laatst gewijzigd-tijd van de bron Hallo Hallo dezelfde of een nieuwer is dan het doel.</span><span class="sxs-lookup"><span data-stu-id="f97b3-411">hello resource is not copied if hello last modified time of hello source is hello same or newer than destination.</span></span>

<span data-ttu-id="f97b3-412">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="f97b3-413">/XO</span><span class="sxs-lookup"><span data-stu-id="f97b3-413">/XO</span></span>
<span data-ttu-id="f97b3-414">Sluit een oudere bronserver resource.</span><span class="sxs-lookup"><span data-stu-id="f97b3-414">Excludes an older source resource.</span></span> <span data-ttu-id="f97b3-415">Hallo wordt resource niet gekopieerd als hello laatst gewijzigd-tijd van de bron Hallo Hallo dezelfde of een ouder zijn dan het doel.</span><span class="sxs-lookup"><span data-stu-id="f97b3-415">hello resource is not copied if hello last modified time of hello source is hello same or older than destination.</span></span>

<span data-ttu-id="f97b3-416">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="f97b3-417">/A</span><span class="sxs-lookup"><span data-stu-id="f97b3-417">/A</span></span>
<span data-ttu-id="f97b3-418">Alleen bestanden die Hallo kenmerk Archief hebben geüpload.</span><span class="sxs-lookup"><span data-stu-id="f97b3-418">Uploads only files that have hello Archive attribute set.</span></span>

<span data-ttu-id="f97b3-419">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="f97b3-420">/ IA: [RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="f97b3-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="f97b3-421">Uploads alleen bestanden die een Hallo opgegeven set kenmerken.</span><span class="sxs-lookup"><span data-stu-id="f97b3-421">Uploads only files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="f97b3-422">Beschikbare kenmerken zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="f97b3-422">Available attributes include:</span></span>

* <span data-ttu-id="f97b3-423">R = alleen-lezen bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-423">R = Read-only files</span></span>
* <span data-ttu-id="f97b3-424">Een = bestanden klaar voor archivering</span><span class="sxs-lookup"><span data-stu-id="f97b3-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="f97b3-425">S = systeembestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-425">S = System files</span></span>
* <span data-ttu-id="f97b3-426">H = Verborgen bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-426">H = Hidden files</span></span>
* <span data-ttu-id="f97b3-427">C = gecomprimeerde bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-427">C = Compressed files</span></span>
* <span data-ttu-id="f97b3-428">N = normale bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-428">N = Normal files</span></span>
* <span data-ttu-id="f97b3-429">E = versleutelde bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-429">E = Encrypted files</span></span>
* <span data-ttu-id="f97b3-430">T = tijdelijke bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-430">T = Temporary files</span></span>
* <span data-ttu-id="f97b3-431">O = offlinebestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-431">O = Offline files</span></span>
* <span data-ttu-id="f97b3-432">Ik = niet-geïndexeerde bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-432">I = Non-indexed files</span></span>

<span data-ttu-id="f97b3-433">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="f97b3-434">/ XA: [RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="f97b3-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="f97b3-435">Sluit bestanden die een opgegeven Hallo set kenmerken.</span><span class="sxs-lookup"><span data-stu-id="f97b3-435">Excludes files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="f97b3-436">Beschikbare kenmerken zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="f97b3-436">Available attributes include:</span></span>

* <span data-ttu-id="f97b3-437">R = alleen-lezen bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-437">R = Read-only files</span></span>
* <span data-ttu-id="f97b3-438">Een = bestanden klaar voor archivering</span><span class="sxs-lookup"><span data-stu-id="f97b3-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="f97b3-439">S = systeembestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-439">S = System files</span></span>
* <span data-ttu-id="f97b3-440">H = Verborgen bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-440">H = Hidden files</span></span>
* <span data-ttu-id="f97b3-441">C = gecomprimeerde bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-441">C = Compressed files</span></span>
* <span data-ttu-id="f97b3-442">N = normale bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-442">N = Normal files</span></span>
* <span data-ttu-id="f97b3-443">E = versleutelde bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-443">E = Encrypted files</span></span>
* <span data-ttu-id="f97b3-444">T = tijdelijke bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-444">T = Temporary files</span></span>
* <span data-ttu-id="f97b3-445">O = offlinebestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-445">O = Offline files</span></span>
* <span data-ttu-id="f97b3-446">Ik = niet-geïndexeerde bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-446">I = Non-indexed files</span></span>

<span data-ttu-id="f97b3-447">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="f97b3-448">/ Scheidingsteken: "scheidingsteken"</span><span class="sxs-lookup"><span data-stu-id="f97b3-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="f97b3-449">Hiermee wordt aangegeven op Hallo scheidingsteken toodelimit virtuele mappen in een blob-naam gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f97b3-449">Indicates hello delimiter character used toodelimit virtual directories in a blob name.</span></span>

<span data-ttu-id="f97b3-450">Standaard maakt gebruik van AzCopy / als Hallo scheidingsteken.</span><span class="sxs-lookup"><span data-stu-id="f97b3-450">By default, AzCopy uses / as hello delimiter character.</span></span> <span data-ttu-id="f97b3-451">AzCopy ondersteunt echter met behulp van een algemene teken (zoals @, # of %) als scheidingsteken.</span><span class="sxs-lookup"><span data-stu-id="f97b3-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="f97b3-452">Als u tooinclude een van deze speciale tekens op Hallo-opdrachtregel moet, plaatst u de bestandsnaam Hallo met dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="f97b3-452">If you need tooinclude one of these special characters on hello command line, enclose hello file name with double quotes.</span></span>

<span data-ttu-id="f97b3-453">Deze optie is alleen van toepassing voor het downloaden van blobs.</span><span class="sxs-lookup"><span data-stu-id="f97b3-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="f97b3-454">**Van toepassing op:** Blobs</span><span class="sxs-lookup"><span data-stu-id="f97b3-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="f97b3-455">/ NC: 'getal-van-gelijktijdige-operations'</span><span class="sxs-lookup"><span data-stu-id="f97b3-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="f97b3-456">Hiermee geeft u het aantal gelijktijdige bewerkingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="f97b3-456">Specifies hello number of concurrent operations.</span></span>

<span data-ttu-id="f97b3-457">AzCopy standaard wordt een bepaald aantal gelijktijdige bewerkingen tooincrease Hallo-gegevensdoorvoer overdracht gestart.</span><span class="sxs-lookup"><span data-stu-id="f97b3-457">AzCopy by default starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="f97b3-458">Vergeet niet dat groot aantal gelijktijdige bewerkingen in een omgeving met lage bandbreedte mogelijk Hallo netwerkverbinding overbelast en te voorkomen dat Hallo bewerkingen volledig is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f97b3-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm hello network connection and prevent hello operations from fully completing.</span></span> <span data-ttu-id="f97b3-459">Vertraging gelijktijdige bewerkingen op basis van de werkelijke beschikbare netwerkbandbreedte.</span><span class="sxs-lookup"><span data-stu-id="f97b3-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="f97b3-460">Hallo bovengrens voor gelijktijdige bewerkingen is 512.</span><span class="sxs-lookup"><span data-stu-id="f97b3-460">hello upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="f97b3-461">**Van toepassing op:** Blobs, bestanden, tabellen</span><span class="sxs-lookup"><span data-stu-id="f97b3-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="f97b3-462">/ SourceType: "Blob" | 'Tabel'</span><span class="sxs-lookup"><span data-stu-id="f97b3-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="f97b3-463">Hiermee geeft u op dat Hallo `source` bron is een blob in Hallo lokale ontwikkelomgeving wordt uitgevoerd in de opslagemulator Hallo beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="f97b3-463">Specifies that hello `source` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="f97b3-464">**Van toepassing op:** Blobs, tabellen</span><span class="sxs-lookup"><span data-stu-id="f97b3-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="f97b3-465">/ DestType: "Blob" | 'Tabel'</span><span class="sxs-lookup"><span data-stu-id="f97b3-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="f97b3-466">Hiermee geeft u op dat Hallo `destination` bron is een blob in Hallo lokale ontwikkelomgeving wordt uitgevoerd in de opslagemulator Hallo beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="f97b3-466">Specifies that hello `destination` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="f97b3-467">**Van toepassing op:** Blobs, tabellen</span><span class="sxs-lookup"><span data-stu-id="f97b3-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="f97b3-468">/ PKRS: "key&#1;key2 key&#3;..."</span><span class="sxs-lookup"><span data-stu-id="f97b3-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="f97b3-469">Splitsingen Hallo partitie sleutel bereik tooenable tabelgegevens parallel verhoogt de snelheid van de exportbewerking Hallo Hallo exporteren.</span><span class="sxs-lookup"><span data-stu-id="f97b3-469">Splits hello partition key range tooenable exporting table data in parallel, which increases hello speed of hello export operation.</span></span>

<span data-ttu-id="f97b3-470">Als deze optie niet is opgegeven, gebruikt een enkele thread tooexport tabelentiteiten met AzCopy.</span><span class="sxs-lookup"><span data-stu-id="f97b3-470">If this option is not specified, then AzCopy uses a single thread tooexport table entities.</span></span> <span data-ttu-id="f97b3-471">Bijvoorbeeld, als hello gebruiker geeft op /PKRS: "aa #bb" en vervolgens AzCopy begint drie gelijktijdige bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="f97b3-471">For example, if hello user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="f97b3-472">Elke bewerking exporteert een van drie partitie sleutel bereiken, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="f97b3-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="f97b3-473">[eerste partitiesleutel, aa)</span><span class="sxs-lookup"><span data-stu-id="f97b3-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="f97b3-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="f97b3-474">[aa, bb)</span></span>

  <span data-ttu-id="f97b3-475">[bb, laatste partitiesleutel]</span><span class="sxs-lookup"><span data-stu-id="f97b3-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="f97b3-476">**Van toepassing op:** tabellen</span><span class="sxs-lookup"><span data-stu-id="f97b3-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="f97b3-477">/ SplitSize: 'bestandsgrootte'</span><span class="sxs-lookup"><span data-stu-id="f97b3-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="f97b3-478">Hiermee geeft u op Hallo geëxporteerde bestand splitsen grootte in MB, Hallo minimaal toegestane waarde is 32.</span><span class="sxs-lookup"><span data-stu-id="f97b3-478">Specifies hello exported file split size in MB, hello minimal value allowed is 32.</span></span>

<span data-ttu-id="f97b3-479">Als deze optie niet is opgegeven, exporteert AzCopy tabel gegevens tooa enkel bestand.</span><span class="sxs-lookup"><span data-stu-id="f97b3-479">If this option is not specified, AzCopy exports table data tooa single file.</span></span>

<span data-ttu-id="f97b3-480">Als Hallo tabelgegevens geëxporteerde tooa blob is en hello geëxporteerde bestandsgrootte Hallo 200 GB limiet voor de Blobgrootte van de bereikt, klikt u vervolgens splitst AzCopy het geëxporteerde bestand hello, zelfs als deze optie is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f97b3-480">If hello table data is exported tooa blob, and hello exported file size reaches hello 200 GB limit for blob size, then AzCopy splits hello exported file, even if this option is not specified.</span></span>

<span data-ttu-id="f97b3-481">**Van toepassing op:** tabellen</span><span class="sxs-lookup"><span data-stu-id="f97b3-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="f97b3-482">/ EntityOperation: 'InsertOrSkip' | 'InsertOrMerge' | 'InsertOrReplace'</span><span class="sxs-lookup"><span data-stu-id="f97b3-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="f97b3-483">Hiermee geeft u gegevens Hallo-import tabelgedrag.</span><span class="sxs-lookup"><span data-stu-id="f97b3-483">Specifies hello table data import behavior.</span></span>

* <span data-ttu-id="f97b3-484">InsertOrSkip - slaat een bestaande entiteit of een nieuwe entiteit ingevoegd als het bestand bestaat niet in de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="f97b3-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="f97b3-485">InsertOrMerge - samenvoegingen van een bestaande entiteit of een nieuwe entiteit ingevoegd als het bestand bestaat niet in de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="f97b3-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="f97b3-486">InsertOrReplace - wordt vervangen door een bestaande entiteit of een nieuwe entiteit ingevoegd als het bestand bestaat niet in de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="f97b3-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="f97b3-487">**Van toepassing op:** tabellen</span><span class="sxs-lookup"><span data-stu-id="f97b3-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="f97b3-488">/ Manifest: 'manifest file'</span><span class="sxs-lookup"><span data-stu-id="f97b3-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="f97b3-489">Hiermee geeft u Hallo manifestbestand voor Hallo tabel exporteren en importeren.</span><span class="sxs-lookup"><span data-stu-id="f97b3-489">Specifies hello manifest file for hello table export and import operation.</span></span>

<span data-ttu-id="f97b3-490">Deze optie is optioneel tijdens de exportbewerking hello, AzCopy genereert een manifestbestand met vooraf gedefinieerde naam als deze optie niet is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f97b3-490">This option is optional during hello export operation, AzCopy generates a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="f97b3-491">Deze optie is vereist tijdens de importbewerking hello om de gegevensbestanden hello te vinden.</span><span class="sxs-lookup"><span data-stu-id="f97b3-491">This option is required during hello import operation for locating hello data files.</span></span>

<span data-ttu-id="f97b3-492">**Van toepassing op:** tabellen</span><span class="sxs-lookup"><span data-stu-id="f97b3-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="f97b3-493">/ SyncCopy</span><span class="sxs-lookup"><span data-stu-id="f97b3-493">/SyncCopy</span></span>
<span data-ttu-id="f97b3-494">Hiermee wordt aangegeven of toosynchronously blobs of bestanden tussen de twee eindpunten voor Azure Storage kopiëren.</span><span class="sxs-lookup"><span data-stu-id="f97b3-494">Indicates whether toosynchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="f97b3-495">AzCopy standaard gebruikt serverzijde asynchrone kopie.</span><span class="sxs-lookup"><span data-stu-id="f97b3-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="f97b3-496">Geef deze optie tooperform een synchrone die downloadt blobs of bestanden toolocal geheugen en uploadt deze tooAzure Storage kopiëren.</span><span class="sxs-lookup"><span data-stu-id="f97b3-496">Specify this option tooperform a synchronous copy, which downloads blobs or files toolocal memory and then uploads them tooAzure Storage.</span></span>

<span data-ttu-id="f97b3-497">U kunt deze optie gebruiken bij het kopiëren van bestanden in Blob storage, binnen de opslag van bestanden of van Blob storage tooFile opslag of vice versa.</span><span class="sxs-lookup"><span data-stu-id="f97b3-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage tooFile storage or vice versa.</span></span>

<span data-ttu-id="f97b3-498">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="f97b3-499">/ SetContentType: 'content-type'</span><span class="sxs-lookup"><span data-stu-id="f97b3-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="f97b3-500">Hiermee geeft u Hallo MIME-inhoudstype voor bestemming blobs of bestanden.</span><span class="sxs-lookup"><span data-stu-id="f97b3-500">Specifies hello MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="f97b3-501">AzCopy sets Hallo inhoudstype voor een blob of tooapplication/octet-stream standaard bestand.</span><span class="sxs-lookup"><span data-stu-id="f97b3-501">AzCopy sets hello content type for a blob or file tooapplication/octet-stream by default.</span></span> <span data-ttu-id="f97b3-502">U kunt Hallo inhoudstype voor alle blobs of bestanden instellen door een waarde op voor deze optie expliciet op te geven.</span><span class="sxs-lookup"><span data-stu-id="f97b3-502">You can set hello content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="f97b3-503">Als u deze optie geen waarde opgeeft, stelt AzCopy elke blob of inhoudstype van het bestand volgens tooits bestandsextensie.</span><span class="sxs-lookup"><span data-stu-id="f97b3-503">If you specify this option without a value, then AzCopy sets each blob or file's content type according tooits file extension.</span></span>

<span data-ttu-id="f97b3-504">**Van toepassing op:** Blobs, bestanden</span><span class="sxs-lookup"><span data-stu-id="f97b3-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="f97b3-505">/ PayloadFormat: 'JSON' | 'CSV'</span><span class="sxs-lookup"><span data-stu-id="f97b3-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="f97b3-506">Hiermee geeft u Hallo-indeling van bestand met geëxporteerde gegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="f97b3-506">Specifies hello format of hello table exported data file.</span></span>

<span data-ttu-id="f97b3-507">Als deze optie niet is opgegeven, standaard exporteert AzCopy gegevensbestand van de tabel in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="f97b3-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="f97b3-508">**Van toepassing op:** tabellen</span><span class="sxs-lookup"><span data-stu-id="f97b3-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="f97b3-509">Bekende problemen en aanbevolen procedures</span><span class="sxs-lookup"><span data-stu-id="f97b3-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="f97b3-510">Limiet voor gelijktijdige schrijfbewerkingen tijdens het kopiëren van gegevens</span><span class="sxs-lookup"><span data-stu-id="f97b3-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="f97b3-511">Als u blobs of bestanden met AzCopy kopieert, houd er rekening mee dat een andere toepassing Hallo gegevens heeft terwijl u kopieert.</span><span class="sxs-lookup"><span data-stu-id="f97b3-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="f97b3-512">Indien mogelijk, zorg dat u kopieert Hallo-gegevens niet wordt gewijzigd tijdens de kopieerbewerking Hallo.</span><span class="sxs-lookup"><span data-stu-id="f97b3-512">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="f97b3-513">Bijvoorbeeld bij het kopiëren van een VHD die is gekoppeld aan een virtuele machine van Azure, zorg dat er geen andere toepassingen toohello VHD momenteel schrijft.</span><span class="sxs-lookup"><span data-stu-id="f97b3-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="f97b3-514">Een goede manier toodo die deze wordt door het Hallo resource toobe leasing gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="f97b3-514">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="f97b3-515">U kunt ook eerst een momentopname van Hallo VHD maken en vervolgens kopieert Hallo momentopname.</span><span class="sxs-lookup"><span data-stu-id="f97b3-515">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="f97b3-516">Als u niet voorkomen andere toepassingen dat bij het schrijven van tooblobs of bestanden terwijl ze worden gekopieerd en vervolgens Houd er rekening mee dat door Hallo tijd Hallo taak is voltooid, hello gekopieerde resources niet meer mogelijk volledige pariteit met Hallo bron resources.</span><span class="sxs-lookup"><span data-stu-id="f97b3-516">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="f97b3-517">Één AzCopy-sessie uitvoeren op één computer.</span><span class="sxs-lookup"><span data-stu-id="f97b3-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="f97b3-518">AzCopy is ontworpen toomaximize Hallo gebruik van uw machine resource tooaccelerate Hallo gegevens worden overgedragen, is het raadzaam u slechts één exemplaar van AzCopy uitvoeren op één machine en geef Hallo optie `/NC` als u meer gelijktijdige bewerkingen nodig.</span><span class="sxs-lookup"><span data-stu-id="f97b3-518">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="f97b3-519">Typ voor meer informatie `AzCopy /?:NC` op Hallo-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="f97b3-519">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="f97b3-520">FIPS-compatibele MD5-algoritmen voor AzCopy inschakelen wanneer u ' gebruik FIPS compatibele algoritmen voor versleuteling, hashing en ondertekening '.</span><span class="sxs-lookup"><span data-stu-id="f97b3-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="f97b3-521">AzCopy standaard .NET MD5 implementatie toocalculate Hallo MD5 gebruikt bij het kopiëren van objecten, maar er zijn bepaalde beveiligingsvereisten voor de die AzCopy tooenable FIPS compatibele MD5-instelling nodig.</span><span class="sxs-lookup"><span data-stu-id="f97b3-521">AzCopy by default uses .NET MD5 implementation toocalculate hello MD5 when copying objects, but there are some security requirements that need AzCopy tooenable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="f97b3-522">U kunt een app.config-bestand maken `AzCopy.exe.config` met de eigenschap `AzureStorageUseV1MD5` en reserveer met AzCopy.exe plaatsen.</span><span class="sxs-lookup"><span data-stu-id="f97b3-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="f97b3-523">Voor de eigenschap 'AzureStorageUseV1MD5' • waar - Hallo-standaardwaarde, AzCopy .NET MD5 implementatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f97b3-523">For property "AzureStorageUseV1MD5" • True - hello default value, AzCopy uses .NET MD5 implementation.</span></span>
<span data-ttu-id="f97b3-524">• ONWAAR – AzCopy hierbij wordt gebruikgemaakt van FIPS-compatibele MD5-algoritmen.</span><span class="sxs-lookup"><span data-stu-id="f97b3-524">• False – AzCopy uses FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="f97b3-525">Houd er rekening mee dat FIPS-algoritmen is standaard uitgeschakeld in uw Windows-computer, kunt u secpol.msc typt in het venster uitvoeren en controleer of deze switch op beveiligingsinstelling -> lokaal beleid -> Beveiliging -> Systeemcryptografie: gebruik FIPS-algoritmen voor versleuteling, hashing en ondertekening.</span><span class="sxs-lookup"><span data-stu-id="f97b3-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f97b3-526">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f97b3-526">Next steps</span></span>
<span data-ttu-id="f97b3-527">Zie voor meer informatie over Azure Storage en AzCopy Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="f97b3-527">For more information about Azure Storage and AzCopy, see hello following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="f97b3-528">Documentatie bij Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="f97b3-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="f97b3-529">Inleiding tooAzure opslag</span><span class="sxs-lookup"><span data-stu-id="f97b3-529">Introduction tooAzure Storage</span></span>](../storage-introduction.md)
* [<span data-ttu-id="f97b3-530">Hoe toouse .NET Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="f97b3-530">How toouse Blob storage from .NET</span></span>](../blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="f97b3-531">Hoe toouse File storage in .NET</span><span class="sxs-lookup"><span data-stu-id="f97b3-531">How toouse File storage from .NET</span></span>](../storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="f97b3-532">Hoe toouse Table storage uit het .NET</span><span class="sxs-lookup"><span data-stu-id="f97b3-532">How toouse Table storage from .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="f97b3-533">Hoe toocreate, beheren of verwijderen van een opslagaccount</span><span class="sxs-lookup"><span data-stu-id="f97b3-533">How toocreate, manage, or delete a storage account</span></span>](../storage-create-storage-account.md)
* [<span data-ttu-id="f97b3-534">Gegevensoverdracht met AzCopy op Linux</span><span class="sxs-lookup"><span data-stu-id="f97b3-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="f97b3-535">Azure Storage-blogberichten:</span><span class="sxs-lookup"><span data-stu-id="f97b3-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="f97b3-536">Inleiding tot Azure Storage Data Movement bibliotheek-Preview</span><span class="sxs-lookup"><span data-stu-id="f97b3-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="f97b3-537">AzCopy: Introducing synchrone kopiëren en aangepaste type inhoud</span><span class="sxs-lookup"><span data-stu-id="f97b3-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="f97b3-538">AzCopy: Aangekondigd algemene beschikbaarheid van AzCopy 3.0 plus preview-versie van AzCopy 4.0 met de ondersteuning voor de tabel en de bestandsnaam</span><span class="sxs-lookup"><span data-stu-id="f97b3-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="f97b3-539">AzCopy: Geoptimaliseerd voor grootschalige kopie scenario 's</span><span class="sxs-lookup"><span data-stu-id="f97b3-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="f97b3-540">AzCopy: Ondersteuning voor geografisch redundante opslag met leestoegang</span><span class="sxs-lookup"><span data-stu-id="f97b3-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="f97b3-541">AzCopy: Gegevensoverdracht met modus opnieuw gestart en SAS-token</span><span class="sxs-lookup"><span data-stu-id="f97b3-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="f97b3-542">AzCopy: Cross-account kopiëren Blob met behulp</span><span class="sxs-lookup"><span data-stu-id="f97b3-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="f97b3-543">AzCopy: Uploaden/downloaden van bestanden voor Azure Blobs</span><span class="sxs-lookup"><span data-stu-id="f97b3-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

