---
title: importtaak aaaSample werkstroom tooprep harde schijven voor een Azure Import/Export - v1 | Microsoft Docs
description: Zie een overzicht voor het volledige proces Hallo stations voorbereiden van een import-taak in hello Azure Import/Export-service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 6eb1b1b7-c69f-4365-b5ef-3cd5e05eb72a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: f836fc6104d8b4ad5660cb110a62f61b40b0b7ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="55db6-103">Voorbeeld werkstroom tooprepare harde schijven voor een import-taak</span><span class="sxs-lookup"><span data-stu-id="55db6-103">Sample workflow tooprepare hard drives for an import job</span></span>
<span data-ttu-id="55db6-104">In dit onderwerp wordt u begeleid Hallo volledige proces van het voorbereiden van stations voor een import-taak.</span><span class="sxs-lookup"><span data-stu-id="55db6-104">This topic walks you through hello complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="55db6-105">In dit voorbeeld volgt de gegevens in een venster Azure storage-account met de naam Hallo geïmporteerd `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="55db6-105">This example imports hello following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="55db6-106">Locatie</span><span class="sxs-lookup"><span data-stu-id="55db6-106">Location</span></span>|<span data-ttu-id="55db6-107">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="55db6-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="55db6-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="55db6-108">H:\Video</span></span>|<span data-ttu-id="55db6-109">Een verzameling van video's, 5 TB in totaal.</span><span class="sxs-lookup"><span data-stu-id="55db6-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="55db6-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="55db6-110">H:\Photo</span></span>|<span data-ttu-id="55db6-111">Een verzameling van foto's, 30 GB in totaal.</span><span class="sxs-lookup"><span data-stu-id="55db6-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="55db6-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="55db6-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="55db6-113">A Blu-ray™ schijfimage, 25 GB.</span><span class="sxs-lookup"><span data-stu-id="55db6-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="55db6-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="55db6-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="55db6-115">Een verzameling van muziekbestanden op een netwerkshare, 10 GB in totaal.</span><span class="sxs-lookup"><span data-stu-id="55db6-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="55db6-116">Hallo import-taak wordt deze gegevens importeren in Hallo bestemmingen in Hallo storage-account te volgen:</span><span class="sxs-lookup"><span data-stu-id="55db6-116">hello import job will import this data into hello following destinations in hello storage account:</span></span>  
  
|<span data-ttu-id="55db6-117">Bron</span><span class="sxs-lookup"><span data-stu-id="55db6-117">Source</span></span>|<span data-ttu-id="55db6-118">Doel-virtuele map of blob</span><span class="sxs-lookup"><span data-stu-id="55db6-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="55db6-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="55db6-119">H:\Video</span></span>|<span data-ttu-id="55db6-120">https://mystorageaccount.BLOB.Core.Windows.NET/video</span><span class="sxs-lookup"><span data-stu-id="55db6-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="55db6-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="55db6-121">H:\Photo</span></span>|<span data-ttu-id="55db6-122">https://mystorageaccount.BLOB.Core.Windows.NET/Photo</span><span class="sxs-lookup"><span data-stu-id="55db6-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="55db6-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="55db6-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="55db6-124">https://mystorageaccount.BLOB.Core.Windows.NET/Favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="55db6-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="55db6-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="55db6-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="55db6-126">https://mystorageaccount.BLOB.Core.Windows.NET/Music</span><span class="sxs-lookup"><span data-stu-id="55db6-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="55db6-127">Met deze toewijzing Hallo bestand `H:\Video\Drama\GreatMovie.mov` worden geïmporteerde toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="55db6-127">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` will be imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="55db6-128">Vervolgens toodetermine hoeveel harde schijven nodig zijn, compute Hallo grootte van Hallo gegevens:</span><span class="sxs-lookup"><span data-stu-id="55db6-128">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="55db6-129">Twee 3TB harde schijven moet voldoende zijn voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="55db6-129">For this example, two 3TB hard drives should be sufficient.</span></span> <span data-ttu-id="55db6-130">Echter sinds Hallo bronmap `H:\Video` 5TB aan gegevens en capaciteit van uw één harde schijf is alleen 3TB is noodzakelijk toobreak `H:\Video` Hallo in twee kleinere mappen voordat u Microsoft Azure-hulpprogramma voor importeren/exporteren: `H:\Video1` en `H:\Video2`.</span><span class="sxs-lookup"><span data-stu-id="55db6-130">However, since hello source directory `H:\Video` has 5TB of data and your single hard drive's capacity is only 3TB, it's necessary toobreak `H:\Video` into two smaller directories before running hello Microsoft Azure Import/Export Tool: `H:\Video1` and `H:\Video2`.</span></span> <span data-ttu-id="55db6-131">Deze stap levert Hallo bron mappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="55db6-131">This step yields hello following source directories:</span></span>  
  
