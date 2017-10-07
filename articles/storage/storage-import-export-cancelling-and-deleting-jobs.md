---
title: aaaCancel en verwijderen van een Azure Import/Export-taak | Microsoft Docs
description: Meer informatie over hoe toocancel en delete taken voor Hallo Microsoft Azure Import/Export-service.
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
ms.openlocfilehash: 5d2aba510dafd0ca9a10f5643f721e7059a6a8f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="8af67-103">Annuleren en het verwijderen van de Azure Import/Export-taken</span><span class="sxs-lookup"><span data-stu-id="8af67-103">Canceling and deleting Azure Import/Export jobs</span></span>

<span data-ttu-id="8af67-104">U kunt aanvragen dat een taak geannuleerd voordat deze in Hallo `Packaging` status door de aanroepende Hallo [Update taakeigenschappen](/rest/api/storageimportexport/jobs#Jobs_Update) bewerking en instelling Hallo `CancelRequested` element te`true`.</span><span class="sxs-lookup"><span data-stu-id="8af67-104">You can request that a job be cancelled before it is in hello `Packaging` state by calling hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and setting hello `CancelRequested` element too`true`.</span></span> <span data-ttu-id="8af67-105">Hallo-taak worden op basis van best-effort geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="8af67-105">hello job will be cancelled on a best-effort basis.</span></span> <span data-ttu-id="8af67-106">Als er stations aanwezig zijn in het Hallo-proces voor het overbrengen van gegevens, blijft gegevens toobe overgedragen zelfs nadat de annulering is aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="8af67-106">If drives are in hello process of transferring data, data may continue toobe transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="8af67-107">Een geannuleerde taak gaat toohello `Completed` status en worden bewaard gedurende 90 dagen op dat moment worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8af67-107">A cancelled job will move toohello `Completed` state and be kept for 90 days, at which point it will be deleted.</span></span>

 <span data-ttu-id="8af67-108">toodelete een taak aanroep Hallo [taak verwijderen](/rest/api/storageimportexport/jobs#Jobs_Delete) bewerking voordat het Hallo-taak is verzonden (*dat wil zeggen*, terwijl het Hallo-taak wordt Hallo `Creating` staat).</span><span class="sxs-lookup"><span data-stu-id="8af67-108">toodelete a job, call hello [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before hello job has shipped (*i.e.*, while hello job is in hello `Creating` state).</span></span> <span data-ttu-id="8af67-109">U kunt ook een taak verwijderen wanneer deze Hallo `Completed` status.</span><span class="sxs-lookup"><span data-stu-id="8af67-109">You can also delete a job when it is in hello `Completed` state.</span></span> <span data-ttu-id="8af67-110">Nadat een taak is verwijderd, worden de gegevens en de status niet langer zijn toegankelijk via Hallo REST-API of hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="8af67-110">After a job has been deleted, its information and status are no longer accessible via hello REST API or hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8af67-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8af67-111">Next steps</span></span>

* [<span data-ttu-id="8af67-112">Met behulp van REST-API voor Hallo Import/Export-service</span><span class="sxs-lookup"><span data-stu-id="8af67-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
