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
ms.openlocfilehash: 1e989c72fc03697bf6d2e515ff53003703665d1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="04ce9-103">Annuleren en het verwijderen van de Azure Import/Export-taken</span><span class="sxs-lookup"><span data-stu-id="04ce9-103">Canceling and deleting Azure Import/Export jobs</span></span>

 <span data-ttu-id="04ce9-104">Om aan te vragen of een taak worden geannuleerd voordat deze zich in de `Packaging` status, neemt u contact de [Update taakeigenschappen](/rest/api/storageimportexport/jobs#Jobs_Update) bewerking en stel de `CancelRequested` element op de `true`.</span><span class="sxs-lookup"><span data-stu-id="04ce9-104">To request that a job be canceled before it is in the `Packaging` state, call the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and set the `CancelRequested` element to `true`.</span></span> <span data-ttu-id="04ce9-105">De taak is geannuleerd op basis van best-effort.</span><span class="sxs-lookup"><span data-stu-id="04ce9-105">The job is canceled on a best-effort basis.</span></span> <span data-ttu-id="04ce9-106">Als er stations zijn bezig het overbrengen van gegevens, blijven gegevens worden overgebracht, zelfs nadat de annulering is aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="04ce9-106">If drives are in the process of transferring data, data may continue to be transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="04ce9-107">Een geannuleerde taak wordt verplaatst naar de `Completed` status en bijgehouden voor 90 dagen op dat moment wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="04ce9-107">A canceled job is moved to the `Completed` state and is kept for 90 days, at which point it is deleted.</span></span>

 <span data-ttu-id="04ce9-108">Aanroepen voor het verwijderen van een taak, de [taak verwijderen](/rest/api/storageimportexport/jobs#Jobs_Delete) bewerking voordat de taak is verzonden (dat wil zeggen, terwijl de taak wordt de `Creating` staat).</span><span class="sxs-lookup"><span data-stu-id="04ce9-108">To delete a job, call the [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before the job has shipped (that is, while the job is in the `Creating` state).</span></span> <span data-ttu-id="04ce9-109">U kunt ook een taak verwijderen wanneer deze zich in de `Completed` staat.</span><span class="sxs-lookup"><span data-stu-id="04ce9-109">You can also delete a job when it is in the `Completed` state.</span></span> <span data-ttu-id="04ce9-110">Nadat een taak is verwijderd, de informatie en de status niet langer zijn toegankelijk via de REST-API of de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="04ce9-110">After a job is deleted, its information and status are no longer accessible via the REST API or the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04ce9-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="04ce9-111">Next steps</span></span>

* [<span data-ttu-id="04ce9-112">Met behulp van de Import/Export-service REST-API</span><span class="sxs-lookup"><span data-stu-id="04ce9-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
