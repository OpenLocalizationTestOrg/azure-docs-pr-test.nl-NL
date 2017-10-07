---
title: aaaDiagnostics en fout herstel voor Azure Import/Export-taken | Microsoft Docs
description: Meer informatie over hoe de taken voor tooenable uitgebreide logboekregistratie voor Microsoft Azure Import/Export-service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 096cc795-9af6-4335-9fe8-fffa9f239a17
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 48164279e7904c78fed802aa3cff66e589c3f12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="5953c-103">Diagnostische gegevens en de fout herstel voor Azure Import/Export-taken</span><span class="sxs-lookup"><span data-stu-id="5953c-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="5953c-104">Voor elk station verwerkt maakt hello Azure Import/Export-service een foutenlogboek in het opslagaccount Hallo die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="5953c-104">For each drive processed, hello Azure Import/Export service creates an error log in hello associated storage account.</span></span> <span data-ttu-id="5953c-105">U kunt ook uitgebreide logboekregistratie inschakelen door de instelling Hallo `LogLevel` eigenschap te`Verbose` bij het aanroepen van Hallo [taak plaatsen](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) of [Update taakeigenschappen](/rest/api/storageimportexport/jobs#Jobs_Update) bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="5953c-105">You can also enable verbose logging by setting hello `LogLevel` property too`Verbose` when calling hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="5953c-106">Standaard Logboeken geschreven tooa container met de naam `waimportexport`.</span><span class="sxs-lookup"><span data-stu-id="5953c-106">By default, logs are written tooa container named `waimportexport`.</span></span> <span data-ttu-id="5953c-107">U kunt een andere naam opgeven door de instelling Hallo `DiagnosticsPath` eigenschap bij het aanroepen van Hallo `Put Job` of `Update Job Properties` bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="5953c-107">You can specify a different name by setting hello `DiagnosticsPath` property when calling hello `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="5953c-108">Hallo logboeken worden opgeslagen als blok-blobs Hello volgende naamconventie: `waies/jobname_driveid_timestamp_logtype.xml`.</span><span class="sxs-lookup"><span data-stu-id="5953c-108">hello logs are stored as block blobs with hello following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="5953c-109">U kunt ophalen Hallo URI van Hallo-logboeken voor een taak door de aanroepende Hallo [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) bewerking.</span><span class="sxs-lookup"><span data-stu-id="5953c-109">You can retrieve hello URI of hello logs for a job by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="5953c-110">Hallo URI voor de uitgebreide logboek hello wordt geretourneerd als Hallo `VerboseLogUri` eigenschap voor elk station terwijl Hallo URI voor Hallo foutenlogboek wordt geretourneerd als Hallo `ErrorLogUri` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="5953c-110">hello URI for hello verbose log is returned in hello `VerboseLogUri` property for each drive, while hello URI for hello error log is returned in hello `ErrorLogUri` property.</span></span>

<span data-ttu-id="5953c-111">U kunt Hallo logboekregistratie gegevens tooidentify Hallo problemen te volgen.</span><span class="sxs-lookup"><span data-stu-id="5953c-111">You can use hello logging data tooidentify hello following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="5953c-112">Station fouten</span><span class="sxs-lookup"><span data-stu-id="5953c-112">Drive errors</span></span>

<span data-ttu-id="5953c-113">Hallo volgende items zijn geclassificeerd als station fouten:</span><span class="sxs-lookup"><span data-stu-id="5953c-113">hello following items are classified as drive errors:</span></span>

-   <span data-ttu-id="5953c-114">Fouten in de toegang tot of het lezen van Hallo-manifestbestand</span><span class="sxs-lookup"><span data-stu-id="5953c-114">Errors in accessing or reading hello manifest file</span></span>

-   <span data-ttu-id="5953c-115">Onjuiste BitLocker-sleutels</span><span class="sxs-lookup"><span data-stu-id="5953c-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="5953c-116">Schijf lezen/schrijven-fouten</span><span class="sxs-lookup"><span data-stu-id="5953c-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="5953c-117">BLOB-fouten</span><span class="sxs-lookup"><span data-stu-id="5953c-117">Blob errors</span></span>

<span data-ttu-id="5953c-118">Hallo volgende items zijn geclassificeerd als blob fouten:</span><span class="sxs-lookup"><span data-stu-id="5953c-118">hello following items are classified as blob errors:</span></span>

-   <span data-ttu-id="5953c-119">Onjuiste of conflicterende blob of -namen</span><span class="sxs-lookup"><span data-stu-id="5953c-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="5953c-120">Ontbrekende bestanden</span><span class="sxs-lookup"><span data-stu-id="5953c-120">Missing files</span></span>

-   <span data-ttu-id="5953c-121">BLOB is niet gevonden</span><span class="sxs-lookup"><span data-stu-id="5953c-121">Blob not found</span></span>

-   <span data-ttu-id="5953c-122">Afgekapte bestanden (bestanden op schijf Hallo Hallo zijn kleiner is dan de opgegeven in het manifest Hallo)</span><span class="sxs-lookup"><span data-stu-id="5953c-122">Truncated files (hello files on hello disk are smaller than specified in hello manifest)</span></span>

-   <span data-ttu-id="5953c-123">Beschadigd bestand inhoud (voor importtaken die is gedetecteerd met een MD5-checksum komt niet overeen)</span><span class="sxs-lookup"><span data-stu-id="5953c-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="5953c-124">Beschadigde blob-eigenschap bestanden met metagegevens en (gedetecteerd met een MD5-checksum komt niet overeen)</span><span class="sxs-lookup"><span data-stu-id="5953c-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="5953c-125">Onjuist schema voor Hallo blob eigenschappen en/of bestanden met metagegevens</span><span class="sxs-lookup"><span data-stu-id="5953c-125">Incorrect schema for hello blob properties and/or metadata files</span></span>

<span data-ttu-id="5953c-126">Mogelijk zijn er gevallen waarbij sommige onderdelen van een taak importeren of exporteren komen niet voltooid, terwijl hello algemene taak nog steeds is voltooid.</span><span class="sxs-lookup"><span data-stu-id="5953c-126">There may be cases where some parts of an import or export job do not complete successfully, while hello overall job still completes.</span></span> <span data-ttu-id="5953c-127">In dit geval kunt u uploaden of downloaden Hallo Hallo gegevens via netwerk ontbreekt of u een nieuwe taak tootransfer Hallo gegevens kunt maken.</span><span class="sxs-lookup"><span data-stu-id="5953c-127">In this case, you can either upload or download hello missing pieces of hello data over network, or you can create a new job tootransfer hello data.</span></span> <span data-ttu-id="5953c-128">Zie Hallo [Azure Import/Export hulpprogramma verwijzing](storage-import-export-tool-how-to-v1.md) toolearn hoe toorepair gegevens Hallo via netwerk.</span><span class="sxs-lookup"><span data-stu-id="5953c-128">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) toolearn how toorepair hello data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5953c-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5953c-129">Next steps</span></span>

* [<span data-ttu-id="5953c-130">Met behulp van REST-API voor Hallo Import/Export-service</span><span class="sxs-lookup"><span data-stu-id="5953c-130">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
