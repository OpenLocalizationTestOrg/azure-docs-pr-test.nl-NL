---
title: Diagnostische gegevens en de fout herstel voor Azure Import/Export taken | Microsoft Docs
description: Informatie over het inschakelen van uitgebreide logboekregistratie voor Microsoft Azure Import/Export-service-taken.
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
ms.openlocfilehash: 0068aae9d6780aa41a070db0eb191d0d5a165d21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="2b569-103">Diagnostische gegevens en de fout herstel voor Azure Import/Export-taken</span><span class="sxs-lookup"><span data-stu-id="2b569-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="2b569-104">Voor elk station dat wordt verwerkt, maakt de Azure Import/Export-service een foutenlogboek in het bijbehorende opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="2b569-104">For each drive processed, the Azure Import/Export service creates an error log in the associated storage account.</span></span> <span data-ttu-id="2b569-105">U kunt ook uitgebreide logboekregistratie inschakelen door in te stellen de `LogLevel` eigenschap `Verbose` bij het aanroepen van de [taak plaatsen](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) of [Update taakeigenschappen](/rest/api/storageimportexport/jobs#Jobs_Update) bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="2b569-105">You can also enable verbose logging by setting the `LogLevel` property to `Verbose` when calling the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="2b569-106">Standaard worden naar een container met de naam Logboeken geschreven `waimportexport`.</span><span class="sxs-lookup"><span data-stu-id="2b569-106">By default, logs are written to a container named `waimportexport`.</span></span> <span data-ttu-id="2b569-107">U kunt een andere naam opgeven door de `DiagnosticsPath` eigenschap bij het aanroepen van de `Put Job` of `Update Job Properties` bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="2b569-107">You can specify a different name by setting the `DiagnosticsPath` property when calling the `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="2b569-108">De logboeken worden opgeslagen als blok-blobs met de volgende naamconventie: `waies/jobname_driveid_timestamp_logtype.xml`.</span><span class="sxs-lookup"><span data-stu-id="2b569-108">The logs are stored as block blobs with the following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="2b569-109">U kunt de URI van de logboeken voor een taak ophalen door het aanroepen van de [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) bewerking.</span><span class="sxs-lookup"><span data-stu-id="2b569-109">You can retrieve the URI of the logs for a job by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="2b569-110">De URI voor het uitgebreide logboek wordt geretourneerd als de `VerboseLogUri` eigenschap voor elke schijf, terwijl de URI voor het foutenlogboek wordt geretourneerd als de `ErrorLogUri` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="2b569-110">The URI for the verbose log is returned in the `VerboseLogUri` property for each drive, while the URI for the error log is returned in the `ErrorLogUri` property.</span></span>

<span data-ttu-id="2b569-111">De logboekgegevens kunt u de volgende problemen te identificeren.</span><span class="sxs-lookup"><span data-stu-id="2b569-111">You can use the logging data to identify the following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="2b569-112">Station fouten</span><span class="sxs-lookup"><span data-stu-id="2b569-112">Drive errors</span></span>

<span data-ttu-id="2b569-113">De volgende items zijn geclassificeerd als station fouten:</span><span class="sxs-lookup"><span data-stu-id="2b569-113">The following items are classified as drive errors:</span></span>

-   <span data-ttu-id="2b569-114">Fouten in de toegang tot of het lezen van het manifestbestand</span><span class="sxs-lookup"><span data-stu-id="2b569-114">Errors in accessing or reading the manifest file</span></span>

-   <span data-ttu-id="2b569-115">Onjuiste BitLocker-sleutels</span><span class="sxs-lookup"><span data-stu-id="2b569-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="2b569-116">Schijf lezen/schrijven-fouten</span><span class="sxs-lookup"><span data-stu-id="2b569-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="2b569-117">BLOB-fouten</span><span class="sxs-lookup"><span data-stu-id="2b569-117">Blob errors</span></span>

<span data-ttu-id="2b569-118">De volgende items zijn geclassificeerd als blob fouten:</span><span class="sxs-lookup"><span data-stu-id="2b569-118">The following items are classified as blob errors:</span></span>

-   <span data-ttu-id="2b569-119">Onjuiste of conflicterende blob of -namen</span><span class="sxs-lookup"><span data-stu-id="2b569-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="2b569-120">Ontbrekende bestanden</span><span class="sxs-lookup"><span data-stu-id="2b569-120">Missing files</span></span>

-   <span data-ttu-id="2b569-121">BLOB is niet gevonden</span><span class="sxs-lookup"><span data-stu-id="2b569-121">Blob not found</span></span>

-   <span data-ttu-id="2b569-122">Afgekapte bestanden (de bestanden op de schijf zijn kleiner is dan de opgegeven in het manifest)</span><span class="sxs-lookup"><span data-stu-id="2b569-122">Truncated files (the files on the disk are smaller than specified in the manifest)</span></span>

-   <span data-ttu-id="2b569-123">Beschadigd bestand inhoud (voor importtaken die is gedetecteerd met een MD5-checksum komt niet overeen)</span><span class="sxs-lookup"><span data-stu-id="2b569-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="2b569-124">Beschadigde blob-eigenschap bestanden met metagegevens en (gedetecteerd met een MD5-checksum komt niet overeen)</span><span class="sxs-lookup"><span data-stu-id="2b569-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="2b569-125">Onjuist schema voor de blob-eigenschappen en/of de bestanden met metagegevens</span><span class="sxs-lookup"><span data-stu-id="2b569-125">Incorrect schema for the blob properties and/or metadata files</span></span>

<span data-ttu-id="2b569-126">Mogelijk zijn er gevallen waarbij sommige onderdelen van een taak importeren of exporteren komen niet voltooid, wordt nog steeds de algehele taak voltooid.</span><span class="sxs-lookup"><span data-stu-id="2b569-126">There may be cases where some parts of an import or export job do not complete successfully, while the overall job still completes.</span></span> <span data-ttu-id="2b569-127">In dit geval kunt u uploaden of downloaden van de ontbrekende onderdelen van de gegevens via het netwerk of u een nieuwe taak om de gegevens kunt maken.</span><span class="sxs-lookup"><span data-stu-id="2b569-127">In this case, you can either upload or download the missing pieces of the data over network, or you can create a new job to transfer the data.</span></span> <span data-ttu-id="2b569-128">Zie de [Azure Import/Export hulpprogramma verwijzing](storage-import-export-tool-how-to-v1.md) voor informatie over het herstellen van de gegevens via het netwerk.</span><span class="sxs-lookup"><span data-stu-id="2b569-128">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) to learn how to repair the data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b569-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2b569-129">Next steps</span></span>

* [<span data-ttu-id="2b569-130">Met behulp van de Import/Export-service REST-API</span><span class="sxs-lookup"><span data-stu-id="2b569-130">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
