---
title: aaaBacking up Azure Import/Export station manifesten | Microsoft Docs
description: Meer informatie over hoe toohave station manifesten voor Hallo Microsoft Azure Import/Export-service automatisch een back-up gemaakt.
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
ms.openlocfilehash: f48b97a2cce62714aace2b30a393305202c7ecd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a><span data-ttu-id="d0f16-103">Back-ups van schijf manifesten voor Azure Import/Export-taken</span><span class="sxs-lookup"><span data-stu-id="d0f16-103">Backing up drive manifests for Azure Import/Export jobs</span></span>

<span data-ttu-id="d0f16-104">Station manifesten kunnen automatisch een back-up tooblobs door Hallo instelling `BackupDriveManifest` eigenschap te`true` in Hallo [taak plaatsen](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) of [Update taakeigenschappen](/rest/api/storageimportexport/jobs#Jobs_Update) REST-API-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="d0f16-104">Drive manifests can be automatically backed up tooblobs by setting hello `BackupDriveManifest` property too`true` in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) REST API operations.</span></span> <span data-ttu-id="d0f16-105">Standaard Hallo station manifesten zijn geen back-up gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d0f16-105">By default, hello drive manifests are not backed up.</span></span> <span data-ttu-id="d0f16-106">Hallo station manifest back-ups worden opgeslagen als blok-blobs in een container in Hallo storage-account aan Hallo taak zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="d0f16-106">hello drive manifest backups are stored as block blobs in a container within hello storage account associated with hello job.</span></span> <span data-ttu-id="d0f16-107">Hallo-containernaam is standaard `waimportexport`, maar u kunt een andere naam opgeven in Hallo `DiagnosticsPath` eigenschap bij het aanroepen van Hallo `Put Job` of `Update Job Properties` bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="d0f16-107">By default, hello container name is `waimportexport`, but you can specify a different name in hello `DiagnosticsPath` property when calling hello `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="d0f16-108">Hallo back-manifest blob zijn met de naam in de volgende indeling Hallo: `waies/jobname_driveid_timestamp_manifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="d0f16-108">hello backup manifest blob are named in hello following format: `waies/jobname_driveid_timestamp_manifest.xml`.</span></span>

 <span data-ttu-id="d0f16-109">U kunt de URI van de back-station Hallo voor een taak door de aanroepende Hallo manifesten Hallo ophalen [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) bewerking.</span><span class="sxs-lookup"><span data-stu-id="d0f16-109">You can retrieve hello URI of hello backup drive manifests for a job by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="d0f16-110">Hallo blob URI wordt geretourneerd als Hallo `ManifestUri` eigenschap voor elk station.</span><span class="sxs-lookup"><span data-stu-id="d0f16-110">hello blob URI is returned in hello `ManifestUri` property for each drive.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0f16-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d0f16-111">Next steps</span></span>

* [<span data-ttu-id="d0f16-112">Met behulp van REST-API voor Hallo Import/Export-service</span><span class="sxs-lookup"><span data-stu-id="d0f16-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
