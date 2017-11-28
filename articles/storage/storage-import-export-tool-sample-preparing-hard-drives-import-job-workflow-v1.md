---
title: De voorbeeldwerkstroom klaarmaken voor harde schijven voor een Azure Import/Export-import-taak - v1 | Microsoft Docs
description: Zie een scenario voor het volledige proces van het voorbereiden van stations voor een import-taak in de Azure Import/Export-service.
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
ms.openlocfilehash: 313f8c1f3962a943b4c98c530c324ff28aa84c10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="sample-workflow-to-prepare-hard-drives-for-an-import-job"></a><span data-ttu-id="c77f1-103">Voorbeeldwerkstroom voor het voorbereiden van harde schijven voor een importtaak</span><span class="sxs-lookup"><span data-stu-id="c77f1-103">Sample workflow to prepare hard drives for an import job</span></span>
<span data-ttu-id="c77f1-104">In dit onderwerp leert u het volledige proces van het voorbereiden van stations voor een import-taak.</span><span class="sxs-lookup"><span data-stu-id="c77f1-104">This topic walks you through the complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="c77f1-105">In dit voorbeeld importeert de volgende gegevens in een venster Azure storage-account met de naam `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="c77f1-105">This example imports the following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="c77f1-106">Locatie</span><span class="sxs-lookup"><span data-stu-id="c77f1-106">Location</span></span>|<span data-ttu-id="c77f1-107">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c77f1-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="c77f1-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="c77f1-108">H:\Video</span></span>|<span data-ttu-id="c77f1-109">Een verzameling van video's, 5 TB in totaal.</span><span class="sxs-lookup"><span data-stu-id="c77f1-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="c77f1-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="c77f1-110">H:\Photo</span></span>|<span data-ttu-id="c77f1-111">Een verzameling van foto's, 30 GB in totaal.</span><span class="sxs-lookup"><span data-stu-id="c77f1-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="c77f1-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="c77f1-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="c77f1-113">A Blu-ray™ schijfimage, 25 GB.</span><span class="sxs-lookup"><span data-stu-id="c77f1-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="c77f1-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="c77f1-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="c77f1-115">Een verzameling van muziekbestanden op een netwerkshare, 10 GB in totaal.</span><span class="sxs-lookup"><span data-stu-id="c77f1-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="c77f1-116">De import-taak wordt deze gegevens importeren in de volgende bestemmingen in de storage-account:</span><span class="sxs-lookup"><span data-stu-id="c77f1-116">The import job will import this data into the following destinations in the storage account:</span></span>  
  
|<span data-ttu-id="c77f1-117">Bron</span><span class="sxs-lookup"><span data-stu-id="c77f1-117">Source</span></span>|<span data-ttu-id="c77f1-118">Doel-virtuele map of blob</span><span class="sxs-lookup"><span data-stu-id="c77f1-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="c77f1-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="c77f1-119">H:\Video</span></span>|<span data-ttu-id="c77f1-120">https://mystorageaccount.BLOB.Core.Windows.NET/video</span><span class="sxs-lookup"><span data-stu-id="c77f1-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="c77f1-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="c77f1-121">H:\Photo</span></span>|<span data-ttu-id="c77f1-122">https://mystorageaccount.BLOB.Core.Windows.NET/Photo</span><span class="sxs-lookup"><span data-stu-id="c77f1-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="c77f1-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="c77f1-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="c77f1-124">https://mystorageaccount.BLOB.Core.Windows.NET/Favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="c77f1-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="c77f1-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="c77f1-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="c77f1-126">https://mystorageaccount.BLOB.Core.Windows.NET/Music</span><span class="sxs-lookup"><span data-stu-id="c77f1-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="c77f1-127">Met deze toewijzing, het bestand `H:\Video\Drama\GreatMovie.mov` wordt geïmporteerd naar de blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="c77f1-127">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` will be imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="c77f1-128">Compute vervolgens om te bepalen hoeveel harde schijven nodig zijn, de grootte van de gegevens:</span><span class="sxs-lookup"><span data-stu-id="c77f1-128">Next, to determine how many hard drives are needed, compute the size of the data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="c77f1-129">Twee 3TB harde schijven moet voldoende zijn voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c77f1-129">For this example, two 3TB hard drives should be sufficient.</span></span> <span data-ttu-id="c77f1-130">Echter, omdat de bronmap `H:\Video` 5TB aan gegevens en capaciteit van uw één harde schijf is alleen 3TB hoeft te verbreken `H:\Video` in twee kleinere mappen voordat u het hulpprogramma voor importeren/exporteren van Microsoft Azure: `H:\Video1` en `H:\Video2`.</span><span class="sxs-lookup"><span data-stu-id="c77f1-130">However, since the source directory `H:\Video` has 5TB of data and your single hard drive's capacity is only 3TB, it's necessary to break `H:\Video` into two smaller directories before running the Microsoft Azure Import/Export Tool: `H:\Video1` and `H:\Video2`.</span></span> <span data-ttu-id="c77f1-131">Deze stap levert de volgende bron-mappen:</span><span class="sxs-lookup"><span data-stu-id="c77f1-131">This step yields the following source directories:</span></span>  
  