|<span data-ttu-id="55db6-132">Locatie</span><span class="sxs-lookup"><span data-stu-id="55db6-132">Location</span></span>|<span data-ttu-id="55db6-133">Grootte</span><span class="sxs-lookup"><span data-stu-id="55db6-133">Size</span></span>|<span data-ttu-id="55db6-134">Doel-virtuele map of blob</span><span class="sxs-lookup"><span data-stu-id="55db6-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="55db6-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="55db6-135">H:\Video1</span></span>|<span data-ttu-id="55db6-136">2.5 TB</span><span class="sxs-lookup"><span data-stu-id="55db6-136">2.5TB</span></span>|<span data-ttu-id="55db6-137">https://mystorageaccount.BLOB.Core.Windows.NET/video</span><span class="sxs-lookup"><span data-stu-id="55db6-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="55db6-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="55db6-138">H:\Video2</span></span>|<span data-ttu-id="55db6-139">2.5 TB</span><span class="sxs-lookup"><span data-stu-id="55db6-139">2.5TB</span></span>|<span data-ttu-id="55db6-140">https://mystorageaccount.BLOB.Core.Windows.NET/video</span><span class="sxs-lookup"><span data-stu-id="55db6-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="55db6-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="55db6-141">H:\Photo</span></span>|<span data-ttu-id="55db6-142">30 GB</span><span class="sxs-lookup"><span data-stu-id="55db6-142">30GB</span></span>|<span data-ttu-id="55db6-143">https://mystorageaccount.BLOB.Core.Windows.NET/Photo</span><span class="sxs-lookup"><span data-stu-id="55db6-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="55db6-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="55db6-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="55db6-145">25 GB</span><span class="sxs-lookup"><span data-stu-id="55db6-145">25GB</span></span>|<span data-ttu-id="55db6-146">https://mystorageaccount.BLOB.Core.Windows.NET/Favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="55db6-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="55db6-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="55db6-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="55db6-148">10GB</span><span class="sxs-lookup"><span data-stu-id="55db6-148">10GB</span></span>|<span data-ttu-id="55db6-149">https://mystorageaccount.BLOB.Core.Windows.NET/Music</span><span class="sxs-lookup"><span data-stu-id="55db6-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="55db6-150">Let op: hoewel Hallo `H:\Video`directory tootwo mappen is gesplitst, ze toohello Wijs dezelfde virtuele map van de bestemming in Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="55db6-150">Note that even though hello `H:\Video`directory has been split tootwo directories, they point toohello same destination virtual directory in hello storage account.</span></span> <span data-ttu-id="55db6-151">Op deze manier alle videobestanden worden beheerd via één `video` container in Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="55db6-151">This way, all video files are maintained under a single `video` container in hello storage account.</span></span>  
  
 <span data-ttu-id="55db6-152">Hallo hierboven bron mappen gelijkmatig zijn verdeeld vervolgens toohello twee harde schijven:</span><span class="sxs-lookup"><span data-stu-id="55db6-152">Next, hello above source directories are evenly distributed toohello two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="55db6-153">Harde schijf</span><span class="sxs-lookup"><span data-stu-id="55db6-153">Hard drive</span></span>|<span data-ttu-id="55db6-154">Bron-mappen</span><span class="sxs-lookup"><span data-stu-id="55db6-154">Source directories</span></span>|<span data-ttu-id="55db6-155">Totale grootte</span><span class="sxs-lookup"><span data-stu-id="55db6-155">Total size</span></span>|  
