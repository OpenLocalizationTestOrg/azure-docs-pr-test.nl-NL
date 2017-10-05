---
title: Een voorbeeldweergave schijfgebruik voor een taak van de export Azure Import/Export - v1 | Microsoft Docs
description: Informatie over het bekijken van de lijst met blobs die u hebt geselecteerd voor een exporttaak in de Azure Import/Export-service.
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
ms.openlocfilehash: 6ec74ae0b0931f3fed99a43f4f7e58f9d425b138
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a><span data-ttu-id="22043-103">Op voorhand het schijfgebruik voor een exporttaak bekijken</span><span class="sxs-lookup"><span data-stu-id="22043-103">Previewing drive usage for an export job</span></span>
<span data-ttu-id="22043-104">Voordat u een exporttaak maakt, moet u kiezen van een reeks blobs worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="22043-104">Before you create an export job, you need to choose a set of blobs to be exported.</span></span> <span data-ttu-id="22043-105">De Microsoft Azure Import/Export-service kunt u voor het gebruik van een lijst met blob-paden of blob-voorvoegsels te vertegenwoordigen de blobs die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="22043-105">The Microsoft Azure Import/Export service allows you to use a list of blob paths or blob prefixes to represent the blobs you've selected.</span></span>  
  
<span data-ttu-id="22043-106">Vervolgens moet u bepalen hoeveel stations die u wilt verzenden.</span><span class="sxs-lookup"><span data-stu-id="22043-106">Next, you need to determine how many drives you need to send.</span></span> <span data-ttu-id="22043-107">Het hulpprogramma voor importeren/exporteren geeft de `PreviewExport` opdracht voor de preview schijfgebruik voor de blobs die u hebt geselecteerd, op basis van de grootte van de stations die u gaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="22043-107">The Import/Export Tool provides the `PreviewExport` command to preview drive usage for the blobs you selected, based on the size of the drives you are going to use.</span></span>

## <a name="command-line-parameters"></a><span data-ttu-id="22043-108">Opdrachtregelparameters</span><span class="sxs-lookup"><span data-stu-id="22043-108">Command-line parameters</span></span>

<span data-ttu-id="22043-109">U kunt de volgende parameters gebruiken wanneer u de `PreviewExport` opdracht van het hulpprogramma voor importeren/exporteren.</span><span class="sxs-lookup"><span data-stu-id="22043-109">You can use the following parameters when using the `PreviewExport` command of the Import/Export Tool.</span></span>

