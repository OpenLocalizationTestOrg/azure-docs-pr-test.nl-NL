---
title: aaaPreviewing schijfgebruik voor een taak van de export Azure Import/Export - v1 | Microsoft Docs
description: Meer informatie over hoe toopreview Hallo lijst met blobs u hebt geselecteerd voor een taak voor het exporteren in hello Azure Import/Export-service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 7707d744-7ec7-4de8-ac9b-93a18608dc9a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 7378c159f6d11702cda9ae7654e84d85f9b671b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a><span data-ttu-id="e8970-103">Op voorhand het schijfgebruik voor een exporttaak bekijken</span><span class="sxs-lookup"><span data-stu-id="e8970-103">Previewing drive usage for an export job</span></span>
<span data-ttu-id="e8970-104">Voordat u een exporttaak maakt, moet u een reeks blobs toobe geëxporteerd toochoose.</span><span class="sxs-lookup"><span data-stu-id="e8970-104">Before you create an export job, you need toochoose a set of blobs toobe exported.</span></span> <span data-ttu-id="e8970-105">Hallo Microsoft Azure Import/Export-service kunt u een lijst met blob-paden toouse of blob-prefixes toorepresent Hallo blobs die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="e8970-105">hello Microsoft Azure Import/Export service allows you toouse a list of blob paths or blob prefixes toorepresent hello blobs you've selected.</span></span>  
  
<span data-ttu-id="e8970-106">Vervolgens moet u toodetermine hoeveel stations moet u toosend.</span><span class="sxs-lookup"><span data-stu-id="e8970-106">Next, you need toodetermine how many drives you need toosend.</span></span> <span data-ttu-id="e8970-107">Hallo hulpprogramma voor importeren/exporteren biedt Hallo `PreviewExport` opdracht toopreview schijfgebruik voor Hallo blobs die u hebt geselecteerd, op basis van de grootte Hallo Hallo stations u gaat toouse.</span><span class="sxs-lookup"><span data-stu-id="e8970-107">hello Import/Export Tool provides hello `PreviewExport` command toopreview drive usage for hello blobs you selected, based on hello size of hello drives you are going toouse.</span></span>

## <a name="command-line-parameters"></a><span data-ttu-id="e8970-108">Opdrachtregelparameters</span><span class="sxs-lookup"><span data-stu-id="e8970-108">Command-line parameters</span></span>

<span data-ttu-id="e8970-109">U kunt volgende parameters bij gebruik van Hallo Hallo `PreviewExport` opdracht Hallo hulpprogramma voor importeren/exporteren.</span><span class="sxs-lookup"><span data-stu-id="e8970-109">You can use hello following parameters when using hello `PreviewExport` command of hello Import/Export Tool.</span></span>

