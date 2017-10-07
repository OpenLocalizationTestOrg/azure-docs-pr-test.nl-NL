---
title: aaaSample werkstroom tooprep harde schijven voor een Azure Import/Export importtaak | Microsoft Docs
description: Zie een overzicht voor het volledige proces Hallo stations voorbereiden van een import-taak in hello Azure Import/Export-service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: muralikk
ms.openlocfilehash: fa7f36300b35b81757523de4960fd583bd4bf305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="ab0c3-103">Voorbeeld werkstroom tooprepare harde schijven voor een import-taak</span><span class="sxs-lookup"><span data-stu-id="ab0c3-103">Sample workflow tooprepare hard drives for an import job</span></span>

<span data-ttu-id="ab0c3-104">In dit artikel begeleidt u bij Hallo complete proces van het voorbereiden van stations voor een import-taak.</span><span class="sxs-lookup"><span data-stu-id="ab0c3-104">This article walks you through hello complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="ab0c3-105">Voorbeeldgegevens</span><span class="sxs-lookup"><span data-stu-id="ab0c3-105">Sample data</span></span>

<span data-ttu-id="ab0c3-106">In dit voorbeeld volgt de gegevens in Azure storage-account met de naam Hallo geïmporteerd `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="ab0c3-106">This example imports hello following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="ab0c3-107">Locatie</span><span class="sxs-lookup"><span data-stu-id="ab0c3-107">Location</span></span>|<span data-ttu-id="ab0c3-108">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ab0c3-108">Description</span></span>|<span data-ttu-id="ab0c3-109">Gegevensgrootte</span><span class="sxs-lookup"><span data-stu-id="ab0c3-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="ab0c3-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="ab0c3-110">H:\Video\\</span></span> |<span data-ttu-id="ab0c3-111">Een verzameling van video 's</span><span class="sxs-lookup"><span data-stu-id="ab0c3-111">A collection of videos</span></span>|<span data-ttu-id="ab0c3-112">12 TB</span><span class="sxs-lookup"><span data-stu-id="ab0c3-112">12 TB</span></span>|
|<span data-ttu-id="ab0c3-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="ab0c3-113">H:\Photo\\</span></span> |<span data-ttu-id="ab0c3-114">Een verzameling van foto 's</span><span class="sxs-lookup"><span data-stu-id="ab0c3-114">A collection of photos</span></span>|<span data-ttu-id="ab0c3-115">30 GB</span><span class="sxs-lookup"><span data-stu-id="ab0c3-115">30 GB</span></span>|
|<span data-ttu-id="ab0c3-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="ab0c3-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="ab0c3-117">De schijfimage A Blu-ray™</span><span class="sxs-lookup"><span data-stu-id="ab0c3-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="ab0c3-118">25 GB</span><span class="sxs-lookup"><span data-stu-id="ab0c3-118">25 GB</span></span>|
|<span data-ttu-id="ab0c3-119">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="ab0c3-119">\\\bigshare\john\music\\</span></span>|<span data-ttu-id="ab0c3-120">Een verzameling van muziekbestanden op een netwerkshare</span><span class="sxs-lookup"><span data-stu-id="ab0c3-120">A collection of music files on a network share</span></span>|<span data-ttu-id="ab0c3-121">10 GB</span><span class="sxs-lookup"><span data-stu-id="ab0c3-121">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="ab0c3-122">Storage-account bestemmingen</span><span class="sxs-lookup"><span data-stu-id="ab0c3-122">Storage account destinations</span></span>

<span data-ttu-id="ab0c3-123">Hallo import-taak wordt Hallo gegevens importeren in Hallo bestemmingen in Hallo storage-account te volgen:</span><span class="sxs-lookup"><span data-stu-id="ab0c3-123">hello import job will import hello data into hello following destinations in hello storage account:</span></span>

|<span data-ttu-id="ab0c3-124">Bron</span><span class="sxs-lookup"><span data-stu-id="ab0c3-124">Source</span></span>|<span data-ttu-id="ab0c3-125">Doel-virtuele map of blob</span><span class="sxs-lookup"><span data-stu-id="ab0c3-125">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="ab0c3-126">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="ab0c3-126">H:\Video\\</span></span> |<span data-ttu-id="ab0c3-127">video /</span><span class="sxs-lookup"><span data-stu-id="ab0c3-127">video/</span></span>|
|<span data-ttu-id="ab0c3-128">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="ab0c3-128">H:\Photo\\</span></span> |<span data-ttu-id="ab0c3-129">Photo /</span><span class="sxs-lookup"><span data-stu-id="ab0c3-129">photo/</span></span>|
|<span data-ttu-id="ab0c3-130">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="ab0c3-130">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="ab0c3-131">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="ab0c3-131">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="ab0c3-132">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="ab0c3-132">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="ab0c3-133">Music</span><span class="sxs-lookup"><span data-stu-id="ab0c3-133">music</span></span>|

<span data-ttu-id="ab0c3-134">Met deze toewijzing Hallo bestand `H:\Video\Drama\GreatMovie.mov` worden geïmporteerde toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="ab0c3-134">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` will be imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="ab0c3-135">Harde schijf vereisten bepalen</span><span class="sxs-lookup"><span data-stu-id="ab0c3-135">Determine hard drive requirements</span></span>