|<span data-ttu-id="55db6-156">Eerste schijf</span><span class="sxs-lookup"><span data-stu-id="55db6-156">First Drive</span></span>|<span data-ttu-id="55db6-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="55db6-157">H:\Video1</span></span>|<span data-ttu-id="55db6-158">2,5 TB + 30 GB</span><span class="sxs-lookup"><span data-stu-id="55db6-158">2.5TB + 30GB</span></span>|  
||<span data-ttu-id="55db6-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="55db6-159">H:\Photo</span></span>||  
|<span data-ttu-id="55db6-160">Tweede station</span><span class="sxs-lookup"><span data-stu-id="55db6-160">Second Drive</span></span>|<span data-ttu-id="55db6-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="55db6-161">H:\Video2</span></span>|<span data-ttu-id="55db6-162">2,5 TB + 35 GB</span><span class="sxs-lookup"><span data-stu-id="55db6-162">2.5TB + 35GB</span></span>|  
||<span data-ttu-id="55db6-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="55db6-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="55db6-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="55db6-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="55db6-165">U kunt bovendien Hallo metagegevens voor alle bestanden volgende instellen:</span><span class="sxs-lookup"><span data-stu-id="55db6-165">In addition, you can set hello following metadata for all files:</span></span>  
  
-   <span data-ttu-id="55db6-166">**UploadMethod:** Windows Azure Import/Export-service</span><span class="sxs-lookup"><span data-stu-id="55db6-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="55db6-167">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="55db6-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="55db6-168">**CreationDate:** 1/10/2013</span><span class="sxs-lookup"><span data-stu-id="55db6-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="55db6-169">tooset metagegevens voor Hallo geïmporteerd bestanden, maak een tekstbestand, `c:\WAImportExport\SampleMetadata.txt`, hello volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="55db6-169">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="55db6-170">U kunt ook een aantal eigenschappen instellen voor Hallo `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="55db6-170">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="55db6-171">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="55db6-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="55db6-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ ==</span><span class="sxs-lookup"><span data-stu-id="55db6-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="55db6-173">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="55db6-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="55db6-174">tooset deze eigenschappen, maak een tekstbestand, `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="55db6-174">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="55db6-175">U bent nu klaar toorun hello Azure-hulpprogramma voor importeren/exporteren tooprepare Hallo twee harde schijven.</span><span class="sxs-lookup"><span data-stu-id="55db6-175">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span> <span data-ttu-id="55db6-176">Opmerking:</span><span class="sxs-lookup"><span data-stu-id="55db6-176">Note that:</span></span>  
  
