---
title: De voorbeeldwerkstroom harde schijven voor de import-taak van een Azure Import/Export voorbereiden | Microsoft Docs
description: Zie een scenario voor het volledige proces van het voorbereiden van stations voor een import-taak in de Azure Import/Export-service.
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
ms.openlocfilehash: 83cb82b9807718e7a509312d159eb766a5da1d2c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="sample-workflow-to-prepare-hard-drives-for-an-import-job"></a><span data-ttu-id="65243-103">Voorbeeldwerkstroom voor het voorbereiden van harde schijven voor een importtaak</span><span class="sxs-lookup"><span data-stu-id="65243-103">Sample workflow to prepare hard drives for an import job</span></span>

<span data-ttu-id="65243-104">Dit artikel begeleidt u bij het volledige proces van het voorbereiden van stations voor een import-taak.</span><span class="sxs-lookup"><span data-stu-id="65243-104">This article walks you through the complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="65243-105">Voorbeeldgegevens</span><span class="sxs-lookup"><span data-stu-id="65243-105">Sample data</span></span>

<span data-ttu-id="65243-106">In dit voorbeeld importeert de volgende gegevens in Azure storage-account met de naam `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="65243-106">This example imports the following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="65243-107">Locatie</span><span class="sxs-lookup"><span data-stu-id="65243-107">Location</span></span>|<span data-ttu-id="65243-108">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="65243-108">Description</span></span>|<span data-ttu-id="65243-109">Gegevensgrootte</span><span class="sxs-lookup"><span data-stu-id="65243-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="65243-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="65243-110">H:\Video\\</span></span> |<span data-ttu-id="65243-111">Een verzameling van video 's</span><span class="sxs-lookup"><span data-stu-id="65243-111">A collection of videos</span></span>|<span data-ttu-id="65243-112">12 TB</span><span class="sxs-lookup"><span data-stu-id="65243-112">12 TB</span></span>|
|<span data-ttu-id="65243-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="65243-113">H:\Photo\\</span></span> |<span data-ttu-id="65243-114">Een verzameling van foto 's</span><span class="sxs-lookup"><span data-stu-id="65243-114">A collection of photos</span></span>|<span data-ttu-id="65243-115">30 GB</span><span class="sxs-lookup"><span data-stu-id="65243-115">30 GB</span></span>|
|<span data-ttu-id="65243-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="65243-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="65243-117">De schijfimage A Blu-ray™</span><span class="sxs-lookup"><span data-stu-id="65243-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="65243-118">25 GB</span><span class="sxs-lookup"><span data-stu-id="65243-118">25 GB</span></span>|
|<span data-ttu-id="65243-119">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="65243-119">\\\bigshare\john\music\\</span></span>|<span data-ttu-id="65243-120">Een verzameling van muziekbestanden op een netwerkshare</span><span class="sxs-lookup"><span data-stu-id="65243-120">A collection of music files on a network share</span></span>|<span data-ttu-id="65243-121">10 GB</span><span class="sxs-lookup"><span data-stu-id="65243-121">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="65243-122">Storage-account bestemmingen</span><span class="sxs-lookup"><span data-stu-id="65243-122">Storage account destinations</span></span>

<span data-ttu-id="65243-123">De import-taak worden de gegevens importeren in de volgende bestemmingen in de storage-account:</span><span class="sxs-lookup"><span data-stu-id="65243-123">The import job will import the data into the following destinations in the storage account:</span></span>

|<span data-ttu-id="65243-124">Bron</span><span class="sxs-lookup"><span data-stu-id="65243-124">Source</span></span>|<span data-ttu-id="65243-125">Doel-virtuele map of blob</span><span class="sxs-lookup"><span data-stu-id="65243-125">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="65243-126">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="65243-126">H:\Video\\</span></span> |<span data-ttu-id="65243-127">video /</span><span class="sxs-lookup"><span data-stu-id="65243-127">video/</span></span>|
|<span data-ttu-id="65243-128">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="65243-128">H:\Photo\\</span></span> |<span data-ttu-id="65243-129">Photo /</span><span class="sxs-lookup"><span data-stu-id="65243-129">photo/</span></span>|
|<span data-ttu-id="65243-130">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="65243-130">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="65243-131">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="65243-131">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="65243-132">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="65243-132">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="65243-133">Music</span><span class="sxs-lookup"><span data-stu-id="65243-133">music</span></span>|

<span data-ttu-id="65243-134">Met deze toewijzing, het bestand `H:\Video\Drama\GreatMovie.mov` wordt geïmporteerd naar de blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="65243-134">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` will be imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="65243-135">Harde schijf vereisten bepalen</span><span class="sxs-lookup"><span data-stu-id="65243-135">Determine hard drive requirements</span></span>

