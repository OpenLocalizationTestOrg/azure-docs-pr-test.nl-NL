---
title: aaaUsing hello Azure Import/Export-service REST-API | Microsoft Docs
description: Meer informatie over waar toofind resources voor het gebruik van hello Azure Import/Export REST API, met inbegrip van beide referentiemateriaal hoe tooand service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: fc7e1007ad632cf6f771c2545644f8de43c8f181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a><span data-ttu-id="89277-103">Met behulp van hello Azure Import/Export-service REST-API</span><span class="sxs-lookup"><span data-stu-id="89277-103">Using hello Azure Import/Export service REST API</span></span>

<span data-ttu-id="89277-104">Hallo Microsoft Azure Import/Export-service wordt een REST-API tooenable programmatisch beheer van importeren/exporteren-taken.</span><span class="sxs-lookup"><span data-stu-id="89277-104">hello Microsoft Azure Import/Export service exposes a REST API tooenable programmatic control of import/export jobs.</span></span> <span data-ttu-id="89277-105">U kunt Hallo REST-API tooperform alle Hallo voor importeren/exporteren bewerkingen die u met Hallo uitvoeren kunt [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="89277-105">You can use hello REST API tooperform all of hello import/export operations that you can perform with hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="89277-106">Bovendien kunt u Hallo REST-API tooperform bepaalde gedetailleerde bewerkingen, zoals het uitvoeren van query's Hallo percentage voltooiing van een taak die momenteel niet beschikbaar in de klassieke Azure-portal Hallo is.</span><span class="sxs-lookup"><span data-stu-id="89277-106">Additionally, you can use hello REST API tooperform certain granular operations, such as querying hello percentage completion of a job, which is not currently available in hello Azure classic portal.</span></span>

<span data-ttu-id="89277-107">Zie [Hallo Microsoft Azure Import/Export-service tooTransfer gegevens tooBlob opslag met](../storage-import-export-service.md) voor een overzicht van Hallo Import/Export-service en een zelfstudie wordt gedemonstreerd hoe toouse Hallo klassieke portal toocreate en importeren beheren en exporteren van taken.</span><span class="sxs-lookup"><span data-stu-id="89277-107">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](../storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello classic portal toocreate and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="89277-108">Service-eindpunten</span><span class="sxs-lookup"><span data-stu-id="89277-108">Service endpoints</span></span>

<span data-ttu-id="89277-109">Hello Azure Import/Export-service is een resourceprovider voor Azure Resource Manager en biedt een set REST-API's op Hallo HTTPS-eindpunt voor het beheren van importeren/exporteren taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="89277-109">hello Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at hello following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="89277-110">Versiebeheer voor onderdelen</span><span class="sxs-lookup"><span data-stu-id="89277-110">Versioning</span></span>

<span data-ttu-id="89277-111">Aanvragen toohello Import/Export-service moet opgeven Hallo `api-version` parameter en stel de waarde te`2016-11-01`.</span><span class="sxs-lookup"><span data-stu-id="89277-111">Requests toohello Import/Export service must specify hello `api-version` parameter and set its value too`2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="89277-112">Servicebewerkingen voor importeren/exporteren</span><span class="sxs-lookup"><span data-stu-id="89277-112">Import/Export service operations</span></span>

[<span data-ttu-id="89277-113">Een importtaak maken</span><span class="sxs-lookup"><span data-stu-id="89277-113">Creating an import job</span></span>](../storage-import-export-creating-an-import-job.md)

[<span data-ttu-id="89277-114">Een exporttaak maken</span><span class="sxs-lookup"><span data-stu-id="89277-114">Creating an export job</span></span>](../storage-import-export-creating-an-export-job.md)

[<span data-ttu-id="89277-115">Statusinformatie van een taak ophalen</span><span class="sxs-lookup"><span data-stu-id="89277-115">Retrieving state information for a job</span></span>](storage-import-export-retrieving-state-info-for-a-job.md)

[<span data-ttu-id="89277-116">Taken opsommen</span><span class="sxs-lookup"><span data-stu-id="89277-116">Enumerating jobs</span></span>](../storage-import-export-enumerating-jobs.md)

[<span data-ttu-id="89277-117">Taken annuleren en verwijderen</span><span class="sxs-lookup"><span data-stu-id="89277-117">Cancelling and deleting jobs</span></span>](storage-import-export-cancelling-and-deleting-jobs.md)

[<span data-ttu-id="89277-118">Een back-Up station manifesten</span><span class="sxs-lookup"><span data-stu-id="89277-118">Backing Up drive manifests</span></span>](../storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="89277-119">Diagnoses en het herstel van fouten voor Import/Export-taken</span><span class="sxs-lookup"><span data-stu-id="89277-119">Diagnostics and error recovery for Import/Export jobs</span></span>](../storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="89277-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="89277-120">Next steps</span></span>

* [<span data-ttu-id="89277-121">Opslag voor importeren/exporteren REST</span><span class="sxs-lookup"><span data-stu-id="89277-121">Storage Import/Export REST</span></span>](/rest/api/storageimportexport)
