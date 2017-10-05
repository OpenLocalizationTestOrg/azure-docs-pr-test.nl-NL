---
title: Overzicht van uw Azure Import/Export-taken | MicrosoftDocs
description: Ontdek hoe u een lijst weer met alle van de Azure Import/Export-service-taken in een abonnement.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f2e619be-1bbd-4a54-9472-9e2f70a83b64
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 1977bfc0e516088310f45ecdd960287eeed2c2d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enumerating-jobs-in-the-azure-importexport-service"></a><span data-ttu-id="1ba73-103">Het inventariseren van taken in de Azure Import/Export-service</span><span class="sxs-lookup"><span data-stu-id="1ba73-103">Enumerating jobs in the Azure Import/Export service</span></span>
<span data-ttu-id="1ba73-104">Aanroepen voor het inventariseren van alle taken in een abonnement, het [lijst taken](/rest/api/storageimportexport/jobs#Jobs_List) bewerking.</span><span class="sxs-lookup"><span data-stu-id="1ba73-104">To enumerate all jobs in a subscription, call the [List Jobs](/rest/api/storageimportexport/jobs#Jobs_List) operation.</span></span> <span data-ttu-id="1ba73-105">`List Jobs`retourneert een lijst met taken, evenals de volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="1ba73-105">`List Jobs` returns a list of jobs as well as the following attributes:</span></span>

-   <span data-ttu-id="1ba73-106">Het type taak (invoer of uitvoer)</span><span class="sxs-lookup"><span data-stu-id="1ba73-106">The type of job (Import or Export)</span></span>

-   <span data-ttu-id="1ba73-107">De huidige taakstatus</span><span class="sxs-lookup"><span data-stu-id="1ba73-107">The current job state</span></span>

-   <span data-ttu-id="1ba73-108">De taak horen storage-account</span><span class="sxs-lookup"><span data-stu-id="1ba73-108">The job's associated storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ba73-109">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1ba73-109">Next steps</span></span>

* [<span data-ttu-id="1ba73-110">Met behulp van de Import/Export-service REST-API</span><span class="sxs-lookup"><span data-stu-id="1ba73-110">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