-   <span data-ttu-id="55db6-177">de eerste schijf Hallo is als station X gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="55db6-177">hello first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="55db6-178">de tweede schijf Hallo is als station Y gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="55db6-178">hello second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="55db6-179">Hallo-sleutel voor opslagaccount hello `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span><span class="sxs-lookup"><span data-stu-id="55db6-179">hello key for hello storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="55db6-180">Voorbereiden van schijf voor het importeren van gegevens vooraf is geladen</span><span class="sxs-lookup"><span data-stu-id="55db6-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="55db6-181">Als Hallo gegevens toobe geïmporteerd al aanwezig op Hallo schijf is, gebruikt u Hallo vlag /skipwrite.</span><span class="sxs-lookup"><span data-stu-id="55db6-181">If hello data toobe imported is already present on hello disk, use hello flag /skipwrite.</span></span> <span data-ttu-id="55db6-182">Waarde van /t en /srcdir moet toohello schijf wordt voorbereid voor het importeren van gegevenspunt.</span><span class="sxs-lookup"><span data-stu-id="55db6-182">Value of /t and /srcdir both should point toohello disk being prepared for import.</span></span> <span data-ttu-id="55db6-183">Als niet alle gegevens op Hallo Hallo schijf toogo toohello moet dezelfde bestemming virtuele map of hoofdmap van het opslagaccount hello, Voer Hallo dezelfde opdracht voor elke map afzonderlijk houden Hallo-waarde van /id hetzelfde voor alle uitvoert.</span><span class="sxs-lookup"><span data-stu-id="55db6-183">If not all hello data on hello disk needs toogo toohello same destination virtual directory or root of hello storage account, run hello same command for each directory separately keeping hello value of /id same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="55db6-184">Geef geen/Format zoals deze wordt Hallo gegevens op Hallo schijf wissen.</span><span class="sxs-lookup"><span data-stu-id="55db6-184">Do not specify /format as it will wipe hello data on hello disk.</span></span> <span data-ttu-id="55db6-185">U kunt opgeven / versleutelen of /bk, afhankelijk van of Hallo schijf al is versleuteld of niet.</span><span class="sxs-lookup"><span data-stu-id="55db6-185">You can specify /encrypt or /bk depending on whether hello disk is already encrypted or not.</span></span> 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="55db6-186">Sessies - kopiëren eerst station</span><span class="sxs-lookup"><span data-stu-id="55db6-186">Copy sessions - first drive</span></span>

<span data-ttu-id="55db6-187">Voer voor de eerste schijf Hallo, hello Azure Import/Export Tool tweemaal toocopy Hallo twee bron mappen:</span><span class="sxs-lookup"><span data-stu-id="55db6-187">For hello first drive, run hello Azure Import/Export Tool twice toocopy hello two source directories:</span></span>  

<span data-ttu-id="55db6-188">**Eerste kopieersessie**</span><span class="sxs-lookup"><span data-stu-id="55db6-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="55db6-189">**Tweede kopieersessie**</span><span class="sxs-lookup"><span data-stu-id="55db6-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="55db6-190">Kopieer sessies - tweede station</span><span class="sxs-lookup"><span data-stu-id="55db6-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="55db6-191">Voor Hallo tweede station, voer hello Azure-hulpprogramma voor importeren/exporteren drie keer wanneer elk voor Hallo bron mappen en eens Hallo zelfstandig Blu-Ray™ afbeeldingsbestand):</span><span class="sxs-lookup"><span data-stu-id="55db6-191">For hello second drive, run hello Azure Import/Export Tool three times, once each for hello source directories, and once for hello standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="55db6-192">**Eerste kopieersessie**</span><span class="sxs-lookup"><span data-stu-id="55db6-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="55db6-193">**Tweede kopieersessie**</span><span class="sxs-lookup"><span data-stu-id="55db6-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="55db6-194">**Derde kopieersessie**</span><span class="sxs-lookup"><span data-stu-id="55db6-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="55db6-195">Kopiëren van de sessie is voltooid</span><span class="sxs-lookup"><span data-stu-id="55db6-195">Copy session completion</span></span>

<span data-ttu-id="55db6-196">Nadat Hallo kopie sessies hebt voltooid, kunt u Verbreek de verbinding tussen twee schijven Hallo Hallo kopie computer en toohello juiste Windows Azure-datacenter worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="55db6-196">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Windows Azure data center.</span></span> <span data-ttu-id="55db6-197">U gaat Hallo twee journaal bestanden uploaden `FirstDrive.jrn` en `SecondDrive.jrn`, wanneer u Hallo import-taak in Hallo maken [Windows Azure-beheerportal](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="55db6-197">You'll upload hello two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create hello import job in hello [Windows Azure Management Portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="55db6-198">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="55db6-198">Next steps</span></span>

* [<span data-ttu-id="55db6-199">Harde schijven voorbereiden voor een importtaak</span><span class="sxs-lookup"><span data-stu-id="55db6-199">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="55db6-200">Naslaggids voor veelgebruikte opdrachten</span><span class="sxs-lookup"><span data-stu-id="55db6-200">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference-v1.md) 