<span data-ttu-id="ab0c3-136">Vervolgens toodetermine hoeveel harde schijven nodig zijn, compute Hallo grootte van Hallo gegevens:</span><span class="sxs-lookup"><span data-stu-id="ab0c3-136">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="ab0c3-137">Twee harde schijven van 8TB moet voldoende zijn voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ab0c3-137">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="ab0c3-138">Echter sinds Hallo bronmap `H:\Video` heeft 12TB aan gegevens en capaciteit van uw één harde schijf is alleen 8TB, kunt u zich kunt toospecify dit op Hallo volgende manier in Hallo **driveset.csv** bestand:</span><span class="sxs-lookup"><span data-stu-id="ab0c3-138">However, since hello source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able toospecify this in hello following way in hello **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="ab0c3-139">Hallo-hulpprogramma wordt gegevens verdelen over twee harde schijven op een geoptimaliseerde manier.</span><span class="sxs-lookup"><span data-stu-id="ab0c3-139">hello tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-hello-job"></a><span data-ttu-id="ab0c3-140">Koppelen van stations en Hallo taak configureren</span><span class="sxs-lookup"><span data-stu-id="ab0c3-140">Attach drives and configure hello job</span></span>
<span data-ttu-id="ab0c3-141">U koppelt beide schijven toohello machine en volumes maken.</span><span class="sxs-lookup"><span data-stu-id="ab0c3-141">You will attach both disks toohello machine and create volumes.</span></span> <span data-ttu-id="ab0c3-142">Vervolgens auteur **dataset.csv** bestand:</span><span class="sxs-lookup"><span data-stu-id="ab0c3-142">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="ab0c3-143">U kunt bovendien Hallo metagegevens voor alle bestanden volgende instellen:</span><span class="sxs-lookup"><span data-stu-id="ab0c3-143">In addition, you can set hello following metadata for all files:</span></span>

* <span data-ttu-id="ab0c3-144">**UploadMethod:** Windows Azure Import/Export-service</span><span class="sxs-lookup"><span data-stu-id="ab0c3-144">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="ab0c3-145">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="ab0c3-145">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="ab0c3-146">**CreationDate:** 1/10/2013</span><span class="sxs-lookup"><span data-stu-id="ab0c3-146">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="ab0c3-147">tooset metagegevens voor Hallo geïmporteerd bestanden, maak een tekstbestand, `c:\WAImportExport\SampleMetadata.txt`, hello volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="ab0c3-147">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="ab0c3-148">U kunt ook een aantal eigenschappen instellen voor Hallo `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="ab0c3-148">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="ab0c3-149">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="ab0c3-149">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="ab0c3-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ ==</span><span class="sxs-lookup"><span data-stu-id="ab0c3-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="ab0c3-151">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="ab0c3-151">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="ab0c3-152">tooset deze eigenschappen, maak een tekstbestand, `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="ab0c3-152">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="ab0c3-153">Voer hello Azure-hulpprogramma voor importeren/exporteren (WAImportExport.exe)</span><span class="sxs-lookup"><span data-stu-id="ab0c3-153">Run hello Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="ab0c3-154">U bent nu klaar toorun hello Azure-hulpprogramma voor importeren/exporteren tooprepare Hallo twee harde schijven.</span><span class="sxs-lookup"><span data-stu-id="ab0c3-154">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span>

<span data-ttu-id="ab0c3-155">**Voor de eerste sessie Hallo:**</span><span class="sxs-lookup"><span data-stu-id="ab0c3-155">**For hello first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="ab0c3-156">Als geen gegevens meer toobe toegevoegd moet, maakt u een andere dataset-bestand (dezelfde indeling als Initialdataset).</span><span class="sxs-lookup"><span data-stu-id="ab0c3-156">If any more data needs toobe added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="ab0c3-157">**Voor Hallo tweede sessie:**</span><span class="sxs-lookup"><span data-stu-id="ab0c3-157">**For hello second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="ab0c3-158">Nadat Hallo kopie sessies hebt voltooid, kunt u Verbreek de verbinding tussen twee schijven Hallo Hallo kopie computer en toohello juiste Azure-datacenter worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="ab0c3-158">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Azure data center.</span></span> <span data-ttu-id="ab0c3-159">U gaat Hallo twee journaal bestanden uploaden `<FirstDriveSerialNumber>.xml` en `<SecondDriveSerialNumber>.xml`, wanneer u Hallo import-taak in hello Azure-portal maken.</span><span class="sxs-lookup"><span data-stu-id="ab0c3-159">You'll upload hello two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create hello import job in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab0c3-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ab0c3-160">Next steps</span></span>

* [<span data-ttu-id="ab0c3-161">Harde schijven voorbereiden voor een importtaak</span><span class="sxs-lookup"><span data-stu-id="ab0c3-161">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="ab0c3-162">Naslaggids voor veelgebruikte opdrachten</span><span class="sxs-lookup"><span data-stu-id="ab0c3-162">Quick reference for frequently used commands</span></span>](../storage-import-export-tool-quick-reference.md)