|<span data-ttu-id="c77f1-132">Locatie</span><span class="sxs-lookup"><span data-stu-id="c77f1-132">Location</span></span>|<span data-ttu-id="c77f1-133">Grootte</span><span class="sxs-lookup"><span data-stu-id="c77f1-133">Size</span></span>|<span data-ttu-id="c77f1-134">Doel-virtuele map of blob</span><span class="sxs-lookup"><span data-stu-id="c77f1-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="c77f1-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="c77f1-135">H:\Video1</span></span>|<span data-ttu-id="c77f1-136">2.5 TB</span><span class="sxs-lookup"><span data-stu-id="c77f1-136">2.5TB</span></span>|<span data-ttu-id="c77f1-137">https://mystorageaccount.BLOB.Core.Windows.NET/video</span><span class="sxs-lookup"><span data-stu-id="c77f1-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="c77f1-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="c77f1-138">H:\Video2</span></span>|<span data-ttu-id="c77f1-139">2.5 TB</span><span class="sxs-lookup"><span data-stu-id="c77f1-139">2.5TB</span></span>|<span data-ttu-id="c77f1-140">https://mystorageaccount.BLOB.Core.Windows.NET/video</span><span class="sxs-lookup"><span data-stu-id="c77f1-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="c77f1-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="c77f1-141">H:\Photo</span></span>|<span data-ttu-id="c77f1-142">30 GB</span><span class="sxs-lookup"><span data-stu-id="c77f1-142">30GB</span></span>|<span data-ttu-id="c77f1-143">https://mystorageaccount.BLOB.Core.Windows.NET/Photo</span><span class="sxs-lookup"><span data-stu-id="c77f1-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="c77f1-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="c77f1-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="c77f1-145">25 GB</span><span class="sxs-lookup"><span data-stu-id="c77f1-145">25GB</span></span>|<span data-ttu-id="c77f1-146">https://mystorageaccount.BLOB.Core.Windows.NET/Favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="c77f1-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="c77f1-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="c77f1-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="c77f1-148">10GB</span><span class="sxs-lookup"><span data-stu-id="c77f1-148">10GB</span></span>|<span data-ttu-id="c77f1-149">https://mystorageaccount.BLOB.Core.Windows.NET/Music</span><span class="sxs-lookup"><span data-stu-id="c77f1-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="c77f1-150">Houd er rekening mee dat zelfs als de `H:\Video`directory is gesplitst in twee mappen ze verwijzen naar dezelfde bestemming virtuele map in het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c77f1-150">Note that even though the `H:\Video`directory has been split to two directories, they point to the same destination virtual directory in the storage account.</span></span> <span data-ttu-id="c77f1-151">Op deze manier alle videobestanden worden beheerd via één `video` container in het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c77f1-151">This way, all video files are maintained under a single `video` container in the storage account.</span></span>  
  
 <span data-ttu-id="c77f1-152">De bovenstaande bron mappen zijn daarna evenredig verdeeld over de twee harde schijven:</span><span class="sxs-lookup"><span data-stu-id="c77f1-152">Next, the above source directories are evenly distributed to the two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="c77f1-153">Harde schijf</span><span class="sxs-lookup"><span data-stu-id="c77f1-153">Hard drive</span></span>|<span data-ttu-id="c77f1-154">Bron-mappen</span><span class="sxs-lookup"><span data-stu-id="c77f1-154">Source directories</span></span>|<span data-ttu-id="c77f1-155">Totale grootte</span><span class="sxs-lookup"><span data-stu-id="c77f1-155">Total size</span></span>|  