|<span data-ttu-id="22043-110">Opdrachtregelparameter</span><span class="sxs-lookup"><span data-stu-id="22043-110">Command-line parameter</span></span>|<span data-ttu-id="22043-111">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="22043-111">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="22043-112">**schakeloptie/LOGDIR op:**< LogDirectory\></span><span class="sxs-lookup"><span data-stu-id="22043-112">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="22043-113">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="22043-113">Optional.</span></span> <span data-ttu-id="22043-114">De logboekmap.</span><span class="sxs-lookup"><span data-stu-id="22043-114">The log directory.</span></span> <span data-ttu-id="22043-115">Uitgebreide logboekbestanden worden geschreven naar deze map.</span><span class="sxs-lookup"><span data-stu-id="22043-115">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="22043-116">Als er geen logboekmap is opgegeven, wordt de huidige map gebruikt als de logboekmap.</span><span class="sxs-lookup"><span data-stu-id="22043-116">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="22043-117">**/sn:**< StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="22043-117">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="22043-118">Vereist.</span><span class="sxs-lookup"><span data-stu-id="22043-118">Required.</span></span> <span data-ttu-id="22043-119">De naam van het opslagaccount voor de taak voor het exporteren.</span><span class="sxs-lookup"><span data-stu-id="22043-119">The name of the storage account for the export job.</span></span>|  
|<span data-ttu-id="22043-120">**/SK:**< StorageAccountKey\></span><span class="sxs-lookup"><span data-stu-id="22043-120">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="22043-121">Vereist als een container SAS is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="22043-121">Required if and only if a container SAS is not specified.</span></span> <span data-ttu-id="22043-122">De accountsleutel voor het opslagaccount voor de taak voor exporteren.</span><span class="sxs-lookup"><span data-stu-id="22043-122">The account key for the storage account for the export job.</span></span>|  
|<span data-ttu-id="22043-123">**/csas:**< ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="22043-123">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="22043-124">Vereist als de sleutel van een opslagaccount is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="22043-124">Required if and only if a storage account key is not specified.</span></span> <span data-ttu-id="22043-125">De container SAS voor het weergeven van de blobs in de taak voor het exporteren worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="22043-125">The container SAS for listing the blobs to be exported in the export job.</span></span>|  
|<span data-ttu-id="22043-126">**/ ExportBlobListFile:**< ExportBlobListFile\></span><span class="sxs-lookup"><span data-stu-id="22043-126">**/ExportBlobListFile:**<ExportBlobListFile\></span></span>|<span data-ttu-id="22043-127">Vereist.</span><span class="sxs-lookup"><span data-stu-id="22043-127">Required.</span></span> <span data-ttu-id="22043-128">Pad naar het XML-bestand met lijst met blob-paden bestand of blob-pad voorvoegsels voor de blobs worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="22043-128">Path to the XML file containing list of blob paths or blob path prefixes for the blobs to be exported.</span></span> <span data-ttu-id="22043-129">De bestandsindeling die wordt gebruikt in de `BlobListBlobPath` -element in de [taak plaatsen](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) bewerking van de Import/Export-service REST-API.</span><span class="sxs-lookup"><span data-stu-id="22043-129">The file format used in the `BlobListBlobPath` element in the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of the Import/Export service REST API.</span></span>|  
|<span data-ttu-id="22043-130">**/ DriveSize:**< DriveSize\></span><span class="sxs-lookup"><span data-stu-id="22043-130">**/DriveSize:**<DriveSize\></span></span>|<span data-ttu-id="22043-131">Vereist.</span><span class="sxs-lookup"><span data-stu-id="22043-131">Required.</span></span> <span data-ttu-id="22043-132">De grootte van stations voor een exporttaak *bijvoorbeeld*, 500 GB, 1,5 TB.</span><span class="sxs-lookup"><span data-stu-id="22043-132">The size of drives to use for an export job, *e.g.*, 500GB, 1.5TB.</span></span>|  

## <a name="command-line-example"></a><span data-ttu-id="22043-133">Voorbeeld van de opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="22043-133">Command-line example</span></span>

<span data-ttu-id="22043-134">Het volgende voorbeeld toont de `PreviewExport` opdracht:</span><span class="sxs-lookup"><span data-stu-id="22043-134">The following example demonstrates the `PreviewExport` command:</span></span>  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
<span data-ttu-id="22043-135">Het exportbestand voor de lijst van blob kan blobnamen bevatten en blob-voorvoegsels, zoals hier wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="22043-135">The export blob list file may contain blob names and blob prefixes, as shown here:</span></span>  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

<span data-ttu-id="22043-136">De Azure-hulpprogramma voor importeren/exporteren geeft een lijst van alle blobs worden geëxporteerd en berekent hoe ze in de stations van de opgegeven grootte pack rekening wordt gehouden met eventuele benodigde overhead en maakt een schatting van het aantal stations die nodig zijn voor het opslaan van blobs en informatie over het gebruik van de schijf.</span><span class="sxs-lookup"><span data-stu-id="22043-136">The Azure Import/Export Tool lists all blobs to be exported and calculates how to pack them into drives of the specified size, taking into account any necessary overhead, then estimates the number of drives needed to hold the blobs and drive usage information.</span></span>  
  
<span data-ttu-id="22043-137">Hier volgt een voorbeeld van uitvoer van de met informatief logboeken die worden weggelaten:</span><span class="sxs-lookup"><span data-stu-id="22043-137">Here is an example of the output, with informational logs omitted:</span></span>  
  
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
  
## <a name="next-steps"></a><span data-ttu-id="22043-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="22043-138">Next steps</span></span>

* [<span data-ttu-id="22043-139">Naslaginformatie over Azure hulpprogramma voor importeren/exporteren</span><span class="sxs-lookup"><span data-stu-id="22043-139">Azure Import/Export Tool reference</span></span>](../storage-import-export-tool-how-to-v1.md)
