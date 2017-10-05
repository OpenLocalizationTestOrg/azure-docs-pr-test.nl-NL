---
title: Back-ups van de Azure Import/Export station manifesten | Microsoft Docs
description: Informatie over hoe u uw station manifesten voor de Microsoft Azure Import/Export-service automatisch een back-up gemaakt.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 594abd80-b834-4077-a474-d8a0f4b7928a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 33eb8e1eea8f8aa7b79ef3e54f2b1ed88dc794ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a><span data-ttu-id="58a13-103">Back-ups van schijf manifesten voor Azure Import/Export-taken</span><span class="sxs-lookup"><span data-stu-id="58a13-103">Backing up drive manifests for Azure Import/Export jobs</span></span>

<span data-ttu-id="58a13-104">Station manifesten kunnen automatisch een back-up naar BLOB's door in te stellen de `BackupDriveManifest` eigenschap `true` in de [taak plaatsen](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) of [Update taakeigenschappen](/rest/api/storageimportexport/jobs#Jobs_Update) REST-API-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="58a13-104">Drive manifests can be automatically backed up to blobs by setting the `BackupDriveManifest` property to `true` in the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) REST API operations.</span></span> <span data-ttu-id="58a13-105">Standaard de manifesten station zijn geen back-up gemaakt.</span><span class="sxs-lookup"><span data-stu-id="58a13-105">By default, the drive manifests are not backed up.</span></span> <span data-ttu-id="58a13-106">De back-ups manifest station worden opgeslagen als blok-blobs in een container in het opslagaccount die is gekoppeld aan de taak.</span><span class="sxs-lookup"><span data-stu-id="58a13-106">The drive manifest backups are stored as block blobs in a container within the storage account associated with the job.</span></span> <span data-ttu-id="58a13-107">De containernaam is standaard `waimportexport`, maar u kunt opgeven dat een andere naam in de `DiagnosticsPath` eigenschap bij het aanroepen van de `Put Job` of `Update Job Properties` bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="58a13-107">By default, the container name is `waimportexport`, but you can specify a different name in the `DiagnosticsPath` property when calling the `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="58a13-108">De back-manifest blob zijn met de naam in de volgende indeling: `waies/jobname_driveid_timestamp_manifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="58a13-108">The backup manifest blob are named in the following format: `waies/jobname_driveid_timestamp_manifest.xml`.</span></span>

 <span data-ttu-id="58a13-109">U kunt de URI van de manifesten back-station voor een taak ophalen door het aanroepen van de [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) bewerking.</span><span class="sxs-lookup"><span data-stu-id="58a13-109">You can retrieve the URI of the backup drive manifests for a job by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="58a13-110">De blob URI wordt geretourneerd als de `ManifestUri` eigenschap voor elk station.</span><span class="sxs-lookup"><span data-stu-id="58a13-110">The blob URI is returned in the `ManifestUri` property for each drive.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58a13-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="58a13-111">Next steps</span></span>

* [<span data-ttu-id="58a13-112">Met behulp van de Import/Export-service REST-API</span><span class="sxs-lookup"><span data-stu-id="58a13-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
