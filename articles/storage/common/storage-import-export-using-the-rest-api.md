---
title: Met de Azure Import/Export-service REST-API | Microsoft Docs
description: Meer informatie over waar u informatie over het gebruik van de Azure Import/Export-service REST API, met inbegrip van de procedures voor-en naslagmateriaal vinden.
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
ms.openlocfilehash: b780385ad0af34bcb15639683d1aa5d689b38b50
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-importexport-service-rest-api"></a><span data-ttu-id="a2f74-103">De REST-API van de Azure-service Import/Export gebruiken</span><span class="sxs-lookup"><span data-stu-id="a2f74-103">Using the Azure Import/Export service REST API</span></span>

<span data-ttu-id="a2f74-104">De Microsoft Azure Import/Export-service wordt een REST-API voor programmatisch beheer van importeren/exporteren-taken.</span><span class="sxs-lookup"><span data-stu-id="a2f74-104">The Microsoft Azure Import/Export service exposes a REST API to enable programmatic control of import/export jobs.</span></span> <span data-ttu-id="a2f74-105">U kunt de REST-API gebruiken om uit te voeren op alle bewerkingen voor importeren/exporteren die u met uitvoeren kunt de [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a2f74-105">You can use the REST API to perform all of the import/export operations that you can perform with the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="a2f74-106">Bovendien kunt u de REST-API om uit te voeren van bepaalde gedetailleerde bewerkingen, zoals het uitvoeren van query's de percentage voltooiing van een taak die momenteel niet beschikbaar in de klassieke Azure portal is.</span><span class="sxs-lookup"><span data-stu-id="a2f74-106">Additionally, you can use the REST API to perform certain granular operations, such as querying the percentage completion of a job, which is not currently available in the Azure classic portal.</span></span>

<span data-ttu-id="a2f74-107">Zie [via de Microsoft Azure Import/Export-service gegevens overdragen naar Blob Storage](../storage-import-export-service.md) voor een overzicht van de Import/Export-service en een zelfstudie waarin wordt getoond hoe u de klassieke portal maken en beheren van importeren en exporteren van taken.</span><span class="sxs-lookup"><span data-stu-id="a2f74-107">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](../storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the classic portal to create and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="a2f74-108">Service-eindpunten</span><span class="sxs-lookup"><span data-stu-id="a2f74-108">Service endpoints</span></span>

<span data-ttu-id="a2f74-109">De Azure Import/Export-service is een resourceprovider voor Azure Resource Manager en biedt een set van REST-API's op de volgende HTTPS-eindpunt voor het beheren van taken voor importeren/exporteren:</span><span class="sxs-lookup"><span data-stu-id="a2f74-109">The Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at the following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="a2f74-110">Versiebeheer voor onderdelen</span><span class="sxs-lookup"><span data-stu-id="a2f74-110">Versioning</span></span>

<span data-ttu-id="a2f74-111">Aanvragen voor de Import/Export-service moeten opgeven de `api-version` parameter en stel de waarde op `2016-11-01`.</span><span class="sxs-lookup"><span data-stu-id="a2f74-111">Requests to the Import/Export service must specify the `api-version` parameter and set its value to `2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="a2f74-112">Servicebewerkingen voor importeren/exporteren</span><span class="sxs-lookup"><span data-stu-id="a2f74-112">Import/Export service operations</span></span>

[<span data-ttu-id="a2f74-113">Een importtaak maken</span><span class="sxs-lookup"><span data-stu-id="a2f74-113">Creating an import job</span></span>](../storage-import-export-creating-an-import-job.md)

[<span data-ttu-id="a2f74-114">Een exporttaak maken</span><span class="sxs-lookup"><span data-stu-id="a2f74-114">Creating an export job</span></span>](../storage-import-export-creating-an-export-job.md)

[<span data-ttu-id="a2f74-115">Statusinformatie van een taak ophalen</span><span class="sxs-lookup"><span data-stu-id="a2f74-115">Retrieving state information for a job</span></span>](storage-import-export-retrieving-state-info-for-a-job.md)

[<span data-ttu-id="a2f74-116">Taken opsommen</span><span class="sxs-lookup"><span data-stu-id="a2f74-116">Enumerating jobs</span></span>](../storage-import-export-enumerating-jobs.md)

[<span data-ttu-id="a2f74-117">Taken annuleren en verwijderen</span><span class="sxs-lookup"><span data-stu-id="a2f74-117">Cancelling and deleting jobs</span></span>](storage-import-export-cancelling-and-deleting-jobs.md)

[<span data-ttu-id="a2f74-118">Een back-Up station manifesten</span><span class="sxs-lookup"><span data-stu-id="a2f74-118">Backing Up drive manifests</span></span>](../storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="a2f74-119">Diagnoses en het herstel van fouten voor Import/Export-taken</span><span class="sxs-lookup"><span data-stu-id="a2f74-119">Diagnostics and error recovery for Import/Export jobs</span></span>](../storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="a2f74-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a2f74-120">Next steps</span></span>

* [<span data-ttu-id="a2f74-121">Opslag voor importeren/exporteren REST</span><span class="sxs-lookup"><span data-stu-id="a2f74-121">Storage Import/Export REST</span></span>](/rest/api/storageimportexport)