|<span data-ttu-id="e8970-110">Opdrachtregelparameter</span><span class="sxs-lookup"><span data-stu-id="e8970-110">Command-line parameter</span></span>|<span data-ttu-id="e8970-111">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e8970-111">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="e8970-112">**schakeloptie/LOGDIR op:**< LogDirectory\></span><span class="sxs-lookup"><span data-stu-id="e8970-112">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="e8970-113">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="e8970-113">Optional.</span></span> <span data-ttu-id="e8970-114">Hallo logboekmap.</span><span class="sxs-lookup"><span data-stu-id="e8970-114">hello log directory.</span></span> <span data-ttu-id="e8970-115">Uitgebreide logboekbestanden geschreven toothis directory.</span><span class="sxs-lookup"><span data-stu-id="e8970-115">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="e8970-116">Als er geen logboekmap is opgegeven, wordt de huidige map hello worden gebruikt als Hallo logboekmap.</span><span class="sxs-lookup"><span data-stu-id="e8970-116">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="e8970-117">**/sn:**< StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="e8970-117">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="e8970-118">Vereist.</span><span class="sxs-lookup"><span data-stu-id="e8970-118">Required.</span></span> <span data-ttu-id="e8970-119">Hallo-naam van Hallo storage-account voor Hallo taak exporteren.</span><span class="sxs-lookup"><span data-stu-id="e8970-119">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="e8970-120">**/SK:**< StorageAccountKey\></span><span class="sxs-lookup"><span data-stu-id="e8970-120">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="e8970-121">Vereist als een container SAS is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e8970-121">Required if and only if a container SAS is not specified.</span></span> <span data-ttu-id="e8970-122">Hallo-toegangssleutel voor opslagaccount Hallo voor Hallo taak exporteren.</span><span class="sxs-lookup"><span data-stu-id="e8970-122">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="e8970-123">**/csas:**< ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="e8970-123">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="e8970-124">Vereist als de sleutel van een opslagaccount is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e8970-124">Required if and only if a storage account key is not specified.</span></span> <span data-ttu-id="e8970-125">Hallo container SAS voor aanbieding Hallo blobs toobe geëxporteerd in Hallo exporttaak.</span><span class="sxs-lookup"><span data-stu-id="e8970-125">hello container SAS for listing hello blobs toobe exported in hello export job.</span></span>|  
|<span data-ttu-id="e8970-126">**/ ExportBlobListFile:**< ExportBlobListFile\></span><span class="sxs-lookup"><span data-stu-id="e8970-126">**/ExportBlobListFile:**<ExportBlobListFile\></span></span>|<span data-ttu-id="e8970-127">Vereist.</span><span class="sxs-lookup"><span data-stu-id="e8970-127">Required.</span></span> <span data-ttu-id="e8970-128">Pad toohello XML-bestand met lijst met blob-paden of blob-pad voorvoegsels voor Hallo blobs toobe geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="e8970-128">Path toohello XML file containing list of blob paths or blob path prefixes for hello blobs toobe exported.</span></span> <span data-ttu-id="e8970-129">Hallo-bestandsindeling die is gebruikt in Hallo `BlobListBlobPath` -element in Hallo [taak plaatsen](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) bewerking Hallo Import/Export-service REST-API.</span><span class="sxs-lookup"><span data-stu-id="e8970-129">hello file format used in hello `BlobListBlobPath` element in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of hello Import/Export service REST API.</span></span>|  
|<span data-ttu-id="e8970-130">**/ DriveSize:**< DriveSize\></span><span class="sxs-lookup"><span data-stu-id="e8970-130">**/DriveSize:**<DriveSize\></span></span>|<span data-ttu-id="e8970-131">Vereist.</span><span class="sxs-lookup"><span data-stu-id="e8970-131">Required.</span></span> <span data-ttu-id="e8970-132">grootte van stations toouse voor een exporttaak Hallo *bijvoorbeeld*, 500 GB, 1,5 TB.</span><span class="sxs-lookup"><span data-stu-id="e8970-132">hello size of drives toouse for an export job, *e.g.*, 500GB, 1.5TB.</span></span>|  

## <a name="command-line-example"></a><span data-ttu-id="e8970-133">Voorbeeld van de opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="e8970-133">Command-line example</span></span>

<span data-ttu-id="e8970-134">Hallo volgende voorbeeld toont Hallo `PreviewExport` opdracht:</span><span class="sxs-lookup"><span data-stu-id="e8970-134">hello following example demonstrates hello `PreviewExport` command:</span></span>  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
<span data-ttu-id="e8970-135">Hallo kan blob-exportbestand bevatten blob-namen en blob-voorvoegsels, zoals hier wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e8970-135">hello export blob list file may contain blob names and blob prefixes, as shown here:</span></span>  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

<span data-ttu-id="e8970-136">Hello Azure-hulpprogramma voor importeren/exporteren geeft een lijst van alle blobs toobe geëxporteerd en berekent hoe ze in de stations Hallo grootte opgegeven, rekening houdend met alle benodigde overhead maakt vervolgens een schatting van het aantal stations dat Hallo toopack nodig toohold Hallo blobs en schijfgebruik informatie.</span><span class="sxs-lookup"><span data-stu-id="e8970-136">hello Azure Import/Export Tool lists all blobs toobe exported and calculates how toopack them into drives of hello specified size, taking into account any necessary overhead, then estimates hello number of drives needed toohold hello blobs and drive usage information.</span></span>  
  
<span data-ttu-id="e8970-137">Hier volgt een voorbeeld van uitvoer hello, met informatief logboeken die worden weggelaten:</span><span class="sxs-lookup"><span data-stu-id="e8970-137">Here is an example of hello output, with informational logs omitted:</span></span>  
  
```  
Number of unique blob paths/prefixes:   3  
Number of duplicate blob paths/prefixes:        0  
Number of nonexistent blob paths/prefixes:      1  
  
Drive size:     500.00 GB  
Number of blobs that can be exported:   6  
Number of blobs that cannot be exported:        2  
Number of drives needed:        3  
        Drive #1:       blobs = 1, occupied space = 454.74 GB  
        Drive #2:       blobs = 3, occupied space = 441.37 GB  
        Drive #3:       blobs = 2, occupied space = 131.28 GB    
```  
  
## <a name="next-steps"></a><span data-ttu-id="e8970-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e8970-138">Next steps</span></span>

* [<span data-ttu-id="e8970-139">Naslaginformatie over Azure hulpprogramma voor importeren/exporteren</span><span class="sxs-lookup"><span data-stu-id="e8970-139">Azure Import/Export Tool reference</span></span>](../storage-import-export-tool-how-to-v1.md)