<span data-ttu-id="65243-136">Compute vervolgens om te bepalen hoeveel harde schijven nodig zijn, de grootte van de gegevens:</span><span class="sxs-lookup"><span data-stu-id="65243-136">Next, to determine how many hard drives are needed, compute the size of the data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="65243-137">Twee harde schijven van 8TB moet voldoende zijn voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="65243-137">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="65243-138">Echter, omdat de bronmap `H:\Video` heeft 12TB aan gegevens en capaciteit van uw één harde schijf is alleen 8TB, kun je dit opgeven in de volgende manier de **driveset.csv** bestand:</span><span class="sxs-lookup"><span data-stu-id="65243-138">However, since the source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able to specify this in the following way in the **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="65243-139">Het hulpprogramma wordt gegevens verdelen over twee harde schijven op een geoptimaliseerde manier.</span><span class="sxs-lookup"><span data-stu-id="65243-139">The tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-the-job"></a><span data-ttu-id="65243-140">Koppelen van stations en configureren van de taak</span><span class="sxs-lookup"><span data-stu-id="65243-140">Attach drives and configure the job</span></span>
<span data-ttu-id="65243-141">U koppelt beide schijven aan de machine en volumes maken.</span><span class="sxs-lookup"><span data-stu-id="65243-141">You will attach both disks to the machine and create volumes.</span></span> <span data-ttu-id="65243-142">Vervolgens auteur **dataset.csv** bestand:</span><span class="sxs-lookup"><span data-stu-id="65243-142">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="65243-143">Bovendien kunt u de volgende metagegevens voor alle bestanden instellen:</span><span class="sxs-lookup"><span data-stu-id="65243-143">In addition, you can set the following metadata for all files:</span></span>

* <span data-ttu-id="65243-144">**UploadMethod:** Windows Azure Import/Export-service</span><span class="sxs-lookup"><span data-stu-id="65243-144">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="65243-145">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="65243-145">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="65243-146">**CreationDate:** 1/10/2013</span><span class="sxs-lookup"><span data-stu-id="65243-146">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="65243-147">Om in te stellen metagegevens voor de geïmporteerde bestanden, maak een tekstbestand, `c:\WAImportExport\SampleMetadata.txt`, met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="65243-147">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="65243-148">U kunt ook bepaalde eigenschappen instellen voor de `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="65243-148">You can also set some properties for the `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="65243-149">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="65243-149">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="65243-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ ==</span><span class="sxs-lookup"><span data-stu-id="65243-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="65243-151">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="65243-151">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="65243-152">Deze eigenschappen instelt, maak een tekstbestand `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="65243-152">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-the-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="65243-153">Voer het Azure Import/Export-hulpprogramma (WAImportExport.exe)</span><span class="sxs-lookup"><span data-stu-id="65243-153">Run the Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="65243-154">U bent nu klaar om uit te voeren van het Azure Import/Export-hulpprogramma voor het voorbereiden van de twee harde schijven.</span><span class="sxs-lookup"><span data-stu-id="65243-154">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span></span>

<span data-ttu-id="65243-155">**Voor de eerste sessie:**</span><span class="sxs-lookup"><span data-stu-id="65243-155">**For the first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="65243-156">Als meer gegevens worden toegevoegd moet, maakt u een andere dataset-bestand (dezelfde indeling als Initialdataset).</span><span class="sxs-lookup"><span data-stu-id="65243-156">If any more data needs to be added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="65243-157">**Voor de tweede sessie:**</span><span class="sxs-lookup"><span data-stu-id="65243-157">**For the second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="65243-158">Nadat de kopie-sessies hebt voltooid, kunt u de twee schijven verbreken van de computer kopiëren en naar de juiste Azure-datacenter worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="65243-158">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Azure data center.</span></span> <span data-ttu-id="65243-159">U gaat de twee journaal-bestanden uploaden `<FirstDriveSerialNumber>.xml` en `<SecondDriveSerialNumber>.xml`, wanneer u de import-taak in de Azure-portal maken.</span><span class="sxs-lookup"><span data-stu-id="65243-159">You'll upload the two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create the import job in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65243-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="65243-160">Next steps</span></span>

* [<span data-ttu-id="65243-161">Harde schijven voorbereiden voor een importtaak</span><span class="sxs-lookup"><span data-stu-id="65243-161">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="65243-162">Naslaggids voor veelgebruikte opdrachten</span><span class="sxs-lookup"><span data-stu-id="65243-162">Quick reference for frequently used commands</span></span>](../storage-import-export-tool-quick-reference.md)
