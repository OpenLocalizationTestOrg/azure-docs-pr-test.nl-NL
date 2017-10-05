---
title: Annuleren en een Azure Import/Export-taak verwijderen | Microsoft Docs
description: Informatie over het annuleren en taken voor de Microsoft Azure Import/Export-service verwijderen.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: e0a7ff391e5a03ed563912dea54c7cfe73111bcf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="26bb0-103">Annuleren en het verwijderen van de Azure Import/Export-taken</span><span class="sxs-lookup"><span data-stu-id="26bb0-103">Canceling and deleting Azure Import/Export jobs</span></span>

<span data-ttu-id="26bb0-104">U kunt aanvragen dat een taak geannuleerd voordat deze wordt de `Packaging` status door het aanroepen van de [taakeigenschappen bijwerken](/rest/api/storageimportexport/jobs#Jobs_Update) bewerking en instelling van de `CancelRequested` element op de `true`.</span><span class="sxs-lookup"><span data-stu-id="26bb0-104">You can request that a job be cancelled before it is in the `Packaging` state by calling the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and setting the `CancelRequested` element to `true`.</span></span> <span data-ttu-id="26bb0-105">De taak worden op basis van best-effort geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="26bb0-105">The job will be cancelled on a best-effort basis.</span></span> <span data-ttu-id="26bb0-106">Als er stations zijn bezig het overbrengen van gegevens, blijven gegevens worden overgebracht, zelfs nadat de annulering is aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="26bb0-106">If drives are in the process of transferring data, data may continue to be transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="26bb0-107">Een geannuleerde taak wordt verplaatst naar de `Completed` status en worden bewaard gedurende 90 dagen op dat moment worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="26bb0-107">A cancelled job will move to the `Completed` state and be kept for 90 days, at which point it will be deleted.</span></span>

 <span data-ttu-id="26bb0-108">Aanroepen voor het verwijderen van een taak, de [taak verwijderen](/rest/api/storageimportexport/jobs#Jobs_Delete) bewerking voordat de taak is verzonden (*dat wil zeggen*, terwijl de taak de `Creating` staat).</span><span class="sxs-lookup"><span data-stu-id="26bb0-108">To delete a job, call the [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before the job has shipped (*i.e.*, while the job is in the `Creating` state).</span></span> <span data-ttu-id="26bb0-109">U kunt ook een taak verwijderen wanneer deze zich in de `Completed` staat.</span><span class="sxs-lookup"><span data-stu-id="26bb0-109">You can also delete a job when it is in the `Completed` state.</span></span> <span data-ttu-id="26bb0-110">Nadat een taak is verwijderd, de informatie en de status niet langer zijn toegankelijk via de REST-API of de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="26bb0-110">After a job has been deleted, its information and status are no longer accessible via the REST API or the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26bb0-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="26bb0-111">Next steps</span></span>

* [<span data-ttu-id="26bb0-112">Met behulp van de Import/Export-service REST-API</span><span class="sxs-lookup"><span data-stu-id="26bb0-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