|<span data-ttu-id="c77f1-156">Eerste schijf</span><span class="sxs-lookup"><span data-stu-id="c77f1-156">First Drive</span></span>|<span data-ttu-id="c77f1-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="c77f1-157">H:\Video1</span></span>|<span data-ttu-id="c77f1-158">2,5 TB + 30 GB</span><span class="sxs-lookup"><span data-stu-id="c77f1-158">2.5TB + 30GB</span></span>|  
||<span data-ttu-id="c77f1-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="c77f1-159">H:\Photo</span></span>||  
|<span data-ttu-id="c77f1-160">Tweede station</span><span class="sxs-lookup"><span data-stu-id="c77f1-160">Second Drive</span></span>|<span data-ttu-id="c77f1-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="c77f1-161">H:\Video2</span></span>|<span data-ttu-id="c77f1-162">2,5 TB + 35 GB</span><span class="sxs-lookup"><span data-stu-id="c77f1-162">2.5TB + 35GB</span></span>|  
||<span data-ttu-id="c77f1-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="c77f1-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="c77f1-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="c77f1-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="c77f1-165">Bovendien kunt u de volgende metagegevens voor alle bestanden instellen:</span><span class="sxs-lookup"><span data-stu-id="c77f1-165">In addition, you can set the following metadata for all files:</span></span>  
  
-   <span data-ttu-id="c77f1-166">**UploadMethod:** Windows Azure Import/Export-service</span><span class="sxs-lookup"><span data-stu-id="c77f1-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="c77f1-167">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="c77f1-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="c77f1-168">**CreationDate:** 1/10/2013</span><span class="sxs-lookup"><span data-stu-id="c77f1-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="c77f1-169">Om in te stellen metagegevens voor de geïmporteerde bestanden, maak een tekstbestand, `c:\WAImportExport\SampleMetadata.txt`, met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="c77f1-169">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="c77f1-170">U kunt ook bepaalde eigenschappen instellen voor de `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="c77f1-170">You can also set some properties for the `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="c77f1-171">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="c77f1-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="c77f1-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ ==</span><span class="sxs-lookup"><span data-stu-id="c77f1-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="c77f1-173">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="c77f1-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="c77f1-174">Deze eigenschappen instelt, maak een tekstbestand `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="c77f1-174">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="c77f1-175">U bent nu klaar om uit te voeren van het Azure Import/Export-hulpprogramma voor het voorbereiden van de twee harde schijven.</span><span class="sxs-lookup"><span data-stu-id="c77f1-175">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span></span> <span data-ttu-id="c77f1-176">Opmerking:</span><span class="sxs-lookup"><span data-stu-id="c77f1-176">Note that:</span></span>  
  
-   <span data-ttu-id="c77f1-177">De eerste schijf is gekoppeld als station X.</span><span class="sxs-lookup"><span data-stu-id="c77f1-177">The first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="c77f1-178">De tweede schijf is als station Y gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="c77f1-178">The second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="c77f1-179">De sleutel voor het opslagaccount `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span><span class="sxs-lookup"><span data-stu-id="c77f1-179">The key for the storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="c77f1-180">Voorbereiden van schijf voor het importeren van gegevens vooraf is geladen</span><span class="sxs-lookup"><span data-stu-id="c77f1-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="c77f1-181">Als de gegevens moeten worden geïmporteerd, al aanwezig op de schijf is, gebruikt u de vlag /skipwrite.</span><span class="sxs-lookup"><span data-stu-id="c77f1-181">If the data to be imported is already present on the disk, use the flag /skipwrite.</span></span> <span data-ttu-id="c77f1-182">De waarde van /t en /srcdir die beide moeten verwijzen naar de schijf die wordt voorbereid voor importeren.</span><span class="sxs-lookup"><span data-stu-id="c77f1-182">Value of /t and /srcdir both should point to the disk being prepared for import.</span></span> <span data-ttu-id="c77f1-183">Als niet alle gegevens op de schijf moet gaat u naar de dezelfde bestemming virtuele map of het basiscertificaat van het opslagaccount voor elke map afzonderlijk houden de waarde van /id dezelfde opdracht uitvoert hetzelfde voor alle uitvoert.</span><span class="sxs-lookup"><span data-stu-id="c77f1-183">If not all the data on the disk needs to go to the same destination virtual directory or root of the storage account, run the same command for each directory separately keeping the value of /id same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="c77f1-184">Geef geen/Format zoals deze wordt de gegevens op de schijf wissen.</span><span class="sxs-lookup"><span data-stu-id="c77f1-184">Do not specify /format as it will wipe the data on the disk.</span></span> <span data-ttu-id="c77f1-185">U kunt opgeven / versleutelen of /bk, afhankelijk van of de schijf al is versleuteld of niet.</span><span class="sxs-lookup"><span data-stu-id="c77f1-185">You can specify /encrypt or /bk depending on whether the disk is already encrypted or not.</span></span> 
>

```
    When data is already present on the disk for each drive run the following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="c77f1-186">Sessies - kopiëren eerst station</span><span class="sxs-lookup"><span data-stu-id="c77f1-186">Copy sessions - first drive</span></span>

<span data-ttu-id="c77f1-187">Voer het hulpprogramma Azure Import/Export twee keer te kopiëren van de twee bron mappen voor de eerste schijf:</span><span class="sxs-lookup"><span data-stu-id="c77f1-187">For the first drive, run the Azure Import/Export Tool twice to copy the two source directories:</span></span>  

<span data-ttu-id="c77f1-188">**Eerste kopieersessie**</span><span class="sxs-lookup"><span data-stu-id="c77f1-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="c77f1-189">**Tweede kopieersessie**</span><span class="sxs-lookup"><span data-stu-id="c77f1-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="c77f1-190">Kopieer sessies - tweede station</span><span class="sxs-lookup"><span data-stu-id="c77f1-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="c77f1-191">Voer de Azure-hulpprogramma voor importeren/exporteren voor het tweede station driemaal, eenmaal elk voor de bron-mappen, en eenmaal voor het installatiekopiebestand zelfstandige Blu-Ray™):</span><span class="sxs-lookup"><span data-stu-id="c77f1-191">For the second drive, run the Azure Import/Export Tool three times, once each for the source directories, and once for the standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="c77f1-192">**Eerste kopieersessie**</span><span class="sxs-lookup"><span data-stu-id="c77f1-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="c77f1-193">**Tweede kopieersessie**</span><span class="sxs-lookup"><span data-stu-id="c77f1-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="c77f1-194">**Derde kopieersessie**</span><span class="sxs-lookup"><span data-stu-id="c77f1-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="c77f1-195">Kopiëren van de sessie is voltooid</span><span class="sxs-lookup"><span data-stu-id="c77f1-195">Copy session completion</span></span>

<span data-ttu-id="c77f1-196">Nadat de kopie-sessies hebt voltooid, kunt u de twee schijven verbreken van de computer kopiëren en naar het juiste Windows Azure-datacenter worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="c77f1-196">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Windows Azure data center.</span></span> <span data-ttu-id="c77f1-197">U gaat de twee journaal-bestanden uploaden `FirstDrive.jrn` en `SecondDrive.jrn`wanneer u de import-taak in de [Windows Azure-beheerportal](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="c77f1-197">You'll upload the two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create the import job in the [Windows Azure Management Portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="c77f1-198">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c77f1-198">Next steps</span></span>

* [<span data-ttu-id="c77f1-199">Harde schijven voorbereiden voor een importtaak</span><span class="sxs-lookup"><span data-stu-id="c77f1-199">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="c77f1-200">Naslaggids voor veelgebruikte opdrachten</span><span class="sxs-lookup"><span data-stu-id="c77f1-200">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference-v1.md) 
